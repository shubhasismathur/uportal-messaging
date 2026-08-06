# Core Business Workflows

The uPortal Messaging application serves targeted portal messages to authenticated users based on their group memberships and each message's scheduling window, enabling portal administrators to deliver time-bound, audience-specific announcements and notifications.

## Domain Entities

| Entity | Service / Bounded Context | Description | Key Relationships |
|---|---|---|---|
| Message | Message Delivery | A portal announcement or notification with content, scheduling, and audience metadata | Contains one optional MessageFilter, up to three optional ActionButtons, and optional Data |
| MessageFilter | Message Delivery | Defines the audience and scheduling window for a message (groups, goLiveDate, expireDate) | Belongs to one Message; evaluated against a User |
| ActionButton | Message Delivery | A labeled hyperlink button displayed on a message (action, moreInfo, confirm) | Belongs to one Message |
| Data | Message Delivery | Optional key-value payload attached to a message for portal widget integration | Belongs to one Message |
| User | Message Delivery | Transient per-request representation of the requesting user and their group memberships | Used by MessageFilter to evaluate audience eligibility |

## Service-to-Domain Mapping

| Service | Domain Context | Owned Entities | External Dependencies |
|---|---|---|---|
| uportal-messaging | Message Delivery | Message, MessageFilter, ActionButton, Data, User | None — all data is self-contained in a classpath JSON file |

This is a single-service application with a single bounded context. There are no cross-service data flows or inter-service dependencies.

## Primary Workflows

### Workflow 1: Retrieve Filtered Messages for a Portal User

**Entry point:** `GET /messages`

**Purpose:** Return the list of messages that are currently applicable to the requesting user — excluding expired, premature, or audience-restricted messages the user is not eligible to receive.

**Steps:**
1. The portal client calls `GET /messages`, attaching the user's group memberships in the `isMemberOf` HTTP header (semicolon-delimited string).
2. `MessagesController` delegates header parsing to `IsMemberOfHeaderParser`, which splits the header value into a `Set<String>` of group names.
3. A `User` object is constructed with the parsed group set.
4. `MessagesService.filteredMessages(user)` is called, which loads all messages from the JSON file.
5. Three predicates are composed and applied to filter the message list:
   - **Expiry check**: Messages whose `expireDate` is in the past are removed.
   - **Go-live check**: Messages whose `goLiveDate` is in the future are removed.
   - **Audience check**: Messages with a group filter that does not include any of the user's groups are removed.
6. The surviving messages are returned as `{ "messages": [...] }`.

**Business rules applied:** BR-1 (expiry), BR-2 (go-live), BR-3 (audience).

---

### Workflow 2: Retrieve a Specific Message for a Portal User

**Entry point:** `GET /message/{id}`

**Purpose:** Retrieve a specific message by ID, validated against the requesting user's context. Throws typed exceptions for scheduling or audience violations rather than silently excluding the message.

**Steps:**
1. The portal client calls `GET /message/{id}` with the user's `isMemberOf` header.
2. `MessagesController` parses the header into a `User` object (same as Workflow 1).
3. `MessagesService.messageByIdForUser(id, user)` is called.
4. `messageById(id)` is called first: all messages are loaded and filtered by ID. If no match, returns null → controller throws `MessageNotFoundException` (404).
5. The matching message is tested sequentially:
   - If `goLiveDate` is in the future → throws `PrematureMessageException`.
   - If `expireDate` is in the past → throws `ExpiredMessageException`.
   - If the user is not in the message's audience → throws `UserNotInMessageAudienceException`.
6. If all checks pass, the message is returned.

**Business rules applied:** BR-2 (go-live), BR-1 (expiry), BR-3 (audience).

---

### Workflow 3: Retrieve All Messages (Admin)

**Entry point:** `GET /admin/allMessages`

**Purpose:** Return the complete, unfiltered list of all messages regardless of scheduling or audience. Intended for portal administrators to inspect the full message inventory.

**Steps:**
1. `MessagesController.allMessages()` calls `MessagesService.allMessages()`.
2. `MessagesFromTextFile.allMessages()` loads and deserializes the JSON file.
3. All messages are returned without any filtering.

**No business rules applied.** This is an administrative bypass of all filtering logic.

---

### Workflow 4: Retrieve a Specific Message (Admin)

**Entry point:** `GET /admin/message/{id}`

**Purpose:** Retrieve a specific message by ID with no user-context restrictions. Allows administrators to inspect any message including premature, expired, or audience-restricted ones.

**Steps:**
1. `MessagesController.adminMessageById(id)` calls `MessagesService.messageById(id)`.
2. All messages are loaded and the first match by ID is returned.
3. If no match is found, `MessageNotFoundException` is thrown (404).

**No scheduling or audience business rules applied.**

## Cross-Service Data Flows

The application is a single-service deployment with no cross-service data flows. All data originates from the local `messages.json` classpath file. There is no gateway aggregation, inter-service REST calls, or event-driven data composition. The only external input per request is the `isMemberOf` HTTP header, which is provided by the upstream portal infrastructure (not another microservice owned by this application).

## Business Workflow Sequence

```mermaid
sequenceDiagram
    participant Client as "Portal Client"
    participant Ctrl as "MessagesController"
    participant Parser as "Header Parser"
    participant Svc as "MessagesService"
    participant Repo as "MessagesFromTextFile"

    Client->>Ctrl: GET /messages (isMemberOf: groupA;groupB)
    Ctrl->>Parser: Parse isMemberOf header
    Parser-->>Ctrl: Set of group names
    Ctrl->>Svc: filteredMessages(user)
    Svc->>Repo: allMessages()
    Repo-->>Svc: Full message list

    loop For each message
        Svc->>Svc: Check expiry (BR-1)
        alt Message is expired
            Note over Svc: Remove message
        else Not expired
            Svc->>Svc: Check go-live date (BR-2)
            alt Message is premature
                Note over Svc: Remove message
            else Gone live
                Svc->>Svc: Check audience (BR-3)
                alt User not in audience
                    Note over Svc: Remove message
                else User in audience
                    Note over Svc: Retain message
                end
            end
        end
    end

    Svc-->>Ctrl: Filtered message list
    Ctrl-->>Client: 200 { "messages": [...] }
```

## Business Rules & Decision Logic

### BR-1: Message Expiry

A message is expired if its `filter.expireDate` is a non-null ISO datetime string that is strictly before the current system time. Messages with no filter, a null `expireDate`, or an unparseable `expireDate` are treated as expired (fail-safe: bogus expiration data is treated as expired). Expired messages are silently excluded from filtered results; accessing an expired message by ID throws `ExpiredMessageException`.

### BR-2: Message Go-Live (Not-Before)

A message is premature if its `filter.goLiveDate` is a non-null ISO datetime string that is strictly after the current system time. Messages with no filter, a null `goLiveDate`, or an unparseable `goLiveDate` are treated as having gone live (they are not premature). Premature messages are silently excluded from filtered results; accessing a premature message by ID throws `PrematureMessageException`.

### BR-3: Audience Filtering

A message is visible to a user if ANY of the following is true:
- The message has no `filter` field at all (universal audience).
- The message's `filter.groups` list is null (universal audience — no group constraint was specified).
- The intersection of `filter.groups` and the user's group memberships is non-empty (the user belongs to at least one required group).

A message is NOT visible if `filter.groups` is an empty list (explicitly restricted to no one) or if none of the required groups match the user's groups.

### BR-4: Message ID Uniqueness

Message IDs are expected to be unique. If `messageById` finds more than one message with the same ID, an `IllegalStateException` is thrown — this is treated as a data-corruption scenario.

### Error Handling

| Exception | Trigger | HTTP Outcome |
|---|---|---|
| `MessageNotFoundException` | No message found for the given ID | 404 Not Found |
| `ExpiredMessageException` | Message exists but is past its expireDate | 4xx (exception handler) |
| `PrematureMessageException` | Message exists but has not yet gone live | 4xx (exception handler) |
| `UserNotInMessageAudienceException` | Message exists and is live but user lacks required group | 4xx (exception handler) |
| `IllegalStateException` | Multiple messages share the same ID | 500 Internal Server Error |

### Authorization

There is no programmatic authorization. The `/admin/*` endpoints bypass all filtering but have no access control enforced by the application. Authorization for admin endpoints must be enforced by external infrastructure (reverse proxy, container network policy, or portal gateway).

### Transactions

No transaction management is used. The application is read-only with no persistence writes, so there are no `@Transactional` boundaries, saga patterns, or consistency concerns.

### Audit / Logging

SLF4J + Logback is used for operational logging. The service logs at `TRACE` level for each filtered message count and individual message lookups, and at `DEBUG` level when no matching message is found or when a message is excluded due to scheduling or audience rules. `ERROR` level is used for data-corruption scenarios (duplicate IDs).

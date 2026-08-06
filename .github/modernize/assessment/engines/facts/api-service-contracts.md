# API & Service Communication Contracts

The uPortal Messaging application exposes 5 REST endpoints across a single Spring MVC controller, communicating synchronously with no external service dependencies.

## Service Catalog

| Service | Port | Category | Purpose |
|---|---|---|---|
| uportal-messaging | 8080 (default) | Business | Serves portal messages filtered by user group membership and scheduling rules |

## API Endpoints Inventory

| Service | Method | Path | Request Type | Response Type |
|---|---|---|---|---|
| MessagesController | GET | / | None | Map (status: "up") |
| MessagesController | GET | /messages | isMemberOf header (String) | Map (messages: List of Message) |
| MessagesController | GET | /admin/allMessages | None | Map (messages: List of Message) |
| MessagesController | GET | /admin/message/{id} | Path param: id (String) | Message or 404 |
| MessagesController | GET | /message/{id} | Path param: id (String), isMemberOf header | Message or 404 / 4xx |

## Management & Observability Endpoints

| Service | Endpoint | Custom Metrics |
|---|---|---|
| uportal-messaging | Spring Boot Actuator defaults (if enabled) | None |

> Note: No explicit Spring Boot Actuator configuration was found in `application.properties`. Default Actuator endpoints may be available but are not explicitly configured. No custom `@Timed` or Micrometer metric registrations were detected.

## DTOs & Contracts

The API uses plain Java POJOs serialized to JSON via Jackson (provided by Spring Boot):

- **Message**: Primary response entity representing a single portal message. Returned directly from `/message/{id}` and as list elements in `/messages` and `/admin/allMessages` responses.
- **MessageArray**: Internal deserialization wrapper used when loading messages from the JSON file. Not exposed in API responses directly.
- **MessageFilter**: Encapsulates filtering parameters; used internally within the service layer and not exposed at the API boundary.
- **ActionButton**: Nested within `Message`; represents an action link/button on a message.
- **Data**: Nested within `Message`; carries additional key-value data associated with a message.
- **User**: Internal model representing the requesting user and their group memberships. Constructed per-request from the `isMemberOf` header; never serialized in API responses.

There are no OpenAPI/Swagger specifications, `.proto` files, or GraphQL schemas. No DTO immutability annotations (Lombok `@Value`, Java records) are used — all model classes are mutable POJOs. Jackson uses default serialization with no custom serializers configured.

## Communication Patterns

**Synchronous**: All communication is synchronous HTTP REST. The application has no client-side HTTP calls to other services — it is entirely a server-side service with no outbound REST, gRPC, or messaging calls.

**Asynchronous**: No asynchronous messaging patterns (Kafka, RabbitMQ, JMS, etc.) are present.

**Resilience**: No circuit breaker, retry policy, timeout configuration, or bulkhead patterns are implemented. There is no Resilience4j, Spring Retry, or similar library on the classpath.

**Service Discovery**: Not applicable. The application is a standalone WAR deployed to Tomcat. There is no Eureka, Consul, or Kubernetes-based service discovery.

**API Gateway**: No API gateway layer exists within this project.

**Security Posture**: No authentication or TLS is configured at the application level. All endpoints are publicly accessible with no authorization checks enforced by the application itself. The `/admin/allMessages` and `/admin/message/{id}` endpoints are prefixed with `/admin` but have no access control — they rely entirely on external infrastructure (reverse proxy, load balancer, or container network policy) to restrict access. The `isMemberOf` HTTP header is trusted implicitly without validation or signature verification; any caller can forge group memberships.

## Service Technology Matrix

| Service | Web Framework | Data Access | Discovery | Gateway | Actuator | Cache | Metrics |
|---|---|---|---|---|---|---|---|
| uportal-messaging | Spring MVC (Servlet) | JSON file via ResourceLoader | None | None | Default (unconfigured) | None | None |

## Service Communication Sequence

```mermaid
sequenceDiagram
    participant Client as "Portal Client"
    participant Ctrl as "MessagesController"
    participant Parser as "IsMemberOfHeaderParser"
    participant Svc as "MessagesService"
    participant Repo as "MessagesFromTextFile"
    participant File as "messages.json"

    Client->>Ctrl: GET /messages (isMemberOf: group1;group2)
    Ctrl->>Parser: groupsFromHeaderValue("group1;group2")
    Parser-->>Ctrl: Set[group1, group2]
    Ctrl->>Svc: filteredMessages(user)
    Svc->>Repo: allMessages()
    Repo->>File: read JSON classpath resource
    File-->>Repo: raw JSON string
    Repo-->>Svc: List of Message
    Svc->>Svc: apply ExpiredMessagePredicate
    Svc->>Svc: apply GoneLiveMessagePredicate
    Svc->>Svc: apply AudienceFilterMessagePredicate
    Svc-->>Ctrl: List of filtered Message
    Ctrl-->>Client: 200 { "messages": [...] }
```

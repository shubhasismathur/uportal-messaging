# Architecture Diagram

This project is a Spring Boot messaging microservice that serves JSON message payloads filtered by user audience and message lifetime rules. The architecture is a single deployable unit with in-process business filtering and file-backed message storage.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Portal Client or Browser"]
    end

    subgraph App["Application Layer - Spring Boot 1.5.9"]
        Api["REST API Controller"]
        Service["Message Filtering Service"]
    end

    subgraph Data["Data Layer"]
        FileRepo["File Message Repository"]
        JsonFile[("messages.json")]
    end

    subgraph External["External Services"]
        HeaderSource["Upstream Header Provider"]
        LinkTargets["External URLs in message actions"]
    end

    Browser -->|"GET requests"| Api
    HeaderSource -->|"isMemberOf header values"| Api
    Api -->|"delegates filtering"| Service
    Service -->|"loads full message set"| FileRepo
    FileRepo -->|"reads JSON"| JsonFile
    Api -->|"returns filtered payload"| Browser
    Browser -->|"follows message links"| LinkTargets
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Presentation | Spring MVC REST (`spring-boot-starter-web`) | Spring Boot 1.5.9.RELEASE | Exposes HTTP endpoints for message retrieval and status |
| Business | Spring Service + Java predicates | Java 8 | Applies audience, go-live, and expiration filtering rules |
| Data Access | Spring `@Repository` + Jackson + org.json + Commons IO | Jackson from Spring Boot BOM; `org.json` 20171018; Commons IO 2.6 | Loads and deserializes message definitions from JSON resource files |
| Runtime | Embedded/provided Tomcat WAR deployment | Spring Boot 1.5.9.RELEASE | Hosts the application as a servlet-based microservice |

### Data Storage & External Services

The service does not use a database, cache, or message broker. Message data is stored in classpath JSON files (`messages.json` by default), and the only external interaction is consumption of request headers from upstream portal components and optional user navigation to URL targets embedded in message action buttons.

### Key Architectural Decisions

- Uses file-backed content (`message.source`) instead of a relational or NoSQL persistence layer.
- Keeps filtering logic in predicate-based service components to enforce consistent audience and date checks.
- Exposes both user-scoped and admin endpoints from a single REST controller for operational simplicity.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation["Presentation"]
        MessagesCtrl["MessagesController"]
        HeaderParser["IsMemberOfHeaderParser"]
    end

    subgraph Business["Business Logic"]
        MsgService["MessagesService"]
        AudiencePred["AudienceFilterMessagePredicate"]
        GoLivePred["GoneLiveMessagePredicate"]
        ExpiredPred["ExpiredMessagePredicate"]
        DateAfter["IsoDateTimeStringAfterPredicate"]
        DateBefore["IsoDateTimeStringBeforePredicate"]
    end

    subgraph DataAccess["Data Access"]
        MsgRepo["MessagesFromTextFile"]
        Models["Message Domain Models"]
    end

    subgraph Infra["Infrastructure"]
        SpringDI["Spring Dependency Injection"]
        JsonResource[("messages.json resource")]
    end

    MessagesCtrl -->|"parses user groups"| HeaderParser
    MessagesCtrl -->|"delegates query"| MsgService
    MsgService -->|"applies predicates"| AudiencePred
    MsgService -->|"applies predicates"| GoLivePred
    MsgService -->|"applies predicates"| ExpiredPred
    GoLivePred -->|"date parsing"| DateAfter
    ExpiredPred -->|"date parsing"| DateBefore
    MsgService -->|"retrieves messages"| MsgRepo
    MsgRepo -->|"maps JSON to objects"| Models
    MsgRepo -->|"reads"| JsonResource
    SpringDI -.->|"wires beans"| MessagesCtrl
    SpringDI -.->|"wires beans"| MsgService
    SpringDI -.->|"wires beans"| MsgRepo
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| MessagesController | Presentation | Spring REST Controller | Handles status and message retrieval endpoints |
| IsMemberOfHeaderParser | Presentation | Utility Component | Converts semicolon-delimited membership header into group set |
| MessagesService | Business Logic | Spring Service | Orchestrates retrieval and filtering of messages for user/admin flows |
| AudienceFilterMessagePredicate | Business Logic | Predicate | Checks whether a user belongs to required message groups |
| GoneLiveMessagePredicate | Business Logic | Predicate | Validates go-live eligibility against current time |
| ExpiredMessagePredicate | Business Logic | Predicate | Flags expired messages based on configured expiration date |
| IsoDateTimeStringAfterPredicate / BeforePredicate | Business Logic | Predicate Utilities | Parses ISO date strings and performs temporal comparisons |
| MessagesFromTextFile | Data Access | Spring Repository | Loads JSON message source and maps into message model objects |
| Message, MessageFilter, MessageArray, Data, ActionButton, User | Data Access | Domain/DTO Models | Represent API payload, filtering metadata, and user context |

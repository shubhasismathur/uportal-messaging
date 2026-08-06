# Configuration & Externalized Settings Inventory

The project uses a small, file-based configuration surface with one runtime properties file and build-time Maven metadata. No profile-specific overlays, secret stores, or external configuration servers were detected.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Spring application properties | Runtime config file | `src/main/resources/application.properties` | Declares message source location |
| Logback config | Logging config file | `src/main/resources/logback.xml` | Controls logging behavior |
| Maven project file | Build/package config | `pom.xml` | Declares dependencies, Java level, plugins, packaging |
| Message content files | Application data config source | `src/main/resources/messages.json`, `src/main/resources/demoMessages.json` | Runtime content loaded via `message.source` |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Default Maven build (no named profiles) | Automatic | Compile, test, package WAR | `spring-boot-maven-plugin`, `maven-failsafe-plugin`, `maven-war-plugin`, `maven-release-plugin` |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| default | Spring Boot default runtime | `application.properties` | `message.source=classpath:messages.json` |

## Properties Inventory

### uportal-messaging

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `message.source` | `classpath:messages.json` | default | `src/main/resources/application.properties` |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| uportal-messaging | Not specified in repository | Not specified in repository | Not specified in repository |

## Startup Dependency Chain

1. `uportal-messaging` starts as a standalone Spring Boot service.
2. During request processing, it requires classpath access to the configured message JSON resource.
3. No external service readiness dependencies or wait-for mechanisms were found.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| None detected in repository configuration | N/A | N/A |

### Secrets Provisioning Workflow

No secret provisioning workflow is defined in this repository. The current configuration model relies on non-secret local/classpath resource references.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| None detected | N/A | N/A |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Spring Boot | `1.5.9.RELEASE` | `pom.xml` parent |
| Java target | `1.8` | `pom.xml` property `java.version` |
| Packaging | `war` | `pom.xml` |
| Commons IO | `2.6` | `pom.xml` |
| Commons Lang | `3.7` | `pom.xml` |
| org.json | `20171018` | `pom.xml` |

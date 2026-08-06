# Configuration & Externalized Settings Inventory

The uPortal Messaging application has a minimal configuration landscape: a single `application.properties` with one custom property, a `logback.xml` for logging, and no runtime profiles, secret stores, or external config servers.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| application.properties | Spring Boot properties | `src/main/resources/application.properties` | Single custom property defining the message source file path |
| logback.xml | Logback XML config | `src/main/resources/logback.xml` | Rolling file appender; includes Spring Boot base logging config |
| messages.json | Data file | `src/main/resources/messages.json` | Static message data; path controlled by `message.source` property |
| demoMessages.json | Data file | `src/main/resources/demoMessages.json` | Alternative demo data file; not wired by default |
| banner.txt | Spring Boot banner | `src/main/resources/banner.txt` | Custom ASCII banner displayed on startup |

No Spring Cloud Config server, external Git config repository, Vault, Azure KeyVault, AWS Secrets Manager, Kubernetes ConfigMaps/Secrets, or Docker Compose environment sections are present.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| (default) | Automatic | Standard WAR build | spring-boot-maven-plugin, maven-failsafe-plugin, maven-war-plugin, coveralls-maven-plugin, cobertura-maven-plugin |
| release | Manual `-PreleaseProfiles` via maven-release-plugin | Deployment to artifact repository | maven-release-plugin 2.4.2, maven-scm-provider-gitexe 1.8.1 |

No `dev`, `docker`, or `cloud` Maven profiles are defined. The `maven-release-plugin` is configured to use the `release` profile during releases and deploy to the artifact repositories defined in `<distributionManagement>`.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| (default/no profile) | None — single profile only | `application.properties` | N/A |

No Spring profile-specific configuration files (`application-dev.properties`, `application-prod.yml`, etc.) exist. There are no `@Profile` annotations in the codebase. The application is intended to run with a single configuration, with any environment-specific overrides expected to be supplied externally (e.g., via JVM `-D` system property for `message.source`).

## Properties Inventory

### uportal-messaging

| Property Key | Default Value | Profiles | Source |
|---|---|---|---|
| `message.source` | `classpath:messages.json` | All | `application.properties` |

No database, security, caching, or messaging properties are present. The only application-specific property is the data file path. Spring Boot's autoconfigured defaults (server port 8080, context path `/`, etc.) apply implicitly.

### Logging Configuration (logback.xml)

| Setting | Value |
|---|---|
| Log directory | `./logs/${CONTEXT_NAME}` (relative to working directory) |
| Log file name | `uportal-messaging.log` |
| Rolling policy | Daily rotation: `uportal-messaging.log.yyyy-MM-dd` |
| Root log level | `WARN` |
| `edu.wisc` package level | `WARN` |
| Scan for changes | Every 30 seconds |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| uportal-messaging | No defined JVM options; defaults apply | Not specified (no Docker/K8s config) | Not specified |

No Docker Compose, Kubernetes manifests, Helm charts, or container configuration files are present. JVM heap size, GC settings, and instance count are left to the deploying environment.

## Startup Dependency Chain

The application has no startup dependencies. It is a standalone Spring Boot WAR with no dependency on external services, config servers, or databases. Startup succeeds as long as the `message.source` classpath resource is accessible, which is guaranteed since `messages.json` is bundled in the WAR.

There are no Kubernetes readiness probes, `dockerize` wait mechanisms, or Spring Cloud Config retry configurations.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| (none detected) | — | — |

No database passwords, API keys, OAuth client secrets, or any other sensitive configuration values are present. The application does not connect to any external authenticated service and has no credentials to manage.

### Secrets Provisioning Workflow

No secrets provisioning workflow exists. The application has no secrets. The sole configuration property (`message.source`) is non-sensitive.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| (none detected) | — | — |

No feature flag frameworks (LaunchDarkly, Unleash, Spring Feature Management), `@ConditionalOnProperty` beans, or A/B testing configurations are present in the codebase.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Java (target/source) | 1.8 | `pom.xml` `<java.version>` |
| Spring Boot | 1.5.9.RELEASE | `pom.xml` parent POM |
| Spring Framework | 4.3.x (managed by Boot 1.5.9) | Transitive via spring-boot-starter-parent |
| Spring MVC | 4.3.x | Transitive via spring-boot-starter-web |
| Spring Data REST / HATEOAS | 2.6.x | Transitive via spring-boot-starter-data-rest |
| Embedded Tomcat | 8.5.x (provided scope — external) | spring-boot-starter-tomcat |
| Jackson | 2.9.x (managed by Boot 1.5.9) | Transitive via spring-boot-starter-web |
| SLF4J | 1.7.x | Transitive via spring-boot-starter |
| Logback | 1.1.x | Transitive via spring-boot-starter; overridden by logback.xml |
| Apache Commons IO | 2.6 | `pom.xml` explicit |
| Apache Commons Lang3 | 3.7 | `pom.xml` explicit |
| org.json | 20171018 | `pom.xml` explicit |
| Maven | 3.x (minimum; not pinned) | Build tool |
| maven-failsafe-plugin | Managed by Spring Boot parent | Integration test execution |
| maven-release-plugin | 2.4.2 | `pom.xml` explicit |
| coveralls-maven-plugin | 4.3.0 | `pom.xml` explicit |
| cobertura-maven-plugin | 2.7 | `pom.xml` explicit |

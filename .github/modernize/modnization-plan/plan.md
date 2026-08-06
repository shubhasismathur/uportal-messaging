# Modernization Plan: modnization-plan

**Project**: uportal-messaging

---

## Technical Framework

- **Language**: Java 8 (1.8)
- **Framework**: Spring Boot 1.5.9.RELEASE
- **Build Tool**: Maven
- **Database**: N/A (file-based, reads from JSON files on classpath)
- **Key Dependencies**: spring-boot-starter-web, spring-boot-starter-data-rest, commons-io 2.6, org.json 20171018, commons-lang3 3.7

---

## Overview

> This migration modernizes the `uportal-messaging` Spring Boot application for deployment on Azure. The application currently runs on Spring Boot 1.5.9 with Java 8, uses file-based logging via a rolling file appender, and is packaged as a WAR file targeting a traditional application server.
>
> The new architecture will:
>
> - Upgrade the application to Spring Boot 3.x and Java 17+ for long-term support and current security posture
> - Migrate file-based logging to console output for cloud-native observability on Azure
> - Remediate known CVEs in outdated dependencies (commons-io 2.6, org.json 20171018, commons-lang3 3.7, Spring Boot 1.5.x)
> - Deploy the application to Azure Container Apps for managed, scalable cloud hosting
>
> The migration follows a phased approach: upgrade the runtime first, then apply code transformations, address security vulnerabilities, and finally containerize and deploy to Azure.

---

## Migration Impact Summary

| Application        | Original Service         | New Azure Service         | Authentication   | Comments                               |
|--------------------|--------------------------|---------------------------|------------------|----------------------------------------|
| uportal-messaging  | File-based rolling log   | Console logging (stdout)  | N/A              | Cloud-native logging for Azure         |
| uportal-messaging  | Spring Boot 1.5.9 / Java 8 | Spring Boot 3.x / Java 17 | N/A            | Runtime upgrade for LTS & security     |
| uportal-messaging  | N/A (no cloud services)  | Azure Container Apps      | Managed Identity | Default Azure deployment target        |

---

## Open Questions & Questionnaire

- [x] Q: What Java/Spring Boot version should the upgrade target? → A: Spring Boot 3.x (latest 3.x) with Java 17, as no explicit version was provided and Spring Boot 3.x is the most recent LTS-aligned major prior to 4.x.
- [x] Q: Should the application be deployed to Azure? → A: Yes, deploying to Azure Container Apps (default).
- [x] Q: Should integration tests be generated? → A: No integration test task included as the user did not explicitly request integration testing.
- [x] Q: Are there infrastructure provisioning requirements? → A: No explicit infrastructure request; deployment task will handle provisioning via Bicep.

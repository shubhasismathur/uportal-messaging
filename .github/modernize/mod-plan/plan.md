# Modernization Plan: uportal-messaging Azure Migration

**Project**: uportal-messaging

---

## Technical Framework

- **Language**: Java 1.8
- **Framework**: Spring Boot 1.5.9.RELEASE
- **Build Tool**: Maven 3.x
- **Database**: None (JSON file-based data store)
- **Key Dependencies**: Spring Boot Web, Spring Data REST, Commons IO, Commons Lang3, org.json

---

## Overview

> This migration modernizes the `uportal-messaging` Spring Boot application for deployment to Azure. The application currently runs as a WAR file on an on-premises servlet container, serving messaging data from local JSON files via a REST API. The new architecture will:
>
> - Eliminate known security vulnerabilities (CVEs) in outdated dependencies such as `org.json 20171018`, `commons-io 2.6`, and Spring Boot 1.5.9
> - Containerize the application and deploy it to Azure Container Apps for scalable, cloud-native hosting
>
> The migration follows a security-first approach: first remediate all CVEs and ensure the project compiles and tests pass, then containerize and deploy to Azure.

---

## Migration Impact Summary

| Application          | Original Service        | New Azure Service         | Authentication     | Comments                             |
|----------------------|-------------------------|---------------------------|--------------------|--------------------------------------|
| uportal-messaging    | On-premises WAR deploy  | Azure Container Apps      | Managed Identity   | REST API serving JSON-file messages  |

---

## Open Questions & Questionnaire

- [x] Q: Should the plan include environment/infrastructure provisioning? → A: No — no infrastructure provisioning; focus on code migration and deployment only
- [x] Q: Should the plan include integration testing? → A: No — skip integration testing entirely (no external service dependencies to verify)
- [x] Q: Should the plan include a security scan and CVE remediation task? → A: Yes — include security/CVE remediation (default)
- [x] Q: Which Azure deployment target should the plan use? → A: Azure Container Apps (default)

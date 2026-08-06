# Modernization Plan: uPortal Messaging – Azure Migration

**Project**: uportal-messaging

---

## Technical Framework

- **Language**: Java 8 (1.8)
- **Framework**: Spring Boot 1.5.9.RELEASE
- **Build Tool**: Maven 3.x
- **Database**: None (file-based message store: `messages.json`)
- **Key Dependencies**: Spring Boot Web, Spring Data REST, commons-io, commons-lang3, org.json

---

## Overview

> This migration modernizes the `uportal-messaging` Spring Boot application from an outdated Java 8 / Spring Boot 1.5.x baseline to a modern, cloud-ready stack running on Azure. The application currently serves a REST API for user-targeted notifications backed by a local JSON file. The new architecture will:
>
> - Upgrade the runtime from Java 8 / Spring Boot 1.5.x to Java 21 / Spring Boot 3.x, replacing legacy `javax.*` namespaces with `jakarta.*` and resolving a large backlog of known CVEs present in the aging dependency set.
> - Containerize the application and deploy it to Azure Container Apps for scalable, fully managed hosting with built-in autoscaling and zero-infrastructure management overhead.
> - Migrate logging from file-based output to console-only output in preparation for cloud-native, centralized log management in Azure.
>
> The migration follows a phased approach: upgrade the runtime and framework first, remediate all known CVEs, modernize logging, containerize, and finally deploy to Azure.

---

## Migration Impact Summary

| Application        | Original Service         | New Azure Service         | Authentication   | Comments                                      |
|--------------------|--------------------------|---------------------------|------------------|-----------------------------------------------|
| uportal-messaging  | Spring Boot 1.5.9 / JDK 8| Spring Boot 3.x / JDK 21  | N/A              | Upgrade framework + Jakarta EE namespace      |
| uportal-messaging  | File-based logback output | Console-only logging      | N/A              | Cloud-native logging for Azure Container Apps |
| uportal-messaging  | Local WAR deployment      | Azure Container Apps       | Managed Identity | Containerized deployment                      |

---

## Open Questions & Questionnaire

- [x] Q: Should the plan include environment/infrastructure provisioning? → A: No — no infrastructure provisioning; focus on code migration and deployment only (default, no IaC configuration found in repository)
- [x] Q: Should the plan include integration testing to verify migrated services? → A: No — skip integration testing entirely (default; no external Azure dependencies to verify post-migration)
- [x] Q: Should the plan include a security scan and CVE remediation task? → A: Yes — include security/CVE remediation (default)
- [x] Q: Which Azure deployment target should the plan use? → A: Azure Container Apps (default)

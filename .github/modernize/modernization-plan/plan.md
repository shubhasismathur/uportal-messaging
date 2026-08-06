# Modernization Plan: uportal-messaging Azure Modernization

**Project**: uportal-messaging

---

## Technical Framework

- **Language**: Java 8 (1.8)
- **Framework**: Spring Boot 1.5.9.RELEASE
- **Build Tool**: Maven 3.x
- **Database**: None (messages loaded from JSON file on classpath)
- **Key Dependencies**: spring-boot-starter-web, spring-boot-starter-data-rest, commons-io 2.6, org.json 20171018, commons-lang3 3.7

---

## Overview

> This migration modernizes the uportal-messaging Spring Boot application from Java 8 / Spring Boot 1.5.x to a current, supported runtime and prepares it for cloud-native deployment on Azure Container Apps. The application currently runs as a WAR-packaged Spring Boot service (Java 8, Spring Boot 1.5.9) with file-based rolling logging. The new architecture will:
>
> - Upgrade the Java runtime and Spring Boot framework to a current supported version, eliminating end-of-life dependencies and known CVEs
> - Migrate logging from file-based rolling output to console-only output, making it cloud-native and compatible with Azure container log aggregation
> - Containerize the application and deploy it to Azure Container Apps for scalable, managed hosting
> - Remediate all known CVE vulnerabilities in transitive and direct dependencies
>
> The migration follows a sequential upgrade-first approach: the Java/Spring Boot upgrade runs first, then logging migration, followed by security CVE remediation, and finally containerization/deployment to Azure Container Apps.

---

## Migration Impact Summary

```
| Application        | Original Service         | New Azure Service        | Authentication   | Comments                              |
|--------------------|--------------------------|--------------------------|------------------|---------------------------------------|
| uportal-messaging  | Java 8 / Spring Boot 1.5 | Java 21 / Spring Boot 3.x| N/A              | Upgrade runtime and framework         |
| uportal-messaging  | File-based rolling logs  | Console logging          | N/A              | Cloud-native logging for Azure        |
| uportal-messaging  | Local WAR deployment     | Azure Container Apps     | Managed Identity | Containerize and deploy to Azure ACA  |
```

---

## Open Questions & Questionnaire

- [x] Q: Should the plan include environment/infrastructure provisioning? → A: No — no infrastructure provisioning; focus on code migration and deployment only (default, no infra configuration found in repository)
- [x] Q: Should the plan include integration testing? → A: No — skip integration testing entirely (default, no environment provisioned)
- [x] Q: Should the plan include a security scan and CVE remediation task? → A: Yes — include security/CVE remediation (default)
- [x] Q: Which Azure deployment target should the plan use? → A: Azure Container Apps (default) — includes containerization; no separate containerization task needed

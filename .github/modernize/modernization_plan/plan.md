# Modernization Plan: uportal-messaging Azure Migration

**Project**: uportal-messaging

---

## Technical Framework

- **Language**: Java 8 (1.8)
- **Framework**: Spring Boot 1.5.9.RELEASE
- **Build Tool**: Maven 3.x (with maven-war-plugin, maven-failsafe-plugin)
- **Database**: None (file-based message storage — `messages.json`)
- **Key Dependencies**: Spring Boot Web, Spring Boot Data REST, commons-io 2.6, org.json 20171018, commons-lang3 3.7
- **Packaging**: WAR

---

## Overview

> This migration modernizes the `uportal-messaging` Spring Boot REST application for cloud-native deployment on Azure. The application currently runs as a WAR artifact with file-based rolling log output, outdated dependencies carrying known CVEs, and no containerization or cloud deployment pipeline.
>
> The new architecture will:
>
> - Replace file-based rolling log appenders with console (stdout) logging, the standard cloud-native pattern required for container and Azure-hosted workloads
> - Scan and remediate all known CVE vulnerabilities in project dependencies to ensure a secure baseline before deployment
> - Package the application as a container image and deploy it to Azure Container Apps, providing managed scaling, ingress, and operational simplicity
>
> The migration follows a sequential approach: log migration first (code change), then security CVE remediation (dependency hygiene), and finally containerized deployment to Azure.

---

## Migration Impact Summary

| Application         | Original Service          | New Azure Service        | Authentication     | Comments                                    |
|---------------------|---------------------------|--------------------------|--------------------|---------------------------------------------|
| uportal-messaging   | File-based log appender   | Console (stdout) logging | N/A                | Required for cloud-native container logging |
| uportal-messaging   | Local WAR deployment      | Azure Container Apps     | Managed Identity   | Default Azure deployment target             |

---

## Open Questions & Questionnaire

- [x] Q: Should the plan include environment/infrastructure provisioning? → A: No — no infrastructure provisioning; focus on code migration and deployment only (default: no infra config found in repository)
- [x] Q: Should the plan include integration testing? → A: No — skipped; no explicit user request and no cloud services being migrated that require integration-level verification
- [x] Q: Should the plan include a security scan and CVE remediation task? → A: Yes — include security/CVE remediation (default)
- [x] Q: Which Azure deployment target should the plan use? → A: Azure Container Apps (default)

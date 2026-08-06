# Security Assessment Report

**Generated:** 2026-08-06T12:00:40.0000000Z

## Summary

| Metric | Count |
|--------|-------|
| Total Findings | 59 |
| CVE Vulnerabilities (high+) | 55 |
| CWE Vulnerabilities | 4 |
| Total CWE Rules Assessed | 59 |
| CWE Rules Passed | 55 |

### By Severity

| Severity | Count |
|----------|-------|
| mandatory | 55 |
| optional | 1 |
| potential | 3 |

## CVE Findings (Dependency Vulnerabilities)

### GHSA-r7wm-3cxj-wff9: jackson-core: Async parser maxNumberLength bypass via chunked digit accumulation
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[GHSA-r7wm-3cxj-wff9](https://github.com/advisories/GHSA-r7wm-3cxj-wff9): jackson-core: Async parser maxNumberLength bypass via chunked digit accumulation (incomplete fix for GHSA-72hv-8253-57qq)

Severity: HIGH

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-core:2.8.10 (vulnerable range: < 2.18.8) (declared at pom.xml)
    Fix: Upgrade to 2.18.8
  - com.fasterxml.jackson.core:jackson-core:2.8.10 (vulnerable range: >= 2.19.0, < 2.21.4) (declared at pom.xml)
    Fix: Upgrade to 2.

### CVE-2026-41850: Spring Framework Algorithmic Denial of Service via SpEL Expressions
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41850](https://github.com/advisories/GHSA-r5w3-xv2f-j59q): Spring Framework Algorithmic Denial of Service via SpEL Expressions

Severity: HIGH

Affected dependencies:
  - org.springframework:spring-expression:4.3.13.RELEASE (vulnerable range: >= 7.0.0, <= 7.0.7) (declared at pom.xml)
    Fix: Upgrade to 7.0.8
  - org.springframework:spring-expression:4.3.13.RELEASE (vulnerable range: >= 6.2.0, <= 6.2.18) (declared at pom.xml)
    Fix: Upgrade to 6.2.19
  - org.springframework:spring-ex

### CVE-2026-41849: Spring Framework Denial of Service via Integer Overflow in SpEL Expressions
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41849](https://github.com/advisories/GHSA-775g-4xr8-78h8): Spring Framework Denial of Service via Integer Overflow in SpEL Expressions

Severity: HIGH

Affected dependencies:
  - org.springframework:spring-expression:4.3.13.RELEASE (vulnerable range: <= 5.3.39) (declared at pom.xml)
    Fix: No patched version available; check advisory

### CVE-2026-41845: Spring Framework Cross-site Scripting via JavaScriptUtils
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41845](https://github.com/advisories/GHSA-3chg-m5w7-qfv5): Spring Framework Cross-site Scripting via JavaScriptUtils

Severity: HIGH

Affected dependencies:
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: >= 7.0.0, <= 7.0.7) (declared at pom.xml)
    Fix: Upgrade to 7.0.8
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: >= 6.2.0, <= 6.2.18) (declared at pom.xml)
    Fix: Upgrade to 6.2.19
  - org.springframework:spring-webmvc:4.3.13.RELEAS

### CVE-2026-41842: Spring Framework Denial of Service via Versioned Resources in Spring MVC and Web
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41842](https://github.com/advisories/GHSA-x23c-287f-qqv5): Spring Framework Denial of Service via Versioned Resources in Spring MVC and WebFlux

Severity: HIGH

Affected dependencies:
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: >= 7.0.0, <= 7.0.7) (declared at pom.xml)
    Fix: Upgrade to 7.0.8
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: >= 6.2.0, <= 6.2.18) (declared at pom.xml)
    Fix: Upgrade to 6.2.19
  - org.springframework:

### CVE-2026-41284: Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41284](https://github.com/advisories/GHSA-gx5v-xp9w-j4cg): Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-embed-co

### CVE-2026-43512: Apache Tomcat - Digest authenticator will authenticate any unknown user
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43512](https://github.com/advisories/GHSA-h6fc-48rj-7qqh): Apache Tomcat - Digest authenticator will authenticate any unknown user

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-

### CVE-2026-43513: Apache Tomcat: LockOutRealm treats user names as case-sensitive
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43513](https://github.com/advisories/GHSA-5mp6-jrq3-r938): Apache Tomcat: LockOutRealm treats user names as case-sensitive

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-embed-core:8

### CVE-2026-43515: Apache Tomcat - Security constraints not correctly applied
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43515](https://github.com/advisories/GHSA-5m62-pw8w-7w9f): Apache Tomcat - Security constraints not correctly applied

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-embed-core:8.

### CVE-2026-41293: Apache Tomcat - HTTP/2 request headers not validated
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41293](https://github.com/advisories/GHSA-r29c-68gh-xp6x): Apache Tomcat - HTTP/2 request headers not validated

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (

### CVE-2026-42498: Apache Tomcat - WebSocket authentication header exposure
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42498](https://github.com/advisories/GHSA-fv25-8xcx-gqjc): Apache Tomcat - WebSocket authentication header exposure

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: < 9.0.118) (declared at pom.xml)
    Fix: Upgrade to 9.0.118
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.55) (declared at pom.xml)
    Fix: Upgrade to 10.1.55
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (

### CVE-2026-24880: Apache Tomcat has an HTTP Request/Response Smuggling vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-24880](https://github.com/advisories/GHSA-563x-q5rq-57qp): Apache Tomcat has an HTTP Request/Response Smuggling vulnerability

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 7.0.0, < 9.0.116) (declared at pom.xml)
    Fix: Upgrade to 9.0.116
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.52) (declared at pom.xml)
    Fix: Upgrade to 10.1.52
  - org.apache.tomcat.embed:tomcat

### CVE-2025-55752: Apache Tomcat Vulnerable to Relative Path Traversal
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-55752](https://github.com/advisories/GHSA-wmwf-9ccg-fff5): Apache Tomcat Vulnerable to Relative Path Traversal

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 11.0.0-M1, < 11.0.11) (declared at pom.xml)
    Fix: Upgrade to 11.0.11
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.45) (declared at pom.xml)
    Fix: Upgrade to 10.1.45
  - org.apache.tomcat.embed:tomcat-embed-core

### CVE-2025-53506: Apache Tomcat Coyote vulnerable to Denial of Service via excessive HTTP/2 stream
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-53506](https://github.com/advisories/GHSA-25xr-qj8w-c4vf): Apache Tomcat Coyote vulnerable to Denial of Service via excessive HTTP/2 streams

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 8.5.0, <= 8.5.100) (declared at pom.xml)
    Fix: No patched version available; check advisory
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 9.0.0.M1, < 9.0.107) (declared at pom.xml)
    Fix: Upgrade to 9

### CVE-2025-52520: Apache Tomcat Catalina is vulnerable to DoS attack through bypassing of size lim
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-52520](https://github.com/advisories/GHSA-wr62-c79q-cv37): Apache Tomcat Catalina is vulnerable to DoS attack through bypassing of size limits

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 11.0.0-M1, < 11.0.9) (declared at pom.xml)
    Fix: Upgrade to 11.0.9
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.43) (declared at pom.xml)
    Fix: Upgrade to 10.1.43
  - org.apache.

### CVE-2025-52999: jackson-core can throw a StackoverflowError when processing deeply nested data
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-52999](https://github.com/advisories/GHSA-h46c-h94j-95f3): jackson-core can throw a StackoverflowError when processing deeply nested data

Severity: HIGH

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-core:2.8.10 (vulnerable range: < 2.15.0) (declared at pom.xml)
    Fix: Upgrade to 2.15.0

### CVE-2025-48988: Apache Tomcat - DoS in multipart upload
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-48988](https://github.com/advisories/GHSA-h3gc-qfqq-6h8f): Apache Tomcat - DoS in multipart upload

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 11.0.0-M1, <= 11.0.7) (declared at pom.xml)
    Fix: Upgrade to 11.0.8
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, <= 10.1.41) (declared at pom.xml)
    Fix: Upgrade to 10.1.42
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vul

### CVE-2025-24813: Apache Tomcat: Potential RCE and/or information disclosure and/or information co
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-24813](https://github.com/advisories/GHSA-83qj-6fr2-vhqg): Apache Tomcat: Potential RCE and/or information disclosure and/or information corruption with partial PUT

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 11.0.0-M1, < 11.0.3) (declared at pom.xml)
    Fix: Upgrade to 11.0.3
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.35) (declared at pom.xml)
    Fix: Upgrade 

### CVE-2024-38819: Spring Framework Path Traversal vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2024-38819](https://github.com/advisories/GHSA-g5vr-rgqm-vf78): Spring Framework Path Traversal vulnerability

Severity: HIGH

Affected dependencies:
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: >= 6.1.0, < 6.1.14) (declared at pom.xml)
    Fix: Upgrade to 6.1.14
  - org.springframework:spring-webmvc:4.3.13.RELEASE (vulnerable range: <= 5.3.39) (declared at pom.xml)
    Fix: No patched version available; check advisory
  - org.springframework:spring-webmvc:4.3.13.

### CVE-2024-50379: Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2024-50379](https://github.com/advisories/GHSA-5j33-cvvr-w245): Apache Tomcat Time-of-check Time-of-use (TOCTOU) Race Condition vulnerability

Severity: HIGH

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 11.0.0-M1, < 11.0.2) (declared at pom.xml)
    Fix: Upgrade to 11.0.2
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (vulnerable range: >= 10.1.0-M1, < 10.1.34) (declared at pom.xml)
    Fix: Upgrade to 10.1.34
  - org.apache.tomcat

> *...and 35 more CVE findings. See security-assessment.json for full list.*

## CWE Findings (Code-Level Vulnerabilities)

### CWE-477: Use of Obsolete Function
- **Category:** Code Quality
- **Severity:** optional
- **Story Points:** 1
- **Files:** src/main/java/edu/wisc/my/messages/model/Message.java

Message.isValidToday() (line 287) is annotated with @Deprecated, indicating it is an obsolete method that should no longer be used. It remains in the production codebase and may still be called by external code despite being marked as deprecated.

### CWE-772: Missing Release of Resource after Effective Lifetime
- **Category:** Code Quality
- **Severity:** potential
- **Story Points:** 3
- **Files:** src/main/java/edu/wisc/my/messages/data/MessagesFromTextFile.java

In MessagesFromTextFile.allMessages() (line 39), an InputStream is obtained via resource.getInputStream() but is never closed. There is no try-with-resources block or finally clause to close the stream, so the InputStream leaks on every call to allMessages(), potentially exhausting file handles under load.

### CWE-775: Missing Release of File Descriptor or Handle after Effective Lifetime
- **Category:** Code Quality
- **Severity:** potential
- **Story Points:** 3
- **Files:** src/main/java/edu/wisc/my/messages/data/MessagesFromTextFile.java

Same instance as CWE-772: MessagesFromTextFile.allMessages() (line 39) opens an InputStream from a classpath resource but never calls is.close(). The stream is not wrapped in a try-with-resources, so the underlying file descriptor is never released.

### CWE-778: Insufficient Logging
- **Category:** Credentials & Secrets
- **Severity:** potential
- **Story Points:** 3
- **Files:** src/main/java/edu/wisc/my/messages/controller/MessagesController.java

The /admin/allMessages and /admin/message/{id} endpoints in MessagesController have no authentication or authorization controls and no logging of access attempts. Security-relevant events such as access to admin endpoints, forged isMemberOf headers, or audience violations (UserNotInMessageAudienceException, ExpiredMessageException, PrematureMessageException) are not logged at WARN or higher severity. The application logs at TRACE/DEBUG for normal operations but does not record security-critical access events, making it impossible to audit who accessed admin data or detect abuse.

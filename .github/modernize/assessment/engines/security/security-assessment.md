# Security Assessment Report

**Generated:** 2026-08-06T11:24:53.0000000Z

## Summary

| Metric | Count |
|--------|-------|
| Total Findings | 21 |
| CVE Vulnerabilities | 21 |
| CWE Vulnerabilities | 0 |
| Total Rules Assessed | 59 |
| Rules Passed | 59 |

### By Severity

| Severity | Count |
|----------|-------|
| mandatory | 21 |
| optional | 0 |
| potential | 0 |

## CVE Findings (Dependency Vulnerabilities)

### CVE-2016-1000027: Pivotal Spring Framework contains unsafe Java deserialization methods
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2016-1000027](https://github.com/advisories/GHSA-4wrc-f8pq-fpqp): Pivotal Spring Framework contains unsafe Java deserialization methods

Severity: CRITICAL

Affected dependencies:
  - org.springframework:spring-web:4.3.13.RELEASE (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2017-5929: QOS.ch Logback vulnerable to Deserialization of Untrusted Data
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2017-5929](https://github.com/advisories/GHSA-vmfg-rjjm-rjrj): QOS.ch Logback vulnerable to Deserialization of Untrusted Data

Severity: CRITICAL

Affected dependencies:
  - ch.qos.logback:logback-classic:1.1.11 (declared at pom.xml:75)
  - ch.qos.logback:logback-core:1.1.11 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2018-11307: Deserialization of Untrusted Data in jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2018-11307](https://github.com/advisories/GHSA-qr7j-h6gg-jmgc): Deserialization of Untrusted Data in jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2018-8014: The defaults settings for the CORS filter provided in Apache Tomcat are insecure and enable 'supportsCredentials' for all origins
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2018-8014](https://github.com/advisories/GHSA-r4x2-3cq5-hqvp): The defaults settings for the CORS filter provided in Apache Tomcat are insecure and enable 'supportsCredentials' for all origins

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-14379: Deserialization of untrusted data in FasterXML jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-14379](https://github.com/advisories/GHSA-6fpp-rgj9-8rwc): Deserialization of untrusted data in FasterXML jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-14540: Polymorphic Typing issue in FasterXML jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-14540](https://github.com/advisories/GHSA-h822-r4r5-v8jg): Polymorphic Typing issue in FasterXML jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-16335: Polymorphic Typing issue in FasterXML jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-16335](https://github.com/advisories/GHSA-85cw-hj65-qqv9): Polymorphic Typing issue in FasterXML jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-16942: Polymorphic Typing in FasterXML jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-16942](https://github.com/advisories/GHSA-mx7p-6679-8g3q): Polymorphic Typing in FasterXML jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-16943: jackson-databind polymorphic typing issue
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-16943](https://github.com/advisories/GHSA-fmmc-742q-jg75): jackson-databind polymorphic typing issue

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-17267: Improper Input Validation in jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-17267](https://github.com/advisories/GHSA-f3j5-rmmp-3fc5): Improper Input Validation in jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-17531: jackson-databind polymorphic typing issue
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-17531](https://github.com/advisories/GHSA-gjmw-vf9h-g25v): jackson-databind polymorphic typing issue

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2019-20330: Deserialization of Untrusted Data in jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2019-20330](https://github.com/advisories/GHSA-gww7-p5w4-wrfv): Deserialization of Untrusted Data in jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2020-1938: Improper Privilege Management in Tomcat
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2020-1938](https://github.com/advisories/GHSA-c9hw-wf7x-jp9j): Improper Privilege Management in Tomcat

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

### CVE-2020-8840: Deserialization of Untrusted Data in jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2020-8840](https://github.com/advisories/GHSA-4w82-r329-3q67): Deserialization of Untrusted Data in jackson-databind

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2020-9547: jackson-databind mishandles the interaction between serialization gadgets and typing
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2020-9547](https://github.com/advisories/GHSA-q93h-jc49-78gg): jackson-databind mishandles the interaction between serialization gadgets and typing

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2020-9548: jackson-databind mishandles the interaction between serialization gadgets and typing
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2020-9548](https://github.com/advisories/GHSA-p43x-xfjf-5jhr): jackson-databind mishandles the interaction between serialization gadgets and typing

Severity: CRITICAL

Affected dependencies:
  - com.fasterxml.jackson.core:jackson-databind:2.8.10 (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2022-22965: Remote Code Execution in Spring Framework
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:75

[CVE-2022-22965](https://github.com/advisories/GHSA-36p3-wjmg-h94x): Remote Code Execution in Spring Framework

Severity: CRITICAL

Affected dependencies:
  - org.springframework:spring-beans:4.3.13.RELEASE (declared at pom.xml:75)
  - org.springframework:spring-webmvc:4.3.13.RELEASE (declared at pom.xml:75)
  - org.springframework.boot:spring-boot-starter-web:1.5.9.RELEASE (declared at pom.xml:75)

Recommended fix:
  - Review advisory for patched versions

### CVE-2025-24813: Apache Tomcat: Potential RCE and/or information disclosure and/or information corruption with partial PUT
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2025-24813](https://github.com/advisories/GHSA-83qj-6fr2-vhqg): Apache Tomcat: Potential RCE and/or information disclosure and/or information corruption with partial PUT

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

### CVE-2026-41293: Apache Tomcat - HTTP/2 request headers not validated
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2026-41293](https://github.com/advisories/GHSA-r29c-68gh-xp6x): Apache Tomcat - HTTP/2 request headers not validated

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

### CVE-2026-43512: Apache Tomcat - Digest authenticator will authenticate any unknown user
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2026-43512](https://github.com/advisories/GHSA-h6fc-48rj-7qqh): Apache Tomcat - Digest authenticator will authenticate any unknown user

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

### CVE-2026-43515: Apache Tomcat - Security constraints not correctly applied
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml:83

[CVE-2026-43515](https://github.com/advisories/GHSA-5m62-pw8w-7w9f): Apache Tomcat - Security constraints not correctly applied

Severity: CRITICAL

Affected dependencies:
  - org.apache.tomcat.embed:tomcat-embed-core:8.5.23 (declared at pom.xml:83)

Recommended fix:
  - Review advisory for patched versions

## CWE Findings (Code-Level Vulnerabilities)

No CWE findings were reported.

# Axios SCA Scanner Test Fixtures

Run `npm audit` or point your SCA scanner at each `package.json` below.
Each folder is a self-contained fixture pinned to the **minimum version** needed to trigger that CVE group.

---

## CVE Coverage Map

| CVE | Severity | CVSS | Type | Fixture Folder | Vulnerable Pin | Fixed In |
|-----|----------|------|------|----------------|----------------|----------|
| CVE-2020-28168 | HIGH | 7.5 | SSRF | `legacy/` | `0.21.0` | 0.21.1 |
| CVE-2021-3749 | HIGH | 7.8 | ReDoS | `legacy/` | `0.21.0` | 0.21.2 |
| CVE-2023-45857 | MODERATE | 6.5 | CSRF / Token Leak | `v1-xsrf/` | `1.5.1` | 1.6.0 |
| CVE-2024-39338 | HIGH | 7.5 | SSRF | `v1-ssrf/` | `1.7.2` | 1.7.4 |
| CVE-2025-27152 | HIGH | — | SSRF + Cred Leak | `v1-ssrf2/` | `1.8.0` | 1.8.2 |
| CVE-2025-58754 | HIGH | — | DoS (stream) | `v1-ssrf2/` | `1.8.0` | 1.8.2 |
| CVE-2026-25639 | HIGH | — | Prototype Pollution / MitM | `v1-latest-unsafe/` | `1.14.0` | 1.15.0 |
| CVE-2025-62718 | MODERATE | — | SSRF (NO_PROXY bypass) | `v1-latest-unsafe/` | `1.14.0` | 1.15.0 |
| CVE-2026-40175 | MODERATE | — | Cloud Metadata Exfil | `v1-latest-unsafe/` | `1.14.0` | 1.15.0 |

> **CVE-2024-57965** — Disputed. NVD marks it as disputed; some parties say it was only a SAST warning message, not a true vulnerability. Your scanner may or may not surface it; do not treat it as a miss if it skips this one.

---

## Supply Chain Incident (Not a CVE)

| Versions | Date | What Happened |
|----------|------|---------------|
| `1.14.1`, `0.30.4` | March 31 2026 | Compromised via maintainer account takeover. Injected `plain-crypto-js` malicious dep with C2 second-stage payloads. Both yanked from npm. |

**Do not install these versions even in isolated environments.**

---

## How To Run

```bash
# Each folder independently
cd legacy && npm audit
cd ../v1-xsrf && npm audit
cd ../v1-ssrf && npm audit
cd ../v1-ssrf2 && npm audit
cd ../v1-latest-unsafe && npm audit
```

Or point your scanner binary at each `package.json` directly:

```bash
snyk test --file=legacy/package.json
trivy fs legacy/
```

---

## Safe Version (as of June 2026)

- **1.x branch:** `1.15.1`
- **0.x branch:** `0.31.1`

Anything below these has at least one unpatched CVE.

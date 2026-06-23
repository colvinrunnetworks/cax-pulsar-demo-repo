# MERIDIAN-GS — demonstration fixture (NON-FUNCTIONAL)

> ## ⚠️ READ FIRST — what this repository is and is not
>
> **This is a dead repository.** It contains **no runnable code, no services, no secrets, and no
> credentials.** It is a static set of dependency *manifests* — and nothing else — used solely as a
> target for the **COSMIC-AX PULSAR** continuous-monitoring demo.
>
> - **No active code.** There is no application, no entrypoint, no server, no script. The `.java`,
>   `.py`, `.js`, and `.go` directories contain only manifest files and inert placeholder notes.
> - **No build / install lifecycle.** `package.json` deliberately defines **no** scripts
>   (no `postinstall`, `prepare`, etc.). Nothing executes on clone, install, or build.
> - **No secrets, no credentials, no tokens.** Nothing here authenticates to, or can reach, any
>   other system or repository. There is no CI/CD, no GitHub Actions workflow, no `.env`.
> - **No lateral movement.** This repo is self-contained and isolated. It holds no references,
>   keys, or access paths to any Colvin Run / internal system. Compromising it gains an attacker
>   nothing beyond a list of old package versions that are already public knowledge.
> - **No CUI.** The system (MERIDIAN-GS) is **fictional**. All threat data is the public CISA KEV
>   catalog. Nothing here is sensitive.
>
> ### 🚫 Do NOT install or build the dependencies
> The dependency versions listed in these manifests are **intentionally outdated and known to be
> vulnerable** — that is the entire point of the fixture. **Do not run `npm install`,
> `pip install -r`, `go build`, or `mvn` against this repository.** Installing the listed packages
> would pull genuinely vulnerable code onto your machine. Treat the manifests as read-only data.

---

## Why this exists

[COSMIC-AX **PULSAR**](https://github.com/) is a mobile-first **continuous ATO (cATO)** demonstrator.
You point it at a system's software boundary; it intersects that boundary with the **live CISA Known
Exploited Vulnerabilities (KEV)** catalog and **OSV.dev** advisory data, then uses generative AI to
map each live threat to the affected **NIST 800-53 Rev 5** controls, score mission impact, and draft
remediation + a POA&M.

To demonstrate the "point it at a real repo and watch it light up" capability **without** exposing any
real system, PULSAR connects to **this** repository. Because the manifests pin deliberately old
package versions, the scan surfaces **real, publicly-documented CVEs in real packages** — including
one on the live CISA KEV catalog — so the demo is honest and independently verifiable, yet there is
nothing sensitive to protect.

## The fictional system

**MERIDIAN-GS** is a fictional USSF-style **satellite ground-segment** service — it receives operator
tasking orders, authenticates and schedules satellite contacts, and relays command uplinks to an
on-orbit asset. It slots into the same space-themed fiction as the rest of the PULSAR demo boundary
(ORION-GS, VANGUARD-C2, TELEMETRY-EDGE, ATLAS-DATALAKE). It does not correspond to any real system.

## Layout (manifests only)

```
meridian-gs/
├── tasking-engine/      pom.xml          Java — command scheduling      (Log4Shell family → CISA KEV)
├── telemetry-ingest/    requirements.txt Python — downlink ingest
├── operator-console/    package.json     Node — operator UI (no scripts)
└── contact-scheduler/   go.mod           Go — pass scheduling sidecar
```

## What PULSAR will report (verifiable)

Every finding below maps to a **real, public advisory** you can confirm at
[osv.dev](https://osv.dev) and [cisa.gov/known-exploited-vulnerabilities-catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog):

| Component | Pinned dependency | Surfaces | On CISA KEV? |
|---|---|---|---|
| tasking-engine | `org.apache.logging.log4j:log4j-core 2.14.1` | **Log4Shell family** (CVE-2021-44228 / **CVE-2021-45046**) | ✅ |
| tasking-engine | `org.apache.struts:struts2-core 2.5.10` | Apache Struts 2 RCE family | — |
| tasking-engine | `com.fasterxml.jackson.core:jackson-databind 2.9.8` | deserialization CVEs | — |
| telemetry-ingest | `requests 2.19.0`, `PyYAML 5.3`, `Jinja2 2.10`, `cryptography 2.3` | multiple OSV advisories | — |
| operator-console | `lodash 4.17.4`, `minimist 1.2.0`, `axios 0.21.0` | prototype-pollution / SSRF / ReDoS | — |
| contact-scheduler | `jwt-go 3.2.0`, `gorilla/websocket 1.4.0` | auth-bypass / DoS advisories | — |

The Log4j2 entry is the marquee: it is **on the live CISA KEV catalog**, so PULSAR's in-boundary KEV
indicator fires for real and an observer can verify it on stage.

---

*Colvin Run Networks · COSMIC-AX portfolio · demonstration artifact. Fictional system, public threat
data, no CUI.*

# Security policy

**This repository is a non-functional demonstration fixture. It contains no running code, no
services, no secrets, and no credentials.** It cannot be "exploited" in any meaningful sense and
has no network reach into any system.

## Intentionally outdated dependencies

The dependency manifests (`pom.xml`, `requirements.txt`, `package.json`, `go.mod`) pin **deliberately
old, known-vulnerable versions on purpose** — they are the demonstration payload for the COSMIC-AX
PULSAR continuous-monitoring demo. **Please do not report these as vulnerabilities; they are
expected.** Automated dependency scanners (Dependabot, etc.) should be disabled for this repo, since
every finding is intended.

## Do not install or build

Do **not** run `npm install`, `pip install`, `go build`, or `mvn` against this repository — doing so
would fetch genuinely vulnerable packages. The manifests are read-only data, not a project to build.

## No secrets / no lateral movement

There are no credentials, tokens, environment files, or CI/CD workflows in this repository, and no
references to any internal or Colvin Run system. Nothing here can be used to pivot anywhere else.

---
id: conventions
title: Naming and default conventions
type: rules
status: draft
---

# Naming and default conventions

- **Domains:** short name in tool calls (`production-domain`); full name in results (`PRODUCTION-DOMAIN.CYTIX.CLOUD`).
- **Services:** lowercase letters and digits, no spaces. Prefix related services with the system name (`fleet`, `fleetdispatch`, `fleetalerts`).
- **Defaults:** `xml: <config/>`, `timeout: 30`, a one-line `description` on every service.
- **Map IDs:** `<system>-<purpose>-map`, e.g. `fleet-demo-map`.
- **Production:** only changed on explicit request, using steps proven in the sandbox.
- TODO: user naming, maximum lengths, reserved names.

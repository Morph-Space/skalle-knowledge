---
id: verification-checklist
title: Verification checklist
type: testing
status: draft
---

# Verification checklist

Run after every build. A build passes only if every applicable line passes.

| Check | Tool | Pass when |
|---|---|---|
| Service exists on the right domain | get_domain_by_service | Returns `<DOMAIN>.<root>` |
| Ghost count | get_domain_resources | `instances` equals the expected count |
| Links | get_domain_resources | Source `linkedTo` contains every target, all `true` |
| Morphs | get_ghost_status | `Secondary Service` contains the source ghost |
| Read access | get_ghost_status | `Read Access` contains the user |
| No side effects | get_domain_resources | No other service changed between before and after |
| Data flow | TODO | TODO: how to prove data reached the target |

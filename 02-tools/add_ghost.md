---
id: tool-add_ghost
title: add_ghost
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_tools: [remove_ghost, get_resources]
---

# add_ghost

## Purpose
Adds a number of ghosts to a service.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| domain | string | yes | Short domain name. | `production-domain` |
| service | string | yes | Existing service. | `fleet` |
| quantity | integer | yes | Number of ghosts to add. | `6` |

## Effects
New ghosts get the next integer IDs (first batch on a new service: 1..quantity).

## Success response
```
Ghost memory allocation success
```

## How to verify
`get_domain_resources`: `instances` increases by `quantity`. `get_resources` lists the ghost IDs.

## Known issue
Once, while adding 5 ghosts to `ttservice`, `primarymorphed` also grew by 5. Cause not confirmed. See `06-troubleshooting/known-issues.md`.

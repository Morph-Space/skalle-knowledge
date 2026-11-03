---
id: tool-add_morphed_ghost
title: add_morphed_ghost
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_tools: [remove_morphed_ghost, get_ghost_status]
related_concepts: [concept-morphing]
---

# add_morphed_ghost

## Purpose
Morphs a ghost from a source service onto a second (target) service.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| refDomain | string | yes | Source domain. | `production-domain` |
| refService | string | yes | Source service. | `fleet` |
| refObjectId | string | yes | Source ghost ID. | `1` |
| ghostId | string | yes | Target ghost ID. | `1` |
| service | string | no | Target service. Default `<refService>morphed`, which must exist. | `fleetdispatch` |

## Effects
- **Allocates 5 new ghosts on the target service on every call** (confirmed).
- Target ghost gets `Secondary Service: {"<DOMAIN>/<REFSERVICE>/<ID>": true}`.

## Success response
```
Ghost successfully morphed on secondary service
```

## How to verify
`get_ghost_status(service=<target>, ghostId=<ghostId>)`.

## How to undo
`remove_morphed_ghost` with the same four IDs. Undo does not remove the 5 allocated ghosts.

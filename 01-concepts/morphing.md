---
id: concept-morphing
title: Morphing
type: concept
status: draft
last_verified: 2026-10-30
related_tools: [add_morphed_ghost, remove_morphed_ghost, get_ghost_status]
related_concepts: [ghost, linking]
---

# Morphing

## In one sentence
Morphing makes a ghost of service A also live on service B, so A's data reaches B transformed to B's data model.

## How it works
- Called with `add_morphed_ghost`. `refService`/`refObjectId` identify the source ghost; `service`/`ghostId` identify the target.
- If `service` is omitted the target defaults to `<refService>morphed` (e.g. `primarymorphed`), which must already exist.
- **Side effect (confirmed):** each call first allocates 5 new ghosts on the target service. Morphing 6 vehicles one by one leaves 30 ghosts on the target.
- Result on the target ghost: `Secondary Service: {"<DOMAIN>/<REFSERVICE>/<ID>": true}`.

## Morphing vs linking
| | Morphing | Linking |
|---|---|---|
| Set up by | Ghost owner (consumer view) | Service provider |
| Scope | One ghost | All ghosts of a service |
| Purpose | Send one user's data to another service | Integrate and transform data between services |

## Open questions (TODO)
- Is the 5-ghost allocation intended? Can the count be set?
- Where is the transformation from A's model to B's model defined?

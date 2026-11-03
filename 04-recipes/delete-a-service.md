---
id: recipe-delete-a-service
title: Delete a service safely
type: recipe
status: draft
last_verified: 2026-10-30
tools: [get_resources, get_ghost_status, remove_morphed_ghost, remove_ghost]
---

# Delete a service safely

## Steps
1. `get_domain_resources`: note links to and from the service.
2. `get_resources`: list its ghosts; note any `mapId`.
3. For each ghost, `get_ghost_status`: remove every morph with `remove_morphed_ghost`.
4. TODO: remove links pointing to it.
5. `remove_ghost` with `ghostId: 0` and the ghosts' `mapId` if they have one.
6. `get_domain_resources`: confirm the service is gone.

## Known problem
Step 5 failed for services whose ghosts had no map, and for empty services. See
`06-troubleshooting/known-issues.md` (KI-003). Until fixed, delete those in the Skalle console.

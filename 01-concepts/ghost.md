---
id: concept-ghost
title: Ghost
type: concept
status: draft
last_verified: 2026-10-30
related_tools: [add_ghost, remove_ghost, get_ghost_status, get_resources, set_map_id, send_data]
related_concepts: [service, morphing, linking]
---

# Ghost

## In one sentence
A ghost is one instance of a service, owned by a specific user, that a data source updates with live data.

## Why it exists
Every real or virtual thing (a sensor, a vehicle, a user) needs its own addressable place
in a service. The ghost is that place.

## How it works
- Ghosts are added to a service in batches with `add_ghost` (parameter `quantity`).
- Ghost IDs are integers starting at 1 per service (confirmed: 6 ghosts on `fleet` got IDs 1–6).
- A ghost's address is `<DOMAIN>.<root>/<SERVICE>/<ID>`, e.g. `PRODUCTION-DOMAIN.CYTIX.CLOUD/FLEET/1`.
- Data is sent to one ghost with `send_data` (JSON payload).
- A ghost can be morphed onto a second service (see `morphing.md`).

## Rules and limits
- Ghost ID `0` in `remove_ghost` means "the whole service", not ghost zero.
- TODO: maximum ghosts per service; are IDs reused after removal?

## How to check it
`get_ghost_status` returns `Linked To`, `Secondary Service`, `Read Access`, `Linked From`.
`get_domain_resources` shows the ghost count per service in `instances`.

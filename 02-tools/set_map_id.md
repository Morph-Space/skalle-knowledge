---
id: tool-set_map_id
title: set_map_id
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
---

# set_map_id

## Purpose
Assigns a ghost to a map. TODO: what a map represents.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| domain | string | yes | | `production-domain` |
| service | string | yes | | `fleet` |
| instance | integer | yes | Ghost ID. | `1` |
| mapId | string | yes | Free text? TODO. | `fleet-demo-map` |

## Success response
No output (empty) on success.

## Notes
Deleting a service whose ghosts are on a map worked only when that `mapId` was passed to `remove_ghost`.

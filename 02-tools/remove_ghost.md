---
id: tool-remove_ghost
title: remove_ghost
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_recipes: [delete-a-service]
---

# remove_ghost

## Purpose
Removes one ghost, or the whole service when `ghostId` is `0`.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| domain | string | yes | Short domain name. | `production-domain` |
| service | string | yes | | `fleet` |
| ghostId | integer | yes | Ghost ID, or `0` to delete the whole service. | `0` |
| mapId | string | no | Map the ghosts are on. | `fleet-demo-map` |

## Success responses
```
Successfully removed the whole service
```

## Errors
| Response | Seen when | Fix |
|---|---|---|
| `'remove_ghost' failed. See server logs.` | `ghostId 0` on a service whose ghosts are not on a map (`fleetdispatch`, 5 ghosts) and on an empty service (`fleetalerts`). Worked on `fleet` when `mapId` was given. | TODO: confirm cause from server logs. |

## Warning
Deleting a service cannot be undone. Remove morphs and links pointing to it first.

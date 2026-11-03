---
id: tool-send_data
title: send_data
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_formats: [payload-json]
---

# send_data

## Purpose
Sends a data payload to one ghost.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| domain | string | yes | | `production-domain` |
| service | string | yes | | `fleet` |
| instance | integer | yes | Ghost ID. | `1` |
| payload | object | yes | JSON. See `03-formats/payload-json.md`. | |

## Success response
No output (empty) on success.

## How to verify
TODO: no read tool shows ghost data yet. Is it visible through `channel_request`?

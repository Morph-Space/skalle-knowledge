---
id: tool-<tool_name>
title: <tool_name>
type: tool
writes_state: true                # true | false
status: todo                      # todo | draft | verified
last_verified: YYYY-MM-DD
related_tools: []
related_formats: []
---

# <tool_name>

## Purpose
<One sentence: what it does.>

## When to use it / when not to
- Use when: <...>
- Do not use when: <...>

## Parameters
| Name | Type | Required | Format and allowed values | Example |
|---|---|---|---|---|
| domain | string | yes | Short domain name, without root. | `production-domain` |
| root_domain | string | no | Defaults to `cytix.cloud`. | `cytix.cloud` |

## Before calling (preconditions)
- <What must already exist, e.g. "service must exist", "ghost must have no morphs".>

## What it changes (effects)
- <Every change, including side effects, e.g. "adds 5 ghosts to the target service".>

## Success response
```
<exact text or JSON returned>
```

## How to verify
<Read tool to call afterwards and what to expect in its output.>

## Errors
| Response | Cause | Fix |
|---|---|---|
| `'<tool>' failed. See server logs.` | <cause> | <fix> |

## How to undo
<Which tool reverses this, or "cannot be undone".>

## Example
```json
{ "domain": "sandbox", "service": "demo", "confirm": true }
```

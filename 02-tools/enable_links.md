---
id: tool-enable_links
title: enable_links
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_formats: [links-xml]
related_concepts: [concept-linking]
---

# enable_links

## Purpose
Links a source service to one or more target services.

## Parameters
| Name | Type | Required | Format | Example |
|---|---|---|---|---|
| domain | string | yes | Domain of the **source** service. | `production-domain` |
| service | string | yes | Source service. | `ffservice` |
| links_xml | string | yes | See `03-formats/links-xml.md`. | |

## Success response
```
Link allocation success
```

## How to verify
`get_domain_resources`: source shows `linkedTo: {"PRODUCTION-DOMAIN/TTSERVICE": true}`.
The target's `linkedFrom` stays `None` (confirmed; TODO: expected?).

## How to undo
TODO.

---
id: tool-create_service
title: create_service
type: tool
writes_state: true
status: draft
last_verified: 2026-10-30
related_tools: [update_service, remove_ghost, get_domain_by_service]
related_formats: [service-schema-xml]
---

# create_service

## Purpose
Creates a new service on a domain.

## Parameters
| Name | Type | Required | Format and allowed values | Example |
|---|---|---|---|---|
| domain | string | yes | Short domain name, without root. | `production-domain` |
| service | string | yes | Lowercase letters and digits. TODO: full naming rules. | `ttservice` |
| xml | string | yes | Service schema. See `03-formats/service-schema-xml.md`. | `<config/>` |
| timeout | number | no | Seconds. Default 30. | `30` |
| description, cmdXML, masterScript, preMasterScript, webjs | string | no | TODO | |

## Effects
Creates the service with 0 ghosts.

## Success response
```
Service created successfully
```

## How to verify
`get_domain_by_service(service_name)` returns `production-domain.cytix.cloud`.
`get_domain_resources` lists the service with `instances: '0'`.

## How to undo
`remove_ghost` with `ghostId: 0` (see that page; this does not always work).

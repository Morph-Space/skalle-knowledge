---
id: recipe-create-and-link-two-services
title: Create two services and link them
type: recipe
status: verified
last_verified: 2026-10-30
tools: [create_service, add_ghost, enable_links, get_domain_resources]
---

# Create two services and link them

## Inputs needed from the user
Domain, source service name, target service name, number of ghosts on the target.

## Steps
| # | Tool | Parameters | Expected response | Verify with |
|---|---|---|---|---|
| 1 | create_service | domain, service=`<target>`, xml=`<config/>` | `Service created successfully` | get_domain_by_service |
| 2 | add_ghost | domain, service=`<target>`, quantity=N | `Ghost memory allocation success` | get_domain_resources: instances = N |
| 3 | create_service | domain, service=`<source>`, xml=`<config/>` | `Service created successfully` | get_domain_by_service |
| 4 | enable_links | domain, service=`<source>`, links_xml (see `03-formats/links-xml.md`) | `Link allocation success` | get_domain_resources |

## Final check
Source shows `linkedTo: {"<DOMAIN>/<TARGET>": true}`; target shows `instances: N`.

## Rollback
Delete the source, then the target (see `delete-a-service.md`).

---
id: format-service-schema-xml
title: Service schema (xml)
type: format
status: todo
used_by_tools: [create_service, update_service]
---

# Service schema (`xml` parameter)

## Known so far
- Minimal value used successfully: `<config/>`.
- The PDF says links are defined inside the schema at element level, so this schema
  describes the service's data elements.

## TODO for the platform team
- Full structure: how to declare data fields (names, types, units).
- How links are declared per element, and how this relates to `enable_links`.
- How a field is mapped (normalized) from a linked service's model.
- A realistic example, e.g. for a vehicle: `vehicleId`, `lat`, `lng`, `speed`, `status`.

---
id: format-normalizer
title: Normalizer format (field mapping)
type: format
status: todo                      # Where and how mappings are written is still unknown
last_verified: 2026-11-20
used_by_tools: [enable_links]     # TODO: possibly also create_service / update_service (schema or masterScript)
related_concepts: [normalizer]
---

# Normalizer format (field mapping)

Concept page: `01-concepts/normalizer.md`.

## What it is for
Describes how fields of a linked (source) service's messages are mapped to fields of the
receiving service's `<rtw>` schema, e.g. `spd` → `speed`.

## Language / encoding
Unknown. The mapping is documented as defined by the service provider inside the schema, at the
level of individual fields. Candidate locations, none confirmed:
- the service schema (`xml` parameter, `03-formats/service-schema-xml.md`)
- `links_xml` (`03-formats/links-xml.md`)
- `masterScript` / `preMasterScript` (`03-formats/master-script.md`)

## Full structure
What is known are the two ends of the mapping; the mapping itself is TODO.

Source and target are both `<rtw>` schemas: six standard fields, then one empty element per
custom field. Fields are untyped; lists are not supported (use JSON strings).

```xml
<!-- Target service schema (fitness tracking) -->
<rtw>
  <receiver></receiver>   <!-- standard; meaning unconfirmed -->
  <payload></payload>     <!-- standard -->
  <sender></sender>       <!-- standard -->
  <refid></refid>         <!-- standard -->
  <timestamp></timestamp> <!-- standard -->
  <topic></topic>         <!-- standard -->
  <speed></speed>         <!-- custom: target of mapping from source `spd` -->
  <distance></distance>
  <heartrate></heartrate>
  <calories></calories>
</rtw>
<!-- TODO: how a field declares its source (e.g. an attribute on <speed>?) -->
```

## Elements and attributes
| Element / attribute | Required | Type | Meaning | Allowed values |
|---|---|---|---|---|
| Source field | — | untyped | Field name in the linked service's schema | Any custom field |
| Target field | — | untyped | Field name in the receiving service's schema | Any custom field |
| Mapping declaration | TODO | TODO | Ties source to target | TODO |
| Transformation (units, computed values) | TODO | TODO | Whether supported is unknown | TODO |

## Inputs and outputs
- **Input:** a message sent (`send_data`) to a ghost of the source service, in the source schema.
- **Output:** the same message, reshaped to the target schema, delivered to the target service
  (and its `webjs` `onMessage`).
- Nothing is stored; each message is normalized as it passes.

## Minimal valid example
```text
TODO: unknown. Intended effect: source { "spd": 32.5 } → target { "speed": 32.5 }
```

## Full realistic example
```text
TODO: unknown. Intended effect:
source (vehicle) { "spd": 32.5, "dist": 4.2 }
→ target (fitness) { "speed": 32.5, "distance": 4.2 }
```

## Common mistakes
- Expecting typed conversion: fields are untyped.
- Mapping a list field directly: lists are not supported; send a JSON string.
- Assuming delivery works: tests so far show the link on the source (`linkedTo`) but an empty
  `linkedFrom` on the target, and delivery is unconfirmed.

## Validation
TODO. Until the format is known: after linking, `send_data` to a source ghost and check that the
target's `webjs` receives the target field names.

## Open questions (TODO)
- Where mapping rules are written, and their syntax (questions doc Q4.5).
- Does link data reach the target at all (Q4.4)?
- Unmapped fields: dropped or passed through?
- Are unit conversions or computed fields supported?

Sources: MorphSpace knowledge base (20 Nov 2026), `linking.md`, `service-schema-xml.md`.

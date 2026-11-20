---
id: concept-normalizer
title: Normalizer
type: concept
status: draft                     # Documented in Skalle docs; not confirmed by the inventor or tested
last_verified: 2026-11-20
related_tools: [enable_links, add_morphed_ghost, create_service, update_service]
related_concepts: [linking, morphing, service, ghost]
related_formats: [format-normalizer, format-service-schema-xml, format-links-xml, format-master-script]
---

# Normalizer

## In one sentence
Normalizing converts data that arrives through a link so it fits the receiving service's own data model, for example mapping one service's `spd` field to another's `speed`.

## Why it exists
Services are built by different providers, each with its own schema (field names and meaning).
A link only moves the data; without normalizing, the receiving service would get fields it
does not know. Normalizing lets a service consume another service's data in its own terms.

## How it works
- A link is created on the **source** service with `enable_links` (see `linking.md`).
- Messages sent to source ghosts are meant to reach the target service through that link.
- On the way, the fields are reshaped to match the target service's `<rtw>` schema
  (see `03-formats/service-schema-xml.md`).
- Links, and so the mapping, are defined by the service provider inside the schema, at the
  level of individual fields; a service can have several links.
- Unclear: where the mapping rules are actually written. Candidates: the service schema
  (`xml`), `links_xml`, or `masterScript` / `preMasterScript`.

## Rules and limits
- Applies at service level: every ghost of a linked service is normalized the same way.
- The platform does not store data, so normalizing works on each message as it passes;
  there is no stored state to re-normalize after a schema change.
- Schema fields are untyped and lists are not supported; structured values travel as JSON strings,
  so a mapping can only rename or reshape fields, not rely on declared types.
- TODO: can a mapping convert units or compute values, or only rename fields?

## How it relates to other concepts
- **Linking** moves the data between services; **normalizing** reshapes it.
- **Morphing** does the same conversion, but for a single ghost instead of a whole service.
- **masterScript / preMasterScript** are the likely place for platform-side processing,
  so they may be where normalizing logic runs (unconfirmed).

## Example
Illustrative only; the mapping syntax is unknown.

A vehicle service sends `spd` and `dist`. A fitness-tracking service with schema fields
`speed`, `distance`, `heartrate`, `calories` links to it:

| Source field (vehicle) | Target field (fitness) |
|---|---|
| `spd` | `speed` |
| `dist` | `distance` |

1. `enable_links` on the vehicle service with `links_xml` naming `production-domain/<fitness service>`.
2. TODO: define the field mapping (location unknown).
3. `send_data` to a vehicle ghost; the fitness service's `webjs` should receive `speed` and `distance`.

## How to check it
- `get_domain_resources` on the source shows `linkedTo: {"PRODUCTION-DOMAIN/TARGET": true}`.
- In tests the target's `linkedFrom` stayed empty, and it is not yet confirmed that data
  reaches the target at all.
- TODO: once delivery works, check the target's `webjs` `onMessage` receives the mapped field names.

## Open questions (TODO)
- Where are mapping rules written: schema, `links_xml`, or a script? (questions doc Q4.5)
- Does link data really reach the target, and in what form? (Q4.4)
- Can one source field map to several target fields, or several to one?
- What happens to source fields with no mapping: dropped or passed through?

Sources: MorphSpace knowledge base (20 Nov 2026), `linking.md`, `glossary.md`.

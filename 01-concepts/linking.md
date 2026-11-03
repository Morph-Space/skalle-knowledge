---
id: concept-linking
title: Linking and normalizing
type: concept
status: draft
last_verified: 2026-10-30
related_tools: [enable_links, get_domain_resources]
related_concepts: [morphing, service]
---

# Linking and normalizing

## In one sentence
A link is a service-level connection from one service to another; normalizing is transforming the linked data to fit the local data model.

## How it works
- Created with `enable_links` on the **source** service; the target goes in `links_xml` (see `03-formats/links-xml.md`).
- Recorded on the source service as `linkedTo: {"PRODUCTION-DOMAIN/TTSERVICE": true}`.
- The PDF says links are defined inside the data schema at element level, and a service can have several links.

## Rules and limits
- Confirmed: the target's `linkedFrom` stays `None` after linking. TODO: is that expected?
- TODO: how to remove or deactivate a link (`<active>false</active>`?).
- TODO: does data sent to the source actually reach the target, and in what form?

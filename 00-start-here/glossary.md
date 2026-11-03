---
id: glossary
title: Glossary
type: concept-index
status: draft
---

# Glossary

Short definitions. Each term with a page in `01-concepts/` links to it.
Terms marked TODO need a definition from the platform team.

| Term | Definition | Page |
|---|---|---|
| Real Time Web (RTW) | A network for live data where sources are addressed directly instead of being copied into databases. | PDF |
| Morph Space | A private RTW address space for one root domain, containing Synx tools and services. | PDF |
| Root domain | The top domain of a Morph Space, e.g. `cytix.cloud`. | — |
| Domain | A domain under the root domain, e.g. `production-domain` → `production-domain.cytix.cloud`. | — |
| Service (morphic service) | A named unit on a domain that holds ghosts and has a schema. | — |
| Node | A service used as a node in a neural-net-style topology. Disables micropage functionality. | PDF |
| Ghost | An instance of a service, owned by a specific user. Data sources (e.g. sensors) update their ghost. | `01-concepts/ghost.md` |
| Morphing (ghost) | Making a ghost from service A also exist on service B, so A's data reaches B transformed to B's data model. | `01-concepts/morphing.md` |
| Link | A connection set up by the service provider from one service to another, defined inside the schema at element level. Applies to all ghosts. | `01-concepts/linking.md` |
| Normalize | Linking to a secondary service and transforming its data to fit the local data model. | `01-concepts/linking.md` |
| Map ID | TODO: what a map is and what assigning a ghost to one does. | — |
| Limbo | State of a ghost whose ownership change is waiting to be confirmed or denied. | — |
| Data Channel | A live, personal stream of data assembled from several sources. | PDF |
| Kernelizer | An empty client that receives and runs its program from the network at connect time. | PDF |
| Synx Pass | The shared identity service used across Morph Spaces. | PDF |
| Synx DNS / Synx BIOS | TODO | — |
| Micropage | TODO | — |
| cmdXML | TODO: command schema of a service. | `03-formats/cmd-xml.md` |
| masterScript / preMasterScript | TODO | `03-formats/master-script.md` |
| webjs | TODO | — |

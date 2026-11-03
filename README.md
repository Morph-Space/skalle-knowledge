---
id: readme
title: Skalle / MorphSpace knowledge base — start here
type: index
status: verified
---

# Skalle / MorphSpace knowledge base

This repository teaches an AI agent (and humans) how to build, change, test and fix
systems on MorphSpace through the Skalle MCP server.

## How an AI agent should use this knowledge base

1. Read `00-start-here/agent-operating-rules.md` before calling any tool that changes state.
2. Look up unfamiliar terms in `00-start-here/glossary.md`.
3. Before calling a tool, read its page in `02-tools/`. Never guess a parameter format.
4. For any XML, JSON or script value, use the exact format in `03-formats/`.
5. For a multi-step task, follow a recipe in `04-recipes/`. To build a whole system, start from a blueprint in `05-blueprints/`.
6. When something fails, search `06-troubleshooting/` for the error message.
7. After building, run the checks in `07-testing/`.

If a page has `status: todo` or `status: draft`, treat its content as unconfirmed. Test it in the
sandbox domain first, and report what you find.

## Map

| Folder | Contains | Answers the question |
|---|---|---|
| `00-start-here/` | Operating rules, glossary | How should I behave? What do words mean? |
| `01-concepts/` | One page per concept | What is a ghost, a link, a morph? |
| `02-tools/` | One page per MCP tool | Exactly how do I call this tool, and what happens? |
| `03-formats/` | XML, JSON and script formats | What goes inside `xml`, `links_xml`, `cmdXML`, payloads? |
| `04-recipes/` | Step-by-step tasks | How do I do X correctly from start to finish? |
| `05-blueprints/` | Whole-system designs | What does a complete working system look like? |
| `06-troubleshooting/` | Errors and known issues | Why did this fail, and how do I fix it? |
| `07-testing/` | Sandbox, checks, test cases | How do I prove it works? |
| `99-meta/` | Conventions, contributing guide | How are names chosen? How do I write a page? |

Background and vision: `Morph Space-info.pdf`.

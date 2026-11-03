---
id: knowledge-plan
title: Knowledge base plan
type: plan
status: verified
---

# Knowledge base plan

## Goal

An AI agent, given only this repository and the Skalle MCP tools, can build, test, fix and
tear down a MorphSpace system with no guessed parameters and no human help beyond approval.

**Done when:** the agent passes every test in `07-testing/test-cases/` in the sandbox, three runs
in a row, without stopping to ask about an undocumented format.

## What the AI needs to know, by priority

| Priority | Knowledge | Where | Why it matters |
|---|---|---|---|
| 1 | Exact behavior of each of the 29 tools | `02-tools/` | Every action goes through a tool; one wrong parameter breaks a build. |
| 2 | Formats: schema XML, links XML, cmdXML, scripts, payloads | `03-formats/` | The agent cannot invent XML; this is where it got stuck before. |
| 3 | Operating rules and conventions | `00-start-here/`, `99-meta/` | Keeps production safe and makes results consistent. |
| 4 | Errors and known issues | `06-troubleshooting/` | Lets the agent fix problems instead of retrying blindly. |
| 5 | Recipes and blueprints | `04-recipes/`, `05-blueprints/` | Turns single tools into working systems. |
| 6 | Concepts | `01-concepts/`, glossary | Lets the agent design sensible systems from a user's goal. |
| 7 | Tests and verification | `07-testing/` | Proves the result, and proves the knowledge base is correct. |

## Phase 1: GitHub knowledge base (now)

### Step 1: Sandbox and rules (day 1)
- Create the `sandbox` domain with `manage_domain`; fill in `07-testing/sandbox-domain.md`.
- Review `agent-operating-rules.md` and `conventions.md`.

### Step 2: Tool reference (week 1, highest value)
- One page per tool from `02-tools/_TEMPLATE-tool.md`. Seven drafts already exist.
- For each tool, run it in the sandbox and record the exact response, effects and errors.
- Update `02-tools/INDEX.md` as pages become `verified`.

### Step 3: Formats (week 1–2)
- The platform team fills in `service-schema-xml.md`, `cmd-xml.md`, `master-script.md`.
- Each needs a full structure, a minimal example and a realistic example.

### Step 4: Troubleshooting (ongoing)
- Resolve KI-001 to KI-005 with the server logs.
- Add a table of every error string the server can return, with cause and fix.

### Step 5: Recipes, blueprints, tests (week 2–3)
- One recipe per common task (create, link, morph, share access, transfer ownership, delete).
- One blueprint per demo (fleet tracker, digital twin, IoT alerts).
- One test case per recipe and blueprint.

### Step 6: Connect to search_knowledge
The Skalle MCP server's knowledge base is currently empty. To feed it from this repo:
- On every push to `main`, a GitHub Action (or webhook) tells the server to re-import the repo.
- The server splits each Markdown file by `##` heading, keeps the frontmatter, and indexes
  `id` as `doc_id` and `title` as the title for `list_documents` and `read_document`.
- Also index `.yaml` blueprints and tests as whole documents.

### Step 7: The fix-and-learn loop
- When the agent finds behavior not in the knowledge base, it records it as a `KI-` entry and
  opens a pull request (needs a GitHub connector or token with write access).
- A person reviews and merges. The knowledge base improves with every run.

## Phase 2: Claude skill (later)

The folder layout is designed so the switch is mostly renaming.

```
skalle-morphspace/
├── SKILL.md               ← from README.md + agent-operating-rules.md (under 500 lines)
├── references/            ← 01-concepts, 02-tools, 03-formats, 06-troubleshooting, 99-meta
├── assets/blueprints/     ← 05-blueprints
├── evals/                 ← 07-testing/test-cases
└── scripts/
    ├── validate_xml.py    ← checks XML against 03-formats before sending
    └── verify_state.py    ← runs the verification checklist
```

Steps:
1. Write `SKILL.md` frontmatter. The `description` decides when Claude uses the skill, so make it broad:
   "Build, change, test and fix systems on MorphSpace with the Skalle MCP tools. Use whenever the user
   mentions MorphSpace, Skalle, ghosts, services, morphing, links or Real Time Web, even if they do not ask for a skill."
2. Body: operating rules, the build loop, and a table telling Claude which reference file to read for which task.
3. Turn the test cases into evals and measure how often Claude builds each blueprint correctly.
4. Keep the GitHub repo as the source; regenerate the skill from it with a script, so there is only one place to edit.
5. Use in Claude Code, the Agent SDK, or upload to claude.ai.

Running both at once is fine: the skill gives Claude the rules and structure up front,
and `search_knowledge` still finds detailed pages on demand.

## Who does what

| Task | Owner |
|---|---|
| Formats, intended behavior, error causes | Platform team |
| Testing tools in the sandbox, drafting tool pages | AI agent (reviewed by a person) |
| Reviewing and merging pull requests | Platform team |
| Sync to search_knowledge | Skalle server developer |
| Skill packaging and evals | AI agent with skill-creator |

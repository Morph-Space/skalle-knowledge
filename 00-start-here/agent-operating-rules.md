---
id: agent-operating-rules
title: Operating rules for AI agents
type: rules
status: verified
---

# Operating rules for AI agents

These rules apply to every task. They exist because state-changing tools act on live
infrastructure and several tools have side effects that are not obvious from their names.

## 1. Work in the sandbox first

Build and test every new system in the sandbox domain (see `07-testing/sandbox-domain.md`).
Only touch `production-domain` when the user explicitly asks, and only with steps already proven in the sandbox.

## 2. Follow the build loop for every change

1. **Read**: check current state (`get_domain_resources`, `get_resources`, `get_ghost_status`).
2. **Plan**: list every tool call with its exact parameters.
3. **Check the knowledge base**: every parameter must come from a `02-tools/` or `03-formats/` page. If a page is missing or `todo`, stop and say so.
4. **Dry run**: call each write tool without `confirm=true`.
5. **Approve**: show the plan to the user. In production, wait for explicit approval.
6. **Apply**: call with `confirm=true`, one step at a time.
7. **Verify**: after each step, read state again and compare with the expected result in the tool page.
8. **Record**: if a tool behaved differently from its page, add the finding to `06-troubleshooting/known-issues.md`.

## 3. Stop instead of guessing

Stop and ask the user when:
- a parameter format is not documented,
- a tool returns an error with no documented cause,
- a step changes more than its page says it should (for example, extra ghosts appear),
- a delete or ownership change is involved and the user has not named the exact target.

Do not retry a failing write with guessed parameters more than once in production.

## 4. Never assume the result

A success message is not proof. Always confirm with a read tool.

## 5. Order matters when removing things

Remove dependent items first: morphed ghosts and links before the services they point to.
See `04-recipes/delete-a-service.md`.

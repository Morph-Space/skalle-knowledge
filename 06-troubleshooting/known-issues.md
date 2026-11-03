---
id: known-issues
title: Known issues and error messages
type: troubleshooting
status: verified
last_verified: 2026-10-30
---

# Known issues and error messages

Search this page for the exact error text. New findings use `_TEMPLATE-issue.md`.

## KI-001: add_morphed_ghost allocates 5 ghosts on every call
- **Status:** open (by design?)
- **Tool:** add_morphed_ghost
- **Seen when:** morphing `fleet/1` onto `fleetdispatch` added 5 ghosts to `fleetdispatch`.
- **Workaround:** morph as few ghosts as possible; plan target sizes as 5 × number of morph calls.

## KI-002: Unexpected ghost growth on primarymorphed
- **Status:** open
- **Seen when:** `primarymorphed` went from 30 to 35 around an `add_ghost` call on `ttservice`.
- **Cause:** unknown; possibly a morph by someone else (see KI-001).

## KI-003: remove_ghost with ghostId 0 fails
- **Status:** open
- **Tool:** remove_ghost
- **Exact response:** `'remove_ghost' failed. See server logs.`
- **Seen when:** deleting `fleetdispatch` (5 ghosts, no map) and `fleetalerts` (0 ghosts), with or without `mapId`. Deleting `fleet` worked with `mapId: fleet-demo-map`.
- **Workaround:** delete in the Skalle console. Check server logs for the real cause.

## KI-004: linkedFrom not updated on link target
- **Status:** open
- **Tool:** enable_links
- **Seen when:** after linking `ffservice → ttservice`, `ttservice.linkedFrom` stayed `None`.

## KI-005: Dry runs give no detail
- **Status:** open
- **Tool:** all write tools
- **Seen when:** a call without `confirm=true` returns only "not executed", not what would happen.
- **Workaround:** use the tool page's "Effects" section to predict changes.

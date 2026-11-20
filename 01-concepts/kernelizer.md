---
id: concept-kernelizer
title: Kernelizer
type: concept
status: draft                     # Kernelizer itself is Documented; webjs details are Confirmed by the inventor
last_verified: 2026-11-20
related_tools: [create_service, update_service]
related_concepts: [service, ghost, micropage, webjs]
related_formats: [format-kernelizer]
---

# Kernelizer

## In one sentence
The Kernelizer is an empty client that downloads and runs its program (the service's `webjs`) from the network when it connects.

## Why it exists
It removes app deployment. The app's UI is stored on the service and sent to the client at
connect time, so publishing a change is just updating the service; there is nothing to
build, install or ship to users.

## How it works
1. The service holds its UI in the `webjs` field: one string of HTML with inline CSS and an
   inline `<script>` (see `03-formats/kernelizer.md`).
2. A user opens the app; the empty client (Kernelizer) connects and receives that `webjs`.
3. The script registers `window.__WEBJS__.onMessage(msg)`.
4. The platform calls `onMessage` for every incoming message on the Data Channel; data
   fields are in `msg.rtw[0]` (or in `msg` itself).
5. To change the app, call `update_service` with new `webjs`; the next connect loads it.

## Rules and limits
- Everything must be inline: no external libraries, images or fonts. (Confirmed)
- Runs in mobile and desktop browsers. (Confirmed)
- The platform does not store data. A client that reloads starts empty and only sees new
  messages, so any state (e.g. a game board) must travel in each message or be kept by clients.
- Logic in `webjs` runs in the browser and can be modified by the user; anything that must be
  trusted needs platform-side processing (masterScript, unconfirmed).
- Unclear: the URL a user opens to start an app.
- Unclear: how `webjs` sends data or commands back to a ghost.

## How it relates to other concepts
- **Service:** the Kernelizer loads one service's `webjs`.
- **Ghost / Data Channel:** messages sent to ghosts with `send_data` arrive in `onMessage`.
- **Micropage:** a separate HTML page that shows information about a service.
- **cmdXML:** may be the intended way for a UI to send actions (unconfirmed).

## Example
1. `create_service` with a schema containing `speed`, `distance`, `heartrate`, and a `webjs`
   that registers `onMessage` and updates elements by ID (full example in `03-formats/kernelizer.md`).
2. Open the app through the Kernelizer (URL TODO).
3. `send_data` to ghost 1 with `{"speed": 32.5, "distance": 4.2, "heartrate": 150}`;
   the page updates live.
4. `update_service` with changed `webjs`; reconnect to see the new UI.

## How to check it
- Open the app and confirm the UI renders with no network errors for external resources.
- Send a message with `send_data` and confirm the values appear (i.e. `onMessage` fired).
- TODO: which read tool shows a service's current `webjs`.

## Open questions (TODO)
- The URL that opens an app through the Kernelizer (questions doc Q1.3, pending).
- How `webjs` sends data or commands to a ghost (next to Q1.2 and Q3.7).
- How `webjs` knows the current user / player identity (Q5.1–Q5.4).
- Size limit of `webjs`; how to debug it and where logs go (Q6.1–Q6.3).

Sources: MorphSpace knowledge base (20 Nov 2026), inventor answers in the questions doc, `glossary.md`.

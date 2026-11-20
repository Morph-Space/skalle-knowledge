---
id: format-kernelizer
title: Kernelizer format (webjs)
type: format
status: draft                     # Structure and rules confirmed by the inventor; send path still unknown
last_verified: 2026-11-20
used_by_tools: [create_service, update_service]
related_concepts: [kernelizer]
---

# Kernelizer format (`webjs`)

Concept page: `01-concepts/kernelizer.md`.

## What it is for
The `webjs` field of a service (set with `create_service`, changed with `update_service`) holds
the program the Kernelizer downloads and runs when a client connects. It is the service's UI.

## Language / encoding
- One string of HTML, with inline CSS (`style` attributes or `<style>`) and one inline `<script>`.
- No external libraries, images or fonts: everything must be inline.
- Runs in mobile and desktop browsers.
- TODO: maximum size; escaping rules when passing the string through the tool.

## Full structure
```html
<!-- 1. Markup, drawn once. Give every value you update an id. -->
<div style="...">
  <span id="field1">--</span>
</div>

<!-- 2. One inline script -->
<script>
(function () {
  window.__WEBJS__ = window.__WEBJS__ || {};          // namespace provided/used by the platform
  // Called by the platform for every incoming message
  window.__WEBJS__.onMessage = function (msg) {
    var d = (msg && msg.rtw && msg.rtw[0]) || msg;    // data fields
    if (!d) return;
    // read d.<field>, update elements by id
  };
  // TODO: how to send data / commands back to a ghost (unknown)
})();
</script>
```

## Elements and attributes
| Element / attribute | Required | Type | Meaning | Allowed values |
|---|---|---|---|---|
| HTML markup | yes | HTML | The visible UI | Inline only; no external `src`/`href` |
| `<script>` | yes | JavaScript | App logic | Inline only |
| `window.__WEBJS__` | yes | object | Namespace the platform uses to reach the app | Create if missing |
| `window.__WEBJS__.onMessage(msg)` | yes | function | Called for every incoming message | — |
| `msg.rtw[0]` | — | object | Data fields of the message, named as in the service's `<rtw>` schema | Fall back to `msg` if absent |
| Field values | — | untyped | Values of schema fields | Lists arrive as JSON strings; parse with `JSON.parse` |

## Inputs and outputs
- **Input:** messages sent to the service's ghosts (`send_data`) arrive on the Data Channel and
  are passed to `onMessage`. Field names match the service schema (`03-formats/service-schema-xml.md`).
- **Output:** the rendered page. Sending data back is not documented yet.
- **State:** the platform stores nothing; on reload the page starts empty until the next message.

## Minimal valid example
```html
<div>Speed: <span id="speed">--</span></div>
<script>
(function () {
  window.__WEBJS__ = window.__WEBJS__ || {};
  window.__WEBJS__.onMessage = function (msg) {
    var d = (msg && msg.rtw && msg.rtw[0]) || msg;
    if (d && d.speed != null) document.getElementById('speed').textContent = d.speed;
  };
})();
</script>
```

## Full realistic example
The inventor's example: shows values from incoming messages and computes a risk score in the
browser. Stored in the service as one string.

```html
<div style="display:flex;justify-content:center;align-items:center;height:100vh;background:linear-gradient(135deg,#1E3C72,#2A5298);font-family:Arial,sans-serif;">
  <div style="background:#ffffff10;padding:30px 40px;border-radius:20px;width:360px;color:#fff;">
    <h2 style="text-align:center;">Insurance Risk Profile</h2>
    <div>Current Speed: <b><span id="speed">--</span> km/h</b></div>
    <div>Total Distance: <b><span id="distance">--</span> km</b></div>
    <div>Heart Rate: <b><span id="hr">--</span> bpm</b></div>
    <div>Risk Score: <b><span id="risk">--</span></b></div>
    <div>Safety Level: <b><span id="safety">--</span></b></div>
  </div>
</div>
<script>
(function () {
  window.__WEBJS__ = window.__WEBJS__ || {};
  window.__WEBJS__.onMessage = function (msg) {
    var d = (msg && msg.rtw && msg.rtw[0]) || msg;
    if (!d) return;
    var riskScore = 0;
    if (typeof d.speed === 'number') {
      document.getElementById('speed').textContent = d.speed.toFixed(1);
      if (d.speed > 35) riskScore += 2;
    }
    if (typeof d.distance === 'number')
      document.getElementById('distance').textContent = d.distance.toFixed(2);
    if (typeof d.heartrate === 'number') {
      document.getElementById('hr').textContent = d.heartrate.toFixed(0);
      if (d.heartrate > 170) riskScore += 1;
    }
    var safety = riskScore === 0 ? 'High' : riskScore === 1 ? 'Medium' : 'Low';
    document.getElementById('risk').textContent = riskScore;
    document.getElementById('safety').textContent = safety;
  };
})();
</script>
```

Pattern to reuse: draw the HTML once, register `window.__WEBJS__.onMessage`, read fields from
`msg.rtw[0]`, update elements by ID.

## Common mistakes
- Loading a library, image or font from a URL: not allowed; inline it (e.g. SVG, data in script).
- Reading only `msg.rtw[0]`: fall back to `msg` itself.
- Assuming field types: fields are untyped; check with `typeof` and parse JSON-string lists.
- Expecting state after reload: nothing is stored; re-send state or keep it in each message.
- Putting trusted rules (e.g. move validation) only in `webjs`: a modified client can bypass them.

## Validation
- No `src=`/`href=` pointing outside the page; no `<link rel="stylesheet">`.
- Script defines `window.__WEBJS__.onMessage`.
- Every element ID used in the script exists in the markup.
- Test: `update_service`, open the app, `send_data` to a ghost, confirm the UI updates.

## Open questions (TODO)
- How `webjs` sends data or commands to a ghost.
- The URL that opens the app through the Kernelizer.
- How the UI learns the current user's identity.
- Maximum `webjs` size; debugging and logs.

Sources: MorphSpace knowledge base (20 Nov 2026), inventor's example in the questions doc.

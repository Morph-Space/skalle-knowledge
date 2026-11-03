---
id: format-payload-json
title: send_data payload
type: format
status: draft
used_by_tools: [send_data]
---

# send_data payload

Payloads are JSON objects. Keep field names consistent with the service schema.

## Example (vehicle)
```json
{ "vehicleId": "VAN-01", "lat": 59.9139, "lng": 10.7522, "speed": 42,
  "heading": 90, "status": "en_route", "ts": "2026-10-30T10:00:00Z" }
```

## TODO
- Is the payload validated against the service schema?
- Size limit and rate limit?

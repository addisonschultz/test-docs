---
description: Send your first notification in about five minutes.
icon: bolt
---

# Quickstart

Get up and running with Relay in a few minutes.

{% stepper %}
{% step %}
## Create an account

Sign up at `https://relay.example.com/signup` and create a project. Each project gets its own API key.
{% endstep %}

{% step %}
## Install the SDK

```bash
npm install @relay/sdk
```
{% endstep %}

{% step %}
## Send a notification

```javascript
import { Relay } from "@relay/sdk";

const relay = new Relay({ apiKey: "rl_live_abc123..." });

await relay.notifications.send({
  to: "jane@example.com",
  channel: "email",
  template: "welcome",
  data: { firstName: "Jane" },
});
```
{% endstep %}

{% step %}
## Check delivery status

```bash
curl https://api.relay.example.com/v1/notifications/ntf_9f8a7b/status \
  -H "Authorization: Bearer rl_live_abc123..."
```

```json
{
  "id": "ntf_9f8a7b",
  "status": "delivered",
  "channel": "email",
  "delivered_at": "2026-06-30T18:22:10Z"
}
```
{% endstep %}
{% endstepper %}

Next: set up [authentication](authentication.md) properly for production, or explore the full [API reference](api-reference.md).

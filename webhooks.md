---
description: Subscribe to delivery events instead of polling.
icon: webhook
---

# Webhooks

Subscribe to delivery events instead of polling the status endpoint.

## Setting up a webhook

Add an endpoint URL in **Project Settings > Webhooks**. Relay will POST an event payload whenever a notification changes state.

## Event types

- `notification.sent`
- `notification.delivered`
- `notification.failed`
- `notification.bounced`

## Payload example

```json
{
  "event": "notification.delivered",
  "data": {
    "id": "ntf_9f8a7b",
    "channel": "email",
    "delivered_at": "2026-06-30T18:22:10Z"
  }
}
```

## Verifying webhook signatures

Each request includes an `X-Relay-Signature` header. Verify it against your signing secret before trusting the payload:

```javascript
const isValid = relay.webhooks.verify(payload, signature, signingSecret);
```

## Retries

{% hint style="info" %}
If your endpoint doesn't return a `2xx` response, Relay retries with exponential backoff: 1m, 5m, 30m, 2h, then gives up after 4 attempts.
{% endhint %}

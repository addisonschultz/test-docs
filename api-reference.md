# API Reference

Base URL: `https://api.relay.example.com/v1`

## Send a notification

`POST /notifications`

| Field | Type | Required | Description |
|---|---|---|---|
| `to` | string | yes | Recipient email, phone, or device token |
| `channel` | string | yes | `email`, `sms`, or `push` |
| `template` | string | no | Predefined template ID |
| `data` | object | no | Variables to inject into the template |

**Response — `201 Created`**

```json
{
  "id": "ntf_9f8a7b",
  "status": "queued",
  "channel": "email",
  "created_at": "2026-06-30T18:21:55Z"
}
```

## Get notification status

`GET /notifications/{id}/status`

Returns one of: `queued`, `sent`, `delivered`, `failed`.

## List notifications

`GET /notifications?limit=20&cursor=...`

Returns a paginated list of notifications for the project.

## Errors

| Code | Meaning |
|---|---|
| `400` | Malformed request body |
| `401` | Missing or invalid API key |
| `422` | Unknown template or unsupported channel |
| `429` | Rate limit exceeded (100 req/min per key) |

```json
{
  "error": {
    "code": "invalid_channel",
    "message": "Channel 'fax' is not supported."
  }
}
```

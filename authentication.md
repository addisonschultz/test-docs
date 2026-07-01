# Authentication

Relay uses API keys to authenticate requests.

## API keys

Every project has two keys, available in **Project Settings > API Keys**:

| Key type | Prefix | Use |
|---|---|---|
| Test | `rl_test_` | Sandbox, no real messages sent |
| Live | `rl_live_` | Production, sends real messages |

Include your key in the `Authorization` header:

```bash
curl https://api.relay.example.com/v1/notifications \
  -H "Authorization: Bearer rl_live_abc123..."
```

## Request signing (optional)

For extra-sensitive endpoints, sign requests with your project's signing secret:

```javascript
const signature = hmacSha256(requestBody, signingSecret);
// send as header: X-Relay-Signature
```

Relay verifies the signature and rejects requests older than 5 minutes to prevent replay attacks.

## Rotating keys

Old keys stay valid for 24 hours after you generate a new one, so you can roll deploys without downtime.

⚠️ Never expose `rl_live_` keys in client-side code. Use test keys for local development.

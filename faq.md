---
description: Common questions and troubleshooting.
icon: circle-question
---

# FAQ

**Is Relay real?**
No — this entire docs set is mocked sample content for testing purposes.

**Why is my notification stuck in `queued`?**
Test-key sends are simulated and may sit in `queued` for a few seconds before flipping to `delivered` — no real message is sent.

**What's the rate limit?**
100 requests/minute per API key. Exceeding it returns a `429` with a `Retry-After` header.

**Can I send to multiple recipients at once?**
Not in a single call — loop over `POST /notifications` per recipient, or use the (fictional) bulk endpoint `POST /notifications/bulk`.

**How long are notification records kept?**
90 days, after which they're purged and no longer available via the API.

**Do you support attachments?**
Email supports attachments up to 10MB via the `attachments` field; SMS and push do not.

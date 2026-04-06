---
date: "2026-04-06T11:15:53+00:00"
title: "Announcing idempot-js: Idempotency Middleware for Node.js, Bun, and Deno"
tags:
  [
    "JavaScript",
    "Node.js",
    "Idempotency",
    "Open Source",
    "Express",
    "Fastify",
    "Hono"
  ]
aliases: /2026/04/06/announcing-idempot-js/
showToc: false
TocOpen: false
draft: true
hidemeta: false
comments: false
description: "Introducing idempot-js — IETF-compliant idempotency middleware for Express, Fastify, and Hono with pluggable storage backends."
canonicalURL: "https://roderick.dk/2026/04/06/announcing-idempot-js/"
disableHLJS: true
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
---

You click a payment button. You wait. You wonder if it worked. You click again—just to be safe. That moment of uncertainty represents one of distributed systems' harder problems: ensuring operations happen exactly once, even when networks fail and clients retry.

I've been working on **[idempot-js](https://js.idempot.dev)** — IETF-compliant idempotency middleware for Express, Fastify, and Hono.

## Why Idempotency Matters

In distributed systems, networks timeout, load balancers retry, users double-click. Without idempotency, these failures create duplicate transactions: double charges, duplicate orders, corrupted state.

A POST request to create a payment:

1. Server processes the request and creates the payment
2. Response gets lost in a network blip
3. Client, seeing a timeout, retries the request
4. Server, not recognising this as a duplicate, creates another payment

The result: a frustrated customer asking why they've been charged twice.

Stripe, PayPal, and other major APIs solved this with the idempotency key pattern. The IETF is now standardising it in [draft-ietf-httpapi-idempotency-key-header-07](https://datatracker.ietf.org/doc/html/draft-ietf-httpapi-idempotency-key-header-07). Clients send a unique key with each request; servers use that key to recognise and deduplicate retries.

Idempotency isn't an edge case. It's foundational to building reliable systems.

## The Standard Pattern

The idempotency key pattern is simple:

1. **Client generates a unique key** — typically a UUID for each distinct operation
2. **Key sent as header** — `Idempotency-Key: <uuid>`
3. **Server stores key + response** — in your database or cache
4. **On duplicate request** — server returns cached response instead of reprocessing

This makes any request safely retryable. The server either processes it once and caches the result, or recognises the key and returns the previous result.

Following the IETF specification matters for interoperability. When your API uses the same patterns as Stripe and PayPal, developers already know how to integrate with it. Standards reduce surprise and cognitive load.

## Introducing idempot-js

**idempot-js** implements the IETF Idempotency-Key header specification—middleware for [Express](https://expressjs.com/), [Fastify](https://fastify.dev/), and [Hono](https://hono.dev/) with pluggable storage backends.

Key features:

- **IETF compliant** — draft-ietf-httpapi-idempotency-key-header-07, returning 409 Conflict for concurrent requests and 422 Unprocessable Entity for key reuse with different payloads
- **RFC 9457 compliant** — structured error responses following the Problem Details for HTTP APIs specification
- **Content negotiation** — returns `application/problem+json` by default, or `text/markdown` for AI agent consumption
- **Framework agnostic** — same core logic, following each framework's conventions
- **Runtime support** — Node.js, Bun, and Deno
- **Pluggable storage** — Redis, PostgreSQL, MySQL, SQLite, or Bun SQL
- **Built-in resilience** — circuit breaker, retries, and timeouts protect against storage backend failures
- **TypeScript friendly** — JSDoc types for full IDE support, no compilation required

Error responses follow [RFC 9457](https://datatracker.ietf.org/doc/html/rfc9457), including `type`, `title`, `detail`, `status`, `instance`, `retryable`, and `idempotency_key` fields. Request `text/markdown` via the `Accept` header for YAML frontmatter with human-readable guidance—useful for AI agents.

I wrote idempot-js because existing solutions were framework-specific or ignored the IETF spec. It's part of the [idempot.dev](https://idempot.dev) initiative.

## Try, Try Again

Sam Newman covers this well in his LeadDev Berlin 2025 talk, "Try, Try Again":

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/29NNiZhXe2Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Without idempotency, retries are a source of bugs. With it, they become a reliability feature.

## Getting Started

The quickest way to try idempot-js is with Hono and SQLite:

```javascript
import { Hono } from "hono";
import { idempotency } from "@idempot/hono-middleware";
import { SqliteIdempotencyStore } from "@idempot/sqlite-store";

const app = new Hono();
const store = new SqliteIdempotencyStore({ path: ":memory:" });

app.post("/orders", idempotency({ store }), async (c) => {
  return c.json({ id: "order-123" }, 201);
});
```

The middleware handles key validation, conflict detection, response caching, and deduplication.

For production: Redis for performance, PostgreSQL or MySQL if you have existing infrastructure, or Bun SQL. Each store implements the same interface.

See the [documentation](https://js.idempot.dev) for configuration options, resilience tuning, and examples for Express and Fastify.

## What's Next

idempot-js is part of the [idempot.dev](https://idempot.dev) ecosystem.

- **Documentation:** [js.idempot.dev](https://js.idempot.dev)
- **GitHub:** [github.com/idempot-dev/idempot-js](https://github.com/idempot-dev/idempot-js)
- **npm:** [express](https://www.npmjs.com/package/@idempot/express-middleware) · [fastify](https://www.npmjs.com/package/@idempot/fastify-middleware) · [hono](https://www.npmjs.com/package/@idempot/hono-middleware)

Issues and contributions welcome on [GitHub](https://github.com/idempot-dev/idempot-js).

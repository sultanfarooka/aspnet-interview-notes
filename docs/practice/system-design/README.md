# System Design Practice

**[← Roadmap](../../ROADMAP.md)** · Topic **[25.5](../../ROADMAP.md#25-interview-preparation-and-practice)** 🔥 🎯

> System design rounds are increasingly common for mid-level .NET roles and standard for
> senior. They are not testing whether you know the "right" architecture — they're
> testing whether you ask about constraints before you draw boxes.

---

## The method (use this every time)

1. **Clarify requirements** — functional and non-functional. Never start drawing first.
   Ask about scale, read/write ratio, consistency needs, latency budget.
2. **Estimate** — requests per second, storage growth, bandwidth. Rough is fine; showing
   you think in numbers is the point.
3. **Define the API** — endpoints and their contracts. This forces concrete thinking.
4. **Data model** — entities, relationships, and the access patterns that drive the schema.
5. **High-level design** — draw the boxes. Client, gateway, services, data stores, queues.
6. **Deep dive** — the interviewer picks a component. Be ready for any of them.
7. **Bottlenecks and scale** — where does this break at 10×? What do you fix first?
8. **Tradeoffs** — say out loud what you gave up and why.

**Step 1 is the one candidates skip and the one interviewers score hardest.** Jumping to
a diagram before establishing constraints is the most common failure in this round.

---

## Worked examples to write

Each gets its own file in this folder. Write them out fully — a design you've written is
one you can improvise from; one you've only read is not.

- [ ] **URL shortener** — hashing, collisions, redirect performance, analytics
- [ ] **E-commerce checkout** — inventory reservation, payment idempotency, order saga
- [ ] **Notification service** — fan-out, delivery guarantees, retries, dead lettering
- [ ] **Rate limiter** — algorithms (token bucket, sliding window), distributed state
- [ ] **File upload service** — presigned URLs, chunking, virus scanning, CDN
- [ ] **Chat / real-time feed** — SignalR, backplane, presence, message ordering
- [ ] **Multi-tenant SaaS API** — tenant isolation, per-tenant data, noisy neighbours
- [ ] **Job scheduler** — durability, exactly-once-ish semantics, poison messages
- [ ] **Audit log service** — write volume, immutability, retention, query patterns
- [ ] **Read-heavy product catalog** — caching layers, invalidation, search

---

## .NET-specific things to bring up

These are what make it an *ASP.NET Core* system design round rather than a generic one.
Working one or two in naturally shows depth:

- `IHttpClientFactory` + Polly for service-to-service resilience → [19.11](../../notes/19-caching-performance/19.11-polly-resilience.md)
- `HybridCache` or Redis for the caching layer → [19.3](../../notes/19-caching-performance/19.03-distributed-cache-redis.md)
- Background processing: `BackgroundService` vs Hangfire vs a queue consumer → [21.1](../../notes/21-advanced-features/21.01-background-services.md), [21.3](../../notes/21-advanced-features/21.03-job-schedulers.md)
- Outbox pattern for reliable event publishing from EF Core → [23.8](../../notes/23-microservices/23.08-saga-outbox.md)
- YARP as gateway/BFF → [23.10](../../notes/23-microservices/23.10-api-gateway-bff.md)
- Health checks driving Kubernetes probes → [18.5](../../notes/18-logging-monitoring/18.05-health-checks.md), [24.6](../../notes/24-devops-hosting/24.06-probes-and-shutdown.md)
- OpenTelemetry for cross-service tracing → [18.7](../../notes/18-logging-monitoring/18.07-opentelemetry.md)
- Stateless app servers so you can scale horizontally → [24.12](../../notes/24-devops-hosting/24.12-scaling.md)

---

## Numbers worth knowing

Rough orders of magnitude. Precision isn't the point — being able to estimate at all is.

| | Latency |
|---|---|
| In-memory cache read | ~100 ns |
| Redis round trip (same DC) | ~0.5–1 ms |
| Database query (indexed, same DC) | ~1–10 ms |
| Cross-region round trip | ~50–150 ms |
| Disk seek (SSD) | ~0.1 ms |

| | Scale |
|---|---|
| One well-tuned ASP.NET Core instance | thousands of req/s for simple endpoints |
| 1M requests/day | ~12 req/s average, plan for 5–10× peak |
| 1 KB per row × 100M rows | ~100 GB |

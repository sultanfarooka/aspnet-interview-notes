# What's New — .NET 6 → .NET 10

**[← Roadmap](ROADMAP.md)** · Topic **[25.10](ROADMAP.md#25-interview-preparation-and-practice)** 🔥

> "What's new in the latest .NET?" is an easy question that catches a surprising number
> of candidates. It's really testing whether you keep up, so a short confident answer
> about two or three features you've actually used beats a memorized changelog.
>
> Verify the details against Microsoft Learn before an interview — this file is a
> memory aid, not a source of truth, and release notes move.

---

## Support status

Even-numbered releases are **LTS** (3 years). Odd-numbered are **STS** (18 months).
Check the current support matrix before interviewing — claiming a version is supported
when it went end-of-life is a bad look.

---

## .NET 6 (LTS) — the baseline

- **Minimal APIs** — endpoints without controllers
- **Minimal hosting model** — `WebApplicationBuilder`, `Program.cs` with top-level statements, no `Startup.cs`
- **Hot reload**
- `DateOnly` / `TimeOnly`
- Nullable reference types on by default in new templates

## .NET 7 (STS)

- **Rate limiting middleware** (`AddRateLimiter`) → [17.10](notes/17-application-security/17.10-rate-limiting.md)
- **Output caching** → [19.6](notes/19-caching-performance/19.06-output-caching.md)
- **Route groups** (`MapGroup`) → [8.9](notes/08-routing/8.09-route-groups.md)
- **Endpoint filters** for Minimal APIs → [12.7](notes/12-filters/12.07-endpoint-filters.md)
- **EF Core `ExecuteUpdate` / `ExecuteDelete`** — bulk operations without loading entities → [13.14](notes/13-entity-framework-core/13.14-bulk-operations.md)
- Native AOT for console apps

## .NET 8 (LTS) — the one most shops are on

- **Keyed DI services** (`AddKeyedSingleton`, `[FromKeyedServices]`) → [6.6](notes/06-dependency-injection/6.06-registration-apis.md)
- **`IExceptionHandler`** — a proper abstraction for global error handling → [5.12](notes/05-middleware-pipeline/5.12-iexceptionhandler.md)
- **`TimeProvider`** — finally makes time testable → [20.12](notes/20-testing/20.12-testing-async-and-time.md)
- **Blazor United** — server and WASM render modes in one app → [9.9](notes/09-mvc-razor-views/9.09-blazor-overview.md)
- **Native AOT for ASP.NET Core** (Minimal APIs) → [21.10](notes/21-advanced-features/21.10-native-aot.md)
- Short-circuit routing, `[FromKeyedServices]`, improved `ProblemDetails` defaults
- Primary constructors, collection expressions (C# 12)

## .NET 9 (STS)

- **`HybridCache`** — combines in-memory + distributed with built-in stampede protection → [19.4](notes/19-caching-performance/19.04-hybridcache.md)
- **Built-in OpenAPI document generation** — no Swashbuckle required → [10.9](notes/10-web-api-rest/10.09-openapi-swagger.md)
- Improved `System.Text.Json` — nullable handling, schema export
- .NET Aspire maturing → [21.14](notes/21-advanced-features/21.14-dotnet-aspire.md)
- Server GC improvements (DATAS on by default)

## .NET 10 (LTS)

The current LTS at time of writing. **Check Microsoft Learn for the feature list before
you interview** — this is the version an interviewer is most likely to probe, and it's
the one where a stale memory is most obvious.

---

## How to answer the question

Don't recite. Pick **two features you've actually used** and say what problem they solved
for you. Something like:

> "We moved to .NET 8 mainly for keyed services — we had a factory-with-a-switch for three
> payment providers that keyed DI let us delete entirely. And `TimeProvider` meant we
> could finally test our expiry logic without an `IClock` abstraction of our own."

That answer demonstrates currency, judgment, and hands-on use in three sentences. A list
of twelve feature names demonstrates that you read a blog post.

If you genuinely haven't used a recent version, say so and describe what you'd want from
it — calibration reads better than bluffing every time.

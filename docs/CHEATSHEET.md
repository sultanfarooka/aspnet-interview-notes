# Cheat Sheet — The 60-Minute Blitz

**[← Roadmap](ROADMAP.md)** · **[Traps](TRAPS.md)** · **[Diagrams](DIAGRAMS.md)**

> One line per concept. No explanations — if a line doesn't trigger recall, that topic is
> 🔴 and you should open the full note instead of re-reading this.
>
> **This file is a recall test, not a lesson.** Read it with the right-hand column
> covered, if you print it.

---

## Middleware order (memorize verbatim)

```
ExceptionHandler → HSTS → HttpsRedirection → StaticFiles → Routing
→ CORS → Authentication → Authorization → custom → Endpoints
```

Authentication *always* before Authorization. CORS before both. Exception handler first
so it wraps everything.

## DI lifetimes

| | Instance per | Typical use |
|---|---|---|
| Transient | every injection | cheap, stateless helpers |
| Scoped | HTTP request | `DbContext`, unit of work, per-request state |
| Singleton | application | config, caches, `HttpClient` factories |

Never inject shorter-lived into longer-lived. Background services must create their own scope.

## HTTP verbs

| Verb | Safe | Idempotent | Body |
|---|:--:|:--:|:--:|
| GET | ✅ | ✅ | ✗ |
| HEAD | ✅ | ✅ | ✗ |
| POST | ✗ | ✗ | ✅ |
| PUT | ✗ | ✅ | ✅ |
| PATCH | ✗ | ✗ | ✅ |
| DELETE | ✗ | ✅ | ✗ |

## Status codes

`200` OK · `201` Created (+ `Location`) · `202` Accepted · `204` No Content
`301` Moved · `304` Not Modified
`400` Bad Request · `401` Unauthenticated · `403` Unauthorized · `404` Not Found
`405` Method Not Allowed · `409` Conflict · `415` Unsupported Media Type
`422` Unprocessable · `429` Too Many Requests
`500` Server Error · `502` Bad Gateway · `503` Unavailable · `504` Gateway Timeout

**401 vs 403:** 401 = I don't know who you are. 403 = I know, and you still can't.

## What `[ApiController]` gives you

Automatic 400 on invalid `ModelState` · inferred binding sources · `ProblemDetails` errors
· attribute routing required · multipart/form-data inference.

## Filter pipeline order

```
Authorization → Resource → [model binding] → Action → [action runs] → Result
```

Exception filters wrap Action and Result. Scope order: global → controller → action on the
way *in*, reversed on the way out.

## EF Core loading

`Include`/`ThenInclude` = eager · lazy = proxies, causes N+1 · `Entry(x).Collection().Load()` = explicit.
`AsNoTracking()` for every read you won't save. `AsSplitQuery()` when Includes cartesian-explode.

## JWT

Three base64 parts: **header.payload.signature**. Signed, *not* encrypted.
Validate: signature, `iss`, `aud`, `exp`, `nbf`. Short-lived access token + refresh token
for revocation.

## Auth vs authz

Authentication = who are you (`ClaimsPrincipal`). Authorization = what may you do
(roles → claims → policies → requirements → resource-based, in increasing power).

## Caching

Cache-aside is the default: read cache → miss → read DB → populate → return.
`IMemoryCache` = per instance. `IDistributedCache`/Redis = shared. `HybridCache` = both + stampede protection.

## `HttpClient`

Always `IHttpClientFactory`. Never `new HttpClient()` per request. Never a raw static
either — it won't see DNS changes.

## SOLID

**S**ingle responsibility · **O**pen/closed · **L**iskov substitution ·
**I**nterface segregation · **D**ependency inversion.

## Async rules

Async all the way down. No `.Result` / `.Wait()`. No `async void` outside event handlers.
Pass `CancellationToken` through. `ConfigureAwait(false)` in libraries only.

## Isolation levels vs read phenomena

| Level | Dirty read | Non-repeatable | Phantom |
|---|:--:|:--:|:--:|
| Read Uncommitted | ✅ | ✅ | ✅ |
| Read Committed | ✗ | ✅ | ✅ |
| Repeatable Read | ✗ | ✗ | ✅ |
| Serializable | ✗ | ✗ | ✗ |

(✅ = the phenomenon can still occur.)

## Testing

xUnit `[Fact]` / `[Theory]` + `[InlineData]`. Mock the boundary, not the thing under test.
`WebApplicationFactory<Program>` for integration. Testcontainers over InMemory.

---

## The four questions you will definitely be asked

1. **Walk me through what happens when a request hits your API.**
   → [25.2](notes/25-interview-practice/25.02-request-lifecycle-narrative.md). Rehearse out loud.
2. **Explain the DI lifetimes and when each is wrong.**
   → [6.3](notes/06-dependency-injection/6.03-service-lifetimes.md) + [6.4](notes/06-dependency-injection/6.04-captive-dependency.md).
3. **This endpoint is slow. How do you find out why?**
   → [19.15](notes/19-caching-performance/19.15-slow-endpoint-playbook.md).
4. **Tell me about something you built and what you'd do differently.**
   → [MY-PROJECTS.md](MY-PROJECTS.md).

---

## Last 5 minutes

Read [TRAPS.md](TRAPS.md). Then close the laptop. Cramming new material in the final
minutes displaces what you already knew — that's the one thing that reliably makes
interviews go worse.

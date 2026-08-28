# Traps — Things That Are Wrong In A Way That Sounds Right

**[← Roadmap](ROADMAP.md)** · **[README](index.md)**

> This is the highest signal-per-minute file in the repo. Every ⚠️ marker in the roadmap
> lands here, in one line each, with the correction.
>
> Interviewers use these deliberately. A candidate who's read blog posts gives the
> plausible answer; a candidate who's shipped gives the correct one. That gap is the
> whole point of the question.

**Read this twice the day before. Then once more in the morning.**

---

## Async and threading

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "`async` makes code run on another thread" | `async`/`await` is about *not blocking a thread*, not about using more of them. A truly async I/O call uses **no** thread while it waits. | [2.11](notes/02-collections-linq-async/2.11-async-await-internals.md) |
| "`.Result` is fine if I know the task is done" | In any context with a synchronization context it can deadlock, and in ASP.NET Core it blocks a thread-pool thread. Under load this cascades into thread-pool starvation. | [2.13](notes/02-collections-linq-async/2.13-async-deadlocks.md) |
| "`async void` is fine for event handlers" | It's *tolerable* for UI event handlers and wrong everywhere else — exceptions can't be caught by the caller and will crash the process. | [2.15](notes/02-collections-linq-async/2.15-async-void.md) |
| "`ConfigureAwait(false)` is needed in ASP.NET Core" | ASP.NET Core has no synchronization context, so it changes nothing in app code. It still matters in **libraries**, which may run on other platforms. | [2.13](notes/02-collections-linq-async/2.13-async-deadlocks.md) |

## Dependency injection

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "Scoped means one instance per class" | Scoped means one instance per **scope**, which in a web app is one per HTTP request. Background services have no ambient scope — you must create one. | [6.5](notes/06-dependency-injection/6.05-scopes.md) |
| "Injecting a scoped service into a singleton is fine" | The singleton captures that instance forever. Your `DbContext` becomes an app-lifetime object shared across all requests — non-thread-safe, leaking, **and returning stale cached entities**. | [6.4](notes/06-dependency-injection/6.04-captive-dependency.md) |
| "Transient services are always safe" | A transient in a singleton lives as long as the singleton — and **`ValidateScopes` does not catch it**, because that combination is technically legal. | [6.4](notes/06-dependency-injection/6.04-captive-dependency.md) |
| "Scope validation protects me" | It's **Development-only by default**. The environment that would catch the bug is the one you never deploy. Enable it everywhere. | [6.13](notes/06-dependency-injection/6.13-di-traps.md) |
| "DI is the same as the Dependency Inversion Principle" | DI is *how* you receive a dependency; dependency inversion is *what* you depend on. And IoC is the broader principle both sit under. | [6.1](notes/06-dependency-injection/6.01-ioc-and-di.md) |
| "Every class should have an interface" | An interface with one implementation and no test double is a file and an indirection buying nothing. Add it when you need to substitute. | [6.1](notes/06-dependency-injection/6.01-ioc-and-di.md) |
| "Registering the same interface twice replaces the first" | Both stay — the collection is a **list**. A single resolve gives the **last**; `IEnumerable<T>` gives all. Duplicates change behaviour silently. | [6.2](notes/06-dependency-injection/6.02-builtin-container.md) |
| "`GetService` and `GetRequiredService` are interchangeable" | `GetService` returns **null**, so a missing registration surfaces later as a null reference somewhere unrelated. | [6.2](notes/06-dependency-injection/6.02-builtin-container.md) |
| "Injecting `IServiceProvider` into a singleton lets me use scoped services" | That's the **root** provider — the scoped service lives forever. Same bug, and validation misses it. Use `IServiceScopeFactory`. | [6.5](notes/06-dependency-injection/6.05-scopes.md) |
| "I created a scope, so I'm fine" | Not if it's **outside** the loop. One `DbContext` for the service's whole lifetime is the captive dependency relocated. | [6.5](notes/06-dependency-injection/6.05-scopes.md) |
| "I can create a scope in my controller" | The request **already has one**. A second scope means a second `DbContext` with its own change tracker and its own transaction. | [6.5](notes/06-dependency-injection/6.05-scopes.md) |
| "`TryAdd` is just a safer `Add`" | With several implementations it **silently skips all but the first**. Use `TryAddEnumerable`. And it needs a separate `using`. | [6.6](notes/06-dependency-injection/6.06-registration-apis.md) |
| "Keyed services replace factories" | Keys are fixed **at registration**. If the choice depends on runtime data like the current tenant, you still need a factory. | [6.6](notes/06-dependency-injection/6.06-registration-apis.md) |
| "The order of `IEnumerable<T>` doesn't matter" | It's registration order, and it usually **should** matter — cheap checks before ones hitting a database or an API. But it's implicit and easy to break. | [6.7](notes/06-dependency-injection/6.07-multiple-implementations.md) |
| "A decorator is easy to register by hand" | Register the inner service as the **interface** and the decorator resolves itself — infinite recursion. Register it as the concrete type. | [6.8](notes/06-dependency-injection/6.08-factories-open-generics.md) |
| "A factory registration is checked at startup" | It runs **lazily**, on first resolution. A config error inside surfaces on the first request that needs it, not at startup. | [6.8](notes/06-dependency-injection/6.08-factories-open-generics.md) |
| "Ten constructor parameters? Inject `IServiceProvider`" | That hides the smell rather than fixing it — and removes the only signal telling you the class does too much. Split it. | [6.9](notes/06-dependency-injection/6.09-injection-styles.md) |
| "The container disposes everything I give it" | It disposes instances **it created**. Pass an already-constructed instance to `AddSingleton(instance)` and you own disposal. | [6.10](notes/06-dependency-injection/6.10-disposal.md) |
| "I should dispose the `DbContext` I injected" | You didn't create it. Disposing it breaks **every other service in that request** sharing the same scope. | [6.10](notes/06-dependency-injection/6.10-disposal.md) |
| "A transient disposable is released when I finish with it" | It's held by the **scope** until that scope ends. Resolving one in a loop means every instance stays open. | [6.10](notes/06-dependency-injection/6.10-disposal.md) |
| "`IOptions<T>` and `IOptionsSnapshot<T>` are interchangeable" | `IOptions<T>` is singleton. **`IOptionsSnapshot<T>` is scoped** — a captive dependency in a singleton constructor. | [6.13](notes/06-dependency-injection/6.13-di-traps.md) |
| "`DateTime.UtcNow` is fine, DI handles the rest" | Time-dependent logic is then untestable or flaky. Inject **`TimeProvider`** (.NET 8+) and use `FakeTimeProvider` in tests. | [6.12](notes/06-dependency-injection/6.12-di-and-testability.md) |
| "Unit tests need the DI container" | They don't. The container composes the **application**; a unit test just `new`s the class with fakes. Needing a container means it's an integration test. | [6.12](notes/06-dependency-injection/6.12-di-and-testability.md) |

## Fundamentals and startup

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "ASP.NET Core is ASP.NET with a new version number" | It's a **rewrite**. `System.Web` doesn't exist, `HttpContext.Current` is gone, and Web Forms never ported. | [4.1](notes/04-fundamentals-startup/4.01-what-is-aspnet-core.md) |
| "IIS hosts my ASP.NET Core app" | The relationship **inverted**. Your app hosts Kestrel; IIS is a reverse proxy in front of it. | [4.2](notes/04-fundamentals-startup/4.02-hosting-model.md) |
| "Behind a load balancer I still see the client IP" | You see the **proxy's** IP. You need `UseForwardedHeaders`, registered **first**, and only loopback proxies are trusted by default — so it works locally and silently fails in Kubernetes. | [4.2](notes/04-fundamentals-startup/4.02-hosting-model.md) |
| "`UseHttpsRedirection` is always correct" | Behind a TLS-terminating proxy it causes an **infinite redirect loop** — the app sees `http`, redirects, the proxy forwards `http` again. | [4.2](notes/04-fundamentals-startup/4.02-hosting-model.md) |
| "Binding to `localhost` works in a container" | The app starts, looks healthy, and **refuses every external connection**. Use `http://+:8080`. | [4.2](notes/04-fundamentals-startup/4.02-hosting-model.md) |
| "I can register a service anywhere in `Program.cs`" | Not after `builder.Build()` — the collection is **frozen**. | [4.3](notes/04-fundamentals-startup/4.03-program-cs-hosting.md) |
| "I can resolve `DbContext` from `app.Services` at startup" | It's scoped and there's **no ambient scope** at startup. Call `CreateScope()` first. | [4.3](notes/04-fundamentals-startup/4.03-program-cs-hosting.md) |
| "`WebApplicationFactory<Program>` just works" | The generated `Program` is **internal**. Add `public partial class Program { }` or `InternalsVisibleTo`. | [4.3](notes/04-fundamentals-startup/4.03-program-cs-hosting.md) |
| "`Startup.cs` implements an interface" | It implements **nothing** — methods are found by **name** via reflection. Misspell `ConfigureServices` and it compiles and silently never runs. | [4.4](notes/04-fundamentals-startup/4.04-startup-cs-legacy.md) |
| "`ValidateScopes` protects me in production" | It's **Development-only by default**, which is exactly why captive dependencies survive to production. | [4.5](notes/04-fundamentals-startup/4.05-host-interfaces.md) |
| "`IHostedService.StartAsync` runs in the background" | It **blocks application startup**. Slow work there delays readiness. Use `BackgroundService.ExecuteAsync`. | [4.5](notes/04-fundamentals-startup/4.05-host-interfaces.md) |
| "Shutdown is fine by default" | You get **5 seconds**. Any request slower than that is cut off — on **every deployment**. | [4.6](notes/04-fundamentals-startup/4.06-app-lifecycle.md) |
| "Longer shutdown timeout is always safer" | It must be **shorter** than the orchestrator's grace period, or Kubernetes SIGKILLs you mid-drain — and SIGKILL can't be caught. | [4.6](notes/04-fundamentals-startup/4.06-app-lifecycle.md) |
| "Kubernetes stops traffic before sending SIGTERM" | Both happen **at the same time** and endpoint removal propagates asynchronously, so requests arrive after you've stopped accepting. Delay shutdown or fail readiness first. | [4.6](notes/04-fundamentals-startup/4.06-app-lifecycle.md) |
| "`Environment.Exit` shuts down cleanly" | It **skips every shutdown handler**. Use `lifetime.StopApplication()`. | [4.6](notes/04-fundamentals-startup/4.06-app-lifecycle.md) |
| "No `ASPNETCORE_ENVIRONMENT` means Development" | It defaults to **Production** — deliberately safe in deployment, confusing locally. | [4.7](notes/04-fundamentals-startup/4.07-environments.md) |
| "The developer exception page is just verbose errors" | It shows **all environment variables** in the browser — connection strings and API keys included. One stray `ASPNETCORE_ENVIRONMENT=Development` in prod exposes them. | [4.7](notes/04-fundamentals-startup/4.07-environments.md) |
| "`appsettings.production.json` works fine" | Environment names are case-insensitive in code, but **file names are case-sensitive on Linux**. That file is silently ignored. | [4.7](notes/04-fundamentals-startup/4.07-environments.md) |
| "I set the environment in `launchSettings.json`" | That file is **never deployed**. It has zero effect on production. | [4.8](notes/04-fundamentals-startup/4.08-launchsettings.md) |
| "In-process IIS hosting uses Kestrel" | It uses **`IISHttpServer`**, a different implementation that talks to IIS directly. | [4.9](notes/04-fundamentals-startup/4.09-kestrel-iis-httpsys.md) |
| "Static files respect `[Authorize]`" | **No.** `UseStaticFiles` runs before authentication, so anything in `wwwroot` is downloadable by anyone with the URL. | [4.10](notes/04-fundamentals-startup/4.10-static-files.md) |
| "Put `UseStaticFiles` wherever" | After authentication, every image runs JWT validation first. Forty assets = forty wasted auth cycles per page. | [4.10](notes/04-fundamentals-startup/4.10-static-files.md) |
| "The file is in `wwwroot` but returns 404" | Unknown **MIME types are not served** by default. Register the extension rather than enabling `ServeUnknownFileTypes`. | [4.10](notes/04-fundamentals-startup/4.10-static-files.md) |
| "Clean Architecture is the professional choice" | Four projects for six endpoints is cost with no benefit. Start with one project and folders; split when the pain is **real**. | [4.11](notes/04-fundamentals-startup/4.11-project-structure.md) |

## Middleware and pipeline

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "Middleware order doesn't really matter" | `UseAuthorization` before `UseAuthentication` means `User` is never populated — the app silently 401s on everything, **with no error**. | [5.2](notes/05-middleware-pipeline/5.02-middleware-order.md) |
| "The pipeline is a list of steps" | It's **nested** — each middleware wraps the rest, like try/finally. That's why `await next()` returns and lets you inspect the response. | [5.1](notes/05-middleware-pipeline/5.01-what-is-middleware.md) |
| "`await next()` hands off and finishes" | It runs the **entire remaining pipeline** and waits. When it returns, the response already exists. | [5.1](notes/05-middleware-pipeline/5.01-what-is-middleware.md) |
| "My CORS policy is wrong" | Often it's **ordering**. `UseCors` after `UseAuthentication` means the unauthenticated `OPTIONS` preflight is 401'd before CORS can answer. | [5.2](notes/05-middleware-pipeline/5.02-middleware-order.md) |
| "`Map` and `UseWhen` are interchangeable" | `Map` is a **dead end** — the branch never rejoins, so `MapControllers` below never runs and every route 404s. `UseWhen` rejoins. | [5.3](notes/05-middleware-pipeline/5.03-use-run-map.md) |
| "`app.Run(...)` starts the app" | `app.Run()` with no args does. `app.Run(handler)` adds **terminal middleware** — nothing after it ever executes. | [5.3](notes/05-middleware-pipeline/5.03-use-run-map.md) |
| "I can resolve a service once and capture it in my inline middleware" | That pins **one instance for the app's lifetime**. Resolve from `context.RequestServices` inside the lambda. | [5.4](notes/05-middleware-pipeline/5.04-inline-middleware.md) |
| "I can inject a scoped service into middleware's constructor" | Conventional middleware is a **singleton**, created once. Scoped services go in the `InvokeAsync` parameters, or use `IMiddleware`. | [5.5](notes/05-middleware-pipeline/5.05-conventional-middleware.md) |
| "`IOptions<T>` and `IOptionsSnapshot<T>` are both fine in a middleware constructor" | `IOptions<T>` is singleton and fine. **`IOptionsSnapshot<T>` is scoped** and must go in `InvokeAsync`. | [5.5](notes/05-middleware-pipeline/5.05-conventional-middleware.md) |
| "`IMiddleware` works like conventional middleware" | It must be **registered in DI yourself**, or you get "No service for type..." on the first request. | [5.6](notes/05-middleware-pipeline/5.06-imiddleware-factory.md) |
| "Returning early from middleware is enough" | Without setting a status code you send an **empty HTTP 200** — no error, nothing to debug from. | [5.7](notes/05-middleware-pipeline/5.07-short-circuiting.md) |
| "Short-circuiting skips everything" | Only what's **below**. Middleware above already called `next` and still runs its "after" half — which is why logging keeps working. | [5.7](notes/05-middleware-pipeline/5.07-short-circuiting.md) |
| "I can keep a reference to `HttpContext`" | It's **pooled and reused** after the response. A stored reference can end up pointing at **another user's request**. | [5.8](notes/05-middleware-pipeline/5.08-httpcontext.md) |
| "Modify the response after `await next()`" | Headers are on the wire once the response has started. Use `OnStarting`, registered **before** `next`. | [5.8](notes/05-middleware-pipeline/5.08-httpcontext.md) |
| "I can read the request body in middleware and the controller still gets it" | The body is forward-only and gets consumed — the action's model is **null**. Needs `EnableBuffering()` **and** `Body.Position = 0`. | [5.9](notes/05-middleware-pipeline/5.09-request-body-buffering.md) |
| "`EnableBuffering()` is enough" | It only makes rewinding **possible**. Forgetting `Position = 0` gives the exact same symptom as not buffering. | [5.9](notes/05-middleware-pipeline/5.09-request-body-buffering.md) |
| "`UseHsts()` is a good default everywhere" | In development it can lock you out of `http://localhost` for **months**, across every project on that port. Production only. | [5.10](notes/05-middleware-pipeline/5.10-builtin-middleware.md) |
| "A 404 returns a JSON error body" | A bare 404 from routing has an **empty body** unless you add `UseStatusCodePages()`. | [5.11](notes/05-middleware-pipeline/5.11-exception-middleware.md) |
| "Returning `ex.Message` to the client is helpful" | Exception messages routinely contain **table names, file paths and connection details**. Log the detail, return a trace ID. | [5.11](notes/05-middleware-pipeline/5.11-exception-middleware.md) |
| "Registering `IExceptionHandler` is enough" | Nothing runs without **`app.UseExceptionHandler()`**. No warning — exceptions just go unhandled. | [5.12](notes/05-middleware-pipeline/5.12-iexceptionhandler.md) |
| "Handler registration order doesn't matter" | They run in order until one returns `true`. A catch-all registered **first** makes every later handler unreachable. | [5.12](notes/05-middleware-pipeline/5.12-iexceptionhandler.md) |
| "I'll validate the request model in middleware" | **Model binding hasn't run yet.** Reading the body yourself also breaks binding downstream. Use a filter. | [5.13](notes/05-middleware-pipeline/5.13-middleware-vs-filters.md) |
| "I'll log requests in an action filter" | Filters only run when a route **matched** — so you silently miss every 404, static file and rate-limited request. | [5.13](notes/05-middleware-pipeline/5.13-middleware-vs-filters.md) |
| "Logging the request is harmless" | Headers carry `Authorization` and `Cookie`; query strings carry API keys and reset tokens. Log `Path`, **not** `QueryString`. | [5.14](notes/05-middleware-pipeline/5.14-logging-middleware.md) |
| "Log everything at Information" | Then the level conveys nothing and you can't alert. And EF Core at Information logs **every SQL statement**. | [5.14](notes/05-middleware-pipeline/5.14-logging-middleware.md) |

## EF Core

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "`DbContext` should be a singleton for performance" | It is **not thread-safe** and its change tracker grows unbounded. Scoped is the correct lifetime; use `AddDbContextPool` if you want the pooling win. | [13.2](notes/13-entity-framework-core/13.02-dbcontext.md) |
| "`.ToList()` then filter — same thing" | `ToList()` executes the query. Everything after it filters **in memory** after pulling the whole table across the wire. | [13.10](notes/13-entity-framework-core/13.10-client-vs-server-eval.md) |
| "Lazy loading is convenient and harmless" | It's the primary cause of N+1 queries, and it fires queries at serialization time, long after the context you expected. | [13.9](notes/13-entity-framework-core/13.09-n-plus-one.md) |
| "`FromSqlRaw` with string interpolation is fine" | That's SQL injection. `FromSqlInterpolated` (or `FromSqlRaw` with parameters) parameterizes; `FromSqlRaw($"...{x}")` does not. | [13.11](notes/13-entity-framework-core/13.11-raw-sql.md) |
| "`AsNoTracking` is a micro-optimization" | On read-heavy endpoints returning many rows it's often a large win, and it prevents accidental updates. Default to it for reads. | [13.7](notes/13-entity-framework-core/13.07-change-tracking.md) |
| "The InMemory provider is fine for testing" | It doesn't enforce relational constraints, transactions, or SQL translation — tests pass that production fails. Use SQLite in-memory or Testcontainers. | [13.20](notes/13-entity-framework-core/13.20-testing-data-access.md) |

## .NET runtime and platform

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| ".NET 4.8 is just an older .NET 8" | **Unrelated products.** 4.8 is the final Windows-only Framework; 8 is the modern cross-platform one. The close numbers are why version 4 was skipped. | [3.1](notes/03-dotnet-runtime/3.01-dotnet-history.md) |
| "The name 'Core' was dropped everywhere" | The runtime dropped it; **ASP.NET Core kept it**. ASP.NET Core 10 runs on .NET 10. | [3.1](notes/03-dotnet-runtime/3.01-dotnet-history.md) |
| "C# compiles to machine code" | It compiles to **IL**. Machine code is produced later by the JIT, per method, on first call. | [3.2](notes/03-dotnet-runtime/3.02-clr-and-compilation.md) |
| "CTS and CLS are the same thing" | CTS is the **full** type system. CLS is the **subset** every .NET language supports — which is why C# allows `Process()` and `process()` but that isn't CLS-compliant. | [3.2](notes/03-dotnet-runtime/3.02-clr-and-compilation.md) |
| "Benchmark the first few calls" | Those measure **Tier 0** unoptimised code plus the compilation itself. You must warm up first. | [3.2](notes/03-dotnet-runtime/3.02-clr-and-compilation.md) |
| "Native AOT is just a faster build" | It **silently breaks reflection**, `Expression.Compile` and `Reflection.Emit`. Compiles fine, fails at runtime. | [3.2](notes/03-dotnet-runtime/3.02-clr-and-compilation.md) |
| "The GC frees everything eventually" | It frees **memory**. File handles, sockets and DB connections need `Dispose` — the GC has no idea what they are. | [3.3](notes/03-dotnet-runtime/3.03-managed-vs-unmanaged.md) |
| "You can take a pointer to a managed array" | Not without `fixed`. The GC **moves objects** during compaction and cannot update a raw pointer. | [3.3](notes/03-dotnet-runtime/3.03-managed-vs-unmanaged.md) |
| "The GC counts references" | It uses **reachability from roots**, not counting. That's why circular references are collected fine. | [3.4](notes/03-dotnet-runtime/3.04-garbage-collection.md) |
| "`GC.Collect()` will fix my memory usage" | If the object is still reachable, no collection frees it. Forcing one triggers an expensive **Gen 2** pass and **promotes** objects that would have died cheaply. | [3.4](notes/03-dotnet-runtime/3.04-garbage-collection.md) |
| "Large objects are handled like any other" | ≥ **85,000 bytes** go to the LOH, collected only on Gen 2 and **not compacted** — so memory climbs from fragmentation with no actual leak. | [3.4](notes/03-dotnet-runtime/3.04-garbage-collection.md) |
| "Server GC is strictly better" | It uses **one heap per core**. In a small container that extra memory can breach the limit and get you OOM-killed. | [3.4](notes/03-dotnet-runtime/3.04-garbage-collection.md) |
| "You can't leak memory in .NET" | You can't forget to free — but you can **keep a reference**, which the GC must honour. Static collections, unremoved event handlers, captured closures. | [3.5](notes/03-dotnet-runtime/3.05-memory-leaks.md) |
| "One memory dump will show the leak" | One dump shows what's **large**. Two dumps minutes apart show what's **growing**, which is what you need. Then `gcroot` to find what holds it. | [3.5](notes/03-dotnet-runtime/3.05-memory-leaks.md) |
| "`IMemoryCache` can't leak, it has eviction" | Without an explicit **`SizeLimit`** it only evicts under memory pressure, which may arrive too late. | [3.5](notes/03-dotnet-runtime/3.05-memory-leaks.md) |
| "Copy the DLL into the output folder and it'll load" | The runtime resolves from **`deps.json`**, not by scanning folders. Not listed there = `FileNotFoundException`. | [3.6](notes/03-dotnet-runtime/3.06-assemblies-nuget.md) |
| "Version conflicts fail the build" | They fail at **runtime** with `MethodNotFoundException`. .NET picks the highest version and hopes it's compatible. | [3.6](notes/03-dotnet-runtime/3.06-assemblies-nuget.md) |
| "`#if NET8_0` covers .NET 8 and later" | It's **false** once you add a `net10.0` target. Use `NET8_0_OR_GREATER`. | [3.7](notes/03-dotnet-runtime/3.07-csproj-and-tfm.md) |
| "`linux-x64` runs in any Linux container" | **Not Alpine.** Alpine uses musl, so it needs `linux-musl-x64`. Fails at startup with a confusing missing-library error. | [3.7](notes/03-dotnet-runtime/3.07-csproj-and-tfm.md) |
| "`dotnet build` output is deployable" | It isn't. `publish` gathers all dependencies plus `deps.json` and `runtimeconfig.json`. Build output may start, then fail on an uncopied package. | [3.8](notes/03-dotnet-runtime/3.08-dotnet-cli.md) |
| "`netstandard2.1` is the better .NET Standard" | .NET Framework **never supported it**, which removes the only reason to target Standard. Target `net10.0` instead. | [3.9](notes/03-dotnet-runtime/3.09-dotnet-standard.md) |
| "STS releases are previews" | They're **full production releases**. The only difference is 18 months of support versus 3 years. | [3.10](notes/03-dotnet-runtime/3.10-release-cadence.md) |
| "A newer .NET is always supported longer" | .NET 7 (STS) went **out of support before** .NET 6 (LTS), despite shipping a year later. | [3.10](notes/03-dotnet-runtime/3.10-release-cadence.md) |

## Configuration and options

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "I set it in `appsettings.json`, so that's the value" | **Later providers win.** An environment variable set by the hosting platform silently overrides it. `GetDebugView()` shows which provider supplied each value. | [7.1](notes/07-configuration-options/7.01-configuration-system.md) |
| "`ConnectionStrings_Default` sets the connection string" | Nested keys need **double** underscores — `ConnectionStrings__Default`. A single one silently does nothing. | [7.1](notes/07-configuration-options/7.01-configuration-system.md) |
| "Overriding an array in a later file replaces it" | Arrays are **indexed keys**, merged per index. A 1-item override of a 3-item list leaves items 2 and 3 in place — a real problem for CORS origins. | [7.2](notes/07-configuration-options/7.02-appsettings.md) |
| "`appsettings.production.json` works fine" | File names are **case-sensitive on Linux**. It's silently ignored when the environment is `Production` — and works on Windows. | [7.2](notes/07-configuration-options/7.02-appsettings.md) |
| "Only the active environment's JSON file is deployed" | **All of them ship** in the published output, including the Development one. "It's only for dev" is not protection. | [7.2](notes/07-configuration-options/7.02-appsettings.md) |
| "User Secrets are encrypted" | They're **plain JSON** in your user profile. The protection is being outside source control, not being secure at rest. | [7.3](notes/07-configuration-options/7.03-env-args-usersecrets.md) |
| "`CreateBuilder()` is fine without `args`" | That silently disables **command-line configuration** entirely. It compiles and runs. | [7.3](notes/07-configuration-options/7.03-env-args-usersecrets.md) |
| "Environment variables are a fine place for production secrets" | They're visible to the whole process, appear in crash dumps, and the **developer exception page renders every one** into the browser. | [7.3](notes/07-configuration-options/7.03-env-args-usersecrets.md) |
| "Key Vault secrets use `__` like environment variables" | **Double hyphen** — `Payments--ApiKey`. That's a *third* escape convention after `:` and `__`. | [7.4](notes/07-configuration-options/7.04-secret-providers.md) |
| "Rotated secrets are picked up automatically" | Read **once at startup** unless you set a `ReloadInterval` — and even then `IOptions<T>` won't see the change. | [7.4](notes/07-configuration-options/7.04-secret-providers.md) |
| "A missing config key throws" | It returns **null**, and `GetValue<int>` returns **0**. A missing batch size silently becomes zero. A *malformed* value does throw — inconsistently. | [7.5](notes/07-configuration-options/7.05-iconfiguration-api.md) |
| "I'll null-check `GetSection`" | It **never returns null** — an absent section is an empty one. Use `Exists()` or `GetRequiredSection`. | [7.5](notes/07-configuration-options/7.05-iconfiguration-api.md) |
| "`IOptionsSnapshot<T>` is the modern `IOptions<T>`" | It's **scoped**. In a singleton or conventional middleware that's a captive dependency — use `IOptionsMonitor<T>`. | [7.6](notes/07-configuration-options/7.06-options-pattern.md) |
| "`CurrentValue` is safe to read repeatedly" | It re-reads **every access**, so two reads in one method can return different objects. Capture it once per operation. | [7.6](notes/07-configuration-options/7.06-options-pattern.md) |
| "`required` on an options property is enforced" | The binder uses **reflection**, bypassing the compiler check. Use `[Required]` + `ValidateOnStart`. | [7.7](notes/07-configuration-options/7.07-binding-to-poco.md) |
| "A typo in a config key will show up" | Silent in **both** directions — an unmatched key is ignored, an unmatched property keeps its default. | [7.7](notes/07-configuration-options/7.07-binding-to-poco.md) |
| "Positional records bind to configuration" | No parameterless constructor, so they don't. Use a class with settable properties. | [7.7](notes/07-configuration-options/7.07-binding-to-poco.md) |
| "`ValidateDataAnnotations()` fails the app at startup" | Validation is **lazy** — it runs on first `.Value` access. **`ValidateOnStart()`** is the line that matters. | [7.8](notes/07-configuration-options/7.08-options-validation.md) |
| "`[Required]` catches a missing setting" | On a **string** it accepts `""` unless you set `AllowEmptyStrings = false`. On an **int** it's meaningless — use `[Range]`. | [7.8](notes/07-configuration-options/7.08-options-validation.md) |
| "Config changes apply without a restart" | Only for `IOptionsMonitor`/`IOptionsSnapshot`. **`IOptions<T>`, connection strings, Kestrel endpoints and DI registrations are all fixed at startup.** | [7.9](notes/07-configuration-options/7.09-reload-on-change.md) |
| "Environment variables reload with the rest" | **Never.** A process reads its environment once at start — an OS behaviour, not a framework one. So most deployments reload nothing. | [7.9](notes/07-configuration-options/7.09-reload-on-change.md) |
| "`OnChange` fires once per edit" | Editors write in two steps, so it commonly fires **twice**. Debounce it, and dispose the subscription or it leaks. | [7.9](notes/07-configuration-options/7.09-reload-on-change.md) |
| "A custom provider can inject `DbContext`" | Providers run **before DI exists**. And a throwing `Load()` stops the app booting — a config source that's also a runtime dependency is risky. | [7.10](notes/07-configuration-options/7.10-custom-provider.md) |
| "`PercentageFilter` gives a 10% rollout" | It's evaluated **per call**, so one user gets different answers on refresh. Use `TargetingFilter` for a real rollout. | [7.11](notes/07-configuration-options/7.11-feature-flags.md) |
| "A misspelled feature flag will error" | `IsEnabledAsync` returns **false** for an unknown flag, so the feature is silently off forever. Use constants. | [7.11](notes/07-configuration-options/7.11-feature-flags.md) |

## Security

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "JWTs are encrypted" | A standard JWT is **signed, not encrypted**. The payload is base64 — anyone can read it. Never put secrets in a JWT. | [15.5](notes/15-authentication/15.05-jwt-structure.md) |
| "Store the JWT in localStorage" | localStorage is readable by any XSS payload. An `HttpOnly`, `Secure`, `SameSite` cookie is safer for browser clients. | [15.12](notes/15-authentication/15.12-token-storage.md) |
| "You can't revoke a JWT, so it's insecure" | You *can't* revoke a stateless token — that's why access tokens are short-lived and revocation happens at the refresh-token layer. | [15.7](notes/15-authentication/15.07-refresh-tokens.md) |
| "APIs don't need CSRF protection" | Cookie-authenticated APIs absolutely do. Bearer-token APIs don't, because the browser doesn't attach the token automatically. The distinction is *how you authenticate*, not *whether you're an API*. | [17.4](notes/17-application-security/17.04-csrf.md) |
| "CORS protects my API" | CORS is a **browser** restriction, not a server-side access control. `curl` ignores it entirely. It is not authorization. | [10.10](notes/10-web-api-rest/10.10-cors.md) |
| "EF Core makes SQL injection impossible" | Only for LINQ. `FromSqlRaw`, `ExecuteSqlRaw`, and dynamic SQL are all still injectable. | [17.2](notes/17-application-security/17.02-sql-injection.md) |
| "Auth works locally, so it works in the farm" | Data Protection keys are per-machine by default. Two servers means cookies and antiforgery tokens issued by one are rejected by the other. | [17.6](notes/17-application-security/17.06-data-protection.md) |

## Web API

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "PUT and PATCH are basically the same" | PUT **replaces** the whole resource and is idempotent. PATCH applies a partial change and is not necessarily idempotent. | [10.2](notes/10-web-api-rest/10.02-http-verbs-idempotency.md) |
| "POST is idempotent if I write it carefully" | POST is *defined* as non-idempotent. Making a POST endpoint safe to retry requires an explicit idempotency key. | [10.13](notes/10-web-api-rest/10.13-idempotency-etags.md) |
| "I need to check `ModelState.IsValid` in every action" | With `[ApiController]`, invalid models are auto-rejected with a 400 before your action runs. The manual check is dead code. | [10.4](notes/10-web-api-rest/10.04-apicontroller-attribute.md) |
| "Return the entity — a DTO is boilerplate" | Entities leak your schema, invite over-posting, and cause lazy-loading serialization cycles. The DTO is the boundary. | [10.11](notes/10-web-api-rest/10.11-dtos-and-mapping.md) |
| "404 means the route was wrong" | It also means "resource not found" — and returning 404 vs 403 for an unauthorized resource is a deliberate choice about information disclosure. | [10.3](notes/10-web-api-rest/10.03-status-codes.md) |

## Performance

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "`new HttpClient()` per call, wrapped in `using`" | Sockets stay in `TIME_WAIT` after disposal. Under load this exhausts ports. Use `IHttpClientFactory`. | [19.10](notes/19-caching-performance/19.10-httpclientfactory.md) |
| "A static `HttpClient` fixes it" | It fixes socket exhaustion but never picks up DNS changes. `IHttpClientFactory` handles both via handler rotation. | [19.10](notes/19-caching-performance/19.10-httpclientfactory.md) |
| "`IMemoryCache` works fine when we scale out" | Each instance has its own cache. Users get inconsistent reads depending on which server they hit. | [19.3](notes/19-caching-performance/19.03-distributed-cache-redis.md) |
| "Adding a cache made it faster, done" | Without stampede protection, a cache miss on a hot key sends every concurrent request to the database at once. | [19.4](notes/19-caching-performance/19.04-hybridcache.md) |

## C#

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "`throw ex;` and `throw;` are the same" | `throw ex;` resets the stack trace, destroying the original throw site. Use bare `throw;`. | [1.20](notes/01-csharp-fundamentals/1.20-exceptions.md) |
| "Structs are always faster than classes" | Large structs are expensive to copy, and boxing them undoes the benefit entirely. The guidance is small, immutable, and short-lived. | [1.2](notes/01-csharp-fundamentals/1.02-struct-class-record.md) |
| "Nullable reference types stop null reference exceptions" | They're **compile-time hints only**. Nothing is enforced at runtime, and data crossing a serialization boundary ignores them completely. | [1.15](notes/01-csharp-fundamentals/1.15-nullability.md) |
| "Value types always live on the stack" | Only as locals. As class fields, captured lambda variables, or async locals they live on the heap. | [1.1](notes/01-csharp-fundamentals/1.01-value-vs-reference-types.md) |
| "Passing a class means pass by reference" | It passes a *reference*, but **by value**. Reassigning the parameter does not change the caller's variable. | [1.1](notes/01-csharp-fundamentals/1.01-value-vs-reference-types.md) |
| "`record` means immutable" | It means **value equality plus `with`**. Immutability comes from `init`, which the positional form happens to generate. | [1.2](notes/01-csharp-fundamentals/1.02-struct-class-record.md) |
| "`name.Trim();` trims the string" | Strings are immutable. Every method returns a *new* string — you must assign the result. | [1.3](notes/01-csharp-fundamentals/1.03-strings-and-stringbuilder.md) |
| "`StringBuilder` is always faster than `+`" | For a fixed handful of joins the compiler emits one `String.Concat`, which beats a `StringBuilder`. Use it for loops and unknown counts. | [1.3](notes/01-csharp-fundamentals/1.03-strings-and-stringbuilder.md) |
| "`protected internal` is the restrictive one" | Backwards. `protected internal` = assembly **OR** derived (wider). `private protected` = derived **AND** same assembly (narrower). | [1.4](notes/01-csharp-fundamentals/1.04-access-modifiers.md) |
| "Changing a `const` in a library updates consumers" | `const` values are **inlined into the consuming assembly**. They keep the old value until recompiled. Use `static readonly`. | [1.6](notes/01-csharp-fundamentals/1.06-const-readonly-init-required.md) |
| "`readonly` makes the object immutable" | It only stops the **field** being reassigned. A `readonly List<T>` can still be added to. | [1.6](notes/01-csharp-fundamentals/1.06-const-readonly-init-required.md) |
| "`new` and `override` do the same thing" | `override` dispatches on the **runtime object**; `new` dispatches on the **declared variable type**. Same object, two answers. | [1.7](notes/01-csharp-fundamentals/1.07-inheritance.md) |
| "You can call a virtual method from a constructor" | Base constructors run first, so the derived override runs before the derived fields are initialised. Null reference exceptions that look impossible. | [1.7](notes/01-csharp-fundamentals/1.07-inheritance.md) |
| "A `for` loop lambda captures the value" | It captures the **variable**, and a `for` loop has only one. All lambdas see the final value. `foreach` is safe since C# 5; `for` is not. | [1.13](notes/01-csharp-fundamentals/1.13-lambdas-closures.md) |
| "An extension method with the same name overrides the real one" | The real instance method always wins, silently. No warning that your extension was ignored. | [1.14](notes/01-csharp-fundamentals/1.14-extension-methods.md) |
| "`a?.B.C` protects the whole chain" | Only `a`. If `B` is null you still get a `NullReferenceException`. Every link needs its own `?.`. | [1.16](notes/01-csharp-fundamentals/1.16-null-operators.md) |
| "`??` handles empty strings" | It only checks **null**. `""`, `0` and `false` all pass through as real values. | [1.16](notes/01-csharp-fundamentals/1.16-null-operators.md) |
| "`var` and `dynamic` are similar" | `var` is compile-time inference with full type safety and zero runtime cost. `dynamic` disables type checking entirely. Nothing alike. | [1.22](notes/01-csharp-fundamentals/1.22-anonymous-dynamic-var.md) |
| "A finalizer is how you clean up" | A finalizer makes the object survive an **extra GC cycle** and runs at an unpredictable time. It's a last-resort safety net. Use `IDisposable`. | [1.21](notes/01-csharp-fundamentals/1.21-idisposable.md) |
| "A class primary constructor parameter is a property" | In a **record** it is. In a **class** it's a private, mutable captured field — not exposed, not readonly. | [1.26](notes/01-csharp-fundamentals/1.26-modern-csharp-versions.md) |
| "`Single()` and `First()` differ only in style" | `Single()` throws if there's more than one match — and to know that, it must scan further. Different semantics *and* different cost. | [2.9](notes/02-collections-linq-async/2.09-first-single-default.md) |
| "Enumerating an `IEnumerable` twice is free" | For a deferred query it executes twice. Against a database, that's two round trips. | [2.6](notes/02-collections-linq-async/2.06-deferred-execution.md) |

## Collections and LINQ

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "Returning `IEnumerable<T>` from a repository is good practice" | It **silently kills SQL translation**. Every later `Where` runs in memory over the whole table. Return `IReadOnlyList<T>` after materialising. | [2.1](notes/02-collections-linq-async/2.01-collection-interfaces.md) |
| "`.Count()` and `.Count` are the same" | `.Count()` on an `IEnumerable` **walks the entire sequence**. `.Count` on an `ICollection` is an instant property. | [2.1](notes/02-collections-linq-async/2.01-collection-interfaces.md) |
| "`list.Contains(x)` is fine inside a loop" | That's O(n×m). Two lists of 10,000 = 100 million comparisons. Convert to a `HashSet` first — one character, ~10,000× faster. | [2.2](notes/02-collections-linq-async/2.02-collections-and-big-o.md) |
| "`Dictionary` iteration order is stable" | **No order is guaranteed**, ever. It looks stable in testing and changes when the internal array resizes. | [2.2](notes/02-collections-linq-async/2.02-collections-and-big-o.md) |
| "A `ConcurrentDictionary` makes my code thread-safe" | Each *operation* is safe; a *sequence* of them is not. `if (!d.ContainsKey(k)) d[k]=v` still races. Use `GetOrAdd`. | [2.3](notes/02-collections-linq-async/2.03-concurrent-collections.md) |
| "`GetOrAdd`'s factory runs once" | Only the **store** is atomic. The factory can run on several threads at once. Wrap in `Lazy<T>` if it's expensive or has side effects. | [2.3](notes/02-collections-linq-async/2.03-concurrent-collections.md) |
| "Argument validation in an iterator method throws when called" | The whole body is deferred, **including the validation**. It throws at the `foreach`, far from the cause. Split into an outer method + local iterator. | [2.4](notes/02-collections-linq-async/2.04-yield-and-iterators.md) |
| "A second `OrderBy` adds a secondary sort" | It **discards the first sort entirely**. Use `ThenBy`. | [2.5](notes/02-collections-linq-async/2.05-linq-basics.md) |
| "`Count() > 0` and `Any()` are equivalent" | `Any()` stops at the first match; `Count()` walks everything. Against a DB that's `EXISTS` vs `COUNT(*)`. | [2.5](notes/02-collections-linq-async/2.05-linq-basics.md) |
| "A LINQ query runs when you write it" | It's a **recipe, not a meal**. It runs on enumeration — and runs *again* every time you enumerate. | [2.6](notes/02-collections-linq-async/2.06-deferred-execution.md) |
| "`Func<T,bool>` and `Expression<Func<T,bool>>` are interchangeable" | `Func` is compiled code you can only run. `Expression` is **data describing code**, which is the only reason EF Core can emit SQL. | [2.7](notes/02-collections-linq-async/2.07-expression-trees.md) |
| "'Could not be translated' is EF Core being unhelpful" | It's the **good** outcome. The old behaviour was silent client evaluation — downloading the whole table. | [2.7](notes/02-collections-linq-async/2.07-expression-trees.md) |
| "`Sum`, `Max` and `Average` behave the same on an empty sequence" | `Sum` returns 0. `Max`, `Min` and `Average` **throw**. | [2.8](notes/02-collections-linq-async/2.08-linq-advanced-operators.md) |
| "`FirstOrDefault` returns null when nothing matches" | For a **value type** it returns `0` / `false`. You cannot tell "missing" from "legitimately zero". | [2.9](notes/02-collections-linq-async/2.09-first-single-default.md) |

## Async and threading (section 2)

| ⚠️ The plausible answer | ✅ What's actually true | Topic |
|---|---|---|
| "A `Task` runs on a separate thread" | Not for I/O. During an async network call **no thread exists for that operation** — the hardware does the work. | [2.10](notes/02-collections-linq-async/2.10-threads-vs-tasks.md) |
| "`Task.Run` makes I/O faster" | It **blocks a pool thread** on something designed not to need one. Just `await` the async method. | [2.10](notes/02-collections-linq-async/2.10-threads-vs-tasks.md) |
| "`await` pauses the method" | It **returns to the caller** and registers a callback. Nothing is paused; the thread is released. | [2.11](notes/02-collections-linq-async/2.11-async-await-internals.md) |
| "Three awaits in a row run concurrently" | They're strictly sequential. Capture the tasks *first*, then `await Task.WhenAll` — 600 ms becomes 200 ms. | [2.12](notes/02-collections-linq-async/2.12-task-valuetask.md) |
| "`Task.WhenAll` gives you all the exceptions" | Awaiting rethrows only the **first**. The rest are on `task.Exception.InnerExceptions`. | [2.12](notes/02-collections-linq-async/2.12-task-valuetask.md) |
| "`ValueTask` is a faster `Task`, use it everywhere" | Await it **once only**, never block on it, never pass it to `WhenAll`. It's a library-author optimisation. | [2.12](notes/02-collections-linq-async/2.12-task-valuetask.md) |
| "`.Result` is safe in ASP.NET Core since there's no deadlock" | True about deadlock, but it **blocks a pool thread** → thread-pool starvation. Signature: huge latency with idle CPU. | [2.13](notes/02-collections-linq-async/2.13-async-deadlocks.md) |
| "Add `ConfigureAwait(false)` everywhere" | In ASP.NET Core app code it does **nothing** — there's no context. It matters in **libraries**. | [2.13](notes/02-collections-linq-async/2.13-async-deadlocks.md) |
| "Accepting a `CancellationToken` makes a method cancellable" | Only if you **pass it down and check it**. An ignored token is worse than none — it advertises a capability that doesn't exist. | [2.14](notes/02-collections-linq-async/2.14-cancellation.md) |
| "`OperationCanceledException` should be logged as an error" | It's **routine traffic** — a user closed a tab. Logging it as an error buries real failures. | [2.14](notes/02-collections-linq-async/2.14-cancellation.md) |
| "A try/catch around an `async void` call catches its exceptions" | It catches nothing — the method already returned. The exception **crashes the process**. | [2.15](notes/02-collections-linq-async/2.15-async-void.md) |
| "`list.ForEach(async x => await F(x))` awaits each item" | `ForEach` takes an `Action`, so every lambda is **`async void`**. Use `foreach` or `Task.WhenAll`. | [2.15](notes/02-collections-linq-async/2.15-async-void.md) |
| "`catch (SqlException)` works the same either way" | With `await`, yes. With `.Result`, the exception is wrapped in **`AggregateException`** and the typed catch is dead code. | [2.16](notes/02-collections-linq-async/2.16-async-exceptions.md) |
| "`[EnumeratorCancellation]` is optional boilerplate" | Without it, `WithCancellation` is **silently ignored** and your async stream cannot be cancelled. | [2.17](notes/02-collections-linq-async/2.17-async-streams.md) |
| "`count++` is one operation" | It's read, add, write. Two threads interleave and an increment is lost. Use `Interlocked.Increment`. | [2.18](notes/02-collections-linq-async/2.18-thread-safety.md) |
| "`volatile` makes a field thread-safe" | It only stops caching and reordering. It does **not** make operations atomic — `volatile` `count++` still races. | [2.18](notes/02-collections-linq-async/2.18-thread-safety.md) |
| "`Parallel.ForEach` speeds up my API endpoint" | The server is **already parallel**. It steals threads from other requests, so one request gets faster and total throughput drops. | [2.19](notes/02-collections-linq-async/2.19-parallel-programming.md) |
| "Adding to a `List<T>` inside `Parallel.ForEach` is fine" | `List<T>` is not thread-safe — you get lost items, corruption, or `IndexOutOfRangeException`. Use a concurrent collection. | [2.19](notes/02-collections-linq-async/2.19-parallel-programming.md) |

---

## Add your own

The traps you personally get wrong are worth ten of the ones above. Every time you fumble
something in a mock or a real interview, add a row here the same day.

| ⚠️ What I said | ✅ What's actually true | Date |
|---|---|---|
| | | |

# ASP.NET Core Interview Preparation — Master Roadmap

**[README](index.md)** · **[Cheat Sheet](CHEATSHEET.md)** · **[Traps](TRAPS.md)** · **[Progress Tracker](PROGRESS.md)** · **[Question Bank](practice/QUESTION-BANK.md)** · **[Diagrams](DIAGRAMS.md)**

---

## Legend

| Marker | Meaning |
|:--:|---|
| 🔥 | **Near-certain.** Asked in almost every ASP.NET Core interview. If you know nothing else, know these. |
| ⭐ | **Common.** Shows up regularly. Expect at least a few of these per interview. |
| 💻 | **Hands-on.** You must be able to *write* this on a whiteboard or in a live-coding round — describing it is not enough. |
| ⚠️ | **Trap.** A classic gotcha. Interviewers use these to separate people who've read a blog from people who've shipped. |
| 🧠 | **Senior.** Only needed if you're targeting senior/lead/architect roles. Safe to skip for junior interviews. |
| 🎯 | **Diagram.** Worth being able to draw. Practise it on paper. |

Checkboxes track **"notes written and read."** Track your *recall confidence* separately in **[PROGRESS.md](PROGRESS.md)** — the two are not the same thing, and confidence is what actually decays.

> Topic numbers are permanent. Once a note file exists at a number, that number never changes.
> Links below are pre-wired — they will be dead until the corresponding note is written.

---

# Phase 0 — Prerequisites

## 1. C# Language Fundamentals

- [x] **1.1** [Value types vs reference types, stack vs heap, boxing/unboxing](notes/01-csharp-fundamentals/1.01-value-vs-reference-types.md) 🔥 ⚠️ 🎯
- [x] **1.2** [`struct` vs `class` vs `record` vs `record struct`](notes/01-csharp-fundamentals/1.02-struct-class-record.md) ⭐ 💻
- [x] **1.3** [String immutability, `StringBuilder`, interning](notes/01-csharp-fundamentals/1.03-strings-and-stringbuilder.md) ⭐
- [x] **1.4** [Access modifiers, including `protected internal` and `private protected`](notes/01-csharp-fundamentals/1.04-access-modifiers.md)
- [x] **1.5** [`static` — classes, members, constructors, local functions](notes/01-csharp-fundamentals/1.05-static.md)
- [x] **1.6** [`const` vs `readonly` vs `init` vs `required`](notes/01-csharp-fundamentals/1.06-const-readonly-init-required.md) ⭐ ⚠️
- [x] **1.7** [Inheritance — `virtual` / `override` / `new` / `sealed` / `abstract`](notes/01-csharp-fundamentals/1.07-inheritance.md) 🔥 ⚠️
- [x] **1.8** [Interfaces — explicit implementation, default methods, vs abstract class](notes/01-csharp-fundamentals/1.08-interfaces.md) 🔥 💻
- [x] **1.9** [Polymorphism — overloading vs overriding](notes/01-csharp-fundamentals/1.09-polymorphism.md) ⭐
- [x] **1.10** [Generics — constraints, covariance and contravariance](notes/01-csharp-fundamentals/1.10-generics.md) ⭐ 🧠
- [x] **1.11** [Delegates, `Func`, `Action`, `Predicate`, multicast](notes/01-csharp-fundamentals/1.11-delegates.md) ⭐ 💻
- [x] **1.12** [Events — and the memory leak from unsubscribed handlers](notes/01-csharp-fundamentals/1.12-events.md) ⭐ ⚠️
- [x] **1.13** [Lambdas and closures — the captured-loop-variable trap](notes/01-csharp-fundamentals/1.13-lambdas-closures.md) ⭐ ⚠️
- [x] **1.14** [Extension methods — resolution rules and appropriate use](notes/01-csharp-fundamentals/1.14-extension-methods.md) ⭐ 💻
- [x] **1.15** [Nullable value types vs nullable reference types](notes/01-csharp-fundamentals/1.15-nullability.md) 🔥 ⚠️
- [x] **1.16** [Null-handling operators — `??`, `??=`, `?.`, `?[]`](notes/01-csharp-fundamentals/1.16-null-operators.md)
- [x] **1.17** [Pattern matching and switch expressions](notes/01-csharp-fundamentals/1.17-pattern-matching.md) ⭐ 💻
- [x] **1.18** [Tuples, deconstruction, `out` / `ref` / `in`](notes/01-csharp-fundamentals/1.18-tuples-ref-out-in.md) ⭐
- [x] **1.19** [Indexers, operator overloading, conversion operators](notes/01-csharp-fundamentals/1.19-indexers-operators.md)
- [x] **1.20** [Exception handling — filters, custom exceptions, `throw` vs `throw ex`](notes/01-csharp-fundamentals/1.20-exceptions.md) 🔥 ⚠️ 💻
- [x] **1.21** [`IDisposable`, `using`, `IAsyncDisposable`, finalizers](notes/01-csharp-fundamentals/1.21-idisposable.md) 🔥 💻
- [x] **1.22** [Anonymous types, `dynamic`, `var` — and when each is wrong](notes/01-csharp-fundamentals/1.22-anonymous-dynamic-var.md)
- [x] **1.23** [Attributes and reflection basics](notes/01-csharp-fundamentals/1.23-attributes-reflection.md) ⭐
- [x] **1.24** [Partial classes, partial methods, local functions](notes/01-csharp-fundamentals/1.24-partial-local-functions.md)
- [x] **1.25** [`Span<T>`, `Memory<T>`, `stackalloc`](notes/01-csharp-fundamentals/1.25-span-memory.md) 🧠
- [x] **1.26** [Modern C# by version (C# 8 → 14)](notes/01-csharp-fundamentals/1.26-modern-csharp-versions.md) ⭐

## 2. Collections, LINQ and Async

- [x] **2.1** [`IEnumerable` vs `ICollection` vs `IList` vs `IQueryable`](notes/02-collections-linq-async/2.01-collection-interfaces.md) 🔥 ⚠️
- [x] **2.2** [Core collections and their Big-O](notes/02-collections-linq-async/2.02-collections-and-big-o.md) ⭐ 🎯
- [x] **2.3** [Concurrent collections](notes/02-collections-linq-async/2.03-concurrent-collections.md) ⭐
- [x] **2.4** [`IEnumerator`, `yield return`, deferred execution](notes/02-collections-linq-async/2.04-yield-and-iterators.md) ⭐ 💻
- [x] **2.5** [LINQ query vs method syntax; the standard operators](notes/02-collections-linq-async/2.05-linq-basics.md) ⭐ 💻
- [x] **2.6** [Deferred vs immediate execution; multiple-enumeration pitfalls](notes/02-collections-linq-async/2.06-deferred-execution.md) 🔥 ⚠️
- [x] **2.7** [`IQueryable` and expression trees — how LINQ becomes SQL](notes/02-collections-linq-async/2.07-expression-trees.md) ⭐ 🧠
- [x] **2.8** [`GroupBy`, `Join`, `SelectMany`, `Aggregate`, `Zip`](notes/02-collections-linq-async/2.08-linq-advanced-operators.md) ⭐ 💻
- [x] **2.9** [`First` vs `FirstOrDefault` vs `Single` vs `SingleOrDefault`](notes/02-collections-linq-async/2.09-first-single-default.md) 🔥 ⚠️
- [x] **2.10** [Threads, `ThreadPool`, `Task` vs `Thread`](notes/02-collections-linq-async/2.10-threads-vs-tasks.md) 🔥 🎯
- [x] **2.11** [`async` / `await` — the state machine underneath](notes/02-collections-linq-async/2.11-async-await-internals.md) 🔥 🎯 🧠
- [x] **2.12** [`Task` vs `ValueTask`, `WhenAll`, `WhenAny`, `Task.Run`](notes/02-collections-linq-async/2.12-task-valuetask.md) ⭐ 💻
- [x] **2.13** [Deadlocks — `.Result`, `.Wait()`, `ConfigureAwait(false)`](notes/02-collections-linq-async/2.13-async-deadlocks.md) 🔥 ⚠️
- [x] **2.14** [`CancellationToken` and cooperative cancellation](notes/02-collections-linq-async/2.14-cancellation.md) 🔥 💻
- [x] **2.15** [`async void` — why it is almost always wrong](notes/02-collections-linq-async/2.15-async-void.md) 🔥 ⚠️
- [x] **2.16** [Exceptions in async code, `AggregateException`](notes/02-collections-linq-async/2.16-async-exceptions.md) ⭐ ⚠️
- [x] **2.17** [`IAsyncEnumerable<T>` and `await foreach`](notes/02-collections-linq-async/2.17-async-streams.md) ⭐
- [x] **2.18** [Thread safety — `lock`, `SemaphoreSlim`, `Interlocked`, `volatile`](notes/02-collections-linq-async/2.18-thread-safety.md) ⭐ ⚠️
- [x] **2.19** [`Parallel.For`, PLINQ — and when not to use them](notes/02-collections-linq-async/2.19-parallel-programming.md) ⭐ ⚠️

## 3. .NET Runtime and Platform

- [ ] **3.1** [.NET Framework vs .NET Core vs .NET 5+](notes/03-dotnet-runtime/3.01-dotnet-history.md) 🔥
- [ ] **3.2** [CLR, CTS, CLS, IL, JIT, AOT, ReadyToRun](notes/03-dotnet-runtime/3.02-clr-and-compilation.md) ⭐ 🎯
- [ ] **3.3** [Managed vs unmanaged code, `unsafe`, P/Invoke](notes/03-dotnet-runtime/3.03-managed-vs-unmanaged.md)
- [ ] **3.4** [Garbage collection — generations, LOH, GC modes](notes/03-dotnet-runtime/3.04-garbage-collection.md) 🔥 🎯
- [ ] **3.5** [Memory leaks in managed code](notes/03-dotnet-runtime/3.05-memory-leaks.md) 🔥 ⚠️
- [ ] **3.6** [Assemblies, load contexts, NuGet packaging](notes/03-dotnet-runtime/3.06-assemblies-nuget.md)
- [ ] **3.7** [SDK-style `.csproj`, target frameworks, multi-targeting](notes/03-dotnet-runtime/3.07-csproj-and-tfm.md) ⭐
- [ ] **3.8** [.NET CLI essentials](notes/03-dotnet-runtime/3.08-dotnet-cli.md) ⭐ 💻
- [ ] **3.9** [.NET Standard — what it was, why it's mostly history](notes/03-dotnet-runtime/3.09-dotnet-standard.md)
- [ ] **3.10** [Release cadence — LTS vs STS, current support matrix](notes/03-dotnet-runtime/3.10-release-cadence.md) ⭐

---

# Phase 1 — ASP.NET Core Core Concepts

> **This is the highest-value phase in the entire roadmap.** Sections 4–8 are what
> "ASP.NET Core interview" actually means. Do not skip ahead to EF Core until these are solid.

## 4. Fundamentals and Application Startup

- [ ] **4.1** [What ASP.NET Core is; differences from ASP.NET (System.Web)](notes/04-fundamentals-startup/4.01-what-is-aspnet-core.md) 🔥
- [ ] **4.2** [Cross-platform hosting, Kestrel, the reverse-proxy model](notes/04-fundamentals-startup/4.02-hosting-model.md) ⭐ 🎯
- [ ] **4.3** [`Program.cs` — Generic Host vs Minimal Hosting](notes/04-fundamentals-startup/4.03-program-cs-hosting.md) 🔥 💻
- [ ] **4.4** [The legacy `Startup.cs` model](notes/04-fundamentals-startup/4.04-startup-cs-legacy.md) ⭐
- [ ] **4.5** [`IHost`, `IHostBuilder`, `IWebHostEnvironment`, lifetime interfaces](notes/04-fundamentals-startup/4.05-host-interfaces.md) ⭐
- [ ] **4.6** [Application lifecycle — start, run, graceful shutdown](notes/04-fundamentals-startup/4.06-app-lifecycle.md) ⭐ 🎯
- [ ] **4.7** [Environments and `ASPNETCORE_ENVIRONMENT`](notes/04-fundamentals-startup/4.07-environments.md) 🔥
- [ ] **4.8** [`launchSettings.json` — and why it is dev-only](notes/04-fundamentals-startup/4.08-launchsettings.md) ⚠️
- [ ] **4.9** [Kestrel vs IIS vs HTTP.sys; in-process vs out-of-process](notes/04-fundamentals-startup/4.09-kestrel-iis-httpsys.md) ⭐ 🎯
- [ ] **4.10** [`wwwroot` and static file serving](notes/04-fundamentals-startup/4.10-static-files.md) ⭐
- [ ] **4.11** [Project structure conventions for a Web API](notes/04-fundamentals-startup/4.11-project-structure.md) ⭐

## 5. Middleware and the Request Pipeline

- [ ] **5.1** [What middleware is; the pipeline model](notes/05-middleware-pipeline/5.01-what-is-middleware.md) 🔥 🎯
- [ ] **5.2** [Middleware order — and the canonical ordering](notes/05-middleware-pipeline/5.02-middleware-order.md) 🔥 ⚠️ 🎯
- [ ] **5.3** [`Use` vs `Run` vs `Map` vs `MapWhen` vs `UseWhen`](notes/05-middleware-pipeline/5.03-use-run-map.md) 🔥 💻
- [ ] **5.4** [Inline custom middleware](notes/05-middleware-pipeline/5.04-inline-middleware.md) ⭐ 💻
- [ ] **5.5** [Conventional middleware class with `InvokeAsync`](notes/05-middleware-pipeline/5.05-conventional-middleware.md) 🔥 💻
- [ ] **5.6** [Factory-based middleware (`IMiddleware`) and scoped services](notes/05-middleware-pipeline/5.06-imiddleware-factory.md) ⭐ ⚠️
- [ ] **5.7** [Short-circuiting and terminal middleware](notes/05-middleware-pipeline/5.07-short-circuiting.md) ⭐
- [ ] **5.8** [`HttpContext` — Request, Response, Items, Features, User](notes/05-middleware-pipeline/5.08-httpcontext.md) 🔥
- [ ] **5.9** [Reading and rewinding the request body (`EnableBuffering`)](notes/05-middleware-pipeline/5.09-request-body-buffering.md) ⚠️ 💻
- [ ] **5.10** [Tour of the built-in middleware](notes/05-middleware-pipeline/5.10-builtin-middleware.md) ⭐
- [ ] **5.11** [Global exception-handling middleware](notes/05-middleware-pipeline/5.11-exception-middleware.md) 🔥 💻
- [ ] **5.12** [`IExceptionHandler` (.NET 8+) vs developer exception page](notes/05-middleware-pipeline/5.12-iexceptionhandler.md) ⭐ 💻
- [ ] **5.13** [Middleware vs filters — when to use which](notes/05-middleware-pipeline/5.13-middleware-vs-filters.md) 🔥 🎯
- [ ] **5.14** [Request/response logging middleware and its pitfalls](notes/05-middleware-pipeline/5.14-logging-middleware.md) ⭐ ⚠️

## 6. Dependency Injection

- [ ] **6.1** [Inversion of Control and Dependency Injection](notes/06-dependency-injection/6.01-ioc-and-di.md) 🔥 🎯
- [ ] **6.2** [The built-in container, `IServiceCollection`, `IServiceProvider`](notes/06-dependency-injection/6.02-builtin-container.md) 🔥 💻
- [ ] **6.3** [Service lifetimes — Transient, Scoped, Singleton](notes/06-dependency-injection/6.03-service-lifetimes.md) 🔥 ⚠️ 🎯
- [ ] **6.4** [The captive dependency problem](notes/06-dependency-injection/6.04-captive-dependency.md) 🔥 ⚠️
- [ ] **6.5** [What a scope is; creating manual scopes](notes/06-dependency-injection/6.05-scopes.md) 🔥 💻
- [ ] **6.6** [`Add` vs `TryAdd` vs `TryAddEnumerable`; keyed services](notes/06-dependency-injection/6.06-registration-apis.md) ⭐
- [ ] **6.7** [Multiple implementations and `IEnumerable<TService>`](notes/06-dependency-injection/6.07-multiple-implementations.md) ⭐ 💻
- [ ] **6.8** [Factory registrations and open generics](notes/06-dependency-injection/6.08-factories-open-generics.md) ⭐
- [ ] **6.9** [Constructor injection vs `[FromServices]` vs service locator](notes/06-dependency-injection/6.09-injection-styles.md) ⭐ ⚠️
- [ ] **6.10** [Who disposes what — container-managed disposal](notes/06-dependency-injection/6.10-disposal.md) ⭐ ⚠️
- [ ] **6.11** [Third-party containers — Autofac, Scrutor](notes/06-dependency-injection/6.11-third-party-containers.md) 🧠
- [ ] **6.12** [Designing for testability through DI](notes/06-dependency-injection/6.12-di-and-testability.md) ⭐
- [ ] **6.13** [Classic DI interview traps](notes/06-dependency-injection/6.13-di-traps.md) 🔥 ⚠️

## 7. Configuration and Options

- [ ] **7.1** [The configuration system — providers and precedence](notes/07-configuration-options/7.01-configuration-system.md) 🔥 ⚠️
- [ ] **7.2** [`appsettings.json` and environment overrides](notes/07-configuration-options/7.02-appsettings.md) 🔥
- [ ] **7.3** [Environment variables, CLI args, User Secrets](notes/07-configuration-options/7.03-env-args-usersecrets.md) ⭐
- [ ] **7.4** [Key Vault / Secrets Manager providers](notes/07-configuration-options/7.04-secret-providers.md) ⭐
- [ ] **7.5** [`IConfiguration` API — sections, `GetValue`, connection strings](notes/07-configuration-options/7.05-iconfiguration-api.md) ⭐ 💻
- [ ] **7.6** [`IOptions` vs `IOptionsSnapshot` vs `IOptionsMonitor`](notes/07-configuration-options/7.06-options-pattern.md) 🔥 ⚠️
- [ ] **7.7** [Binding configuration to POCOs](notes/07-configuration-options/7.07-binding-to-poco.md) ⭐ 💻
- [ ] **7.8** [Options validation and `ValidateOnStart`](notes/07-configuration-options/7.08-options-validation.md) ⭐ 💻
- [ ] **7.9** [Reloadable configuration and its limits](notes/07-configuration-options/7.09-reload-on-change.md) ⚠️
- [ ] **7.10** [Writing a custom configuration provider](notes/07-configuration-options/7.10-custom-provider.md) 🧠 💻
- [ ] **7.11** [Feature flags and feature management](notes/07-configuration-options/7.11-feature-flags.md) ⭐

## 8. Routing

- [ ] **8.1** [Endpoint routing fundamentals](notes/08-routing/8.01-endpoint-routing.md) 🔥 🎯
- [ ] **8.2** [`UseRouting` and `UseEndpoints` — what happens between them](notes/08-routing/8.02-userouting-useendpoints.md) 🔥 ⚠️
- [ ] **8.3** [Conventional vs attribute routing](notes/08-routing/8.03-conventional-vs-attribute.md) 🔥 💻
- [ ] **8.4** [Route templates, parameters, optionals, defaults](notes/08-routing/8.04-route-templates.md) ⭐ 💻
- [ ] **8.5** [Route constraints, including custom ones](notes/08-routing/8.05-route-constraints.md) ⭐ 💻
- [ ] **8.6** [Route tokens, named routes, link generation](notes/08-routing/8.06-link-generation.md) ⭐
- [ ] **8.7** [Endpoint selection and precedence — how ties break](notes/08-routing/8.07-endpoint-precedence.md) ⭐ ⚠️
- [ ] **8.8** [Areas](notes/08-routing/8.08-areas.md)
- [ ] **8.9** [Route groups (`MapGroup`)](notes/08-routing/8.09-route-groups.md) ⭐ 💻
- [ ] **8.10** [Catch-all routes, slugs, SEO-friendly URLs](notes/08-routing/8.10-catchall-and-slugs.md)

---

# Phase 2 — Building Web APIs and Web Apps

## 9. MVC, Razor Pages and Views

- [ ] **9.1** [The MVC pattern in ASP.NET Core](notes/09-mvc-razor-views/9.01-mvc-pattern.md) 🔥 🎯
- [ ] **9.2** [`Controller` vs `ControllerBase`; action conventions](notes/09-mvc-razor-views/9.02-controllers.md) 🔥
- [ ] **9.3** [`IActionResult` vs `ActionResult<T>`; result types](notes/09-mvc-razor-views/9.03-action-results.md) 🔥 💻
- [ ] **9.4** [Razor syntax, layouts, `_ViewStart`, `_ViewImports`](notes/09-mvc-razor-views/9.04-razor-and-layouts.md) ⭐
- [ ] **9.5** [Partial views, View Components, Tag Helpers vs HTML Helpers](notes/09-mvc-razor-views/9.05-partials-components-taghelpers.md) ⭐
- [ ] **9.6** [ViewData vs ViewBag vs TempData](notes/09-mvc-razor-views/9.06-viewdata-viewbag-tempdata.md) 🔥 ⚠️
- [ ] **9.7** [Razor Pages and `PageModel`](notes/09-mvc-razor-views/9.07-razor-pages.md) ⭐ 💻
- [ ] **9.8** [ViewModels vs entities; strongly-typed views](notes/09-mvc-razor-views/9.08-viewmodels.md) ⭐
- [ ] **9.9** [Blazor overview — Server vs WASM vs Auto](notes/09-mvc-razor-views/9.09-blazor-overview.md) ⭐
- [ ] **9.10** [Front-end integration, bundling, minification](notes/09-mvc-razor-views/9.10-frontend-integration.md)

## 10. Web API Design and REST

- [ ] **10.1** [REST principles — resources, statelessness, uniform interface](notes/10-web-api-rest/10.01-rest-principles.md) 🔥 🎯
- [ ] **10.2** [HTTP verbs; idempotency and safety](notes/10-web-api-rest/10.02-http-verbs-idempotency.md) 🔥 ⚠️
- [ ] **10.3** [HTTP status codes that actually get asked about](notes/10-web-api-rest/10.03-status-codes.md) 🔥
- [ ] **10.4** [`[ApiController]` — what it changes](notes/10-web-api-rest/10.04-apicontroller-attribute.md) 🔥 ⚠️
- [ ] **10.5** [Content negotiation and JSON serialization](notes/10-web-api-rest/10.05-content-negotiation-json.md) 🔥 ⚠️
- [ ] **10.6** [API versioning strategies](notes/10-web-api-rest/10.06-api-versioning.md) ⭐ 💻
- [ ] **10.7** [Pagination, filtering, sorting conventions](notes/10-web-api-rest/10.07-pagination-filtering.md) ⭐ 💻
- [ ] **10.8** [`ProblemDetails` / RFC 7807 and consistent error contracts](notes/10-web-api-rest/10.08-problem-details.md) ⭐ 💻
- [ ] **10.9** [OpenAPI / Swagger — Swashbuckle, NSwag, built-in OpenAPI](notes/10-web-api-rest/10.09-openapi-swagger.md) ⭐
- [ ] **10.10** [CORS — preflight, policies, common misconfigurations](notes/10-web-api-rest/10.10-cors.md) 🔥 ⚠️ 🎯
- [ ] **10.11** [DTOs vs entities; mapping approaches](notes/10-web-api-rest/10.11-dtos-and-mapping.md) 🔥
- [ ] **10.12** [Minimal APIs — syntax, filters, when to choose them](notes/10-web-api-rest/10.12-minimal-apis.md) ⭐ 💻
- [ ] **10.13** [Idempotency keys, `ETag`, `If-Match`](notes/10-web-api-rest/10.13-idempotency-etags.md) 🧠
- [ ] **10.14** [REST vs gRPC vs GraphQL vs SOAP](notes/10-web-api-rest/10.14-rest-vs-grpc-vs-graphql.md) ⭐ 🎯

## 11. Model Binding and Validation

- [ ] **11.1** [Binding sources — `[FromBody]`, `[FromQuery]`, `[FromRoute]`, …](notes/11-model-binding-validation/11.01-binding-sources.md) 🔥 ⚠️
- [ ] **11.2** [How binding works — value providers, prefixes, collections](notes/11-model-binding-validation/11.02-how-binding-works.md) ⭐
- [ ] **11.3** [Custom model binders](notes/11-model-binding-validation/11.03-custom-model-binders.md) ⭐ 💻
- [ ] **11.4** [DataAnnotations validation attributes](notes/11-model-binding-validation/11.04-dataannotations.md) 🔥 💻
- [ ] **11.5** [`ModelState` and automatic 400 responses](notes/11-model-binding-validation/11.05-modelstate.md) 🔥 💻
- [ ] **11.6** [Custom validation attributes and `IValidatableObject`](notes/11-model-binding-validation/11.06-custom-validation.md) ⭐ 💻
- [ ] **11.7** [FluentValidation](notes/11-model-binding-validation/11.07-fluentvalidation.md) ⭐ 💻
- [ ] **11.8** [Client-side vs server-side validation](notes/11-model-binding-validation/11.08-client-vs-server-validation.md) ⭐
- [ ] **11.9** [File uploads — `IFormFile`, streaming, limits, security](notes/11-model-binding-validation/11.09-file-uploads.md) ⭐ ⚠️
- [ ] **11.10** [Over-posting / mass assignment](notes/11-model-binding-validation/11.10-over-posting.md) 🔥 ⚠️

## 12. Filters and Cross-Cutting Concerns

- [ ] **12.1** [The filter pipeline and the five filter types](notes/12-filters/12.01-filter-pipeline.md) 🔥 🎯
- [ ] **12.2** [Execution order, scopes, and `IOrderedFilter`](notes/12-filters/12.02-filter-order.md) 🔥 ⚠️
- [ ] **12.3** [Sync vs async filter interfaces](notes/12-filters/12.03-sync-vs-async-filters.md) ⭐ 💻
- [ ] **12.4** [`ServiceFilter` vs `TypeFilter` vs plain attribute](notes/12-filters/12.04-servicefilter-typefilter.md) 🔥 ⚠️
- [ ] **12.5** [Exception filters vs exception middleware](notes/12-filters/12.05-exception-filters.md) ⭐ ⚠️
- [ ] **12.6** [Result filters and response shaping](notes/12-filters/12.06-result-filters.md) ⭐ 💻
- [ ] **12.7** [Endpoint filters in Minimal APIs](notes/12-filters/12.07-endpoint-filters.md) ⭐ 💻
- [ ] **12.8** [Practical filters — logging, validation, caching, auditing](notes/12-filters/12.08-practical-filters.md) ⭐ 💻

---

# Phase 3 — Data Access

## 13. Entity Framework Core

- [ ] **13.1** [ORM concepts; EF Core vs Dapper vs ADO.NET](notes/13-entity-framework-core/13.01-orm-comparison.md) 🔥 🎯
- [ ] **13.2** [`DbContext`, `DbSet<T>`, and context lifetime](notes/13-entity-framework-core/13.02-dbcontext.md) 🔥 ⚠️
- [ ] **13.3** [Code First vs Database First](notes/13-entity-framework-core/13.03-code-first-db-first.md) ⭐
- [ ] **13.4** [DataAnnotations vs Fluent API; `IEntityTypeConfiguration`](notes/13-entity-framework-core/13.04-entity-configuration.md) 🔥 💻
- [ ] **13.5** [Relationships and conventions](notes/13-entity-framework-core/13.05-relationships.md) 🔥 💻
- [ ] **13.6** [Migrations — create, apply, roll back, script](notes/13-entity-framework-core/13.06-migrations.md) 🔥 💻
- [ ] **13.7** [Change tracking, entity states, `AsNoTracking`](notes/13-entity-framework-core/13.07-change-tracking.md) 🔥 ⚠️
- [ ] **13.8** [Eager vs lazy vs explicit loading](notes/13-entity-framework-core/13.08-loading-strategies.md) 🔥 ⚠️
- [ ] **13.9** [The N+1 query problem](notes/13-entity-framework-core/13.09-n-plus-one.md) 🔥 ⚠️ 🎯
- [ ] **13.10** [Client vs server evaluation](notes/13-entity-framework-core/13.10-client-vs-server-eval.md) 🔥 ⚠️
- [ ] **13.11** [Raw SQL safely — `FromSqlRaw` vs `FromSqlInterpolated`](notes/13-entity-framework-core/13.11-raw-sql.md) 🔥 ⚠️ 💻
- [ ] **13.12** [Transactions and `SaveChanges` semantics](notes/13-entity-framework-core/13.12-transactions-savechanges.md) ⭐ 💻
- [ ] **13.13** [Concurrency — optimistic vs pessimistic](notes/13-entity-framework-core/13.13-concurrency.md) ⭐ 💻
- [ ] **13.14** [Bulk operations — `ExecuteUpdate` / `ExecuteDelete`](notes/13-entity-framework-core/13.14-bulk-operations.md) ⭐
- [ ] **13.15** [Query performance — projections, split queries, compiled queries](notes/13-entity-framework-core/13.15-query-performance.md) ⭐ ⚠️
- [ ] **13.16** [Query filters, shadow properties, value converters, owned types](notes/13-entity-framework-core/13.16-advanced-modeling.md) ⭐
- [ ] **13.17** [Seeding data](notes/13-entity-framework-core/13.17-seeding.md)
- [ ] **13.18** [Connection resiliency and retries](notes/13-entity-framework-core/13.18-resiliency.md) ⭐
- [ ] **13.19** [Repository and Unit of Work — and the case against them](notes/13-entity-framework-core/13.19-repository-unit-of-work.md) 🔥 🧠
- [ ] **13.20** [Testing data access — InMemory vs SQLite vs Testcontainers](notes/13-entity-framework-core/13.20-testing-data-access.md) ⭐ ⚠️

## 14. Databases and Beyond EF

- [ ] **14.1** [SQL fundamentals — joins, grouping, subqueries, window functions](notes/14-databases/14.01-sql-fundamentals.md) 🔥 💻
- [ ] **14.2** [Indexes — clustered vs non-clustered, covering, and when they hurt](notes/14-databases/14.02-indexes.md) 🔥 🎯
- [ ] **14.3** [Transactions and isolation levels](notes/14-databases/14.03-isolation-levels.md) 🔥 ⚠️ 🎯
- [ ] **14.4** [Deadlocks — causes and mitigation](notes/14-databases/14.04-deadlocks.md) ⭐
- [ ] **14.5** [Stored procedures, views, functions from EF Core](notes/14-databases/14.05-stored-procedures.md) ⭐
- [ ] **14.6** [Query plans and basic tuning](notes/14-databases/14.06-query-plans.md) ⭐ 🧠
- [ ] **14.7** [Dapper — usage and when it beats EF](notes/14-databases/14.07-dapper.md) ⭐ 💻
- [ ] **14.8** [NoSQL overview — Mongo, Cosmos, Redis](notes/14-databases/14.08-nosql-overview.md) ⭐
- [ ] **14.9** [Migrations in CI/CD; zero-downtime schema change](notes/14-databases/14.09-migrations-in-cicd.md) 🧠
- [ ] **14.10** [Connection pooling and `DbContext` pooling](notes/14-databases/14.10-connection-pooling.md) ⭐

---

# Phase 4 — Security

## 15. Authentication

- [ ] **15.1** [Authentication vs Authorization, stated precisely](notes/15-authentication/15.01-authn-vs-authz.md) 🔥
- [ ] **15.2** [Schemes, handlers, `ClaimsPrincipal`, `ClaimsIdentity`](notes/15-authentication/15.02-schemes-and-claims.md) 🔥 🎯
- [ ] **15.3** [Cookie authentication](notes/15-authentication/15.03-cookie-auth.md) ⭐ 🎯
- [ ] **15.4** [ASP.NET Core Identity](notes/15-authentication/15.04-aspnet-identity.md) ⭐ 💻
- [ ] **15.5** [JWT structure — header, payload, signature](notes/15-authentication/15.05-jwt-structure.md) 🔥 🎯
- [ ] **15.6** [JWT bearer authentication and `TokenValidationParameters`](notes/15-authentication/15.06-jwt-bearer-setup.md) 🔥 💻
- [ ] **15.7** [Access vs refresh tokens; rotation and revocation](notes/15-authentication/15.07-refresh-tokens.md) 🔥 ⚠️ 🎯
- [ ] **15.8** [OAuth 2.0 — roles, grants, authorization code + PKCE](notes/15-authentication/15.08-oauth2.md) 🔥 🎯
- [ ] **15.9** [OpenID Connect over OAuth 2.0](notes/15-authentication/15.09-openid-connect.md) 🔥 🎯
- [ ] **15.10** [External logins, Duende IdentityServer, Entra ID, Auth0](notes/15-authentication/15.10-external-identity-providers.md) ⭐
- [ ] **15.11** [API keys, HMAC signing, mutual TLS](notes/15-authentication/15.11-api-keys-hmac-mtls.md) ⭐
- [ ] **15.12** [Where to store tokens client-side — cookie vs localStorage](notes/15-authentication/15.12-token-storage.md) 🔥 ⚠️
- [ ] **15.13** [Multi-tenant authentication basics](notes/15-authentication/15.13-multi-tenant-auth.md) 🧠

## 16. Authorization

- [ ] **16.1** [`[Authorize]` and `[AllowAnonymous]`](notes/16-authorization/16.01-authorize-attribute.md) 🔥 💻
- [ ] **16.2** [Role-based authorization](notes/16-authorization/16.02-role-based.md) 🔥 💻
- [ ] **16.3** [Claims-based authorization](notes/16-authorization/16.03-claims-based.md) 🔥 💻
- [ ] **16.4** [Policy-based authorization](notes/16-authorization/16.04-policy-based.md) 🔥 💻
- [ ] **16.5** [Custom requirements and handlers](notes/16-authorization/16.05-custom-requirements.md) 🔥 💻
- [ ] **16.6** [Resource-based authorization](notes/16-authorization/16.06-resource-based.md) ⭐ 💻
- [ ] **16.7** [Multiple schemes, fallback and default policies](notes/16-authorization/16.07-schemes-and-fallback.md) ⭐ ⚠️
- [ ] **16.8** [Authorization in views, Razor Pages, Minimal APIs](notes/16-authorization/16.08-authz-everywhere.md) ⭐
- [ ] **16.9** [Permission-based authorization at scale](notes/16-authorization/16.09-permission-based.md) 🧠

## 17. Application Security

- [ ] **17.1** [OWASP Top 10 mapped to ASP.NET Core defences](notes/17-application-security/17.01-owasp-top-10.md) 🔥 🎯
- [ ] **17.2** [SQL injection and how parameterization stops it](notes/17-application-security/17.02-sql-injection.md) 🔥 ⚠️
- [ ] **17.3** [XSS — Razor encoding, `HtmlString`, CSP](notes/17-application-security/17.03-xss.md) 🔥 ⚠️
- [ ] **17.4** [CSRF — antiforgery tokens and SameSite](notes/17-application-security/17.04-csrf.md) 🔥 ⚠️ 🎯
- [ ] **17.5** [HTTPS, HSTS, certificates, TLS termination](notes/17-application-security/17.05-https-hsts-tls.md) ⭐
- [ ] **17.6** [Data Protection API — and why it breaks in web farms](notes/17-application-security/17.06-data-protection.md) ⭐ ⚠️
- [ ] **17.7** [Secrets management](notes/17-application-security/17.07-secrets-management.md) 🔥
- [ ] **17.8** [Password hashing — salting, PBKDF2, bcrypt, Argon2](notes/17-application-security/17.08-password-hashing.md) ⭐ ⚠️
- [ ] **17.9** [Security headers](notes/17-application-security/17.09-security-headers.md) ⭐
- [ ] **17.10** [Rate limiting and throttling](notes/17-application-security/17.10-rate-limiting.md) ⭐ 💻
- [ ] **17.11** [Input sanitization, upload security, path traversal](notes/17-application-security/17.11-input-and-upload-security.md) ⭐ ⚠️
- [ ] **17.12** [Insecure deserialization, SSRF, IDOR](notes/17-application-security/17.12-deserialization-ssrf-idor.md) ⭐ 🧠
- [ ] **17.13** [Audit logging, PII and GDPR](notes/17-application-security/17.13-audit-and-pii.md) ⭐

---

# Phase 5 — Quality, Performance and Operations

## 18. Logging, Monitoring and Diagnostics

- [ ] **18.1** [`ILogger<T>`, log levels, structured logging](notes/18-logging-monitoring/18.01-ilogger-and-levels.md) 🔥 💻
- [ ] **18.2** [Logging providers](notes/18-logging-monitoring/18.02-logging-providers.md) ⭐
- [ ] **18.3** [Serilog and NLog](notes/18-logging-monitoring/18.03-serilog-nlog.md) ⭐ 💻
- [ ] **18.4** [Log scopes and correlation IDs](notes/18-logging-monitoring/18.04-scopes-correlation-ids.md) ⭐ 💻
- [ ] **18.5** [Health checks — liveness vs readiness](notes/18-logging-monitoring/18.05-health-checks.md) 🔥 💻
- [ ] **18.6** [Metrics and dashboards](notes/18-logging-monitoring/18.06-metrics.md) ⭐
- [ ] **18.7** [Distributed tracing and OpenTelemetry](notes/18-logging-monitoring/18.07-opentelemetry.md) ⭐ 🎯 🧠
- [ ] **18.8** [Application Insights and APM tooling](notes/18-logging-monitoring/18.08-apm-tooling.md) ⭐
- [ ] **18.9** [Debugging production — dumps and `dotnet-*` diagnostic tools](notes/18-logging-monitoring/18.09-production-debugging.md) ⭐ 🧠
- [ ] **18.10** [What to log — and what never to log](notes/18-logging-monitoring/18.10-what-not-to-log.md) ⭐ ⚠️

## 19. Caching and Performance

- [ ] **19.1** [Caching strategies — cache-aside, read/write-through, write-behind](notes/19-caching-performance/19.01-caching-strategies.md) 🔥 🎯
- [ ] **19.2** [`IMemoryCache`](notes/19-caching-performance/19.02-memory-cache.md) 🔥 💻
- [ ] **19.3** [`IDistributedCache` and Redis](notes/19-caching-performance/19.03-distributed-cache-redis.md) 🔥 💻
- [ ] **19.4** [`HybridCache` and stampede protection](notes/19-caching-performance/19.04-hybridcache.md) ⭐ 🧠
- [ ] **19.5** [Response caching and `Cache-Control`](notes/19-caching-performance/19.05-response-caching.md) ⭐
- [ ] **19.6** [Output caching and tag-based invalidation](notes/19-caching-performance/19.06-output-caching.md) ⭐ 💻
- [ ] **19.7** [Cache invalidation strategies and TTL design](notes/19-caching-performance/19.07-cache-invalidation.md) 🔥 ⚠️
- [ ] **19.8** [ETags and conditional requests](notes/19-caching-performance/19.08-etags.md) ⭐
- [ ] **19.9** [Response compression](notes/19-caching-performance/19.09-compression.md)
- [ ] **19.10** [`HttpClientFactory` and socket exhaustion](notes/19-caching-performance/19.10-httpclientfactory.md) 🔥 ⚠️
- [ ] **19.11** [Resilience with Polly — retry, circuit breaker, timeout, bulkhead](notes/19-caching-performance/19.11-polly-resilience.md) 🔥 💻 🎯
- [ ] **19.12** [Async all the way; thread-pool starvation](notes/19-caching-performance/19.12-threadpool-starvation.md) 🔥 ⚠️
- [ ] **19.13** [Reducing allocations — pooling, `ArrayPool`, source-generated JSON](notes/19-caching-performance/19.13-allocations.md) 🧠
- [ ] **19.14** [Benchmarking and load testing](notes/19-caching-performance/19.14-benchmarking-load-testing.md) ⭐
- [ ] **19.15** [Systematic method for diagnosing a slow endpoint](notes/19-caching-performance/19.15-slow-endpoint-playbook.md) 🔥 🎯

## 20. Testing

- [ ] **20.1** [The testing pyramid](notes/20-testing/20.01-testing-pyramid.md) 🔥 🎯
- [ ] **20.2** [xUnit vs NUnit vs MSTest; `[Fact]`, `[Theory]`, `[InlineData]`](notes/20-testing/20.02-test-frameworks.md) 🔥 💻
- [ ] **20.3** [AAA, naming, and test independence](notes/20-testing/20.03-test-structure.md) ⭐
- [ ] **20.4** [Mocking — Moq / NSubstitute; mocks vs stubs vs fakes](notes/20-testing/20.04-mocking.md) 🔥 💻
- [ ] **20.5** [FluentAssertions and Shouldly](notes/20-testing/20.05-assertion-libraries.md) ⭐
- [ ] **20.6** [Unit-testing controllers, services, filters, middleware](notes/20-testing/20.06-unit-testing-aspnet.md) 🔥 💻
- [ ] **20.7** [Integration testing with `WebApplicationFactory`](notes/20-testing/20.07-integration-testing.md) 🔥 💻
- [ ] **20.8** [Testing against a real database — Testcontainers, Respawn](notes/20-testing/20.08-database-testing.md) ⭐ 💻
- [ ] **20.9** [Test data builders, AutoFixture, Bogus](notes/20-testing/20.09-test-data.md) ⭐
- [ ] **20.10** [Code coverage — and why 100% is not the goal](notes/20-testing/20.10-code-coverage.md) ⭐
- [ ] **20.11** [TDD and BDD](notes/20-testing/20.11-tdd-bdd.md) ⭐
- [ ] **20.12** [Testing async code, time (`TimeProvider`), and randomness](notes/20-testing/20.12-testing-async-and-time.md) ⭐ 💻

---

# Phase 6 — Advanced and Architecture

## 21. Advanced ASP.NET Core Features

- [ ] **21.1** [`IHostedService` and `BackgroundService`](notes/21-advanced-features/21.01-background-services.md) 🔥 💻
- [ ] **21.2** [Scoped services inside background services](notes/21-advanced-features/21.02-scoped-in-background.md) 🔥 ⚠️
- [ ] **21.3** [Hangfire, Quartz.NET, and scheduled jobs](notes/21-advanced-features/21.03-job-schedulers.md) ⭐
- [ ] **21.4** [SignalR — hubs, groups, Redis backplane](notes/21-advanced-features/21.04-signalr.md) ⭐ 🎯
- [ ] **21.5** [WebSockets vs SSE vs long polling](notes/21-advanced-features/21.05-realtime-transports.md) ⭐ 🎯
- [ ] **21.6** [gRPC in ASP.NET Core](notes/21-advanced-features/21.06-grpc.md) ⭐ 💻
- [ ] **21.7** [Minimal APIs deep dive — `TypedResults`, AOT](notes/21-advanced-features/21.07-minimal-apis-deep.md) ⭐ 🧠
- [ ] **21.8** [Localization and globalization](notes/21-advanced-features/21.08-localization.md) ⭐
- [ ] **21.9** [`IStartupFilter` and startup work](notes/21-advanced-features/21.09-istartupfilter.md) 🧠
- [ ] **21.10** [Native AOT and trimming](notes/21-advanced-features/21.10-native-aot.md) 🧠
- [ ] **21.11** [Streaming requests and responses; large payloads](notes/21-advanced-features/21.11-streaming.md) ⭐ 🧠
- [ ] **21.12** [`IHttpContextAccessor` — legitimate uses and dangers](notes/21-advanced-features/21.12-httpcontextaccessor.md) ⭐ ⚠️
- [ ] **21.13** [Source generators](notes/21-advanced-features/21.13-source-generators.md) 🧠
- [ ] **21.14** [.NET Aspire](notes/21-advanced-features/21.14-dotnet-aspire.md) ⭐

## 22. Architecture, Patterns and Design

- [ ] **22.1** [SOLID with concrete C# examples](notes/22-architecture-patterns/22.01-solid.md) 🔥 💻 🎯
- [ ] **22.2** [DRY, KISS, YAGNI, composition over inheritance](notes/22-architecture-patterns/22.02-design-principles.md) ⭐
- [ ] **22.3** [Creational patterns](notes/22-architecture-patterns/22.03-creational-patterns.md) 🔥 💻
- [ ] **22.4** [Structural patterns](notes/22-architecture-patterns/22.04-structural-patterns.md) 🔥 💻
- [ ] **22.5** [Behavioural patterns](notes/22-architecture-patterns/22.05-behavioural-patterns.md) 🔥 💻
- [ ] **22.6** [Layered / N-tier architecture](notes/22-architecture-patterns/22.06-layered-architecture.md) ⭐ 🎯
- [ ] **22.7** [Clean / Onion / Hexagonal architecture](notes/22-architecture-patterns/22.07-clean-architecture.md) 🔥 🎯
- [ ] **22.8** [Domain-Driven Design building blocks](notes/22-architecture-patterns/22.08-ddd.md) ⭐ 🧠 🎯
- [ ] **22.9** [CQRS, with and without event sourcing](notes/22-architecture-patterns/22.09-cqrs.md) ⭐ 🎯
- [ ] **22.10** [MediatR and the in-process mediator — plus the criticism](notes/22-architecture-patterns/22.10-mediatr.md) ⭐ 💻
- [ ] **22.11** [Vertical slice architecture](notes/22-architecture-patterns/22.11-vertical-slice.md) 🧠
- [ ] **22.12** [Event sourcing](notes/22-architecture-patterns/22.12-event-sourcing.md) 🧠
- [ ] **22.13** [Specification pattern; Result pattern vs exceptions](notes/22-architecture-patterns/22.13-specification-result.md) ⭐ 🧠
- [ ] **22.14** [Anti-patterns — anemic model, God object, service locator](notes/22-architecture-patterns/22.14-anti-patterns.md) 🔥 ⚠️

## 23. Microservices and Distributed Systems

- [ ] **23.1** [Monolith vs modular monolith vs microservices](notes/23-microservices/23.01-monolith-vs-microservices.md) 🔥 🎯
- [ ] **23.2** [Service boundaries and bounded contexts](notes/23-microservices/23.02-service-boundaries.md) ⭐ 🧠
- [ ] **23.3** [Synchronous communication and service discovery](notes/23-microservices/23.03-sync-communication.md) ⭐
- [ ] **23.4** [Async messaging — RabbitMQ, Kafka, Service Bus](notes/23-microservices/23.04-async-messaging.md) ⭐ 🎯
- [ ] **23.5** [MassTransit / NServiceBus](notes/23-microservices/23.05-masstransit.md) ⭐
- [ ] **23.6** [Message patterns — pub/sub, competing consumers, request/reply](notes/23-microservices/23.06-message-patterns.md) ⭐ 🎯
- [ ] **23.7** [Delivery guarantees, idempotent consumers, dead-letter queues](notes/23-microservices/23.07-delivery-guarantees.md) ⭐ ⚠️
- [ ] **23.8** [Saga and Outbox patterns](notes/23-microservices/23.08-saga-outbox.md) ⭐ 🎯 🧠
- [ ] **23.9** [Eventual consistency and CAP](notes/23-microservices/23.09-cap-eventual-consistency.md) ⭐ 🎯
- [ ] **23.10** [API Gateway and BFF — YARP, Ocelot, APIM](notes/23-microservices/23.10-api-gateway-bff.md) ⭐ 🎯
- [ ] **23.11** [Resilience patterns in a distributed system](notes/23-microservices/23.11-resilience-patterns.md) ⭐ 🎯
- [ ] **23.12** [Distributed caching and distributed locking](notes/23-microservices/23.12-distributed-locking.md) 🧠
- [ ] **23.13** [Cross-service observability](notes/23-microservices/23.13-observability.md) ⭐
- [ ] **23.14** [Configuration and secrets across services](notes/23-microservices/23.14-distributed-config.md) ⭐
- [ ] **23.15** [Versioning and backward compatibility between services](notes/23-microservices/23.15-service-versioning.md) ⭐ ⚠️

## 24. DevOps, Hosting and Cloud

- [ ] **24.1** [Publishing — framework-dependent vs self-contained, RIDs](notes/24-devops-hosting/24.01-publishing.md) ⭐ 💻
- [ ] **24.2** [Deploying to IIS, Linux + Nginx, Windows Services](notes/24-devops-hosting/24.02-deployment-targets.md) ⭐
- [ ] **24.3** [A good multi-stage `Dockerfile` for ASP.NET Core](notes/24-devops-hosting/24.03-dockerfile.md) 🔥 💻
- [ ] **24.4** [Docker Compose for local multi-service dev](notes/24-devops-hosting/24.04-docker-compose.md) ⭐ 💻
- [ ] **24.5** [Kubernetes basics](notes/24-devops-hosting/24.05-kubernetes-basics.md) ⭐ 🎯
- [ ] **24.6** [Probes, graceful shutdown, readiness in containers](notes/24-devops-hosting/24.06-probes-and-shutdown.md) ⭐ ⚠️
- [ ] **24.7** [CI/CD pipelines for .NET](notes/24-devops-hosting/24.07-ci-cd.md) ⭐ 💻
- [ ] **24.8** [Environment-specific config in pipelines](notes/24-devops-hosting/24.08-pipeline-config.md) ⭐
- [ ] **24.9** [Azure hosting options compared](notes/24-devops-hosting/24.09-azure-hosting.md) ⭐
- [ ] **24.10** [AWS equivalents](notes/24-devops-hosting/24.10-aws-hosting.md)
- [ ] **24.11** [Blue-green, canary, and feature-flag releases](notes/24-devops-hosting/24.11-deployment-strategies.md) ⭐ 🎯
- [ ] **24.12** [Scaling — horizontal vs vertical, statelessness, sticky sessions](notes/24-devops-hosting/24.12-scaling.md) 🔥 ⚠️ 🎯
- [ ] **24.13** [Load balancers, `ForwardedHeaders`, real client IP](notes/24-devops-hosting/24.13-forwarded-headers.md) ⭐ ⚠️

---

# Phase 7 — Interview Execution

## 25. Interview Preparation and Practice

- [ ] **25.1** [The 50 most-asked questions — write out your own answers](practice/QUESTION-BANK.md) 🔥
- [ ] **25.2** [Narrate the full request lifecycle, end to end](notes/25-interview-practice/25.02-request-lifecycle-narrative.md) 🔥 🎯
- [ ] **25.3** [Live-coding drill — CRUD API with validation, auth and tests in 45 minutes](notes/25-interview-practice/25.03-live-coding-drill.md) 🔥 💻
- [ ] **25.4** [Code-review exercises — spot the bug](notes/25-interview-practice/25.04-code-review-exercises.md) ⭐ 💻
- [ ] **25.5** [System design worked examples](practice/system-design/README.md) 🔥 🎯
- [ ] **25.6** [Debugging scenarios — slow API, memory growth, random 500s](notes/25-interview-practice/25.06-debugging-scenarios.md) 🔥 🎯
- [ ] **25.7** [Talking about your own projects](MY-PROJECTS.md) 🔥
- [ ] **25.8** [Behavioural questions in STAR format](notes/25-interview-practice/25.08-behavioural-star.md) 🔥
- [ ] **25.9** [Questions to ask the interviewer](notes/25-interview-practice/25.09-questions-to-ask.md) ⭐
- [ ] **25.10** [What's new in .NET 6 → 10](VERSIONS.md) 🔥
- [ ] **25.11** [Diagrams worth memorizing](DIAGRAMS.md) 🔥 🎯
- [ ] **25.12** [Final-week revision plan and mock checklist](notes/25-interview-practice/25.12-final-week-plan.md) 🔥

---

## Suggested study order

| Stage | Sections | Focus |
|---|---|---|
| Week 1–2 | 1, 2, 3 | C#, LINQ, async, runtime |
| Week 3–4 | 4, 5, 6, 7, 8 | Pipeline, DI, config, routing — the heart of the framework |
| Week 5 | 9, 10, 11, 12 | Building APIs properly |
| Week 6 | 13, 14 | EF Core and SQL |
| Week 7 | 15, 16, 17 | Security |
| Week 8 | 18, 19, 20 | Logging, performance, testing |
| Week 9 | 21, 22 | Advanced features and architecture |
| Week 10 | 23, 24 | Distributed systems and DevOps |
| Week 11–12 | 25 | Practice, mocks, revision |

### If you only have one week

Do every 🔥 topic in sections **4, 5, 6, 8, 10, 11, 12, 13, 15, 16, 19**, then read
[CHEATSHEET.md](CHEATSHEET.md) and [TRAPS.md](TRAPS.md) twice, and rehearse
[25.2 the request lifecycle narrative](notes/25-interview-practice/25.02-request-lifecycle-narrative.md) out loud until it's fluent.

### If you have one hour

[CHEATSHEET.md](CHEATSHEET.md) → [TRAPS.md](TRAPS.md) → [DIAGRAMS.md](DIAGRAMS.md). Nothing else.

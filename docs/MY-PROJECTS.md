# My Projects — Rehearsed Talking Points

**[← Roadmap](ROADMAP.md)** · Topic **[25.7](ROADMAP.md#25-interview-preparation-and-practice)**

> **This is the most-asked question in every interview, and the least-prepared-for.**
>
> Candidates spend forty hours on EF Core internals and then improvise the answer to
> *"tell me about something you've built."* That answer is the one the interviewer
> actually remembers — it's the only part of the conversation where you control the
> material entirely.
>
> Fill this in early. Rewrite it as you learn more from the roadmap: topics you study
> will keep reminding you of decisions you made without knowing there was a decision.

---

## Template — copy this block per project

### Project name

**One-sentence pitch.** What it does and who used it. No jargon. If a non-engineer
couldn't follow this sentence, rewrite it.

**My role.** What *you* built, specifically. Say "I" for your work and "we" for the
team's — interviewers notice people who blur that line, and they notice people who are
scrupulous about it too.

**Scale.** Requests/day, users, data volume, team size. Real numbers if you have them,
honest approximations if not. "A few hundred users" beats a vague "at scale."

**Stack.** Framework version, database, hosting, notable libraries.

**Architecture.** Two or three sentences. Be ready to draw it — see [DIAGRAMS.md](DIAGRAMS.md).

**The hardest problem.** One concrete technical problem, how you diagnosed it, what you
tried, what worked. This is the answer that separates candidates. It needs a *specific*
symptom, a *specific* investigation, and a measurable outcome.

**A decision I'd make differently.** Name a real one and explain what you know now that
you didn't then. Saying "nothing, it was all correct" reads as either inexperience or
lack of reflection — there is no third reading.

**Tradeoffs I made deliberately.** Things that look wrong but were the right call in
context. Interviewers love this because it's unfakeable.

---

## Rehearsal checklist

For each project you list, make sure you can answer these without hesitating:

- [ ] Explain it in 30 seconds, and again in 3 minutes
- [ ] Draw the architecture on a whiteboard
- [ ] Name the single biggest technical risk and how you handled it
- [ ] Explain one thing you'd rebuild and why
- [ ] Explain how you tested it
- [ ] Explain how it was deployed, and what happened when it broke
- [ ] Say what you'd do if traffic went up 100×
- [ ] Name something you learned that changed how you write code since

---

## Questions they'll drill into

Anticipate these — they follow almost any project description:

- "Why did you choose *X* over *Y*?" — have a real reason, and "it's what the team knew" is a real reason
- "How did you handle authentication?" → [15](ROADMAP.md#15-authentication)
- "What happened when the database went down?" → [19.11](notes/19-caching-performance/19.11-polly-resilience.md)
- "How did you know it was working in production?" → [18](ROADMAP.md#18-logging-monitoring-and-diagnostics)
- "What was your test coverage like?" — and be honest; [20.10](notes/20-testing/20.10-code-coverage.md)
- "How would you scale it?" → [24.12](notes/24-devops-hosting/24.12-scaling.md)

---

## Your projects

<!-- Copy the template block above for each project. Aim for two or three, well-rehearsed,
     rather than a list of everything you've touched. -->

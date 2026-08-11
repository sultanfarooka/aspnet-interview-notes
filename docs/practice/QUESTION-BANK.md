# Question Bank

**[← Roadmap](../ROADMAP.md)** · **[README](../index.md)** · Topic **[25.1](../ROADMAP.md#25-interview-preparation-and-practice)**

> Answers are hidden inside collapsible blocks. **Say your answer out loud before you
> expand one.** Reading the answer and thinking "yes, I knew that" is recognition, not
> recall — and the interview tests recall.
>
> **Printing:** closed `<details>` blocks print as questions with no answers. Before
> exporting to PDF, find-and-replace `<details>` → `<details open>`. (For a paper copy
> that's usually what you want anyway.)

Write answers **in your own words**. A pasted answer you can't paraphrase is worse than
no answer, because it gives you false confidence.

---

## Section 5 — Middleware

**Q1. What is middleware, and how does the pipeline work?** 🔥

<details><summary>Answer</summary>

*Your answer here. See [5.1](../notes/05-middleware-pipeline/5.01-what-is-middleware.md).*

</details>

**Q2. Why does middleware order matter? Give a concrete example of getting it wrong.** 🔥

<details><summary>Answer</summary>

*Your answer here. See [5.2](../notes/05-middleware-pipeline/5.02-middleware-order.md).*

</details>

**Q3. What's the difference between `Use`, `Run` and `Map`?** 🔥

<details><summary>Answer</summary>

*Your answer here. See [5.3](../notes/05-middleware-pipeline/5.03-use-run-map.md).*

</details>

**Q4. You need a scoped service in your custom middleware. What goes wrong, and how do you fix it?** ⚠️

<details><summary>Answer</summary>

*Your answer here. See [5.6](../notes/05-middleware-pipeline/5.06-imiddleware-factory.md).*

</details>

---

## Section 6 — Dependency Injection

**Q5. Explain the three service lifetimes and when each is appropriate.** 🔥

<details><summary>Answer</summary>

*Your answer here. See [6.3](../notes/06-dependency-injection/6.03-service-lifetimes.md).*

</details>

**Q6. What is a captive dependency? Walk me through what actually breaks.** 🔥

<details><summary>Answer</summary>

*Your answer here. See [6.4](../notes/06-dependency-injection/6.04-captive-dependency.md).*

</details>

**Q7. You need a `DbContext` inside a `BackgroundService`. How?** 🔥 ⚠️

<details><summary>Answer</summary>

*Your answer here. See [21.2](../notes/21-advanced-features/21.02-scoped-in-background.md).*

</details>

---

## How to grow this file

Add a question every time one of these happens:

1. You're asked something in a real or mock interview — write it down the same day,
   verbatim, before you rewrite it in your head into something you answered well
2. You read a note and think "how would this get asked?"
3. You fumble a follow-up — the follow-up is the real question, not the original

Aim for roughly one question per 🔥 topic. That's about 120 questions, which is a
realistic target over the full study period and far more useful than a downloaded list
of 500 you've never spoken aloud.

---

## Drill format

**Solo:** cover the answers, work through one section, mark every fumble in
[PROGRESS.md](../PROGRESS.md) under *Weak spots*.

**With a partner:** hand them this file. Ask them to pick randomly and to always ask
"why?" once after your answer. The follow-up is where interviews are actually won and
lost — a confident first answer followed by silence when probed is worse than a hesitant
answer that survives two levels of "why."

**Out loud, alone:** record yourself. Painful, effective. You will hear the filler words
and the places where you trail off, and you can't hear either while you're speaking.

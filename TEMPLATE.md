<!--
  WRITING STYLE — read before writing a note.

  1. Short sentences. One idea per sentence.
  2. Plain words. If a technical term is unavoidable, explain it in brackets the
     first time it appears — every time, even if it appeared in another note.
  3. Use an analogy for anything abstract. A concrete picture beats a precise
     definition when you are trying to remember something under pressure.
  4. Explain code line by line. Comment the interesting lines inside the block,
     then say why it matters underneath.
  5. Say "why" before "how". A reader who knows why a feature exists can often
     work out how it behaves.
  6. Write answers the way you would SAY them, not the way you would write a
     specification.
-->

# N.M — Topic Title

> **[← Roadmap](../../ROADMAP.md)** · **Section:** [N. Section Name](../../ROADMAP.md#n-section-name)
> **Prev:** [N.M-1 Previous Topic](N.0M-previous.md) · **Next:** [N.M+1 Next Topic](N.0M-next.md)

**Markers:** 🔥 ⚠️ 💻 · **Confidence:** 🔴 · **Last reviewed:** —

---

## TL;DR

**Open with one sentence that DEFINES the topic**, in plain English. Not what it's good
for — what it *is*. Then three bullets maximum.

This is what you read the morning of the interview. Write it *last*, after the rest of the
note exists, so it summarizes rather than promises.

- Point one.
- Point two.
- Point three.

---

## Definitions

**Required section.** Every term and API the note uses, defined before it is used.

The critical column is the middle one: say **what kind of C# thing each term is** — a
keyword, a class, a static class, a field modifier, an interface, a build setting, or just
a concept with no code behind it. A reader who doesn't know whether `lock` is a keyword or
a class cannot follow anything else.

| Term | What it is in C# | What it means |
|---|---|---|
| **SomeThing** | a **C# keyword** | One plain sentence. What it does, not when to use it. |
| **SomeClass** | a **class you create with `new`** | One plain sentence. |
| **Some.Static** | a **static class** in `System.Whatever` | One plain sentence. |
| **someConcept** | *a property / a bug / a strategy* | Use italics for things that aren't code. |

Keep each definition to one sentence. Say when to use it later, in "How it works" — not
here. Mixing definition and advice is what makes a definition feel vague.

---

## The concept

What it is and, more importantly, **what problem it solves**. Interviewers can tell the
difference between someone who memorized a definition and someone who understands why
the thing exists. Lead with the problem.

---

## How it works

The mechanism. Under the hood. This is where you earn the follow-up question.

---

## Code

```csharp
// Minimal, runnable, and no wider than ~90 characters so it prints cleanly.
// Comment only what isn't obvious from the code itself.
```

---

## Interview questions

**Q: The question, phrased the way an interviewer would actually say it.**

The answer, written as spoken prose — the way you'd say it out loud, not as bullet
points. Practise saying it. Reading is not the same as speaking.

**Q: A follow-up that goes one level deeper.**

Answer.

---

## Traps ⚠️

Things that are wrong in a way that sounds right. Each one also goes in
[TRAPS.md](../../TRAPS.md).

- **The trap.** Why people believe it, and what's actually true.

---

## Related

- [N.M Some prerequisite](../0N-section/N.0M-file.md) — why it's related
- [N.M Something that builds on this](../0N-section/N.0M-file.md) — why it's related

---

## Sources

- [Microsoft Learn — page title](https://learn.microsoft.com/...)

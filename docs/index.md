# ASP.NET Core Interview Notes

A personal study repository, readable on a phone and printable on paper. Built for two
very different modes of use: **deep study over weeks**, and **a 60-minute panic revision
the morning of an interview.**

!!! tip "Reading on your phone"
    This site works offline once a page has loaded, has full-text search across every
    note, and follows your phone's dark mode. In your mobile browser choose
    **Share → Add to Home Screen** and it opens like an app.

---

## Start here

| File | When to open it |
|---|---|
| **[ROADMAP.md](ROADMAP.md)** | The master index. Every topic, numbered and linked. Start of every study session. |
| **[CHEATSHEET.md](CHEATSHEET.md)** | The single page you read in the car park. One-liners only. |
| **[TRAPS.md](TRAPS.md)** | Every ⚠️ gotcha in the repo, collected. The highest signal-per-minute file here. |
| **[DIAGRAMS.md](DIAGRAMS.md)** | Everything worth drawing on a whiteboard. |
| **[VERSIONS.md](VERSIONS.md)** | What changed in .NET 6 → 10. Interviewers love a "what's new" question. |
| **[PROGRESS.md](PROGRESS.md)** | Confidence tracker and spaced-repetition schedule. |
| **[MY-PROJECTS.md](MY-PROJECTS.md)** | Your own work, rehearsed. The most-asked question in every interview. |
| **[GLOSSARY.md](GLOSSARY.md)** | Every acronym, one line each. |
| **[practice/QUESTION-BANK.md](practice/QUESTION-BANK.md)** | Q&A drill, answers hidden until you look. |

---

## Folder layout

```
Asp.net Notes/
├── mkdocs.yml                 ← site config (nav lives here)
├── requirements.txt
├── TEMPLATE.md                ← the shape every note follows
├── overrides/404.html         ← "not written yet" page
├── .github/workflows/         ← auto-deploy on push
│
└── docs/                      ← everything published lives here
    ├── index.md               ← you are here
    ├── ROADMAP.md             ← master index, all 25 sections
    ├── CHEATSHEET.md          ← one-page blitz
    ├── TRAPS.md               ← all gotchas collected
    ├── DIAGRAMS.md            ← mermaid diagrams
    ├── VERSIONS.md            ← .NET 6 → 10 changes
    ├── GLOSSARY.md            ← acronyms
    ├── PROGRESS.md            ← confidence + review schedule  (not published)
    ├── MY-PROJECTS.md         ← your own project talking points (not published)
    │
    ├── notes/
    │   ├── 01-csharp-fundamentals/
    │   │   ├── 1.01-value-vs-reference-types.md
    │   │   ├── 1.02-struct-class-record.md
    │   │   └── ...
    │   └── ... (one folder per roadmap section)
    │
    └── practice/
        ├── QUESTION-BANK.md
        └── system-design/
```

### Why the filenames look like `4.03-` and not `4.3-`

The minor number is **zero-padded to two digits** so files sort correctly in every file
explorer. Without padding you get `4.1, 4.10, 4.11, 4.2, 4.3…` which is unusable once a
section passes nine topics.

The roadmap displays `4.3`; the file is `4.03-…`. The mapping is obvious and the sort
order stays correct forever.

**Rule: topic numbers never change.** If a topic turns out to be wrong or redundant,
mark it deprecated in place. Renumbering silently breaks every link in the repo.

---

## Printing

Yes — and there are two separate workflows depending on what you want.

### One-time setup

Install **[Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)** in VS Code:

```
code --install-extension shd101wyy.markdown-preview-enhanced
```

This is the better choice over the more popular "Markdown PDF" extension because it
renders **Mermaid diagrams** (used in [DIAGRAMS.md](DIAGRAMS.md)) and supports
`@import`, which is what makes the whole-book export below work.

### Printing a file

1. Open the `.md` file
2. `Ctrl+K V` — opens the enhanced preview
3. Right-click in the preview → **Chrome (Puppeteer) → PDF**
4. The PDF lands next to the source file

For a quick paper copy without a PDF step: right-click preview → **Open in Browser** →
`Ctrl+P`. Browser print gives you the best control over margins and scale.

### Print-specific notes

- **Collapsible Q&A does not print.** The question bank uses `<details>` blocks so you
  can self-test on screen; a closed `<details>` prints as just the question with no
  answer. Before printing the question bank, find-and-replace `<details>` → `<details open>`.
  (That's arguably what you want for a paper copy anyway — read-through, not self-test.)
- **Emoji markers print fine** in Chrome-based export. They render as monochrome glyphs
  in some PDF viewers, which is harmless — the shapes stay distinguishable.
- **Keep code blocks under ~90 characters wide.** Anything longer gets clipped in A4
  portrait rather than wrapped.
- **Use `---` between major topics.** MPE turns a horizontal rule into a clean section
  break, and it gives you a natural place to insert a page break if you want one.

---

## Writing a new note

Copy [TEMPLATE.md](TEMPLATE.md). Every note has the same seven sections in the same
order, which matters more than it sounds: once the shape is muscle memory you can jump
straight to "Traps" on a file you've never opened and know exactly what you're getting.

Then do three things:

1. Tick the checkbox in [ROADMAP.md](ROADMAP.md)
2. Copy any ⚠️ items into [TRAPS.md](TRAPS.md)
3. **Add one line to the `nav:` block in `mkdocs.yml`** — otherwise the note builds but
   never appears in the site navigation

---

## How this gets published

Preview locally:

```bash
pip install -r requirements.txt
mkdocs serve          # then open http://127.0.0.1:8000
```

Publish:

```bash
mkdocs gh-deploy      # live in about a minute
```

(Automatic deploy on push is set up in `.github/workflows/deploy.yml` but currently
disabled — see the repo README for why and how to switch it back on.)

`MY-PROJECTS.md` and `PROGRESS.md` are deliberately **excluded** from the published site —
they hold personal project details and a self-assessment of weak topics, and the site is
public. That exclusion is the `exclude_docs:` block in `mkdocs.yml`. Deleting those two
lines would publish them.

---

## Marker legend

| Marker | Meaning |
|:--:|---|
| 🔥 | Near-certain to be asked |
| ⭐ | Commonly asked |
| 💻 | Must be able to *write* it, not just describe it |
| ⚠️ | Classic trap |
| 🧠 | Senior/architect level only |
| 🎯 | Worth being able to draw |

Six markers, deliberately. A legend you have to look up is a legend that isn't working —
resist adding more.

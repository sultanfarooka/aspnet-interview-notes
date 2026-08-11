# ASP.NET Core Interview Notes

**📖 Read the notes: <https://sultanfarooka.github.io/aspnet-interview-notes/>**

Study notes and interview preparation for ASP.NET Core — a numbered roadmap of ~330
topics from C# fundamentals through to distributed systems, with per-topic notes covering
the concept, how it works, code, interview questions and answers, and the traps that catch
people out.

The site has full-text search, dark mode, and works on a phone.

---

## Repository layout

| Path | What it is |
|---|---|
| `docs/` | All content. This is what gets published. |
| `docs/ROADMAP.md` | The master index — every topic, numbered and linked |
| `docs/notes/` | One folder per roadmap section, one file per topic |
| `mkdocs.yml` | Site config. **The `nav:` block needs a line per new note.** |
| `TEMPLATE.md` | The shape every note follows |
| `overrides/404.html` | Shown when a link points at a note that isn't written yet |

Start at [`docs/index.md`](docs/index.md) for how the notes are organised and how to use
them.

## Running it locally

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>.

## Deploying

Automatic. Every push to `main` triggers `.github/workflows/deploy.yml`, which builds the
site and publishes it to GitHub Pages in about 60–90 seconds.

## A note on what is published

`docs/MY-PROJECTS.md` and `docs/PROGRESS.md` are **excluded** from the built site via the
`exclude_docs:` block in `mkdocs.yml`. They hold personal project details and a
self-assessment of weak topics, and this site is public. Removing those two lines would
publish them.

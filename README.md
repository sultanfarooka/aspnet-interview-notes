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

```bash
mkdocs gh-deploy
```

That builds the site and pushes it to the `gh-pages` branch, which GitHub Pages serves.
Takes about a minute to go live.

> **Why not automatic?**
> `.github/workflows/deploy.yml` does exactly this on every push, but it is currently
> **disabled** because GitHub Actions is blocked on this account by a billing issue
> ("your account is locked due to a billing issue"). Once that is resolved at
> <https://github.com/settings/billing>, re-enable it with
> `gh workflow enable "Deploy notes site"` and switch Pages back to the Actions source
> with:
> ```bash
> gh api -X PUT repos/sultanfarooka/aspnet-interview-notes/pages -f build_type=workflow
> ```
> Until then, `mkdocs gh-deploy` is the deploy step and does not need Actions at all.

## A note on what is published

`docs/MY-PROJECTS.md` and `docs/PROGRESS.md` are **excluded** from the built site via the
`exclude_docs:` block in `mkdocs.yml`. They hold personal project details and a
self-assessment of weak topics, and this site is public. Removing those two lines would
publish them.

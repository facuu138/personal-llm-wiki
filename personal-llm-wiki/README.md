# personal-llm-wiki

A template for a personal knowledge base that Claude Code maintains.
You add sources. Claude compiles them into a linked Markdown wiki. You approve every change.
It works as an Obsidian vault, but Obsidian is optional.

## Start a new wiki

1. Copy the template into a new folder:
   ```sh
   git clone <this-repo-url> my-wiki
   cd my-wiki
   rm -rf .git && git init    # optional: start fresh history
   ```
2. Open the folder in Claude Code and run `/setup`. It asks about your scope and projects and fills in `CLAUDE.md` and `SCHEMA.md`.
3. Optional: open the folder as an Obsidian vault and install the community plugin **Kanban**, which renders `TODO.md` as a board.
4. Start adding sources with `/add`.

## Commands

| Command | What it does |
|---|---|
| `/setup` | Fills in the placeholders for a new wiki. Run once. |
| `/add` | Saves a note, file, or pasted text in the right place. |
| `/ingest` | Plans updates from pending sources, asks for approval, then writes records, wiki pages, cards, and ideas. |
| `/ask` | Answers a question from the wiki, with links to sources. |
| `/lint` | Reports broken links, missing fields, pending sources, and contradictions. Changes nothing. |

## How it is organized

| Path | Holds |
|---|---|
| `raw/` | Sources exactly as they arrived. Never edited after saving. |
| `records/` | One structured note per event: `notes/`, `meetings/`, `decisions/`. |
| `wiki/` | The synthesis: overview, timeline, open questions, projects, people, topics. |
| `log/` | One entry per ingest. A source counts as ingested once a log entry names it. |
| `templates/` | One template per record type. |
| `TODO.md` | Kanban board. Claude only adds cards to the Automated column. |
| `IDEAS.md` | Idea dump. Claude only adds bullets under `## From notes`. |
| `CLAUDE.md` | Short rules and scope. |
| `SCHEMA.md` | Detailed rules: projects, record types, wiki pages, ingest steps. |

## Guardrails

`.claude/hooks/wiki-guard.sh` runs on every edit Claude makes:
- It blocks changes to `wiki/`, `log/`, and `TODO.md` unless `/ingest` is running.
- It blocks edits to files that already exist in `raw/`.
- At session start, it lists sources not yet ingested.

`.claude/scripts/lint.sh` runs the mechanical checks behind `/lint`. You can run it yourself: `bash .claude/scripts/lint.sh`.

## Customize

- New project: add a row to the Projects table in `SCHEMA.md`.
- New record type: add a template, a folder under `records/`, and a row in the Records table in `SCHEMA.md`.

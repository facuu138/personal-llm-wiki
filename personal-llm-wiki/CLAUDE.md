# <FILL: Wiki name>

This vault is my knowledge base about <FILL: the project, job, or subject>.
<FILL: One or two sentences about who I am and my role.>
I add sources. You compile them into a linked wiki. I approve the result.

> Not set up yet? Run `/setup`. It fills in every `<FILL: ...>` in this file and in `SCHEMA.md`.

## Scope

It covers:
- <FILL: The projects this wiki tracks.>
- <FILL: The data, tools, and methods behind them.>
- The people involved, and what each of them owns.
- Decisions, and the reasons behind them.

It does not cover:
- <FILL: Things to keep out, like other jobs, studies, or personal life.>

If a source is out of scope, tell me instead of ingesting it.

## Commands

| Command | Use it to |
|---|---|
| `/setup` | Fill in this file and `SCHEMA.md` for a new wiki. Run it once. |
| `/add` | Save a note, file, or pasted text in the right place. |
| `/ingest` | Turn pending sources into records, wiki pages, cards, and ideas, after my approval. Name files to re-ingest them. |
| `/ask` | Answer a question from the wiki, with links to sources. |
| `/lint` | Report problems in the wiki. Changes nothing. |

When I give you something to keep, use `/add`.
When I ask to update the wiki, use `/ingest`.
When I ask about my work, projects, people, tasks, or ideas, use `/ask`. Answer from the files, not from memory.

## Folders and files

| Path | Who writes | What it holds |
|---|---|---|
| `raw/` | Me | Sources exactly as they arrived. |
| `records/` | Me, or you during ingest | One structured note per event. |
| `wiki/` | You, only during `/ingest` | The synthesis: overview, projects, people, topics. |
| `log/` | You, only during `/ingest` | One entry per ingest. |
| `templates/` | Me | One template per record type. |
| `TODO.md` | Me, and you only in its Automated column | My Kanban board of tasks. |
| `IDEAS.md` | Me, and you only in its From notes section | A messy dump of ideas. |

## Rules

1. Only change `wiki/` and `log/` during `/ingest`.
2. Never edit a file in `raw/` after it is saved.
3. Name files `YYYY-MM-DD-short-slug.md`, using the date of the event.
4. Use standard Markdown links with relative paths.
5. Only write facts that a source supports. If sources disagree, show both.
6. Never store passwords, API keys, tokens, or <FILL: other sensitive data, like personal data about customers>.
7. Never touch `.obsidian/`.
8. Write plainly: short sentences, one idea per sentence.
9. In `TODO.md`, only add cards to the Automated column, and only during `/ingest`. Never move, edit, or delete a card.
10. In `IDEAS.md`, only add short bullets under `## From notes`: during `/ingest` for ideas found in sources, or when I ask. Never edit or delete a line.
11. If a hook blocks an action, follow its reason. Never work around it with terminal commands. Only `/ingest` creates `.claude/ingest-running`.

# Schema

The detailed rules for this wiki. `CLAUDE.md` has the short version.

## Projects

The `project` field in every record uses one of these names:

| Name | What it is |
|---|---|
| `<FILL: project-slug>` | <FILL: What it is.> |
| `general` | About the whole area, not one project. |
| `misc` | Fits no project above. |

To add a project, add a row here.

## Records

Every record starts with frontmatter from its template.
Required fields: `type`, `title`, `date`, `project`, `sources`.
A record made from a raw file also gets `generated_from: <path to the raw file>`.

| Type | Folder | Extra fields |
|---|---|---|
| `note` | `records/notes/` | None. The default type. |
| `meeting` | `records/meetings/` | `attendees` |
| `decision` | `records/decisions/` | `status`: proposed, accepted, rejected, superseded. `supersedes`. |

To add a type, add a template, a folder, and a row here.

### Imported meetings

Optional. Delete this section if you do not import meeting notes.

A script imports Google Meet notes from Drive into `raw/`. Each file starts with a header that has `drive_file_id` and `revision`.

- Revision 1 is `raw/YYYY-MM-DD-slug.md`. Later versions of the same doc are `...-rev2.md`, `...-rev3.md`, and so on.
- All files with the same `drive_file_id` are one meeting. Keep one meeting record for them.
- For a revision, update that record from the newest revision. Set `generated_from` to the newest revision, and list every revision in `sources`.
- In the plan, show what the revision changes compared to the record.
- Gemini's "Suggested next steps" become unchecked `- [ ]` actions in the record.

## Wiki pages

| Page | What it holds |
|---|---|
| `wiki/index.md` | Every wiki page, one line each. |
| `wiki/overview.md` | The current state of the work. |
| `wiki/timeline.md` | All events in date order, each linked to its record. |
| `wiki/open-questions.md` | Contradictions and missing information. Two sections: Open, and Resolved. |
| `wiki/projects/<name>.md` | One page per project: goal, status, people, decisions, open actions. |
| `wiki/people/<name>.md` | One page per person: role, what they own, which projects. |
| `wiki/topics/<name>.md` | One page per subject that spans projects: tools, datasets, methods, data gathering. |

Every wiki page:
- Starts with frontmatter: `title`, `type: wiki`, `updated`, `sources`.
- Shows the current state first and history below.
- Links every statement to the record or raw file that supports it.
- Shows both sides when sources disagree, and adds the conflict to `wiki/open-questions.md`.

Create a new page only when a subject appears in at least two sources, or when I ask.

Never delete a question from `wiki/open-questions.md`. When a source answers it, move it to Resolved with a link to that source. When I say a question does not matter, move it to Resolved as dismissed, with a link to my note.

## Board and ideas

`TODO.md` is my Kanban board. Its columns, in order:

| Column | Who writes | What it holds |
|---|---|---|
| Automated | You, only during ingest | Actions you found. I review them here. |
| Backlog | Me | Tasks I accepted but haven't started. |
| Doing | Me | Tasks in progress. |
| Waiting | Me | Tasks blocked on someone else. |
| Done | Me | Finished tasks. |

A card looks like this:
`- [ ] Action (owner) @{YYYY-MM-DD} · [source](records/meetings/2026-09-24-sprint-planning.md)`

`@{YYYY-MM-DD}` is the Kanban plugin's due date. Include it only when the source gives a date. Leave out `(owner)` when the source names no owner.

The source link shows where a task came from. It also prevents duplicates: before adding a card, check whether a card with the same source and action exists anywhere on the board, including Done.

If `TODO.md` does not exist, do not create it. Tell me instead.

The Kanban plugin reads `TODO.md` as plain Markdown. To add a card:
- Add it as a new `- [ ]` line under `## Automated`, after any cards already there.
- Keep one blank line before the next `## ` heading.
- Never change the header at the top, other columns, the `**Complete**` line, or the `%% kanban:settings %%` block at the bottom.

`IDEAS.md` is my messy dump of ideas. The top part is mine. You only add to the `## From notes` section at the bottom:
- During ingest, when a source contains an idea. An idea is a suggestion or possibility, not a task or a decision.
- When I ask.

Each idea is one short bullet, never a paragraph:
`- YYYY-MM-DD · project · short idea · [source](records/notes/2026-09-24-weekly-sync.md)`

Skip an idea that is already in the file. Never edit or delete a line.

## Ingest

1. Read each pending source. If one is out of scope, stop and tell me.
2. For each raw file without a record, create one from its template and set `generated_from`.
3. Update the overview, the timeline, open questions, and every project, person, and topic page the sources touch. Add new pages to `wiki/index.md`. If a pending source answers an open question, update the affected pages and move the question to Resolved.
4. For each unchecked `- [ ]` item in the pending records, add a card to the Automated column of `TODO.md`, following "Board and ideas".
5. For each idea in the pending sources, add a bullet to `IDEAS.md`, following "Board and ideas".
6. Write `log/YYYY-MM-DD-HHMM.md`. List the sources, records, pages changed, cards added, and ideas added. Write every source and record by its full path from the vault root, after any rename, like `records/notes/2026-09-24-weekly-sync.md`. The pending check depends on it.

## Ask

Read `wiki/index.md`, then the pages that apply, then the records they cite.
Answer with links. Change nothing.

## Lint

Report only. Check for sources not yet ingested, broken links, pages missing from the index, statements without a source, and contradictions.

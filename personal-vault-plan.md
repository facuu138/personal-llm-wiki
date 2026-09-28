# Personal Vault Plan

A second vault for my personal knowledge: CBS, finance, resources, and more.
It reuses the engine from `ap-wiki`, but is organized for me, not for Claude.
`ap-wiki` stays separate and keeps working as it is.

## The idea: three shelves

Everything in the vault sits on one of three shelves.
The difference is how much Claude does with it.

| Shelf | What goes there | What Claude does |
|---|---|---|
| Inbox | Messy notes, quick dumps, half-thoughts | Sorts them into the right folder, when I ask. Never rewrites my text. |
| Notes | My notes inside project and area folders | Ingests them into one `_overview.md` per folder. |
| Library | Books, PDFs, manuals, reference material | Nothing by default. Reads them only when I ask a question. |

## Principles

- Folders are organized by project and area, the way I think. Not by note type.
- The note type (meeting, decision, note) is a frontmatter field, not a folder.
- Messy notes need no structure to be saved.
- Claude writes one overview page per folder, not a page for every topic.
- Claude never rewrites my notes. It only writes overviews, the shared wiki, and the board's Automated column.
- Not everything needs ingestion. The Library is for keeping and searching, not compiling.

## Draft structure

```
brain/
  Inbox/           # dump anything; /add sorts it later
  Projects/        # things with an end
    <project>/
      _overview.md     ← Claude writes this
      my notes...
  Areas/           # ongoing, no end: CBS, Finance, ...
    <area>/
      _overview.md
      my notes...
  Library/         # books, PDFs, reference; not ingested
  Archive/         # finished projects, moved as they are
  raw/             # imported sources, frozen
  wiki/            # only what spans folders: index, people, timeline, open questions
  log/             # one entry per ingest
  templates/
  TODO.md          # Kanban board
  IDEAS.md         # messy idea dump
  CLAUDE.md
  SCHEMA.md
```

## Reused from ap-wiki

| Piece | Reuse as is | Needs changes |
|---|---|---|
| `/add` | | Sorts into project and area folders. Handles the Inbox and the Library. |
| `/ingest` | | Writes `_overview.md` per folder. Skips the Library. |
| `/ask` | | Also searches the Library. |
| `/lint` | Mostly | Checks overviews and the new folders. |
| Hooks | | Allow `_overview.md` files during ingest. |
| `pending-sources.sh` | | Notices edited notes, not only new ones. Skips the Library. |
| `lint.sh` | Mostly | New folders and naming rules. |
| Templates | Yes | Lighter frontmatter. |
| `TODO.md` board | Yes | |
| `IDEAS.md` | Yes | |

---

## Phase 1: Foundations

### Step 1: Structure

- [ ] Choose the vault name and location, for example `~/Documents/brain`.
- [ ] Choose the starting Areas: CBS, Finance, Resources, and others.
- [ ] Choose the starting Projects, if any.
- [ ] Confirm the vault is separate from `ap-wiki`.
- [ ] Create the folders and open the vault in Obsidian.
- [ ] Set Obsidian's link settings: Wikilinks off, relative paths on.
- [ ] Add the vault to the Filesystem connector.

Done when: the empty vault exists with its folders, and Claude can reach it.

### Step 2: Rules

- [ ] Write the purpose and scope in `CLAUDE.md`.
- [ ] Decide what is out of scope. AudienceProject work goes to `ap-wiki`.
- [ ] Add privacy rules. Finance: no account numbers, card numbers, or passwords.
- [ ] Add the core rules: Claude never rewrites my notes, only writes overviews and the wiki during ingest.

Done when: `CLAUDE.md` describes the vault and its rules.

### Step 3: Schema

- [ ] Decide which folders are ingested and which are not.
- [ ] Decide what an `_overview.md` holds: status, key points, decisions, open actions, links.
- [ ] Decide how much frontmatter my notes need. Goal: as little as possible.
- [ ] Decide how ingest handles notes with no frontmatter at all.
- [ ] Decide what stays in the shared `wiki/`.
- [ ] Write `SCHEMA.md`.
- [ ] Adapt the templates.

Done when: `SCHEMA.md` and the templates exist.

## Phase 2: Getting things in

### Step 4: Inbox and /add

- [ ] Decide how `/add` picks a folder for a messy note.
- [ ] Decide whether `/add` asks me before moving a note, or moves and reports.
- [ ] Decide on file names: dated names everywhere, or only for some notes.
- [ ] Build `/add`.
- [ ] Test with three messy notes.

Done when: a messy note in the Inbox ends up in the right folder with my text unchanged.

### Step 5: Library

- [ ] Decide how the Library is organized: by topic, by type, or flat.
- [ ] Decide whether each book or PDF gets a short catalog entry, so it can be found without being read.
- [ ] Teach `/add` to put books and PDFs in the Library.
- [ ] Test by adding one PDF.

Done when: a PDF lands in the Library and is not treated as pending.

## Phase 3: Making sense of it

### Step 6: Pending check, version 2

- [ ] Detect notes I edited after their last ingest, using the file's modified time.
- [ ] Skip the Library, the Inbox, and Archive.
- [ ] Write and test the script in a sandbox first.

Done when: editing a note makes it pending again, and Library files never show up.

### Step 7: /ingest, version 2

- [ ] Write and update `_overview.md` in each folder the sources touch.
- [ ] Update the shared wiki: people, timeline, open questions.
- [ ] Keep the plan-then-write approval and batching from `ap-wiki`.
- [ ] Keep the board and ideas steps.
- [ ] Test with notes in two different folders.

Done when: an ingest updates the right overviews, and nothing else of mine changes.

### Step 8: /ask, version 2

- [ ] Search order: overviews, then notes, then the Library.
- [ ] Say when an answer comes from the Library, since it was never ingested.
- [ ] Test with one question per shelf.

Done when: I can ask about my notes and about a book, and get sourced answers.

## Phase 4: Safety and upkeep

### Step 9: Guards

- [ ] Allow Claude to write `_overview.md`, `wiki/`, `log/`, and `TODO.md` only during ingest.
- [ ] Block edits to my notes, except when moving or renaming through `/add`.
- [ ] Keep `raw/` frozen.
- [ ] Test every case in a sandbox before installing.

Done when: every guard case passes, and a normal session cannot change my notes.

### Step 10: /lint, board, and ideas

- [ ] Adapt `/lint` and `lint.sh` to the new folders.
- [ ] Create the `TODO.md` board with the Kanban plugin: Automated, Backlog, Doing, Waiting, Done.
- [ ] Create `IDEAS.md` with a From notes section.

Done when: `/lint` passes on a clean vault, and the board and ideas work like in `ap-wiki`.

## Phase 5: Moving in

### Step 11: Migration

- [ ] List where my existing personal notes live today.
- [ ] Decide what moves in, what stays, and what gets archived.
- [ ] Move notes in small groups, by area.
- [ ] Ingest each group, oldest first.

Done when: my personal notes live in the new vault, and each area has an overview.

---

## Open decisions

| Decision | Step | Answer |
|---|---|---|
| Vault name and location | 1 | |
| Starting Areas | 1 | CBS, Finance, Resources, ... |
| Starting Projects | 1 | |
| Separate from ap-wiki | 1 | Yes (assumed) |
| Which folders are ingested | 3 | |
| Minimum frontmatter for notes | 3 | |
| `/add` asks or moves | 4 | |
| File naming | 4 | |
| Library organization | 5 | |
| Catalog entries for Library items | 5 | |

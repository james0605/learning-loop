# learning-loop

A Claude Code plugin that gives engineers taking over an unfamiliar technical domain a repeatable learning loop: capture the handover material, research it, verify understanding through Feynman-style questioning, and prepare it for your own hand-written permanent notes.

Everything lands in your Obsidian vault as plain Markdown. The plugin is domain-agnostic — it was born out of a server BIOS handover, but nothing in it is BIOS-specific.

**The core constraint:** the AI never writes your permanent notes. Rewriting an idea in your own words *is* the act of understanding — outsourcing it means giving up the learning. The loop deliberately stops one step short and hands you the pen.

## The loop

```
  once per domain
  ---------------
  [learn-new-domain]
      creates the domain pack: learning map, glossary,
      question queue, decision log
          |
          v
  [capture-handover]           <-- run again whenever new
      splits material into          material shows up
      terms / questions / decisions
          |
          v
  daily
  -----
  [learn-session]              <-- repeat until the queue
      pick 1-2 questions            runs dry
      research, explain, Feynman-check
      updates the queue and glossary
      emits one seed note in 00_Inbox
          |
          v
  when a seed note is ready
  -------------------------
  [scaffold-cards]
      splits it into blank cards, checks for duplicates,
      lists link candidates
          |
          v
      YOU write the cards        <-- the AI stops here
          |
          v
      10_Permanent  ->  MOC curation
```

## The four skills

| Skill | What it does |
| --- | --- |
| **learn-new-domain** | Interviews you, then creates the four-file domain pack (learning map, glossary, question queue, decision log) that the rest of the loop reads and writes. |
| **capture-handover** | Splits handover notes, meeting minutes, or spec fragments into glossary terms, open questions, and tribal-knowledge decisions. Never invents an explanation it did not find in the material. |
| **learn-session** | The daily engine: picks 1-2 questions, researches, explains in plain language, then asks you application questions to verify you actually understood. Records the raw Q&A as a seed note for later transcription. |
| **scaffold-cards** | Prepares transcription: asks how you want to split a seed note and what to call each card, checks for duplicates in your existing permanent notes, creates the empty files, and lists link candidates. Then it gets out of the way. |

Each skill triggers on natural phrasing (e.g. "let's start learning X", "break down this handover doc", "what should I study today", "I'm ready to transcribe") or by name.

## Requirements

| | Required? | Why |
| --- | --- | --- |
| [Claude Code](https://claude.com/claude-code) | yes | The plugin runs as a Claude Code plugin. |
| An [Obsidian](https://obsidian.md) vault | yes | The skills read and write Markdown notes in it. Obsidian itself is only needed to *view* the vault — the skills operate on plain files. |
| Git remote for the vault | recommended | The skills commit and push after each run so other devices pick the changes up. Without it, changes stay local. |
| [Obsidian CLI](https://github.com/yakitrak/obsidian-cli) | optional | Lets the skills locate the vault and open files without asking you. Requires the Obsidian app to be running. |

The skills never hardcode an absolute path. They locate the vault by trying, in order: the Obsidian CLI, a path recorded in your project instructions, and finally by asking you.

## Installation

```
/plugin marketplace add james0605/learning-loop
/plugin install learning-loop
```

This repository is both the marketplace and the plugin — `marketplace.json` points its `source` at the repository root.

## Vault conventions the skills assume

The skills are written for a Zettelkasten-style vault with these folders:

| Folder | Role |
| --- | --- |
| `00_Inbox/` | Seed notes awaiting transcription |
| `10_Permanent/` | Permanent notes — hand-written by you, never by the AI |
| `20_Project/` | Domain packs and in-progress project notes |
| `30_MOC/` | Manually curated maps of content |
| `90_Templates/` | Note templates the skills read at runtime |

Notes carry a minimal YAML frontmatter (`created`, `type`, `tags`, optional `source`). The skills read your vault's own rules file and template files at runtime rather than baking the format in, so adjusting your conventions does not require editing the plugin.

If your vault uses a different layout, adjust the folder names in the skill files — the logic does not otherwise depend on them.

## Design principle

The AI lowers the cost of *capturing* and *researching*, and takes over the clerical work around transcription — creating files, checking for duplicates, surfacing link candidates. It never produces the prose of a permanent note, never drafts one "for you to edit", and never adds links to your maps of content without asking.

That boundary is the whole point. Everything else is scaffolding around it.

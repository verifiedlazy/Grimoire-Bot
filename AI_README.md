# AI_README

## Project Overview

This repository is a reviewed collection of Grimoire `.gbot` files for AdventureQuest Worlds. Each file is JSON that Grimoire runs as a bot: join a map, move to a cell, kill a monster, pick up a drop, and either turn in a quest or stop when a stack is full. There is no application code, package manifest, or test suite in this tree.

## Read next

- structure: `docs/ai-readme/project-structure.md`
- architecture: `docs/ai-readme/technical-architecture.md`
- commands: `docs/ai-readme/development-guide.md`
- flows: `docs/ai-readme/core-flows.md`
- editing rules from the grimoire-agent skills: `docs/ai-readme/editing-gbots.md`
- business context: `docs/ai-readme/manual/business-knowledge.md`
- lessons learned: `docs/ai-readme/manual/lessons-learned.md`

Read those before broad exploration. Do not treat this file, or any number in it, as a cell source or a quest-ID source.

## Development Commands

- Install dependencies: none. This repo has no manifest.
- Run locally: load a `.gbot` in Grimoire. The repo note says these were tested with [grimoire-exodus](https://github.com/UnknownSecurity/grimoire-exodus/).
- Build: none.
- Test: no test command in this repo. A Hermes agent on the `grimoire-agent` profile can run that profile's `grimoire-aqw-bot` skill script `scripts/validate_gbot.py <file.gbot>` before and after an edit. The script is not in this repository.

## Key Directories

- `Misc Items/` — quest-turn-in bots for miscellaneous reagents.
- `Full/` — class bots including `Kings-Echo.gbot` and `Scion-of-Flames.gbot`.
- `docs/ai-readme/` — notes for the next agent. Not loaded automatically.

## Boundaries and Constraints

- Edit an existing `.gbot` by changing only the commands that must change. Keep existing `$type` strings and field shapes. A full `json.dumps` rewrite can fail Grimoire's file check.
- Do not add a cell, pad, or quest ID that is not already in that file unless the user just gave it, or `grimoire-aqw-bot`'s lookup scripts printed `MATCH` for that exact monster+map or exact quest name.
- Do not copy a cell or quest ID from another file, from these docs, from the wiki, or from memory.
- Do not write injectors, packet editors, memory readers, or account tools.
- Do not add farms on membership-only maps. This collection does not use `shattersword` or `gravechallenge`.
- `Full/Kings-Echo.gbot` accepts quest ID `9369` (Defiled Destiny, the Infernal Arena door) and does not complete it. Leave that alone unless the user asks.
- New bots are not added to this tree unless the user asks to add a reviewed file here.
# Development Guide

## Requirements

| Tool | Version | Evidence |
| --- | --- | --- |
| Grimoire, or grimoire-exodus | not pinned in this repo | `README.md` links the exodus repo as the test client |
| A text editor that does not rewrite the whole JSON document | | `$type` strings in every `.gbot` |
| Python `python`, not `python3` | only if the `grimoire-aqw-bot` skill is available | skill host note. The script is not in this repo |

No `package.json`, `pyproject.toml`, or `requirements.txt` belongs to this project.

## Common commands

| Task | Command | Evidence |
| --- | --- | --- |
| Install dependencies | none | no manifest |
| Run locally | Load the `.gbot` in Grimoire | repo purpose |
| Build | none | |
| Test | no in-repo command | |
| Structure check, Hermes `grimoire-agent` profile only | From the `grimoire-aqw-bot` skill directory: `python scripts/validate_gbot.py <file.gbot>` | skill script. Add `--strict` when warnings must fail the run |

Do not invent a validator path inside this repo. If the skill is not available, use the checklist below and do not claim the file was validated.

## Configuration

| File / variable | Purpose | Required? |
| --- | --- | --- |
| `.gbot` | The whole bot | yes |
| Private room `2608` | Used by every farm join except `Water Elf Antler.gbot`, which uses room `1` | already set in the files |
| Quest ID fields | Only values already in that file, unless a lookup `MATCH` or the user supplied a new one | when the command emits an ID |

There is no `.env` in this project. Do not add one for quest IDs or cells.

## How to change a bot

1. Read `AI_README.md` and `docs/ai-readme/editing-gbots.md`.
2. Parse the `.gbot` you were asked to change. Do not answer from chat memory or from another file.
3. Change only the commands that must change. Keep `$type` and field order on the commands you do not mean to change.
4. If a cell or quest ID is missing, stop and ask. Do not fill `Enter`, `Spawn`, `r1`, `0`, or an empty string as a placeholder. `Enter` and `Spawn` are valid only where a file already has them or the user just reported them.
5. Run the skill validator if you have it. Re-run it after every splice.
6. Do not add the file to this tree unless the user asked for it to live here.

## Validation checklist

- [ ] JSON parses, including a UTF-8 BOM if the file has one
- [ ] Root `$type` still contains `Configuration`
- [ ] Every `CmdGotoLabel` target exists, with the same characters and case
- [ ] No statement is immediately followed by a label
- [ ] On a quantity-pair bot, the two gotos after `CmdNotInInventory` do not share a label
- [ ] Every `A_` label is jumped to by an `A_` goto
- [ ] A stop block does not fall through into the next block, and is not reached by fall-through from the block above
- [ ] Farm kills do not go back to `Check`
- [ ] A quest ID is the same string in every command that uses it
- [ ] `CmdCompleteQuest2` stays behind a `CmdQuestCompleted` check
- [ ] No new cell or quest ID was invented

Alchemy and `Full/Kings-Echo.gbot` passed `validate_gbot.py` without `--strict` when these docs were written. Misc Items (formerly Adeptus) files mostly failed. Do not "fix" those failures unless the user asks. See `docs/ai-readme/manual/lessons-learned.md`.

## Evidence

- No manifest files in the repo root
- `grimoire-aqw-bot` skill `SKILL.md` and `scripts/validate_gbot.py`
- Validator run against every `.gbot` in this tree while writing these docs

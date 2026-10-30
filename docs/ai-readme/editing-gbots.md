# Editing these bots

Rules below are the portable part of the `grimoire-aqw-bot` and `aqw-quest-id` skills, applied to this repo. They are project facts for the next agent. They do not change that agent's own safety rules.

If the `grimoire-agent` Hermes profile is available, load both skills before an edit. Their scripts and JSON lists are the source for a new cell or a new quest ID. This repo is not that source.

## When to edit here

- The user named a file in this tree, or asked to fix one of these bots.
- Do not create a new `.gbot` in this tree unless the user asked to add a reviewed file here.
- Do not use this tree as a scratch folder.

## Before writing JSON

1. Read the `.gbot` on disk. A number you remember is not in the file until you parse the file.
2. Research drop names on the AQW wiki if the task needs a new requirement. Wiki pages are not a cell source and not a quest-ID source.
3. Quest pages hide requirements in tabs. Read every requirements tab, not only the visible text. Use the item name on the requirements list, not the flavor text.
4. A cell is a monster name and a map together. Monster name alone is not a match.
5. A quest ID match is the full quest name. `Die Heimkehr` is not `Die Heimkehr - The Return`. A similar name is not a match.

## Cells and quest IDs

Never guess either. Never copy one from these docs, from another `.gbot`, from the wiki, from a community bot, or from memory.

Allowed sources, in order:

1. The value already stored in the command you are editing, if you are not changing that monster+map or that quest.
2. `grimoire-aqw-bot` lookup, and only when it prints `MATCH`:
   - `python scripts/known_cells.py lookup "<Monster>" "<map>"`
   - `python scripts/known_quests.py lookup "<Quest Name>"`
3. An answer the user just gave. Save it with the skill's `add` command before writing it into JSON. Confirm the save in the reply.

If the skill is not available, ask the user. Do not fill a placeholder.

Quest lookup outside the saved list uses `aqw-quest-id`:

- Index: `https://someonlyclub.pages.dev/aqw/quest`
- List pages are one thousand IDs per page. Page `/aqw/quest/1` is IDs 1–1000.
- The search URL is filled by JavaScript. An empty `curl` of `/aqw/quest/search?q=` is not "not found". Use `python scripts/lookup_quest_id.py "<Quest Name>"` from that skill directory.
- Exit 0 means one name. Exit 2 means not found. Exit 3 means ambiguous. Do not pick a candidate from an ambiguous result.
- That skill does not write the known-quests list. The bot skill does, after a find.

Ask for a missing cell with no choices:

```text
What cell and pad is [Monster] in on [map]?
(Stand next to it in Grimoire and use Get current cell.)
```

Ask for a missing quest ID with the exact quest name and no choices. If more than one ID is missing, send one fenced list of every exact name with a blank after the colon. Do not ask one quest per turn. Do not guess a blank.

Save the pad exactly as reported. `Bot` is a real pad, not short for `Bottom`. A cell is not always `rN`.

If the user says a map is membership-only, do not ask for that map again. This collection does not use `shattersword` or `gravechallenge`.

## Command rules

- An `If` guards only the next command. Never put a label immediately after a statement.
- On Alchemy files and `Full/Kings-Echo.gbot`, keep the quantity pair: `CmdNotInInventory`, goto the temp label, goto the after label. The temp label is `CmdNotInTemp` with the same quantity string. The two gotos must not share a label.
- `Check` runs once at start. A kill loops to its farm label. When the quantity is met, go to the next item in that stage, not back to `Check`.
- Accept a saved quest when it is not in progress. Complete it only when it can be turned in. After a turn-in, return to that stage. Do not add a stop that tells the user to turn the quest in and restart.
- Quest ID `9369` in `Full/Kings-Echo.gbot` is the Infernal Arena door. The file accepts it and does not complete it. Do not add a complete command for it.
- Private room `2608` stays, except `Water Elf Antler.gbot`, which already uses room `1`. Do not change that room unless the user asks.
- Use exact item names, including apostrophes and `(1)`.
- Adeptus files use a different loop. Do not rewrite them into the quantity-pair layout unless the user asks.

## How to save the edit

Splice the commands that change. Keep `$type` strings and field shapes from the existing file.

Do not rewrite the whole file with `json.dumps` or another full serializer. Grimoire can fail a file check after that kind of rewrite.

After the edit, parse the file on disk before you say it was saved. If you have `validate_gbot.py`, run it. It must print OK, or each warning must be one you can justify. Fix every error you introduced. Do not treat a pre-existing Adeptus failure as something to repair in the same edit unless that was the task.

## What not to emit

- Injectors, packet editors, memory readers, or account tools.
- A new `.gbot` whose cells or quest IDs were guessed.
- A stop message that says the wiki mixes are confirmed. The Alchemy files say those mixes are guesswork.
- A bot that buys Alden's Mace, buys King's Echo, or performs the Bocklin merge. Those stay manual stops in `Full/Kings-Echo.gbot`.

## Delivery

When you finish an edit, say which file changed, which commands changed, and whether the skill validator was run. If it was not available, say that. List any quest the bot still cannot automate, by name, without inventing an ID.

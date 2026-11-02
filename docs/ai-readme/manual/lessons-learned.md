# Lessons Learned

## Pitfalls

| Problem | Cause | Solution |
| --- | --- | --- |
| Bot farms forever and never reaches the next stage | Both gotos after `CmdNotInInventory` share a label | Second goto must be the after label. Alchemy and King's Echo already do this |
| Branch does nothing | A statement is followed by a label. The label is the guarded command | Put the goto immediately after the statement |
| Grimoire rejects the file after an edit | Whole file rewritten with a JSON dump | Splice only the commands that change. Keep `$type` |
| Wrong cell or quest ID in a new bot | Copied from a wiki, an old file, or a doc | Use a `MATCH` from the skill scripts, or ask. Do not copy from this repo's docs |
| Empty quest search | `curl` of the SomeOnlyClub search URL | That page is filled by JavaScript. Use `aqw-quest-id`'s list-page script |
| Adeptus file fails `validate_gbot.py` | Those files predate the quantity-pair rules. Missing `Check`, case-mismatched gotos, or a dead empty `QuestID` | Do not rewrite them unless that was the task |
| King's Echo door farm cannot start | Defiled Destiny was completed, or never accepted | The file accepts `9369` and does not complete it |

### Known file mismatches

Observed while documenting. Not fixed, because the task was documentation.

| File | What the file does | Why it matters |
| --- | --- | --- |
| `Misc Items/Sun Zone Chit.gbot` | Stop condition is `Sundered Tentacle` 200. `Check` exists and is not reached from the start. Validator warned, then passed | Do not treat the stop item as confirmed |
| `Misc Items/Water Elf Antler.gbot` | Labels are `Main`, `ScavengerFoam`, `AdipocereAntler`. Later gotos use `MAIN`, `SCAVENGERFOAM`, `ADIPOCEREANTLER`. Room is `1`, not `2608`. Validator failed | Case must match. Do not assume Grimoire ignores case |
| `Misc Items/Sundered Tentacle.gbot` | A `CmdQuestlist` with an empty `QuestID` sits after `goto MAIN`, so it is not on the live path. Validator still flags the empty ID. Live ID is `9269` | Do not copy the empty command |
| `Misc Items/Sundered Tentacle.gbot` | Leviathan join pad is `Left`. The following move pad is `Right` | Do not "align" them unless the user confirms the pad |
| Misc Items kills | Several `CmdKill` values are `*` while `CmdMonsterInRoom` names one monster | Leave it unless the user asks |
| Alchemy stop messages | Each one says the wiki mixes are guesswork | Do not document a mix as confirmed |

Validator result while writing these docs, `validate_gbot.py` without `--strict`:

- Passed: `Full/Kings-Echo.gbot`, and `Sun Zone Chit.gbot` with warnings.
- Failed: the other five Misc Items files. Dark Elf Pearl, Sur-gion Token, and Water Elf Pearl failed on a missing `Check` label. Sundered Tentacle also failed on the empty quest ID. Water Elf Antler failed on undefined gotos and a loop with no exit.

## Decisions

| Decision | Reason | Date / owner |
| --- | --- | --- |
| This tree is the reviewed set, not the scratch folder | New unreviewed bots were being written somewhere else. This repo is what other agents should read before editing a shipped bot | 2026-10-30, docs pass |
| Docs list IDs only as file inventory | The grimoire-agent skills forbid treating a written number as a quest-ID or cell source | 2026-10-30, docs pass |
| Validator script stays with the skill, not in this repo | The user asked for markdown for other agents, not a copied toolchain | 2026-10-30, docs pass |
| Adeptus validator failures were recorded, not repaired | The request was to update the README and add agent docs | 2026-10-30, docs pass |

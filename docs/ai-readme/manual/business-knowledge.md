# Business Knowledge

## Project context

These files are personal Grimoire bots for AdventureQuest Worlds. A person loads one `.gbot` in Grimoire and lets it farm. This repository is the reviewed copy of those bots, not the place a new unreviewed bot is generated.

The collection avoids membership-only maps. `shattersword` and `gravechallenge` are not used. Endured Against the Defiler, when it appears, is the Infernal Arena farm already written in `Full/Kings-Echo.gbot`.

## Domain terms

| Term | Code name | Meaning |
| --- | --- | --- |
| Bot file | `.gbot` | One Grimoire command list |
| Statement | `$type` containing `.Statements.` | If true, run the next command. If false, skip it |
| Label | `CmdLabel.Name` | Jump target. Case-sensitive |
| Check | label `Check` | Bank transfer, once, at start |
| Handle | label `HANDLE` | Quantity and ownership checks |
| Quantity pair | `T_` then `A_` | Inventory check, then temp check, then the after path |
| Temp item | `CmdNotInTemp` / `CmdInTemp` | Quest progress stack, not a normal inventory stack |
| Private room | `Room` `2608` | Farm room used by every file except Water Elf Antler |
| Door quest | quest ID `9369` in King's Echo | Accepted so Infernal Arena can be entered. Not completed |
| Mix | Alchemy stop message | Manual. The bot does not mix |

## Business rules

- Alchemy bots stop at 100 of each reagent they check. The person mixes, banks, and starts the bot again. The stop text says the wiki mixes are guesswork.
- King's Echo is not bought by the bot. Alden's Mace is not bought by the bot. Bocklin merges are not performed by the bot. Those are stop messages.
- A saved quest in King's Echo and in the Adeptus files is accepted and turned in by the bot, except Defiled Destiny, which is accepted only.
- Owning an intermediate King's Echo item changes which farm branch runs. Read the file. Do not raise a shard or ornament count because an armor is owned.
- Gold vouchers are not drop farms.
- A count below the required quantity is not done. A quest temp such as 9/50 is not done.

## Not verified here

<!-- TODO: human to fill if a mix in an Alchemy stop message has since been confirmed in game. The files still say the wiki mixes are guesswork. -->

<!-- TODO: human to fill if Sun Zone Chit's stop on Sundered Tentacle 200 is intentional. The file does that. The filename does not. -->

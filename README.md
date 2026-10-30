# Grimoire Bot

Reviewed Grimoire `.gbot` files for AdventureQuest Worlds. This tree is the fixed set. It is not a scratch folder and it is not an application.

The original note for this repo:

- Made with: https://grimoire-bot-builder.vercel.app/
- Tested with: https://github.com/UnknownSecurity/grimoire-exodus/

Load a `.gbot` in Grimoire. There is nothing to install, build, or run from this repository.

## What is here

| Folder | Files | What they do |
| --- | --- | --- |
| `Adeptus Kathooli/` | 6 | Quest turn-in farms for Adeptus Kathooli reagents |
| `Alchemy/` | 7 | Farm reagent stacks to 100, then stop so a person can mix and bank |
| `Full/` | 1 | King's Echo class farm, including nested merges and saved quests |

Alchemy and `Full/Kings-Echo.gbot` passed the `grimoire-aqw-bot` structure check used while these docs were written. Most Adeptus files did not. "Fixed" means this is the reviewed collection, not that every file passes that check. Details are in [docs/ai-readme/manual/lessons-learned.md](docs/ai-readme/manual/lessons-learned.md).

## For another agent

Read [AI_README.md](AI_README.md) before exploring or editing. Then read the files it links.

If you are a Hermes agent and the `grimoire-agent` profile is available, also load `grimoire-aqw-bot` and `aqw-quest-id`. Those skills own the cell list, the quest-ID list, and `validate_gbot.py`. This repo does not ship them.

Do not copy a cell, pad, or quest ID out of these docs or out of a `.gbot` into a different bot. A number written here is an inventory of a file that already contains it.

## License

[MIT](LICENSE).

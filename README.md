# Tool Shed

A phone-first page for every tool in the shed. Colours follow the 60/30/10 rule: graphite, sawdust cream and one hi-vis yellow accent.

## How it flows

- **Shed (home):** a dark dotted opening screen that shrinks into mist as you scroll. Then "On the bench" (tools out on loan and care jobs due), a tape-measure strip of totals, and the pegboard wall, where tools swing onto their hooks. Next is a scroll reel: one tool fills the screen at a time on its brand colour, numbered, with a giant action word behind it (CUT, SAND, CLEAN…) and the drawing tilting as you scroll. It ends with "Less buying. More fixing.", which lights up word by word, plus the bargain meter and battery platform.
- **Power · Hand · Yard:** a big animated title, a picker row, then full tool pages you swipe through sideways. Each page has the moving drawing in front of its action word, then prices, what it's good for, what's in the kit, specs, care jobs, what it pairs with, and lending.
- **Care:** small maintenance jobs. Tick one off and it comes back when it's due again.
- **Lent:** who has what. A lent tool shows as a dashed outline on the wall until it's back.
- **Search** (magnifying glass, top right) looks through names, brands, kit and uses.

Every drawing moves differently: the saw blade spins, the sander buzzes, the vacuum hose sways, the blower blows leaves, the battery charger blinks, the wheelbarrow rocks and the level bubble drifts. Motion switches off when the phone's Reduce Motion setting is on.

Care ticks, loans and the light/dark choice are saved on each phone (browser storage), not in the repo.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site in one file, with no build step. All tool drawings are original inline SVGs. |
| `data.json` | Every tool. The page works everything out from this file. |
| `manifest.webmanifest`, `icon*.png`, `apple-touch-icon.png` | Add to Home Screen icon and app settings. |

## How it updates

Add, change or remove tools through the owner's Claude chat. Claude edits `data.json`, checks it parses, commits and pushes. The page has no add or remove buttons.

## data.json shape

- `updated`: date of the last change (`YYYY-MM-DD`).
- `careStart`: care timers for jobs never ticked count from this date.
- `shed`: `{ name, place }`.
- `categories[]`: `{ id, name }`.
- `tools[]`:
  - `id`: short kebab-case, unique.
  - `name`: what it is, without the brand.
  - `tag`: short name for the wall label (about 12 characters).
  - `verb`: one action word shown huge behind the drawing (Cut, Sand, Clean…).
  - `brand`, `model`: `null` if unknown.
  - `category`: a category `id` (`power`, `hand` or `yard`). Each category is a tab in the bottom bar.
  - `art`: drawing key (`mitresaw`, `sander`, `vac`, `blower`, `battery`, `wheelbarrow`, `toolbag`, `sockets`, `handset`, `screwdrivers`, `knife`, `bits`, `level`, `shed`, `generic`).
  - `colour`: brand colour for the drawing and the tool page.
  - `size`: wall slot size: `small`, `wide` or `big`.
  - `paid`: what was paid. `null` if not recorded.
  - `newPrice`, `newFrom`: current NZ new price and the shop it came from. Look it up, never guess.
  - `power`: `Corded 240V`, a battery platform such as `Ryobi One+ 18V`, or `null` for hand tools.
  - `includes[]`, `specs[[label, value]]`, `notes`.
  - `uses[]`: what it's good for.
  - `pairs[]`: ids of tools it works with.
  - `condition` (optional): `good`, `fair` or `worn`.
  - `spot` (optional): where it lives in the shed.
  - `lentTo`, `lentOn` (optional): a loan recorded in the repo rather than on the phone.
  - `care[]`: `{ id, text, every }` (`every` = days between jobs). Add `now: true` if the job is needed straight away.

## Where the starting list came from

The "kept" tools in Flip Ledger, plus the Makita BO5030 sander and Makita VC2000L vacuum. Lights, remotes, gym gear and the speaker were left out because they aren't tools.

# Tool Shed

A phone-first page for every tool in the shed. The front page is a pegboard wall: each tool hangs on its own hook with a label-tape name. Tap one to open its page, then swipe sideways to move through the tools.

## Tabs

- **Shed:** the pegboard, totals (tools, at home, paid), the bargain meter, care jobs due and battery platforms.
- **Tools:** search plus category filters (power, cordless, hand, measuring, garden, storage).
- **Care:** small maintenance jobs. Tick one off and it comes back when it's due again.
- **Lent:** who has what. A lent tool shows as a dashed outline on the wall until it's back.

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
  - `brand`, `model`: `null` if unknown.
  - `category`: a category `id`.
  - `art`: drawing key (`mitresaw`, `sander`, `vac`, `blower`, `battery`, `wheelbarrow`, `toolbag`, `sockets`, `handset`, `screwdrivers`, `knife`, `bits`, `level`, `shed`, `generic`).
  - `colour`: brand colour for the drawing and the tool page.
  - `size`: wall slot size: `small`, `wide` or `big`.
  - `paid`: what was paid. `null` if not recorded.
  - `newPrice`, `newFrom`: current NZ new price and the shop it came from. Look it up, never guess.
  - `power`: `Corded 240V`, a battery platform such as `Ryobi One+ 18V`, or `null` for hand tools.
  - `includes[]`, `specs[[label, value]]`, `notes`.
  - `condition` (optional): `good`, `fair` or `worn`.
  - `spot` (optional): where it lives in the shed.
  - `lentTo`, `lentOn` (optional): a loan recorded in the repo rather than on the phone.
  - `care[]`: `{ id, text, every }` (`every` = days between jobs). Add `now: true` if the job is needed straight away.

## Where the starting list came from

The "kept" tools in Flip Ledger, plus the Makita BO5030 sander and Makita VC2000L vacuum. Lights, remotes, gym gear and the speaker were left out because they aren't tools.

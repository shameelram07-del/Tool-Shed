# Tool Shed

A phone-first page for every tool in the shed. Colours follow the 60/30/10 rule: gunmetal and black, steel grey, and one signal-red accent, with diamond-plate texture on the dark panels.

## How it flows

- **Shed (home):** a dark dotted opening screen with a big saw blade that turns as you scroll, then shrinks into mist. After that:
  - **Whole shed value:** a steel plate with the total cost to replace everything new, what it's worth second-hand, and how many tools there are.
  - **Tape measure:** counts of power tools, hand tools and brands pull out of a tape-measure case.
  - **The wall:** a pegboard where every tool swings onto its hook.
  - **The whole kit:** every tool on one long shelf that slides sideways as you scroll down.
  - **Barrier tape**, then "Less buying. More fixing." lighting up word by word.
- **Power · Hand · Yard:** each tab opens with its own artwork (drill, crossed hammer and spanner, spade). Then a picker row and full tool pages you swipe through sideways. Each page opens up as it arrives, and has two tabs: **Details** and **Care** (how to look after that tool). Details shows a blueprint drawing sheet (white linework on grid paper, a dimension line and a title block with drawing number, scale, make, model and brand colour), what it's good for, what's in the kit, specs where known, care jobs and what it pairs with.
- **Search** (magnifying glass, top right) looks through names, brands, kit and uses.
- **Spirit level** (top of every page): the bubble shows how far down the page you are.

Every drawing moves differently: the saw blade spins, the sander buzzes, the vacuum hose sways, the blower blows leaves, the drill throws dust, the tape measure slides and the level bubble drifts. Motion switches off when the phone's Reduce Motion setting is on.

The light/dark choice is saved on each phone (browser storage), not in the repo.

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
- `pricedOn`: the date the new prices were checked.
- `shed`: `{ name }`.
- `categories[]`: `{ id, name, blurb }`. Tab artwork exists for `power`, `hand` and `yard`.
- `tools[]`:
  - `id`: short kebab-case, unique.
  - `name`: what it is, without the brand.
  - `tag`: short name for the wall label (about 12 characters).
  - `brand`, `model`: `null` if unknown.
  - `category`: a category `id` (`power`, `hand` or `yard`). Each category is a tab in the bottom bar.
  - `art`: drawing key (`mitresaw`, `sander`, `vac`, `blower`, `battery`, `wheelbarrow`, `toolbag`, `sockets`, `handset`, `screwdrivers`, `knife`, `bits`, `level`, `shed`, `drill`, `circsaw`, `tape`, `clamp`, `spade`, `ladder`, `rotaryhammer`, `bblower`, `rros`, `polisher`, `inflator`, `sprayer`, `detector`, `square`, `hacksaw`, `prybar`, `caulkgun`, `toolbox`, `generic`).
  - `colour`: brand colour for the drawing and the tool page.
  - `size`: wall slot size: `small`, `wide` or `big`.
  - `paid`: what was paid. `null` if not recorded.
  - `newPrice`, `newFrom`, `newUrl`: current NZ new price, the shop (and the model matched, if not the exact one) and the page it came from. Look it up, never guess.
  - `priceCheck` (optional): `true` when the price came from a search result rather than a confirmed page; the tool page shows "To confirm".
  - `usedValue` (optional): a set used value, used for old or discontinued tools (estimated from Trade Me or the tool's age). Without it, used value is 55% of new, or 40% if `condition` is `worn`.
  - `power`: `Corded 240V`, a battery platform such as `Ryobi One+ 18V`, or `null` for hand tools.
  - `includes[]`, `specs[[label, value]]`, `notes`.
  - `uses[]`: what it's good for.
  - `pairs[]`: ids of tools it works with.
  - `condition` (optional): `good`, `fair` or `worn`.
  - `spot` (optional): where it lives (e.g. Pegboard, Bench, Off the board).
  - `board` (optional): `false` keeps the tool off the pegboard wall on the home page (it still has its own page).
  - `storedIn` (optional): the `id` of the tool it's kept in, e.g. `keter-shed` for garden tools. The tool page links to it, and the Keter shed's page lists everything stored inside.
  - `care[]`: `{ id, text, every }` (`every` = days between jobs). Shown on the tool's Care tab with a plain-English frequency, plus general tips for that kind of tool.

## Where the list came from

- **The pegboard photo (23 Nov 2026):** added the Bosch SDS rotary hammer and GBL 18V-120 blower, Ryobi corded orbital sander, polisher and One+ inflator, Wagner cordless sprayer, stud detector, and the hand tools on the white board (speed square, hacksaw, pry bar, box level, caulking gun, metal tool box, more hammers, second hex key set). The GOP 250 CE, old drill and sheet sander are kept but off the board.
- **The pegboard photo (22 Nov 2026):** the Bosch, Ryobi and Makita power tools and the hand tools on the wall, plus the ToolPro socket set, Makita VC2000L vac and Makita BO5030 sander from separate photos. Every drawing is based on those photos.
- **Flip Ledger "kept" items:** the Bosch mitre saw, Ryobi blower vac and batteries, Stanley hand tool lot, Bosch hand set, screwdriver set, Kincrome knife, drill bits, OX levels, wheelbarrow and Keter shed. These are not confirmed yet as still being in the shed.

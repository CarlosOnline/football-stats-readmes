
# Football Stats Tracker

Modern web app for entering and tracking American football stats on a per-play basis. Built with React, TypeScript, Vite, and Material UI. Supports multi-game management, cloud sync, and flexible import/export.

## Key Features

- **Game Management:** Create, edit, and select games. All data is organized by game.
- **Per-Play Stat Entry:** Enter down, distance, play type, yards, players, and detailed play attributes.
- **Live Summaries:** Real-time breakdowns by player, play type, and team unit.
- **Notes & Play Editor:** Enter notes for each play, with navigation and editing tools.
- **Import/Export:** Supports Hudl, MaxPreps, spreadsheets, and internal JSON schema.
- **Cloud Sync:** Save/load games and plays to AWS DynamoDB (with credentials page).
- **Offline Support:** All data is stored locally using useLocalStorage for offline use.
- **Material UI:** Clean, responsive UI using React MUI components.

## Tech Stack

- React 19 + TypeScript
- Vite (dev/build tooling)
- Material UI (MUI) for all UI components
- useLocalStorage for all local data (plays, games, session state)
- AWS DynamoDB for cloud sync (optional)
- React Router for navigation

## Project Structure

- `src/` — React + TypeScript source
  - `main.tsx` — app entry
  - `App.tsx` — root component
  - `Themer.tsx` — theme provider
  - `types/` — internal types and schemas (see `tracker/play-state.ts`)
  - `ui/` — all UI components, hooks, and pages
  - `data-sources/` — import/export helpers for Hudl, MaxPreps, spreadsheets, DynamoDB
- `public/` — static assets
- `index.html` — Vite HTML template
- `package.json`, `tsconfig.json`, `vite.config.ts` — build/tooling config

## Usage

### Development

1. Install dependencies:
	```sh
	npm install
	```
2. Start the dev server:
	```sh
	npm run dev
	```
3. Open the printed URL (usually http://localhost:5173)

### Production Build

```sh
npm run build
npm run preview
```

### Cloud Sync (DynamoDB)

- Go to the Credentials page and enter your AWS credentials.
- Use the save/load buttons on the Games page to sync data with DynamoDB.

## Data Model

- The core data shape is `PlayState` (see `src/types/tracker/play-state.ts`).
- All importers/exporters convert to/from this structure.
- Games are stored with unique IDs; each play is linked to a game by `gameId`.

## Contributing

1. Fork the repo and create a feature branch.
2. Keep changes focused and add unit tests for parsing/serialization logic.
3. Open a pull request describing the change and any manual testing steps.

## License

Specify your license here (e.g. MIT) or add a `LICENSE` file in the project root.

## Color Palettes
https://www.color-hex.com/color-palette/89069
https://www.color-hex.com/color-palette/1040990
https://www.color-hex.com/color-palette/1006744


---

## Features

- Per-play stat entry (down, yards, play type, players)
- Support for many play types: run, pass, sack, fumble, interception, etc.
- Live summaries and breakdowns by player and play type
- Import and export support for common data sources and internal schema

## Supported Data Sources

This project includes import/export helpers for these sources and formats:

- Hudl (standard breakdown format)
- MaxPreps export format
- Generic spreadsheets (CSV / Excel)
- TrackerPlayState (internal JSON schema used by this app)

If you need an additional format, add a parser/serializer that maps fields into the internal `TrackerPlayState` shape.

## Quick start (development)

Prerequisites: Node.js (16+ recommended) and npm, or use yarn/pnpm if you prefer.

Open a terminal in the project root and run:

```powershell
npm install
npm run dev
```

Then open the URL printed by Vite (usually http://localhost:5173).

## Build and preview

Create an optimized production build and preview it locally:

```powershell
npm run build
npm run preview
```

## Project layout (important files)

- `src/` — React + TypeScript source
	- `main.tsx` — app entry
	- `App.tsx` — root component
	- `Themer.tsx` — theme helper
	- `types/` — internal types and schemas (e.g. `tracker-play-state.ts`)
- `public/` — static assets
- `index.html` — Vite HTML template
- `package.json`, `tsconfig.json`, `vite.config.ts` — build/tooling config

## Internal data shape

The canonical in-app representation is `TrackerPlayState` (see `src/types/tracker-play-state.ts`).
When adding importers/exporters, convert external formats into this structure so the rest of the app can remain format-agnostic.

## Contributing

1. Fork the repo and create a feature branch.
2. Keep changes focused and add unit tests for parsing/serialization logic.
3. Open a pull request describing the change and any manual testing steps.

### Suggested small improvements

- Add import validation and helpful error messages when a file fails to parse.
- Add sample data fixtures for each supported source to `dev/fixtures/` for easier testing.

## Notes for maintainers

- This project is intentionally small and assumes a browser-based UI for manual stat entry.
- Use the types in `src/types/tracker` when introducing new features that interact with play data.

## License

Specify your license here (e.g. MIT) or add a `LICENSE` file in the project root.

---


# Tracking

### Touchdowns
- 0 `NA` Row after touchdown

# Punt
- `NA` Row after Opponent **Punt** - `No Return - Touchback`
- No row after `No Return`
- **Punt Return** row after `LW Punt`

# Kick-Off
- **Kick Return** row after Opponent `Kick-Off`
- No **Kick Return** row after `LW Kick-Off` with `touchback`

# Field Goals, Extra Points
From the place from where it was kicked, and the 10 yards for the end zone is included.
The spreadsheet should show the calculated yardage, in the `Special Teams` columns

### PAT example:
Holder is usually 7 yards back from the line of scrimmage.
 It should be the line of scrimmage plus 17 yards.

---

# Azure Static Web App

- rg: lw-football-rg
- url: https://gray-cliff-06b2bfc10.1.azurestaticapps.net


# Spreadsheet

### Int / Fum / Block Return
`Return of a Interception, Fumble, or Block`

If the Kangs are on defense, and are the ones making the return, then that info would be recorded in the “Defense / Special Teams” set of columns. If there are return yards for any of those sorts of turnovers, the yards would go there.

If the opponent is the one with the return, then the intent is to enter that as a new row, with a play type of “Int / Fum / Block Return”. This then allows for the Kang tackler to be recorded.

If I were to do it over, I’d set the file up to record both scenarios as a row with the Play Type selection. I’ll look to see how involved it would be to re-wire that part.

I think the “Int Fum Block Return” play type is for when the opposing team has a return, so that the LW tackler can be recorded.

#### Opponent throws the pass
When the opponent throws an interception. Should the play type be Int Fum Block?

If the opponent throws it, then the play type would still be “pass”. There are columns to capture the interception return yards if any.

I think the “Int Fum Block Return” play type is for when the opposing team has a return, so that the LW tackler can be recorded.


### 2-pt Attempt
- I don’t think a 2-pt attempt counts for yardage, or a carry, just a successful 2-pt conversion.

- How do you record point after attempt where the snap was mishandled and the holder had to scramble and was pushed out of bounds before the end zone?

If the kick was not actually attempted, then I would change the play type to “2-pt Attempt”, since if the holder would have been able to run it in, it would count for 2.

Usually with a bad snap, I list the runner as “Team”, so as not to penalize the stats of an individual.

I don’t remember if there is a spot to capture a failed 2-pt conversion, so I would just put in the comments that the 2-pt attempt was unsuccessful. I’d also double check that the calculated score (over to the right hand part of the spreadsheet, where all of the columns are shaded gray) are bit counting the 2 points.

### Fumble

- LW fumble and turnover to other team
You list the play type was “Run”, then put the jersey number in for the running back. There should be a column a few to the right where you can select an option for a lost fumble. It’s the same column where you would capture a touchdown.

**Extra Row** If the runner gained yards on the play, you can use the row below to capture the line of scrimmage where the fumble happened.

If the opponent is receiving the punt, then the Play Type would be “Punt Return”, and then I would use Column AK to record who forced the fumble, and column AL for who recovered the fumble. If it was a muffed punt, and if we are calling it a fumble, I would list “Team” in Column AK for causing the fumble.

The columns in the screen shot are for when LW is returning the punt, to record the returner’s stats.

## Opponent QB Scrambling
You record anything for opponent QB passing but is forced to scramble instead?
I’d just count it as a run. It could also be a QB hurry if it seems like the defensive pressure caused it. I don’t have a column to capture a Hurry. If I notice one, I will usually mention it in the comments column.

QB Hurry is similar to a Pancake block in that it is difficult to look for without rewatching each play a few extra times. So if I notice it, I will try to take note. But I don’t necessarily seek it out.

I’d just put “QB hurry by # xx” in the comments column.

# Kick Returner
Not tracked if no return yards.

For opponent kick off, is the kick return person tracked if there is no return.  Just falls on the ball.  Its kind of like an onsides kick.


## Punt Return
Punt Return caught on yard 26 and return to yard 44.

On one line, you log the punt portion of the play, with the Play Type as “Punt”

On the next row, you capture the Punt Return portion, listing the 26 yard line as the line of scrimmage. The possession column would switch teams, and the Play Type would be “Punt Return”.

If LW is the one returning the punt, then you put the jersey number in the Returner column, over towards the right hand side of the spreadsheet.

If the punt were returned to the 41, then you list that on the next row as the line of scrimmage for the following first down play.

The yardage should auto calculate from that.
You can always check the Player Stat tab to see if the stats are recording as expected.

## Fumble on Hand Off
I think technically, the fumble goes to the QB, since he was last to have possession.

So QB jersey would be listening the “Runner” category. Then you’d either pick the Fumble - Retained or the Fumble - Lost option.
The line of scrimmage for the next play will then calculate the lost yardage.

## Safety by 2 players
There's only one Jersey slot for safety.
Maybe on one row give them both a tackle assist, and assign one of the jerseys in the safety column. In the comments column, you can capture the other jersey in the comments column.

It might then require a manual tweak in the conference forms, I don’t remember if those track individual safety stats.

Another option that might work is to use the next row to capture the second jersey in the safety column.

You’d enter “NA” for down, use the line of scrimmage from after the play to calculate the tackle for loss yards on the main row, and then list the second jersey in the safety column (while keeping the tackle columns in the lower row blank).

## Side Of Field
The LW side is the side the Kangs are defending, and the end zone that the opponents are driving towards.

The opponents side is the end zone the Kangs are trying to score in.

## Field Goal Yardage
For the FG, the end zone and the snap distance count in the yardage. So the 6 yd FG should be 23 yards.

For field goals, and extra points, it is from the place from where it was kicked, and the 10 yards for the end zone is included. I think that the holder is usually 7 yards back from the line of scrimmage.  The spreadsheet should show the calculated yardage, over in the Special Teams columns towards the right of the game log tab. It should be the line of scrimmage plus 17 yards.

Punts are different, they are just from the line of scrimmage, and do not count the drop-back.

## PAT Miss due to hold
For the PAT miss that was the bad hold, you might want to change that description to something like “2-pt attempt failed”. Otherwise Sandy will expect Oliver’s stats to show 2 missed PATs.

## Defender forces player out of bounds
Do you score a tackle for someone if the player goes out of bounds and the players nearby?
I usually try to, with the theory that if the defenders wasn’t there, the runner would have gone for longer. You can also list “Team” s the tackler, but I try to give it to a player.

## QB Sack when scrambling
Is it a sack if the quarterback runs but gets hit behind the line?
If it looked more like a running play than a passing play, then it wouldn’t be a sack. If it is unclear, then might as well count it as a sack.
It was definitely a running play. Thank you.

# Extra Yardage Rows
Add extra yardage rows for the following

### Touchdowns
- 0 `NA` Row after touchdown

### Punt
- `NA` Row after Opponent **Punt** - `No Return - Touchback`
- No row after `No Return`
- **Punt Return** row after `LW Punt`

### Kick-Off
- **Kick Return** row after Opponent `Kick-Off`
- No **Kick Return** row after `LW Kick-Off` with `touchback`

### Field Goals, Extra Points
From the place from where it was kicked, and the 10 yards for the end zone is included.
The spreadsheet should show the calculated yardage, in the `Special Teams` columns

### PAT example:
Holder is usually 7 yards back from the line of scrimmage.
 It should be the line of scrimmage plus 17 yards.

### First Downs From Penalties

 If LW is on offense, then the Play Type would be “penalty - opponent”, and we would mark “First Down” in the “First Down Achieved” column.

If LW is on defense, then the play type would be “Penalty - LW”, and we would mark “First Down” in the “First Down Allowed” column.

This will feed the summary sheets, since Sandy wants to track how many first downs came from Runs, Passes, and Penalties.

### Receiver yards with Penaly

A completion for the Washington receiver. Followed by a penalty that brings the ball back.

The offensive player gets credit to the Yardline where the penalty happened. So in the case above, if it was a 5 yard penalty, then the WR would get credit for the 7 yards, and then the penalty would count as -5.

### Interception for QB
counts as incomplete


# TODO:
- remove runningBackJersey for special teams / non-offensive plays from test files

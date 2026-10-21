# AMD Cycles — TradingView indicator

Pine Script v6 indicator that draws Accumulation / Manipulation / Distribution time cycles, macro time zones, session highs and lows, and key open lines.

## Install

1. Open TradingView → **Pine Editor**.
2. Paste the contents of [`amd_cycles.pine`](amd_cycles.pine).
3. Click **Add to chart**.

All times are in the **Timezone** input (default `America/New_York`).

On **daily and higher** timeframes only the Y.O. / M.O. / W.O. lines and the status table are drawn; cycles, sessions, macro zones, C.O., NY open / midnight lines and day separators are hidden.

## 2. AMD cycles

Starting at **Start Hour : Start Minute** (default 02:30), the day is split into three nested levels:

| Level | Length | Split |
|---|---|---|
| Macro | 270m | A · M · D (02:30–07:00, 07:00–11:30, 11:30–16:00) |
| Middle | 90m | each 270m → A · M · D |
| Small | 30m | each 90m → A · M · D |

Each cycle is a box from its start time to its end time, spanning the high and low of the cycle so far. Boxes use the Accumulation, Manipulation and Distribution colors. A level is skipped when the chart timeframe is longer than the cycle.

**History**: the current AMD day shows all three levels. Earlier days keep only their 270m and 90m boxes, for as many days as TradingView allows (500 boxes, roughly a month). A new AMD day starts at the Start time (02:30).

## 4. Macro time zones

A zone runs every hour from `xx:Start` to the next `yy:End` (default xx:45 → yy:15). Only one zone is drawn:

- **Inside a zone**: a full-height band in **Active Zone Color** from the zone's start to its end.
- **Outside a zone**: dotted vertical lines in **Upcoming Zone Color** at the next zone's start and end.

Time labels (e.g. `1:45`, `2:15`) sit on each boundary, just above the current price. Zones are not drawn on timeframes above 15m.

## 6. Open lines

Dashed lines from the open of the trigger bar to the current bar + **Extend with N bars**. Only the latest line of each kind is kept.

- **C.O.**: Cycle Open, the open of the latest AMD cycle (**C.O. Cycle**: 270m / 90m / 30m, default 90m). The line stops extending when the AMD day ends.
- **NY Open** (09:30) and **NY Midnight** (00:00), labelled with their time.
- **Y.O. / M.O. / W.O.**: yearly, monthly and weekly opens.
- **Day Separator**: dotted vertical line at 00:00.

## 7. Status table

| | A | M | D |
|---|---|---|---|
| 270m | ○ | ● | ○ |
| 90m | ● | ○ | ○ |
| 30m | ○ | ○ | ● |
| Macro | ● ACTIVE | | |

`●` marks the current phase of each level, in that phase's color. **Macro** shows whether a macro time zone is active.

## 8. Sessions

| Session | Default | Drawn |
|---|---|---|
| Asia | 18:00–02:30 | optional box + high/low lines |
| London | 02:30–07:00 | high/low lines |
| New York | 07:00–17:00 | high/low lines |

Lines run from session open to session close and follow the session's high and low. The session name is shown above the high of the latest session of each kind; older sessions show only their colors. Sessions are kept for as many days as TradingView allows (500 lines / labels / boxes per script).

## Future improvements

- **5. 369 Mode**: `Enable 369 Mode`, `Calculation Mode`, `Label Position`, `Label Color`, with 3 / 6 / 9 Top and Bottom markers above and below bars.

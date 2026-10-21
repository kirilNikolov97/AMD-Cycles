# AMD Cycles — TradingView indicator

Pine Script v6 indicator that draws Accumulation / Manipulation / Distribution time cycles, macro time zones, session highs and lows, and key open lines.

## Install

1. Open TradingView → **Pine Editor**.
2. Paste the contents of [`amd_cycles.pine`](amd_cycles.pine).
3. Click **Add to chart**.

All times are in the **Timezone** input (default `America/New_York`).

## 2. AMD cycles

Starting at **Start Hour : Start Minute** (default 02:30), the day is split into three nested levels:

| Level | Length | Split |
|---|---|---|
| Macro | 270m | A · M · D (02:30–07:00, 07:00–11:30, 11:30–16:00) |
| Middle | 90m | each 270m → A · M · D |
| Small | 30m | each 90m → A · M · D |

Each cycle is a box from its start time to its end time, spanning the high and low of the cycle so far. Boxes use the Accumulation, Manipulation and Distribution colors. Macro and middle boxes carry an `Acc` / `Man` / `Dist` label. A level is skipped when the chart timeframe is longer than the cycle.

## 4. Macro time zones

A zone runs every hour from `xx:Start` to the next `yy:End` (default xx:45 → yy:15). Only one zone is drawn: the active one in **Active Zone Color**, or the next one in **Upcoming Zone Color**. Time labels show the zone's start and end. The zone's height covers roughly the last 6 hours of price.

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

Lines run from session open to session close and follow the session's high and low. The session name is shown above the high.

## Future improvements

- **5. 369 Mode**: `Enable 369 Mode`, `Calculation Mode`, `Label Position`, `Label Color`, with 3 / 6 / 9 Top and Bottom markers above and below bars.

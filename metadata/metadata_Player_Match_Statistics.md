# FotMob Premier League Player Match Statistics Metadata

This dataset contains **Premier League player-level match statistics** collected directly from **FotMob web API endpoints**.

The notebook covers these seasons:

- **2023/2024**
- **2024/2025**
- **2025/2026**

Each row represents **one player appearance in one completed Premier League match**.

The provided dataset contains:

- **34,443 player-match rows**
- **127 columns**
- **1,140 unique matches**
- **944 unique players**
- **0 duplicate primary keys** using `Season + Match_ID + Player_ID`

> FotMob's web endpoints used by this notebook are unversioned and may change over time.

## Source Code

The notebook used to collect, transform, validate, and export the dataset is:

[View Source Code](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/src/data_collection/FotMob_API_Player_Match_Statistics_to_XLSX_Colab.ipynb)

The notebook does not require previously downloaded FotMob JSON files. It requests the data directly from FotMob when it runs.

---

## What This Dataset Represents

This dataset is designed for **player performance analysis at match level**.

It can help answer questions such as:

- How did a player perform in individual Premier League matches?
- How do players compare on goals, assists, xG, xA, passing, dribbling, duels, and defensive actions?
- How does performance differ by opponent, home/away status, position, or season?
- Which players have stronger per-90 attacking or defensive statistics?
- How do goalkeeper metrics such as saves, xGOT faced, and goals prevented compare?
- How can football performance data be joined with soccer-card market data for player-level analysis?

The dataset includes both:

- **raw statistics returned by FotMob**, and
- **derived metrics created by the notebook**, such as accuracy ratios and per-90 values.

---

## Dataset Coverage

<div align="center">

<table>
  <thead>
    <tr>
      <th>Season</th>
      <th>Player-Match Rows</th>
      <th>Unique Matches</th>
      <th>Unique Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>2023/2024</td>
      <td align="right">11,384</td>
      <td align="right">380</td>
      <td align="right">571</td>
    </tr>
    <tr>
      <td>2024/2025</td>
      <td align="right">11,567</td>
      <td align="right">380</td>
      <td align="right">562</td>
    </tr>
    <tr>
      <td>2025/2026</td>
      <td align="right">11,492</td>
      <td align="right">380</td>
      <td align="right">537</td>
    </tr>
  </tbody>
</table>

</div>

Across all three seasons, the file contains **1,140 unique matches** and **944 unique players**.

---

## Important Notes

Before using the dataset, keep these points in mind:

- Only matches where FotMob reports `finished = True` and `cancelled != True` are collected.
- Duplicate fixture IDs are removed before downloading match details.
- One row represents one player appearance in one match.
- The intended primary key is `Season + Match_ID + Player_ID`.
- The current provided dataset has **0 duplicate primary keys**.
- The notebook keeps all available player statistics returned by FotMob, so some columns are only populated for relevant players or matches.
- Goalkeeper-only metrics such as `Saves` and `xGOT_Faced` are naturally missing for outfield players.
- Some event-based statistics are missing when the event did not occur or when FotMob did not return the field.
- Ratio metrics are stored as decimal values. For example, `0.90` means **90%**.
- Per-90 metrics are calculated using actual minutes played. Very short appearances can therefore produce unusually large per-90 values.
- The notebook does not convert the units of physical metrics such as `Top speed`, `Distance covered`, `Running`, or `Sprinting`; values are retained as returned by FotMob.
- `Is_Captain` can be missing when the field is not present in the lineup response. Missing values should not automatically be treated as `False`.
- The uploaded CSV contains some `Team_Formation` values that look date-like, such as `4/3/2003` or `5/4/2001`. These are consistent with spreadsheet auto-conversion of formations such as `4-3-3` or `5-4-1`. Use the original XLSX or force this column to text when converting files.

---

## Output File

The notebook exports:

```text
Player_Match_Statistics.xlsx
```

The Excel workbook contains three sheets:

1. **Player Match Statistics** — the complete player-by-match dataset.
2. **Collection Summary** — collection results by season.
3. **Failed Matches** — matches that could not be collected or parsed.

The workbook is formatted with:

- frozen headers,
- filters,
- bold column names,
- readable column widths.

---

## Data Dictionary

<div align="center">

<table>
  <thead>
    <tr>
      <th>Column</th>
      <th>Type</th>
      <th>Source</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>Season</code></td><td>string</td><td>Notebook configuration</td><td>Premier League season requested by the notebook, for example 2023/2024.</td></tr>
    <tr><td><code>Date</code></td><td>date</td><td>Derived from FotMob API</td><td>Calendar date of the match, derived from the UTC kickoff timestamp.</td></tr>
    <tr><td><code>Kickoff_UTC</code></td><td>datetime</td><td>FotMob API</td><td>Match kickoff date and time in UTC.</td></tr>
    <tr><td><code>Gameweek</code></td><td>integer / nullable</td><td>FotMob API</td><td>Premier League match round or gameweek returned by FotMob.</td></tr>
    <tr><td><code>Match_ID</code></td><td>integer / nullable</td><td>FotMob API</td><td>FotMob match identifier.</td></tr>
    <tr><td><code>Player_ID</code></td><td>integer / nullable</td><td>FotMob API</td><td>FotMob player identifier.</td></tr>
    <tr><td><code>Opta_ID</code></td><td>integer / nullable</td><td>FotMob API</td><td>Opta player identifier returned in the FotMob player record.</td></tr>
    <tr><td><code>Player</code></td><td>string</td><td>FotMob API</td><td>Player name returned by FotMob.</td></tr>
    <tr><td><code>Team_ID</code></td><td>integer / nullable</td><td>FotMob API</td><td>FotMob team identifier for the player&#x27;s team in the match.</td></tr>
    <tr><td><code>Team</code></td><td>string</td><td>FotMob API</td><td>Player&#x27;s team in the match.</td></tr>
    <tr><td><code>Position</code></td><td>string</td><td>Derived from FotMob API</td><td>Simplified position mapped from FotMob&#x27;s usual playing position: GK, DEF, MID, or FWD.</td></tr>
    <tr><td><code>Opponent_ID</code></td><td>integer / nullable</td><td>Derived from FotMob API</td><td>FotMob team identifier of the opponent, derived from the match home and away teams.</td></tr>
    <tr><td><code>Opponent</code></td><td>string</td><td>Derived from FotMob API</td><td>Opponent team name, derived from the match home and away teams.</td></tr>
    <tr><td><code>Home_Away</code></td><td>string</td><td>Derived from FotMob API</td><td>Whether the player&#x27;s team was Home or Away.</td></tr>
    <tr><td><code>Minutes</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Minutes played in the match.</td></tr>
    <tr><td><code>Starts</code></td><td>boolean</td><td>FotMob API lineup</td><td>True when the player appears in the starting lineup; False when listed as a substitute.</td></tr>
    <tr><td><code>Rating</code></td><td>float</td><td>FotMob API player stats</td><td>FotMob match rating for the player.</td></tr>
    <tr><td><code>Team_Formation</code></td><td>string</td><td>FotMob API lineup</td><td>Team formation associated with the player&#x27;s lineup, for example 4-2-3-1.</td></tr>
    <tr><td><code>Is_Captain</code></td><td>boolean</td><td>FotMob API lineup</td><td>Captain indicator returned in the lineup data. Missing values should not automatically be interpreted as False.</td></tr>
    <tr><td><code>Sub_In_Minute</code></td><td>integer / nullable</td><td>FotMob API lineup</td><td>Minute when a substitute entered the match, when available.</td></tr>
    <tr><td><code>Sub_Out_Minute</code></td><td>integer / nullable</td><td>FotMob API lineup</td><td>Minute when a player left the match, when available.</td></tr>
    <tr><td><code>Is_Goalkeeper</code></td><td>boolean</td><td>FotMob API</td><td>FotMob goalkeeper indicator.</td></tr>
    <tr><td><code>Usual_Position_ID</code></td><td>integer / nullable</td><td>FotMob API lineup</td><td>FotMob usual playing position ID used by the notebook for the simplified Position mapping.</td></tr>
    <tr><td><code>Lineup_Position_ID</code></td><td>integer / nullable</td><td>FotMob API lineup</td><td>FotMob lineup position ID for the match.</td></tr>
    <tr><td><code>Starter_X</code></td><td>float</td><td>FotMob API lineup</td><td>Horizontal starting-position coordinate from FotMob&#x27;s lineup layout.</td></tr>
    <tr><td><code>Starter_Y</code></td><td>float</td><td>FotMob API lineup</td><td>Vertical starting-position coordinate from FotMob&#x27;s lineup layout.</td></tr>
    <tr><td><code>Sub_Reason</code></td><td>string</td><td>FotMob API lineup</td><td>Reason associated with a substitution event, such as tactical or injury, when available.</td></tr>
    <tr><td><code>Shirt_Number</code></td><td>integer / nullable</td><td>FotMob API</td><td>Player shirt number for the match.</td></tr>
    <tr><td><code>Goals</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goals scored by the player.</td></tr>
    <tr><td><code>Assists</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Assists credited to the player.</td></tr>
    <tr><td><code>xA</code></td><td>float</td><td>FotMob API player stats</td><td>Expected assists (xA).</td></tr>
    <tr><td><code>xG_xA</code></td><td>float</td><td>FotMob API player stats</td><td>Combined expected goals plus expected assists value (xG + xA).</td></tr>
    <tr><td><code>Accurate_Passes</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of completed passes.</td></tr>
    <tr><td><code>Pass_Attempts</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total pass attempts.</td></tr>
    <tr><td><code>Chances_Created</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of chances created.</td></tr>
    <tr><td><code>Shotmap</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Raw FotMob Shotmap statistic or indicator as returned by the player-stat payload.</td></tr>
    <tr><td><code>Fantasy points</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Fantasy points value returned by FotMob.</td></tr>
    <tr><td><code>Defensive_Actions</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of defensive actions.</td></tr>
    <tr><td><code>Touches</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total player touches.</td></tr>
    <tr><td><code>Touches_Opp_Box</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Touches inside the opposition penalty area.</td></tr>
    <tr><td><code>Successful_Dribbles</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Successful dribbles.</td></tr>
    <tr><td><code>Dribble_Attempts</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total dribble attempts.</td></tr>
    <tr><td><code>Passes_Final_Third</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Passes into the final third.</td></tr>
    <tr><td><code>Accurate_Long_Balls</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Completed long balls.</td></tr>
    <tr><td><code>Long_Ball_Attempts</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total long-ball attempts.</td></tr>
    <tr><td><code>Dispossessed</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of times the player was dispossessed.</td></tr>
    <tr><td><code>Tackles</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Tackles recorded for the player.</td></tr>
    <tr><td><code>Blocks</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Blocks recorded for the player.</td></tr>
    <tr><td><code>Clearances</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Clearances recorded for the player.</td></tr>
    <tr><td><code>Interceptions</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Interceptions recorded for the player.</td></tr>
    <tr><td><code>Recoveries</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Ball recoveries recorded for the player.</td></tr>
    <tr><td><code>Dribbled_Past</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of times the player was dribbled past.</td></tr>
    <tr><td><code>Ground_Duels_Won</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Ground duels won.</td></tr>
    <tr><td><code>Ground_Duels_Total</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total ground duels.</td></tr>
    <tr><td><code>Aerial_Duels_Won</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Aerial duels won.</td></tr>
    <tr><td><code>Aerial_Duels_Total</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total aerial duels.</td></tr>
    <tr><td><code>Fouls_Won</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Fouls won / times the player was fouled.</td></tr>
    <tr><td><code>Fouls_Committed</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Fouls committed by the player.</td></tr>
    <tr><td><code>Duels_Won</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total duels won.</td></tr>
    <tr><td><code>Duels_Lost</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total duels lost.</td></tr>
    <tr><td><code>xG</code></td><td>float</td><td>FotMob API player stats</td><td>Expected goals (xG).</td></tr>
    <tr><td><code>xGOT</code></td><td>float</td><td>FotMob API player stats</td><td>Expected goals on target (xGOT).</td></tr>
    <tr><td><code>Shots</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total shots.</td></tr>
    <tr><td><code>Shots_On_Target</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Shots on target.</td></tr>
    <tr><td><code>Shots_Off_Target</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Shots off target.</td></tr>
    <tr><td><code>Shot accuracy</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Successful or on-target shot count used in FotMob&#x27;s raw shot-accuracy statistic.</td></tr>
    <tr><td><code>Shot accuracy Total</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total attempts paired with FotMob&#x27;s raw shot-accuracy statistic.</td></tr>
    <tr><td><code>Accurate_Crosses</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Completed crosses.</td></tr>
    <tr><td><code>Cross_Attempts</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total cross attempts.</td></tr>
    <tr><td><code>Corners</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Corners taken or recorded for the player by FotMob.</td></tr>
    <tr><td><code>npxG</code></td><td>float</td><td>FotMob API player stats</td><td>Non-penalty expected goals.</td></tr>
    <tr><td><code>Big_Chances_Created</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Big chances created.</td></tr>
    <tr><td><code>Saves</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goalkeeper saves.</td></tr>
    <tr><td><code>Goals_Conceded</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goals conceded while the goalkeeper was playing.</td></tr>
    <tr><td><code>xGOT_Faced</code></td><td>float</td><td>FotMob API player stats</td><td>Expected goals on target faced by the goalkeeper.</td></tr>
    <tr><td><code>Diving save</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Diving saves recorded by FotMob.</td></tr>
    <tr><td><code>Saves inside box</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goalkeeper saves made from shots inside the box.</td></tr>
    <tr><td><code>Acted as sweeper</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Sweeper actions recorded by FotMob.</td></tr>
    <tr><td><code>Punches</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goalkeeper punches.</td></tr>
    <tr><td><code>Throws</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goalkeeper throws.</td></tr>
    <tr><td><code>High_Claims</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>High claims by the goalkeeper.</td></tr>
    <tr><td><code>Headed clearance</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Headed clearances.</td></tr>
    <tr><td><code>Blocked_Shots</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Blocked shots.</td></tr>
    <tr><td><code>Fantasy points Bonus</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Bonus component associated with the FotMob fantasy-points statistic.</td></tr>
    <tr><td><code>Offsides</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Offside occurrences.</td></tr>
    <tr><td><code>Last_Man_Tackle</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Last-man tackles.</td></tr>
    <tr><td><code>Big_Chances_Missed</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Big chances missed.</td></tr>
    <tr><td><code>Clearance off the line</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Goal-line clearances.</td></tr>
    <tr><td><code>Hit woodwork</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Shots or attempts that hit the woodwork.</td></tr>
    <tr><td><code>Conceded penalty</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Penalties conceded by the player.</td></tr>
    <tr><td><code>Error led to goal</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Errors directly recorded as leading to a goal.</td></tr>
    <tr><td><code>Penalties won</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Penalties won by the player.</td></tr>
    <tr><td><code>Saved penalties</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Penalties saved by the goalkeeper.</td></tr>
    <tr><td><code>Missed penalty</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Penalties missed by the player.</td></tr>
    <tr><td><code>Own goal</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Own goals.</td></tr>
    <tr><td><code>Goals_Prevented</code></td><td>float</td><td>FotMob API player stats</td><td>FotMob goals-prevented goalkeeper metric.</td></tr>
    <tr><td><code>Line breaking passes</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Line-breaking passes returned by FotMob.</td></tr>
    <tr><td><code>Top speed</code></td><td>float</td><td>FotMob API player stats</td><td>Top-speed metric returned by FotMob. Unit is not transformed by the notebook.</td></tr>
    <tr><td><code>Distance covered</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Distance-covered metric returned by FotMob. Unit is not transformed by the notebook.</td></tr>
    <tr><td><code>Running</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Running-distance/statistic value returned by FotMob.</td></tr>
    <tr><td><code>Running Total</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total value paired with the FotMob Running statistic.</td></tr>
    <tr><td><code>Sprinting</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Sprinting-distance/statistic value returned by FotMob.</td></tr>
    <tr><td><code>Sprinting Total</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Total value paired with the FotMob Sprinting statistic.</td></tr>
    <tr><td><code>Number of sprints</code></td><td>integer / nullable</td><td>FotMob API player stats</td><td>Number of sprints recorded by FotMob.</td></tr>
    <tr><td><code>Pass_Accuracy</code></td><td>float</td><td>Derived</td><td>Completed passes divided by total pass attempts. Stored as a decimal ratio from 0 to 1.</td></tr>
    <tr><td><code>Long_Ball_Accuracy</code></td><td>float</td><td>Derived</td><td>Accurate long balls divided by total long-ball attempts. Stored as a decimal ratio from 0 to 1.</td></tr>
    <tr><td><code>Dribble_Success_Rate</code></td><td>float</td><td>Derived</td><td>Successful dribbles divided by total dribble attempts. Stored as a decimal ratio from 0 to 1.</td></tr>
    <tr><td><code>Ground_Duel_Win_Rate</code></td><td>float</td><td>Derived</td><td>Ground duels won divided by total ground duels. Stored as a decimal ratio from 0 to 1.</td></tr>
    <tr><td><code>Aerial_Duel_Win_Rate</code></td><td>float</td><td>Derived</td><td>Aerial duels won divided by total aerial duels. Stored as a decimal ratio from 0 to 1.</td></tr>
    <tr><td><code>Goals_Per90</code></td><td>float</td><td>Derived</td><td>Goals per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Assists_Per90</code></td><td>float</td><td>Derived</td><td>Assists per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>xG_Per90</code></td><td>float</td><td>Derived</td><td>Expected goals per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>xGOT_Per90</code></td><td>float</td><td>Derived</td><td>Expected goals on target per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>xA_Per90</code></td><td>float</td><td>Derived</td><td>Expected assists per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Shots_Per90</code></td><td>float</td><td>Derived</td><td>Shots per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Shots_On_Target_Per90</code></td><td>float</td><td>Derived</td><td>Shots on target per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Chances_Created_Per90</code></td><td>float</td><td>Derived</td><td>Chances created per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Touches_Opp_Box_Per90</code></td><td>float</td><td>Derived</td><td>Touches in the opposition box per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Successful_Dribbles_Per90</code></td><td>float</td><td>Derived</td><td>Successful dribbles per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Tackles_Per90</code></td><td>float</td><td>Derived</td><td>Tackles per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Interceptions_Per90</code></td><td>float</td><td>Derived</td><td>Interceptions per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Recoveries_Per90</code></td><td>float</td><td>Derived</td><td>Recoveries per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Clearances_Per90</code></td><td>float</td><td>Derived</td><td>Clearances per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Ground_Duels_Won_Per90</code></td><td>float</td><td>Derived</td><td>Ground duels won per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Aerial_Duels_Won_Per90</code></td><td>float</td><td>Derived</td><td>Aerial duels won per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Fouls_Won_Per90</code></td><td>float</td><td>Derived</td><td>Fouls won per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
    <tr><td><code>Fouls_Committed_Per90</code></td><td>float</td><td>Derived</td><td>Fouls committed per 90 minutes, calculated as statistic ÷ Minutes × 90.</td></tr>
  </tbody>
</table>

</div>

---

## Data Collection Rules

### Competition

```text
Premier League
FotMob League ID = 47
Country Code = ENG
```

### Seasons

```text
2023/2024
2024/2025
2025/2026
```

### Match Selection

The notebook requests the Premier League fixture list for each season and keeps only matches where:

```text
finished = True
cancelled != True
```

Duplicate match IDs are removed before requesting player-level match details.

### API Endpoints

The notebook first tries:

```text
https://www.fotmob.com/api/data
```

and falls back to:

```text
https://www.fotmob.com/api
```

The main endpoint names used are:

```text
leagues
matchDetails
```

The `leagues` endpoint is used to identify completed matches.

The `matchDetails` endpoint is used to collect lineup information and player statistics for each match.

---

## Position Mapping

The notebook converts FotMob's usual playing position ID into a simplified position:

| FotMob Position ID | Position |
| ---: | --- |
| 0 | GK |
| 1 | DEF |
| 2 | MID |
| 3 | FWD |

This mapping creates the `Position` column.

---

## Ratio Metrics

The notebook creates the following ratio metrics:

```text
Pass_Accuracy
Long_Ball_Accuracy
Dribble_Success_Rate
Ground_Duel_Win_Rate
Aerial_Duel_Win_Rate
```

The general formula is:

```text
Ratio = Successful Actions / Total Attempts
```

Examples:

```text
Pass_Accuracy = Accurate_Passes / Pass_Attempts
Long_Ball_Accuracy = Accurate_Long_Balls / Long_Ball_Attempts
Dribble_Success_Rate = Successful_Dribbles / Dribble_Attempts
```

If the denominator is zero, the notebook returns a missing value instead of dividing by zero.

Ratio values are stored as decimals:

```text
0.90 = 90%
0.75 = 75%
```

---

## Per-90 Metrics

The notebook creates per-90 statistics using:

```text
Per 90 = Statistic / Minutes × 90
```

Per-90 columns include:

```text
Goals_Per90
Assists_Per90
xG_Per90
xGOT_Per90
xA_Per90
Shots_Per90
Shots_On_Target_Per90
Chances_Created_Per90
Touches_Opp_Box_Per90
Successful_Dribbles_Per90
Tackles_Per90
Interceptions_Per90
Recoveries_Per90
Clearances_Per90
Ground_Duels_Won_Per90
Aerial_Duels_Won_Per90
Fouls_Won_Per90
Fouls_Committed_Per90
```

> For player comparisons, consider applying a minimum-minutes threshold because a one- or two-minute appearance can create extreme per-90 values.

---

## How Match and Player Information Is Created

The notebook combines information from several parts of each FotMob `matchDetails` response.

### Match Information

```text
Season
Date
Kickoff_UTC
Gameweek
Match_ID
```

### Player and Team Information

```text
Player_ID
Opta_ID
Player
Team_ID
Team
Opponent_ID
Opponent
Home_Away
Shirt_Number
```

### Lineup Information

```text
Position
Starts
Team_Formation
Is_Captain
Usual_Position_ID
Lineup_Position_ID
Starter_X
Starter_Y
Sub_In_Minute
Sub_Out_Minute
Sub_Reason
Is_Goalkeeper
```

### Player Statistics

All available FotMob player-stat groups are read dynamically.

For each statistic, the notebook stores:

```text
value
```

and, when available:

```text
total
bonus
```

This is why the final dataset contains some raw columns such as:

```text
Shot accuracy
Shot accuracy Total
Fantasy points
Fantasy points Bonus
Running
Running Total
Sprinting
Sprinting Total
```

---

## Validation

The notebook validates the final dataset using the intended primary key:

```text
Season + Match_ID + Player_ID
```

The provided file has:

```text
Rows                 = 34,443
Columns              = 127
Unique matches       = 1,140
Unique players       = 944
Duplicate primary key = 0
```

---

## Data Limitations

FotMob may return different statistics depending on:

- player position,
- match,
- season,
- whether a statistic occurred,
- whether that statistic was available in the FotMob response.

Because of this, missing values do not always mean zero.

For example:

- a missing `Saves` value for an outfield player should not be converted to a goalkeeper performance of zero without context,
- a missing event statistic may mean the API did not return that field,
- a missing ratio can occur because the denominator was zero.

The dataset also contains provider-specific metrics whose exact methodology may not be fully documented in the notebook, including fields such as:

```text
Rating
Goals_Prevented
Line breaking passes
Top speed
Distance covered
Running
Sprinting
Fantasy points
```

These fields should be interpreted as **FotMob-provided metrics** rather than independently calculated measures unless explicitly identified as derived in this metadata.


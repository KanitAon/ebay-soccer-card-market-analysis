# FotMob Premier League Player Profiles Metadata

This dataset contains **Premier League player profiles** collected and prepared using **FotMob web API endpoints**.

The dataset focuses on players who appeared in Premier League matches across these seasons:

- **2023/2024**
- **2024/2025**
- **2025/2026**

Each row represents **one unique FotMob player**.

The provided dataset contains:

- **943 unique players**
- **13 columns**
- **943 unique FotMob player IDs**
- **943 unique player keys**
- **0 duplicate FotMob player IDs**

## Source Code

The notebook used to collect and prepare the player profile data is available here:

[View Source Code](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/src/data_collection/FotMob_API_Player_Profiles_to_XLSX_Colab.ipynb)

The notebook collects the data directly from FotMob when it runs.

> **Important:** FotMob's web API endpoints used by this notebook are unofficial and unversioned. Endpoint structures may change over time.

---

## What This Dataset Represents

This dataset provides a **master player profile table** for Premier League players found in the selected seasons.

It can be used to answer questions such as:

- What is the canonical name of each player?
- What is the player's FotMob ID or Opta ID?
- What detailed playing position does FotMob assign to the player?
- Which teams did the player appear for across the selected seasons?
- In which Premier League seasons did the player appear?
- What alternative player names appeared in FotMob match statistics?
- What stable player key can be used when joining football performance data with soccer-card market data?

The table is designed to work as a **player dimension or player master table** that can be joined with match-level statistics or card-market datasets.

---

## Important Notes

Before using the dataset, keep these points in mind:

- Each row represents **one unique FotMob player**.
- `FotMob_Player_ID` is the main source identifier.
- `Player_Key` is a project-generated stable key using the format `FM_<FotMob_Player_ID>`.
- The player universe is discovered from completed Premier League matches in the selected seasons.
- Duplicate match IDs are removed before match details are requested.
- Only players with player statistics in the FotMob match response are added to the player universe.
- `Player_Canonical` is selected from the most common player name found in match statistics.
- `Stats_Name_Aliases` stores all observed FotMob match-stat names for the same player.
- `Teams` stores all observed Premier League teams for the player across the selected seasons.
- `Seasons` stores all selected seasons in which the player appeared.
- Detailed profile position information comes from FotMob `playerData`.
- If the profile position is too generic, the notebook uses a detailed-position fallback.
- If a profile position still cannot be resolved, the notebook uses historical match position as a fallback.
- The final dataset contains **no missing `Final_Position` values**.
- The values in `Teams`, `Seasons`, and `Stats_Name_Aliases` may contain multiple values separated by ` | `.

Because this table combines profile information and historical match context, some fields are **derived values** rather than direct FotMob profile attributes.

---

## Output File

```text
Player_Profiles.xlsx
```

The Excel workbook contains four sheets:

```text
Player Profiles
Match Collection Summary
Failed Matches
Failed Profiles
```

The workbook is formatted with:

- frozen headers,
- filters,
- bold column names,
- readable column widths.

---

## Dataset Coverage

<div align="center">

<table>
  <thead>
    <tr>
      <th>Season</th>
      <th>Unique Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>2023/2024</td>
      <td align="right">570</td>
    </tr>
    <tr>
      <td>2024/2025</td>
      <td align="right">562</td>
    </tr>
    <tr>
      <td>2025/2026</td>
      <td align="right">537</td>
    </tr>
  </tbody>
</table>

</div>

> A player can appear in more than one season, so the season counts should not be added together to calculate the number of unique players.

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
    <tr>
      <td><code>FotMob_Player_ID</code></td>
      <td>integer</td>
      <td>FotMob API</td>
      <td>Unique FotMob identifier for the player. This is the main source-level player ID used by the notebook.</td>
    </tr>
    <tr>
      <td><code>Opta_ID</code></td>
      <td>integer</td>
      <td>FotMob API</td>
      <td>Opta player identifier returned in FotMob match statistics.</td>
    </tr>
    <tr>
      <td><code>Player_Key</code></td>
      <td>string</td>
      <td>Derived</td>
      <td>Project-generated stable player key using the format <code>FM_&lt;FotMob_Player_ID&gt;</code>. Example: <code>FM_737066</code>.</td>
    </tr>
    <tr>
      <td><code>Player_Canonical</code></td>
      <td>string</td>
      <td>Derived from FotMob match statistics</td>
      <td>Canonical player name selected as the most common non-null player name observed in FotMob match statistics.</td>
    </tr>
    <tr>
      <td><code>Profile_Name</code></td>
      <td>string</td>
      <td>FotMob playerData API</td>
      <td>Player name returned directly from the player's FotMob profile.</td>
    </tr>
    <tr>
      <td><code>Primary_Position</code></td>
      <td>string</td>
      <td>FotMob playerData API</td>
      <td>Primary position label returned from FotMob <code>positionDescription.primaryPosition</code>. This value may be specific, such as <code>Left Back</code>, or generic, such as <code>Defender</code>.</td>
    </tr>
    <tr>
      <td><code>Resolved_Profile_Position</code></td>
      <td>string</td>
      <td>Derived from FotMob player profile</td>
      <td>Resolved detailed profile position. A specific primary position is used first; otherwise the notebook uses the best detailed position available in the profile.</td>
    </tr>
    <tr>
      <td><code>Historical_Broad_Position</code></td>
      <td>string</td>
      <td>Derived from FotMob match data</td>
      <td>Broad historical position with the highest total minutes played across collected matches. Values are generally <code>GK</code>, <code>DEF</code>, <code>MID</code>, or <code>FWD</code>.</td>
    </tr>
    <tr>
      <td><code>Final_Position</code></td>
      <td>string</td>
      <td>Derived</td>
      <td>Final position used by the project. It uses <code>Resolved_Profile_Position</code> when available and falls back to <code>Historical_Broad_Position</code> when necessary.</td>
    </tr>
    <tr>
      <td><code>Final_Position_Source</code></td>
      <td>string</td>
      <td>Derived</td>
      <td>Indicates how <code>Final_Position</code> was determined. Values include <code>Primary Profile Position</code>, <code>Detailed Position Fallback</code>, and <code>Historical Match Fallback</code>.</td>
    </tr>
    <tr>
      <td><code>Stats_Name_Aliases</code></td>
      <td>string</td>
      <td>Derived from FotMob match statistics</td>
      <td>All unique player names observed in FotMob match statistics for the same player, sorted and joined with <code> | </code>.</td>
    </tr>
    <tr>
      <td><code>Teams</code></td>
      <td>string</td>
      <td>Derived from FotMob match statistics</td>
      <td>All unique Premier League teams observed for the player in the selected seasons, sorted and joined with <code> | </code>.</td>
    </tr>
    <tr>
      <td><code>Seasons</code></td>
      <td>string</td>
      <td>Derived from FotMob match statistics</td>
      <td>All selected Premier League seasons in which the player appeared, sorted and joined with <code> | </code>.</td>
    </tr>
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

For each season, the notebook requests the Premier League fixture list and keeps only matches where:

```text
finished = True
cancelled != True
```

Duplicate match IDs are removed before requesting match details.

### Player Selection

A player is added to the player universe when:

```text
player ID is available
player statistics are available
```

The notebook then requests one FotMob profile for every discovered player.

---

## FotMob API Endpoints

The notebook first tries:

```text
https://www.fotmob.com/api/data
```

and then falls back to:

```text
https://www.fotmob.com/api
```

The main endpoints used are:

```text
leagues
matchDetails
playerData
```

### `leagues`

Used to retrieve Premier League fixtures and identify completed matches.

### `matchDetails`

Used to collect:

```text
FotMob player ID
Opta ID
player name
team
historical position
minutes played
```

### `playerData`

Used to collect:

```text
profile name
primary position
detailed positions
```

The notebook requests player profiles using:

```text
includeMarketValues = false
```

---

## How the Player Universe Is Built

The notebook first collects player-level context from all selected completed Premier League matches.

The match-level records are then grouped by:

```text
FotMob_Player_ID
```

to create one row per player.

### Canonical Name

`Player_Canonical` is selected using the most common non-null `Stats_Name`.

Conceptually:

```text
Player_Canonical = mode(Stats_Name)
```

If multiple values tie for the mode, the first mode is used.

### Name Aliases

All unique observed match-stat names are stored in:

```text
Stats_Name_Aliases
```

Multiple values are separated by:

```text
 |
```

### Teams

All unique teams observed for the player are stored in:

```text
Teams
```

For example:

```text
Arsenal | Newcastle United | Southampton
```

### Seasons

All selected seasons in which the player appeared are stored in:

```text
Seasons
```

For example:

```text
2023/2024 | 2024/2025 | 2025/2026
```

---

## Historical Broad Position

The notebook maps FotMob's broad position IDs as follows:

<div align="center">

<table>
  <thead>
    <tr>
      <th>FotMob Position ID</th>
      <th>Historical Broad Position</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>0</td><td>GK</td></tr>
    <tr><td>1</td><td>DEF</td></tr>
    <tr><td>2</td><td>MID</td></tr>
    <tr><td>3</td><td>FWD</td></tr>
  </tbody>
</table>

</div>

A player may appear in more than one broad position across different matches.

To select one historical broad position, the notebook:

1. sums minutes played for each player and broad position,
2. sorts positions by total minutes,
3. selects the position with the highest total minutes.

Conceptually:

```text
Historical_Broad_Position
=
position with maximum total Minutes
```

This makes the historical position more representative than simply selecting the position from one match.

---

## How Profile Position Is Resolved

FotMob's `playerData` response contains:

```text
positionDescription
```

The notebook uses two parts of this object:

```text
primaryPosition
positions
```

### Step 1 — Specific Primary Position

If `Primary_Position` is specific, it becomes:

```text
Resolved_Profile_Position
```

Example:

```text
Primary_Position          = Left Back
Resolved_Profile_Position = Left Back
```

The source becomes:

```text
Primary Profile Position
```

### Step 2 — Detailed Position Fallback

The following generic primary labels are considered too broad:

```text
defender
midfielder
forward
keeper
coach
```

When a generic primary position is found, the notebook examines the detailed positions.

Detailed positions are ranked by:

1. `isMainPosition = True`
2. highest number of occurrences

The best available detailed position is then used.

Example:

```text
Primary_Position          = Midfielder
Resolved_Profile_Position = Defensive Midfielder
```

The source becomes:

```text
Detailed Position Fallback
```

### Step 3 — Historical Match Fallback

If the profile still does not provide a usable detailed position:

```text
Final_Position = Historical_Broad_Position
```

The source becomes:

```text
Historical Match Fallback
```

---

## Final Position Source

In the provided dataset, the final position was resolved as follows:

<div align="center">

<table>
  <thead>
    <tr>
      <th>Final Position Source</th>
      <th>Players</th>
      <th>Share</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Primary Profile Position</td>
      <td align="right">896</td>
      <td align="right">95.0%</td>
    </tr>
    <tr>
      <td>Detailed Position Fallback</td>
      <td align="right">45</td>
      <td align="right">4.8%</td>
    </tr>
    <tr>
      <td>Historical Match Fallback</td>
      <td align="right">2</td>
      <td align="right">0.2%</td>
    </tr>
  </tbody>
</table>

</div>

This means that almost all players receive a detailed position directly from FotMob profile information, while only a small number require historical match data as a fallback.

---

## Final Position Distribution

The most common final positions in the provided dataset are:

<div align="center">

<table>
  <thead>
    <tr>
      <th>Final Position</th>
      <th>Players</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Center Back</td><td align="right">175</td></tr>
    <tr><td>Defensive Midfielder</td><td align="right">130</td></tr>
    <tr><td>Striker</td><td align="right">130</td></tr>
    <tr><td>Attacking Midfielder</td><td align="right">82</td></tr>
    <tr><td>Left Winger</td><td align="right">73</td></tr>
    <tr><td>Right Winger</td><td align="right">72</td></tr>
    <tr><td>Left Back</td><td align="right">69</td></tr>
    <tr><td>Keeper</td><td align="right">69</td></tr>
    <tr><td>Right Back</td><td align="right">64</td></tr>
    <tr><td>Central Midfielder</td><td align="right">48</td></tr>
    <tr><td>Right Wing-Back</td><td align="right">8</td></tr>
    <tr><td>Left Wing-Back</td><td align="right">8</td></tr>
    <tr><td>Right Midfielder</td><td align="right">7</td></tr>
    <tr><td>Left Midfielder</td><td align="right">6</td></tr>
    <tr><td>MID</td><td align="right">2</td></tr>
  </tbody>
</table>

</div>

The two records with `Final_Position = MID` are players whose detailed profile position could not be resolved and therefore use the historical broad-position fallback.

---

## Validation

The notebook validates the final player table using `FotMob_Player_ID` and `Player_Key`.

For the provided dataset:

```text
Rows                    = 943
Columns                 = 13
Unique FotMob IDs       = 943
Unique Player Keys      = 943
Duplicate FotMob IDs    = 0
Missing Opta_ID         = 0
Missing Profile_Name    = 0
Missing Final_Position  = 0
```

This confirms that the provided file contains one unique record per FotMob player.

---

## Data Limitations

FotMob profile and match data may change over time.

Important limitations include:

- FotMob's web API is unofficial and unversioned.
- A player profile may be updated after the dataset is collected.
- Player names may differ between match statistics and profile data.
- Team history only reflects teams observed in the selected Premier League seasons.
- The dataset does not represent a player's complete career team history.
- The dataset does not include players who did not appear in the collected Premier League match statistics.
- `Historical_Broad_Position` is based on minutes played in the selected Premier League seasons, not the player's entire career.
- `Primary_Position` may be too generic for detailed analysis.
- `Final_Position` is therefore a resolved field created using several fallback rules.
- `Stats_Name_Aliases`, `Teams`, and `Seasons` are multi-value strings rather than normalized child tables.
- Position labels come from FotMob and may differ from position classifications used by other football data providers.

Because of these limitations, `Final_Position` should be treated as a **project-defined resolved position based on FotMob data**, rather than a universal official player position.

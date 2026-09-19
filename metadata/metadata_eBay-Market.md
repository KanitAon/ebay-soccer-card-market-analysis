# eBay Premier League Card Dataset Metadata

This dataset contains **current eBay listings for Premier League soccer cards** collected using the **eBay Browse API**.

The dataset focuses on two major brands:

- **Panini**
- **Topps**

The search covers these seasons:

- 2023
- 2023-24
- 2024-25
- 2025
- 2025-26
- 2026

Example search keywords:

```text
premier league panini 2025
premier league topps 2025
```

Each row represents one unique eBay listing after duplicate listings are removed.

## Source Code

The notebook used to collect and prepare the eBay data is available here:

[View Source Code](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/src/data_collection/eBay_Market_Data.ipynb)

---

## What This Dataset Represents

This dataset is useful for understanding the **current soccer card market on eBay**.
It can help answer questions such as:

- What card products are commonly listed?
- Which brands appear more often?
- What price ranges are common?
- Which players or clubs appear frequently?
- How often do listings include rookie, autograph, patch, or graded cards?

> **Important:** This dataset contains current listings, not historical sold prices.

The `price` column shows the seller's current asking price on eBay.

---

## Important Notes

Before using the dataset, keep these points in mind:

- The data represents **current eBay listings**.
- It does not represent completed or sold transactions.
- Only listings with a price greater than **$10** are included.
- Duplicate listings are removed before the final dataset is created.
- Many card details are extracted from the listing title.
- Some extracted values may be missing or incorrect because sellers use different title formats.
- The `brand` field comes from the search keyword used by the notebook.

Because of this, fields such as player name, product line, rookie status, and grade should be treated as **derived values** rather than official eBay attributes.

---

## Output File

```text
ebay_premier_league_cards.xlsx
```

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
    <tr><td><code>title</code></td><td>string</td><td>eBay API</td><td>Full title of the eBay listing.</td></tr>
    <tr><td><code>player</code></td><td>string</td><td>Derived from title</td><td>Player name detected from the listing title.</td></tr>
    <tr><td><code>position</code></td><td>string</td><td>Derived from title</td><td>Player position detected from the title, such as <code>GK</code>, <code>DF</code>, <code>MF</code>, or <code>FW</code>.</td></tr>
    <tr><td><code>club</code></td><td>string</td><td>Derived from title</td><td>Premier League club detected from the listing title.</td></tr>
    <tr><td><code>season</code></td><td>string</td><td>Derived from title</td><td>Soccer season detected from the title, such as <code>2024-25</code>.</td></tr>
    <tr><td><code>brand</code></td><td>string</td><td>Search keyword</td><td>Brand used in the search. Values are <code>Panini</code> or <code>Topps</code>.</td></tr>
    <tr><td><code>product_line</code></td><td>string</td><td>Derived from title</td><td>Product or card set detected from the title, such as <code>Prizm</code>, <code>Select</code>, or <code>Donruss</code>.</td></tr>
    <tr><td><code>year</code></td><td>integer/string</td><td>Derived from title</td><td>First 4-digit year found in the title.</td></tr>
    <tr><td><code>card_number</code></td><td>integer/string</td><td>Derived from title</td><td>Card number detected from patterns such as <code>#123</code>.</td></tr>
    <tr><td><code>serial</code></td><td>integer/string</td><td>Derived from title</td><td>Print-run number detected from numbered cards. Example: <code>12/99</code> becomes <code>99</code>.</td></tr>
    <tr><td><code>price</code></td><td>float</td><td>eBay API</td><td>Current listing price. Only prices greater than 10 are included.</td></tr>
    <tr><td><code>price_log</code></td><td>float</td><td>Derived</td><td>Log-transformed price using <code>log(1 + price)</code>.</td></tr>
    <tr><td><code>currency</code></td><td>string</td><td>eBay API</td><td>Currency code, such as <code>USD</code>.</td></tr>
    <tr><td><code>condition</code></td><td>string</td><td>eBay API</td><td>Listing condition provided by eBay.</td></tr>
    <tr><td><code>graded</code></td><td>boolean</td><td>Derived from title</td><td><code>True</code> when grading terms such as PSA, BGS, SGC, or CGC are found.</td></tr>
    <tr><td><code>grade</code></td><td>integer/string</td><td>Derived from title</td><td>Numeric card grade detected from the title.</td></tr>
    <tr><td><code>autograph</code></td><td>boolean</td><td>Derived from title</td><td><code>True</code> when autograph-related keywords are detected.</td></tr>
    <tr><td><code>patch</code></td><td>boolean</td><td>Derived from title</td><td><code>True</code> when patch, jersey, relic, or similar terms are detected.</td></tr>
    <tr><td><code>rookie</code></td><td>boolean</td><td>Derived from title</td><td><code>True</code> when rookie-related terms such as <code>rookie</code>, <code>RC</code>, or <code>RPA</code> are detected.</td></tr>
    <tr><td><code>buying_options</code></td><td>string</td><td>eBay API</td><td>Available buying methods, such as Buy It Now or Auction.</td></tr>
    <tr><td><code>is_auction</code></td><td>boolean</td><td>Derived from eBay API</td><td><code>True</code> when the listing is an auction.</td></tr>
    <tr><td><code>bids</code></td><td>integer</td><td>eBay API</td><td>Number of bids on the listing.</td></tr>
    <tr><td><code>end_date</code></td><td>datetime</td><td>eBay API</td><td>Date and time when the listing ends.</td></tr>
    <tr><td><code>days_until_end</code></td><td>integer/string</td><td>Derived</td><td>Number of days until the listing ends.</td></tr>
    <tr><td><code>end_weekday</code></td><td>integer/string</td><td>Derived</td><td>Weekday of the listing end date, where <code>0 = Monday</code> and <code>6 = Sunday</code>.</td></tr>
    <tr><td><code>num_images</code></td><td>integer</td><td>eBay API</td><td>Number of listing images returned by the API.</td></tr>
    <tr><td><code>category</code></td><td>string</td><td>eBay API</td><td>eBay category of the listing.</td></tr>
    <tr><td><code>country</code></td><td>string</td><td>eBay API</td><td>Country from the listing item location.</td></tr>
    <tr><td><code>seller</code></td><td>string</td><td>eBay API</td><td>eBay seller username.</td></tr>
    <tr><td><code>seller_feedback_count</code></td><td>integer</td><td>eBay API</td><td>Seller feedback score.</td></tr>
    <tr><td><code>seller_feedback_pct</code></td><td>float/string</td><td>eBay API</td><td>Seller feedback percentage.</td></tr>
    <tr><td><code>title_length</code></td><td>integer</td><td>Derived</td><td>Number of characters in the listing title.</td></tr>
    <tr><td><code>has_emoji</code></td><td>boolean</td><td>Derived from title</td><td><code>True</code> when the title contains an emoji or supported symbol.</td></tr>
    <tr><td><code>url</code></td><td>string</td><td>eBay API</td><td>Direct link to the eBay listing.</td></tr>
  </tbody>
</table>

</div>

---

## Data Collection Rules

### Brands

```text
Panini
Topps
```

### Seasons

```text
2023
2023-24
2024-25
2025
2025-26
2026
```

### Price Filter

Only listings with:

```text
price > 10
```

are kept in the final dataset.

This filter helps remove very low-priced listings that may not be useful for the main market analysis.

---

## How Card Information Is Extracted

Some card information is not directly provided by eBay as structured data.

Instead, the notebook reads the listing title and tries to identify information such as:

```text
player
position
club
season
product_line
year
card_number
serial
graded
grade
autograph
patch
rookie
has_emoji
```

For example:

```text
2024 Panini Prizm Cole Palmer Rookie PSA 10
```

may be interpreted as:

```text
player       = Cole Palmer
brand        = Panini
product_line = Prizm
year         = 2024
rookie       = True
graded       = True
grade        = 10
```

This makes the dataset easier to analyze, but these fields are not always perfect.

---

## Data Limitations

eBay sellers write listing titles in many different ways.

They may use:

- abbreviations
- spelling variations
- incomplete card information
- marketing words
- different product names

Because of this, title-based fields may contain missing or incorrect values.

These fields should therefore be treated as **parsed or estimated values** and checked before high-accuracy analysis.

One known issue is that the current `autograph` rule also matches:

```text
swatch
patch
```

As a result, some memorabilia cards may incorrectly appear as:

```text
autograph = True
```

This should be considered when analyzing autograph cards.

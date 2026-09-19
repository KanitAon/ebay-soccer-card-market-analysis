# eBay Soccer Card Market Analysis

## Project Background

Buying soccer cards on eBay can be confusing for **new collectors**.

The same player can have many different cards, and prices can vary by **brand, product line, card type, rarity, and market demand**. Without a clear way to compare them, it can be hard to know what a reasonable price looks like or which cards are worth exploring.

This project uses data to make the soccer card market easier to understand.

It focuses on two major brands, **Topps and Panini**, and looks at how their products are distributed and priced on eBay. It also connects card prices with player performance to explore how the market values different players.

## Objective

This project aims to help **new soccer card collectors make more informed buying decisions on eBay** by answering three simple questions:

1. What types of soccer cards are available on eBay?

    Understand the distribution of **Topps and Panini** products in the market.

2. How much do different card products usually cost?

    Compare **product lines and price ranges** across Topps and Panini.

3. Do card prices match player performance?

    Compare **on-field performance** with **player card values on eBay**.


> **Goal:** This project does not aim to predict future card prices.  
> Instead, it provides a **simple, data-driven learning guide** to help newcomers understand the soccer card market before buying.

## Dataset

This project uses three main datasets:

1. **eBay Market Data**  
   Historical soccer card market data collected from **eBay Marketplace Insights**.  
   The dataset includes card information, listing details, and market prices.  
    [View Metadata](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/metadata/metadata_eBay-Market.md)

2. **Player Match Statistics**  
   Match-level player performance data collected from **FotMob**.  
   The dataset includes statistics such as minutes played, goals, assists, shots, passing, and other match performance metrics.  
   [View Metadata](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/metadata/metadata_Player_Match_Statistics.md)

3. **Player Profiles**  
   Player profile data collected from **FotMob**.  
   The dataset includes player information such as name, position, team, nationality, and other profile details.  
   [View Metadata](https://github.com/KanitAon/ebay-soccer-card-market-analysis/blob/main/metadata/metadata_Player_Profiles.md)

## Market Distribution Overview

To understand what the eBay soccer card market looks like.

This section looks at the market from four views:

- **Seller Asking-Price Market Distribution** — Understand the typical price range of soccer card listings and how prices are distributed.
- **Player Market Distribution** — See whether listings are spread across many players or concentrated among a smaller group.
- **Brand and Product Line Distribution** — Compare how listings are distributed across **Topps, Panini, and their major product lines**.

Together, these views show **where most listings are found, which players have the most market coverage, and which brands and products are most visible on eBay**.

### Seller Asking-Price Market Distribution

<p align="center">
  <img src="figure/figure_01.png"
       alt="Seller Asking-Price Market Distribution"
       width="900">
</p>

<p align="center">
  <b>Figure 1.</b> Distribution of seller asking prices for 7,248 single-player soccer card listings. The x-axis shows price ranges in USD, while the y-axis shows the percentage of listings in each range.
</p>

The graph shows that most soccer card listings are concentrated in the lower price ranges.

**Nearly 3 out of 4 listings (74.4%) are priced below $100**, and the largest group is the **$25–49 range**, which represents **30.7% of all listings**.

As prices increase, the number of listings drops quickly. Only **4.7% of listings are priced at $500 or more**, showing that very expensive cards make up only a small part of the market.

The difference between the **mean price of $187** and the **median price of $45** is also important. A few very expensive listings push the average much higher, so the average does not represent a typical card very well.

For this reason, the **median price** is more useful when trying to understand what a typical soccer card listing looks like.

> [!IMPORTANT]
> **Key Finding:** Most soccer cards in this dataset are priced below $100. For newcomers, the **median price and similar listings** are better reference points than the overall average because a small number of very expensive cards can make the market look more expensive than it really is.

### Player Market Distribution

The dataset contains **7,248 listings from 443 players**, but the listings are not evenly distributed across players.

Some players appear hundreds of times, while many players appear only a few times.

> Listing volume shows **market representation**, not buyer demand.  
> A player with more listings may simply have more cards available, more product releases, or more seller activity.

#### How Concentrated Is the Market?

<p align="center">
  <img src="figure/figure_02.png"
       alt="Cumulative Concentration of Listings Across Players"
       width="900">
</p>

<p align="center">
  <b>Figure 2.</b> Cumulative share of eBay listings across 443 players, ranked from the highest to lowest listing volume.
</p>

The graph shows that listings are highly concentrated among a relatively small group of players.

- The **top 10% of players account for about 59.8% of all listings**
- Around **24% of players account for about 80% of all listings**
- More than half of the players have **5 listings or fewer**

This means that the eBay sample is dominated by a smaller group of highly represented players, while many other players have limited market coverage.

> [!IMPORTANT]
> **Key Finding:** A large number of listings does not mean a player has stronger demand. It means there is **more market information available** for that player.

#### Which Players Appear Most Often?

<p align="center">
  <img src="figure/figure_03.png"
       alt="Players with the Highest Listing Volume"
       width="900">
</p>

<p align="center">
  <b>Figure 3.</b> Players with the highest number of observed listings in the eBay sample.
</p>

**Erling Haaland** has the largest listing volume with **489 listings**, or about **6.8% of the full dataset**.

He is followed by:

- **Julián Álvarez — 254 listings**
- **Lewis Miley — 253 listings**
- **Alejandro Garnacho — 245 listings**

The large differences between players show that some player markets have much more available data than others.

> [!IMPORTANT]
> **Key Finding:** Be more careful when comparing players with very different listing counts. A price based on many listings gives a stronger picture of the observed market than a price based on only a few cards.

### Brand and Product Line Market Overview

The next step is to understand how the market is divided between **Topps and Panini**, and which product lines appear most often.

<p align="center">
  <img src="figure/figure_04.png"
       alt="Listing Volume by Product Line"
       width="900">
</p>

<p align="center">
  <b>Figure 4.</b> Top product lines by observed listing volume for Topps and Panini. Both charts use the same scale to make the brands easier to compare.
</p>


Among the top 10 product lines shown in Figure 4:

Panini therefore represents about **56%** of the listings shown, compared with about **44% for Topps**.
This suggests that **Panini has a larger listing presence** in the observed sample.

For **Topps**, the market is mainly concentrated in:

- **Chrome — 1,139 listings**
- **Finest — 547 listings**
- **Merlin — 439 listings**

Chrome is clearly the most common Topps product line in the sample.

For **Panini**, the main product lines are:

- **Prizm — 1,807 listings**
- **Select — 611 listings**
- **Obsidian — 393 listings**

Prizm dominates Panini's listing volume and is also the most frequently observed product line across both brands.

> [!IMPORTANT]
> **Key Finding:** Panini has more listings overall in the product lines shown, while **Prizm and Chrome are the main entry points** for understanding each brand's market.

## What Affects Soccer Card Asking Prices?

After understanding the overall eBay market, the next step is to explore **why some cards are priced higher than others**.

A card's asking price can be influenced by many factors beyond the player alone. This section looks at several important card characteristics:

- **Autograph & Patch** — Do special card features lead to higher asking prices?
- **Grading** — Are professionally graded cards priced higher than ungraded cards?
- **Rookie Status** — Does being a rookie card increase the asking price?
- **Product Tier** — How do card prices differ across Core, Mid, and Luxury products?

The goal is to understand **which card characteristics are associated with higher asking prices** and which factors may not matter as much as newcomers might expect.

> **For Newcomers:** A card is not expensive because of only one feature. The best comparison is usually with cards that have a similar **player, product line, grading status, rarity, and card type**.

### Card Features Affect Asking Price

#### **Do special card features make cards more expensive?**

This analysis compares four card types:

- No Autograph / Patch
- Autograph Only
- Patch Only
- Autograph + Patch

<p align="center">
  <img src="figure/figure_05.png"
       alt="Average Asking Price by Card Type"
       width="900">
</p>

<p align="center">
  <b>Figure 5.</b> Average asking price by card type. The labels also show the number of observed listings in each group.
</p>

The graph shows that cards with both an **autograph and patch** have the highest average asking price at about **$271**, followed by **autograph-only cards at $236**.

Standard cards without an autograph or patch average about **$175**, while **patch-only cards average $146**.

However, average prices can be affected by a small number of very expensive listings. The median prices are much closer:

| Card Type | Listings | Average Price | Median Price |
|---|---:|---:|---:|
| No Autograph / Patch | 5,784 | $174.75 | $44.99 |
| Autograph Only | 1,125 | $235.87 | $48.00 |
| Patch Only | 90 | $145.88 | $44.00 |
| Autograph + Patch | 249 | $271.11 | $64.99 |

The statistical results support an important point.

The difference in **average prices** is not statistically significant using Welch's ANOVA (`p = 0.106`), partly because prices vary widely and include extreme values.

However, the overall **price distributions are significantly different** using the Kruskal–Wallis test (`p < 0.001`).

The strongest difference appears in **Autograph + Patch cards**, which are significantly different from the other card groups in the pairwise comparisons.

> [!IMPORTANT]
> **Key Finding:** Cards with both an **autograph and patch** show the strongest price premium in this dataset. However, **special features do not always mean a higher price**. For example, **Patch Only** cards have a median price of about **$44**, which is very close to standard cards without an autograph or patch.

#### **Does Brand Matter for the Same Card Type?**

After looking at autograph and patch features, the next question is:

> **For the same card type, do Panini and Topps have different asking prices?**

<p align="center">
  <img src="figure/figure_06.png"
       alt="Average Asking Price by Card Type: Panini vs Topps"
       width="900">
</p>

<p align="center">
  <b>Figure 6.</b> Average asking prices for Panini and Topps across four card types: standard cards, autograph cards, patch cards, and autograph + patch cards.
</p>

The graph shows that the difference between **Panini and Topps depends on the card type**.

The largest gap appears in cards with **no autograph or patch**. Panini averages about **$263**, compared with only **$72 for Topps**. This is also the only category where the difference in average price is statistically significant (`p < 0.001`).

For cards with special features, the two brands are much closer:

- **Autograph Only:** Panini $237 vs. Topps $235
- **Patch Only:** Panini $168 vs. Topps $128
- **Autograph + Patch:** Panini $279 vs. Topps $249

The average-price differences in these three groups are **not statistically significant**.

This suggests that once a card includes features such as an **autograph or patch**, the feature itself may become more important to asking price than the brand alone.

Because card prices are highly skewed, these averages should still be read together with median prices and comparable listings.

> [!IMPORTANT]
> **Key Finding:** Brand does not affect every card type in the same way. The strongest Panini–Topps price gap appears among cards with **no autograph or patch**, while autograph and patch cards have much closer average prices. For newcomers, this means **do not assume one brand is always more expensive — compare the same card type across brands before buying**.

### Grading Affect Asking Price

Before comparing prices, it is useful to understand what **card grading** means.

Professional grading is when a card is sent to a third-party grading company to evaluate its **condition and authenticity**. The card is usually given a numerical grade and sealed in a protective holder.

For collectors, grading can make a card easier to compare because the condition has been reviewed by an independent company. Higher grades, especially for cards in strong condition, may also receive higher asking prices.

However, a graded card is not automatically more valuable. Price can still depend on the **player, card rarity, product line, grade score, grading company, and collector demand**.

To better understand the effect of grading, this analysis compares graded and ungraded cards only within the **same player and same box set**.

<p align="center">
  <img src="figure/figure_07.png"
       alt="Average Asking Price: Graded vs Ungraded"
       width="900">
</p>

<p align="center">
  <b>Figure 7.</b> Average asking price of graded and ungraded cards within 411 matched Player × Box Set groups.
</p>

The graph shows a clear difference between graded and ungraded cards.

- **Ungraded cards:** average asking price of **$121.30**
- **Graded cards:** average asking price of **$423.02**

On average, graded cards are priced about **249% higher** than ungraded cards within the same player and box set groups.

The difference is also statistically significant using a paired t-test:

**t = 4.54, p < 0.001**

This means the observed price difference is unlikely to be explained by random variation alone in this matched sample.

However, grading itself is not the only possible reason for the higher price. Graded cards may also differ in **card quality, rarity, grade score, or collector interest**.

> [!IMPORTANT]
> **Key Finding:** Graded cards have a much higher average asking price than ungraded cards in the matched sample. For newcomers, grading can be an important price factor, but always check the **grade, grading company, card rarity, and comparable listings** before assuming that every graded card is worth more.check the **grade, grading company, card rarity, and comparable listings** before assuming that every graded card is worth more.

### Rookie Status Affect Asking Price

A **rookie card** is a card connected to a player's early professional career or first major card releases. Rookie cards often receive special attention from collectors because they represent an early stage of a player's career.

However, a card labeled as a rookie is **not automatically more expensive**. Price can also depend on the player, product line, rarity, autograph, grading, and overall collector interest.

To make the comparison fairer, rookie and non-rookie cards were compared only within the **same player and same box set**.

<p align="center">
  <img src="figure/figure_08.png"
       alt="Average Asking Price: Rookie vs Non-Rookie"
       width="900">
</p>

<p align="center">
  <b>Figure 8.</b> Average asking price of rookie and non-rookie cards within 154 matched Player × Box Set groups.
</p>

Interestingly, the graph shows that **non-rookie cards have a higher average asking price** in this sample:

- **Non-Rookie:** $262.19
- **Rookie:** $170.48

However, the difference is **not statistically significant**.

The paired t-test gives:

**t = -0.89, p = 0.374**

A Wilcoxon signed-rank test gives a similar result:

**p = 0.195**

Since both p-values are above **0.05**, there is not enough evidence to conclude that rookie and non-rookie cards have different asking prices after matching the same player and box set.

> [!IMPORTANT]
> **Key Finding:** A **rookie label does not automatically mean a higher asking price**. In this matched sample, rookie cards are actually priced lower on average, but the difference is not statistically significant. For newcomers, rookie status should be considered together with **rarity, product line, autograph, grading, and comparable listings** rather than used as a price signal by itself.

### How Product Tier Relates to Card Asking Price

Before comparing individual card prices, it is useful to understand the **price of the box they come from**.

A higher-priced box usually represents a more premium product, but this does **not** mean every card inside the box will be expensive.

The box price is the **cost of entering the product**, while the card asking price shows how individual cards from that product are priced on eBay.

| Tier | Panini | Approx. Box Price | Topps | Approx. Box Price |
|---|---|---:|---|---:|
| **Core** | Prizm | ~$270 | Chrome | ~$228 |
| **Mid** | Select | ~$300–320 | Merlin | ~$261 |
| **Luxury** | Immaculate | Higher-end | Dynasty | ~$1,782 |

> **Important:** Box prices and individual card asking prices should not be compared as a direct return on investment. A box contains multiple cards, while eBay listings often represent selected cards with different players, rarity, grading, autographs, and serial numbers.

---

### Average Asking Price by Product Tier

<p align="center">
  <img src="figure/figure_09.png"
       alt="Average Asking Price by Product Tier"
       width="900">
</p>

<p align="center">
  <b>Figure 9.</b> Average asking price of individual cards from comparable Panini and Topps product tiers.
</p>

### Core: Prizm vs Chrome

At the Core tier, the box prices are relatively close:

- **Prizm:** about $270 per box
- **Chrome:** about $228 per box

The individual cards show a similar direction:

- **Prizm average:** $186
- **Chrome average:** $140

Prizm cards have a higher average asking price, but the difference in the means is **not statistically significant** (`p = 0.413`).

The median prices are:

- **Prizm:** $56.03
- **Chrome:** $29.58

This suggests that a typical Prizm listing is also priced higher, even though large price variation makes the difference in average prices statistically unclear.

---

### Mid: Select vs Merlin

The box prices are again relatively close:

- **Select:** about $300–320
- **Merlin:** about $261

However, the individual card market looks very different.

- **Select average:** $523
- **Merlin average:** $121

Select has an average asking price more than **4 times higher** than Merlin.

This is the strongest comparison in the analysis, and the difference in average prices is **statistically significant** (`p = 0.0005`).

However, the medians are much lower:

- **Select:** $90
- **Merlin:** $29.99

This shows that a small number of very expensive Select cards push the average much higher.

> The average tells us about the overall price level, while the median gives a better picture of a typical listing.

---

### Luxury: Immaculate vs Dynasty

The Luxury tier looks very different.

- **Immaculate average:** $259
- **Dynasty average:** $1,875

Dynasty appears dramatically more expensive, which is also consistent with its much higher box price.

However, there are only **2 Dynasty listings** in the dataset, compared with **214 Immaculate listings**.

Because of this very small sample, the Dynasty average should **not be treated as representative of the full market**.

---

> [!IMPORTANT]
> **Key Finding:** A more expensive box does not automatically mean every card from that product will have a higher asking price. The relationship depends heavily on the cards that appear in the market. In this dataset, the clearest difference appears in the **Mid tier**, where Select has a much higher average asking price than Merlin. For newcomers, use **box price to understand the product tier**, then compare **median prices, average prices, and similar individual cards** before buying.

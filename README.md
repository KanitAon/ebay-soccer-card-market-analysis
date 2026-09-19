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


# Visualizing APR with Grafana + InfluxDB: Comparing Binance and OKX Simple Earn Programs

## Introduction

Special thanks to [@taresky](https://twitter.com/taresky) for the insightful article "[360% APR? Beginner-Friendly Guide to Crypto Arbitrage](https://taresky.com/crypto-arbitrage)," which offers a balanced and accessible introduction to understanding risks, logic, and profit sources in crypto investments.

This article dives deeper into comparing **OKX** and **Binance**’s USDT/USDC simple earn programs, focusing on their average APR (Annual Percentage Rate) performance.

---

🚀 **Unlock Your Crypto Journey with OKX!**  
Trade with zero fees, access cutting-edge Web3 features, and join millions of global traders. New users get an exclusive welcome bonus of up to **100 USDT**!  

👉 Click to view ☞ [OKX Welcome Limited-Time Offer, Claim Up to 100 USDT Reward](https://bit.ly/OKXe)

---

## Legal Notice

This article provides a technical comparison of average APRs offered by **OKX** and **Binance** for their USDT/USDC simple earn programs. It does **not** constitute financial advice.

### Key Disclaimer from Regulatory Notice:
> Virtual currencies such as Bitcoin, Ethereum, and Tether do not have the same legal status as fiat currencies. Their transactions carry inherent legal risks, and any associated losses are the responsibility of the participants. Activities that harm financial stability or security may face investigation by relevant authorities.

## Comparing Binance and OKX Simple Earn Programs

Both **Binance** and **OKX** offer unique features for their simple earn programs, but they differ in several key aspects:

### Binance
- Binance uses a **"Dark Pool Matching"** model.
- Interest is calculated and settled **every minute**.
- The APR adjusts dynamically, typically on a minute-by-minute basis.

### OKX
- OKX operates using a **"Dark Pool Auction"** model.
- Interest is settled **hourly** and fluctuates with auction results.
- However, OKX charges a **15% platform fee** on earnings, meaning a displayed APR of 39% equates to an effective APR of **33.15%**.  

### Key Observations:
- OKX includes platform rewards that may increase the displayed APR for smaller amounts (e.g., the first 1,000 USDT might yield 10%, while the remaining balance might drop to 2%).
- Both platforms display APRs in their respective apps:

![APR Comparison Between Binance and OKX](https://1e674d5.webp.li/pics/crypto-simple-earn/compare.png)

## Data Collection and Visualization

To effectively compare these products and calculate average APRs, we need reliable historical data. Unfortunately, app-displayed data from both Binance and OKX is insufficient for long-term analysis. To address this, I utilized **InfluxDB** to store historical APR data and **Grafana** to visualize it.

### Collecting APR Data:
- A Python script was created to scrape APR data from the official websites of Binance and OKX, running at regular intervals using `crontab`.
- Data is stored in an **InfluxDB** database for easy querying and visualization.

### Results:
After collecting one month of data, I visualized the APR trends in Grafana. The comparison also includes BTC and ETH price movements to help explain APR fluctuations.

## APR Trends vs. Crypto Price Movements

The relationship between APR fluctuations and price movements of BTC/ETH is significant:

![BTC/ETH Price vs. Binance APR](https://1e674d5.webp.li/pics/crypto-simple-earn/price-apr.png)

#### Observations:
- APR increases sharply during periods of rapid price surges and decreases during price drops.
- This correlation occurs because earn programs fund interest through lending, where borrowers use crypto as collateral.

## Comparing Binance and OKX APRs

To highlight differences in APR trends, I plotted both Binance and OKX USDT/USDC APRs on a single chart:

![Merged APR Comparison Between Binance and OKX](https://1e674d5.webp.li/pics/crypto-simple-earn/binance-okx-merge.png)

### Observations:
- OKX’s APR fluctuates significantly compared to Binance’s stable curve.
- While Binance maintains consistent APRs, OKX exhibits rapid changes due to its auction model.

## Calculating Realistic Average APRs

To determine which platform offers better returns, I calculated daily average APRs using InfluxDB’s query language.

#### Adjusted Query for OKX APRs:
```sql
SELECT mean("apr") * 0.85 FROM "autogen"."simpleEarn" WHERE ("asset"::tag = 'USDT_OKX') AND $timeFilter GROUP BY time(24h) fill(null)
```

This accounts for OKX’s **15% platform fee deduction**. The resulting visualization reveals:

![Daily Average APRs of Binance and OKX](https://1e674d5.webp.li/pics/crypto-simple-earn/binance-okx-merge-daily.png)

### Key Takeaways:
- Between **March 20-22, 2024**, Binance and OKX delivered similar daily average APRs (~9%).
- Post **March 23, 2024**, OKX consistently outperformed Binance in daily average APR.

## Hidden Factors Affecting OKX APRs

While OKX’s advertised APR appears higher, there are caveats:
1. **Tiered Rewards:** The first 1,000 USDT might earn 10%, while the remainder earns just 2%. This tiering isn’t immediately obvious to users.
2. **Platform Fees:** OKX’s 15% fee must be factored in to compute actual returns.

### Suggested Automation:
For advanced users, integrating OKX’s API (e.g., `/api/v5/finance/savings/balance`) can fetch actual lent-out balances and their respective rates. Automation scripts can help maximize returns by managing balances dynamically.

---

## Conclusion

This analysis reveals nuanced differences between Binance and OKX earn programs. While OKX offers higher potential returns, its complex structure and APR variability require closer monitoring. In contrast, Binance provides stable yet lower returns.

For those seeking higher rewards and willing to manage APR fluctuations, **OKX** is the better choice. For hands-off investors prioritizing stability, **Binance** is more suitable.

---

🚀 **Maximize Your Crypto Earnings with OKX!**  
Join millions of users leveraging the world’s leading crypto platform for higher returns. Earn up to **100 USDT** as a welcome bonus!  

👉 Click to view ☞ [OKX Welcome Limited-Time Offer, Claim Up to 100 USDT Reward](https://bit.ly/OKXe)

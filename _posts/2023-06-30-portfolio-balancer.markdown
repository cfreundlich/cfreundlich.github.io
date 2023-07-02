---
layout: post
title: "Introducing Portfolio Balancer"
date:  2023-06-29 12:36:57 -0800
toc: true
---

Today, common investors have access to a complete set of investing tools. In this blog post, I will promote a fundamentals-based approach to using these existing tools, and I will introduce a new tool that will help individual investors execute it.

## Introduction

There's no longer a need for human stock brokers or "wealth managers" that siphon 1% of one's savings every year. The only conceivable reason to retain one of these people is if the investor is completely clueless about how to buy and sell assets using an online tool like ETRADE, which does describe a large swath of the population.

For many investors, simply picking a Vangaurd target retirement date fund, parking all their savings in that, and not thinking about it until they approach that date is a fine strategy. I personally do not think these funds offer as broad exposure to various sectors and market caps as I would like. I also think investing in one and only one fund limits one's ability to exploit market fluctuations by buying low and selling high.

Most investors instead try to pick stocks. This is unsurprising because the marketing departments of banks and brokerages exist in order to push investors toward a frenzy of stock picking. They game-ify investing because higher volumes means higher commissions and profits for them. I am by no means claiming there is something inherently wrong with this, essentially gambling, whether one does it with slot machines, stocks, or crypto, as long as it is done with disposable income. I am claiming that such fun approaches to investing are not sound strategies. Professional humans [consistently lose to monkeys](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwitprKq--7_AhUEiO4BHU_fAVUQFnoECA4QAQ&url=https%3A%2F%2Fwww.wsj.com%2Farticles%2FSB991681622136214659&usg=AOvVaw1h5PZgbOQdKpsBhkcSi7hF&opi=89978449) in this game.

With target date funds not providing enough diversity or flexibility for me, and stock-picking not a viable strategy for my family's savings, I propose hand-crafting a diverse portfolio of low-cost ETFs. I will describe how to do this, offer a sample that you may adopt, and explain why the software I am providing makes this easier, after a few brief remarks:

#### Remark: Margin Accounts
Margin trading benefits from a tax code that is rigged in favor of the rich: Interest paid on margin debt is tax-deductible in Schedule A of the Form 1040 as interest paid on taxable assets. This acts like a discount on the interest equal to one's Federal tax bracket; the more the individual earns, the larger the tax break. But that doesn't mean middle class people would not or should not benefit from exploiting this tax loophole.

Please note that the product described in this post works for unleveraged brokerage accounts as well. Users are also free to maintain the moral high ground and leverage your assets with margin accounts and not deduct the interest, if they feel uncomfortable.

In the context of this post, leveraging what you have and plowing the margins into these low-risk strategies is a multiplier for long-term returns. That is the only benefit.  The cost is the risk of a margin call. I recommend starting very slow with margin trading, borrowing no more than 20% of your assets. This will provide a large enough cushion to avoid a margin call in even an apocalyptic scenario, but talk to a fiduciary certified financial advisor (which I am not) if you have questions.

For me, I am by no means ultra-wealthy, but I am happy with [IBKR's low cost margin trading accounts](https://www.interactivebrokers.com/en/index.php?f=44427&gclid=EAIaIQobChMIicWVrfru_wIVJQ2tBh2P6gkyEAAYASAAEgI6FPD_BwE).
IBKR offers the cheapest margin rates I could find (IBKR does not pay me anything to promote their products).

#### Remark: Trying to Time the Market
Trying to time the market does not work (though I have succumbed to the urge many times). Similar to stock picking, whatever idea you had, an insider already had it. It is priced into the market. Having said that, it is up to you how often to balance your portfolio, but I typically do it once per quarter or less. I also recommend not looking at your portfolio until you go to rebalance it to avoid making emotional decisions.

#### Remark: Retirement Accounts
Clearly, I don't believe that timing the market or stocking picking are reliable strategies, so I don't offer any advice for short term investing. The strategies I am promoting here are long-term (more than 10 years). As such, investors generally should take advantage of tax-advantaged retirement accounts first before adopting the strategies promoted in this post. If you are not familiar with accounts like an IRA, 401(k), HSA, or 529s, [educate yourself](https://www.nerdwallet.com/article/investing/retirement-investments-beginners-guide), then come back to this post.

## Strategies
[Portfolio Balancer](https://github.com/cfreundlich/portfolio-balancer/)'s currently supported strategies are predicated on the assumption that the investor wants equal distribution of value across all assets in their portfolio.

### Setting a target
Investors can pick whatever collection of assets they want, but the general idea is that they span a broad array of sectors, equity types, and market capitalizations using low cost ETFs. Diversity is a simple way to minimize risk of any individual crisis. It avoids over-exposure on any area of the economy without stock picking.

One additional consideration is to pick ETFs that represent sections of the economy far away from the area where the investor herself is employed, further de-risking a crisis.

For example, one may want to target 10% allocation to each of these ten ETFs:
  1. FTEC - Fidelity MSCI Information Technology Index ETF
  1. VAW - Vanguard Materials Index Fund ETF
  1. VCR - Vanguard Consumer Discretionary ETF
  1. VDC - Vanguard Consumer Staples ETF
  1. VHT - Vanguard Health Care ETF
  1. VIS - Vanguard Industrials ETF
  1. VNQ - Vanguard Industrials ETF
  1. VOX - Vanguard Communication Services ETF
  1. VPU - Vanguard Utilities ETF
  1. VSMAX - Vanguard Small-Cap Index Fund Admiral Shares

The list above is by no means complete (notably, it lacks exposure to emerging markets or any fixed income), but if you inspect the distribution of assets in a target date retirement fund, you will notice less diversity in equity markets than the list of ten that I proposed above.  
 
### Rebalancing Toward the Target
The software assumes the user has very recently downloaded their current portfolio positions as a CSV file. Then, the user has two options for how they want to software to suggest trades that would rebalance their portfolio toward a target of equal distribution of assets: 'Hard Rebalance' and 'Try to Never Sell.'

### Hard Rebalance
The 'Hard Rebalance' strategy suggests buying assets that have depreciated (or not appreciated as fast as other assets) and selling assets that have appreciated more than others, bringing your portfolio to a perfectly equal value distribution across assets, despite potential tax liabilities if there were unrealized gains.  The value of each asset afte rebalancing will be equal to the total value of the portfolio before rebalancing, plus the additional investment if any, divided by the total number of assets in the portfolio.

### Try to Never Sell
The 'Try to Never Sell' strategy will only buy assets that have depreciated (or not appreciated as fast as other assets), approaching the target distribution without realizing gains tax. It may not lead to a completely equalized portfolio distribution, but it avoids potential tax implications of the hard rebalance. 

One way to think of this strategy is that it raises the floor of your portfolio, buying low incrementally.  The implementation in the code uses a MinHeap to execute the flood fill. 

#### Remark: Convex Optimization
The flood fill algorithm used by this strategy solves a convex optimization problem.

We want to change the value of each by executing trades.  Let *x<sub>i</sub>* denote the amount we change the *i-th* asset, and *n* denote the number of assets in the portfolio. Let *c* denote the amount cash the investor wants to add (or subtract if withdraw). Then *x<sub>1</sub> + ... + x<sub>n</sub>=c* constrains our choice not to over- or under-spend. Let *v* denote the total initial value of the portfolio and *p<sub>i</sub>* the initial value of the *i-th* asset, so that *p<sub>1</sub> + ... + p<sub>n</sub>=v*. Then, we desire that

*x<sub>i</sub> = (v+c)/n - p<sub>i</sub>*.

This is exactly what is done in 'Hard Rebalance' strategy. However, constraining the strategy to only execute buy transactions, as in the 'Try to Never Sell' strategy, means that all *x<sub>i</sub>* must be nonnegative. One can easily verify that if *(v+c)/n < p<sub>i</sub>*, the target cannot be met.

We can try to approximately solve the system by casting the problem as convex optimization:

*min<sub>x>0</sub> |x-b|*

s.t. *x<sub>1</sub> + ... + x<sub>n</sub>=c*,

Where the vector *b* has $i$-th entry equal to *(v+c)/n - p<sub>i</sub>* and *|.|* is any norm.

### Providing flexibility by factoring in Deposits and Withdrawals
A key feature of both strategies supported by the Portfolio Balancer is that they offer users the flexibility to specify an amount of cash they wish to invest or withdraw, allowing the software to reallocate funds accordingly. 

An interesting behavior of the 'Try to Never Sell' strategy is that if you give the cash option a negative sign when invoking this strategy, then it will sell your highest value assets first, using capital gains tax exposure as a tie-breaker.

I invite you to dive into [the code](https://github.com/cfreundlich/portfolio-balancer/tree/main/src/pbal) to understand exactly how these strategies make their suggestions.

## Learning from the Development Process
Throughout the process of building this project, I discovered the use of `project.toml` for easy binary creation, finding it more efficient than the traditional `setup.py`. 

However, not all aspects of the development process were smooth sailing. The interaction with Interactive Brokers' (IBKR) Client Portal API proved challenging. While the IBKR web application functioned well for downloading CSV files, their Client Portal, a local app for facilitating API calls, proved to be less user-friendly. It's authentication system and redirects posed significant challenges, proving to be problematic with tools like cURL, Python's request package, or even when trying to log in through a local host browser.

## A Tool for the Individual Investor
The creation of Portfolio Balancer is not just the birth of an open-source project but an attempt to democratize investing, making the art of investment accessible to everyone, from the novice to the experienced trader. It signals a shift towards a more stable and calculated investing strategy, making wealth creation not just a privilege of the rich, but a right of every individual.

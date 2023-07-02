---
layout: post
title: "Democratizing Investing: Introducing Portfolio Balancer"
date:  2023-06-29 12:36:57 -0800
toc: true
---

# Democratizing Investing: Introducing Portfolio Balancer

For the most part, the the tools once reserved exclusively for the ultra-wealthy are today accessible to common investors. There's no longer a need for human stock brokers or "wealth managers" that siphon 1% of one's savings every year. In this blog post, I will promote a cold, calculated approach to investing and provide a command line interface (CLI) that will tell individual investors exactly how to execute it.

## A Remark on Margin Accounts
Margin trading is particularly rigged in favor of the rich: Interest paid on such margin accounts is tax-deductible in Schedule A of the Form 1040, which acts like a discount on the interest equal to one's Federal tax bracket; the more the individual earns, the larger the tax break. Obviously, there is a big part of me that would like to point out that this is a tax loophole created by the rich for the rich, but rather than take a moral highground here, I will simply shine a spotlight on it. Sunlight is often the best sanitizer.

If you're not comfortable with this kind of morality, note that the product described in this post works well for traditional brokerage accounts; leveraging what you have and plowing the margins into these strategies is just a boost. I recommend starting very slow with margin trading, if you are curious about its benefits. You are also free to claim deductions however you want! I recommend talking to a tax advisor.

For me, I am by no means ultra-wealthy, but I am happy with [IBKR's low cost margin trading accounts](https://www.interactivebrokers.com/en/index.php?f=44427&gclid=EAIaIQobChMIicWVrfru_wIVJQ2tBh2P6gkyEAAYASAAEgI6FPD_BwE).
IBKR offers the cheapest margin rates I could find.

## Introducing the Portfolio Balancer

I've been a proponent of boring, low cost ETF-driven investing since I started investing when I was in my 20s. For many investors, simply picking a Vangaurd target retirement date fund, parking all their savings in that, and not thinking about it until they approach that date is a fine strategy. I personally do not think target date funds offer as broad exposure to various sectors and market caps as I would like, increasing short term risk. Additionally, investing in one and only one fund limits one's ability to leverage market fluctuations by "buying low and selling high."

On the other hand, marketing departments of most banks and brokerages push investors toward a frenzy of stock picking and gamification because higher volumes means higher commissions and profits for them. I am not claiming there is anything inherently wrong with gambling, whether one does it with slot machines, stocks, or crypto as long as it is done with disposable income. I am claiming that such "fun" to investing are not sound strategies, with professional humans [consistently losing to monkeys](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwitprKq--7_AhUEiO4BHU_fAVUQFnoECA4QAQ&url=https%3A%2F%2Fwww.wsj.com%2Farticles%2FSB991681622136214659&usg=AOvVaw1h5PZgbOQdKpsBhkcSi7hF&opi=89978449).

With target date funds not providing enough diversity or flexibility for me, and stock-picking not a viable strategy for my family's savings, I give you [Portfolio Balancer](https://github.com/cfreundlich/portfolio-balancer/).


### A Remark on Trying to Time the Market
Trying to time the market, or catch the falling knife, does not work (though I have succumbed to the urge many times). Similar to stock picking, whatever idea you had, an insider already had it. It is priced into the market. Having said that, it is up to you how often to balance your portfolio, but I typically do it once per quarter, or randomly. I also recommend not looking at your portfolio until you go to rebalance it to avoid making emotional decisions.


## Portfolio Balancer's Strategy

Portfolio Balancer's currently supported strategies are predicated on the assumption that the investor wants equal distribution of value across all assets in their portfolio.

### Setting a target
Users can pick whatever collection of assets they want, but the general idea is that they span a broad array of sectors and market capitalizations using low cost ETFs, for example, one may want to target 10% allocation to each of these ten ETFs:
  1. FTEC
  1. VAW
  1. VCR
  1. VDC
  1. VHT
  1. VIS
  1. VNQ
  1. VOX
  1. VPU
  1. VSMAX

Having a broad array of sector and market cap coverage is a simple way to minimize risk of any individual company or sector having a crisis.
It avoids over-exposure on any area of the economy, and likewise avoids stock picking.
 
### Rebalancing Toward the Target

The software assumes the user has very recently downloaded their current portfolio positions as a CSV file. Then, the user has two options for how they want to software to suggest trades that would rebalance their portfolio toward a target of equal distribution of assets: 'Hard Rebalance' and 'Try to Never Sell.'

### Hard Rebalance
The 'Hard Rebalance' strategy suggests buying assets that have depreciated (or not appreciated as fast as other assets) and selling assets that have appreciated more than others, bringing your portfolio to a perfectly equal value distribution across assets, despite potential tax liabilities if there were unrealized gains. 

### Try to Never Sell
On the other hand, the 'Try to Never Sell' strategy will only buy assets that have depreciated (or not appreciated as fast as other assets), approaching the target distribution without realizing gains tax. It may not lead to a completely equalized portfolio distribution, but it avoids potential tax implications of the hard rebalance. One way to think of this strategy is that it raises the floor of your portfolio, buying low incrementally.

### Providing flexibility by factoring in Deposits and Withdrawals
A key feature of both strategies supported by the Portfolio Balancer is that they offer users the flexibility to specify an amount of cash they wish to invest or withdraw, allowing the software to reallocate funds accordingly. 

An interesting behavior of the 'Try to Never Sell' strategy is that if you give the cash option a negative sign when invoking this strategy, then it will sell your highest value assets first, using capital gains tax exposure as a tie-breaker.

I invite you to dive into [the code](https://github.com/cfreundlich/portfolio-balancer/tree/main/src/pbal) to understand exactly how these strategies make their suggestions.

## Learning from the Development Process
Throughout the process of building this project, I discovered the use of `project.toml` for easy binary creation, finding it more efficient than the traditional `setup.py`. 

However, not all aspects of the development process were smooth sailing. The interaction with Interactive Brokers' (IBKR) Client Portal API proved challenging. While the IBKR web application functioned well for downloading CSV files, their Client Portal, a local app for facilitating API calls, proved to be less user-friendly. It's authentication system and redirects posed significant challenges, proving to be problematic with tools like cURL, Python's request package, or even when trying to log in through a local host browser.

## A Tool for the Individual Investor
The creation of Portfolio Balancer is not just the birth of an open-source project but an attempt to democratize investing, making the art of investment accessible to everyone, from the novice to the experienced trader. It signals a shift towards a more stable and calculated investing strategy, making wealth creation not just a privilege of the rich, but a right of every individual.

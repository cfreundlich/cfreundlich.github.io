---
layout: post
title:  "Democratizing Investing: Introducing Portfolio Balancer"
date:   2023-06-29 12:36:57 -0800
toc: true
---

# Democratizing Investing: Introducing Portfolio Balancer

As financial markets evolve and technology accelerates, it's high time that the benefits once enjoyed exclusively by the ultra-wealthy and hedge funds become accessible to every individual investor. Thus was born the open source project - Portfolio Balancer. It's a tool created with a vision to bring financial empowerment to individuals, enabling them to benefit from efficient investment strategies and tax breaks traditionally enjoyed by the elite few.

With my daughter sick, requiring me to isolate with her away from my newborn son, I found the time and motivation to build this tool that goes beyond the usual frenzy of stock picking and gambling-esque investing. Portfolio Balancer instead brings a calculated, data-oriented approach to the forefront of individual investing strategy. 

## Portfolio Balancer's Strategy

Portfolio Balancer uses a simple user-supplied CSV data file to guide portfolio rebalancing, helping users attain optimal returns with two strategic approaches: 'Hard Rebalance' and 'Try to Never Sell'. 

- The 'Hard Rebalance' strategy suggests selling assets that have appreciated to realize capital gains, bringing your portfolio closer to an optimal equal value distribution across assets, despite potential tax liabilities. 

- On the other hand, the 'Try to Never Sell' strategy advocates buying assets that have depreciated, enhancing the overall portfolio value without realizing gains tax. It may not lead to a completely equalized portfolio distribution, but it avoids potential tax implications.

A key feature of Portfolio Balancer is that it offers users the flexibility to specify an amount of cash they wish to invest or withdraw, allowing the software to reallocate funds based on the selected strategy.

## Learning from the Development Process

Throughout the process of building this project, I learnt to master the Python `argparse` package for creating an easy-to-use command line interface. I discovered the use of `project.toml` for easy binary creation, finding it more efficient than the traditional `setup.py`. 

However, not all aspects of the development process were smooth sailing. The interaction with Interactive Brokers' (IBKR) Client Portal API proved challenging. While the IBKR web application functioned well for downloading CSV files, their Client Portal, a local app for facilitating API calls, proved to be less user-friendly. It's authentication system and redirects posed significant challenges, proving to be problematic with tools like CURL, Python's request package, or even when trying to log in through a local host browser.

## A Tool for the Individual Investor

Portfolio Balancer truly shines when used with IBKR's margin trading accounts. Here, individual investors can access low-cost overnight rates, previously a privilege of hedge funds and the richest people. Interestingly, the interest paid on such margin loans is tax-deductible, giving an additional tax benefit to small-scale investors.

The creation of Portfolio Balancer is not just the birth of an open-source project but an attempt to democratize investing, making the art of investment accessible to everyone, from the novice to the experienced trader. It signals a shift towards a more stable and calculated investing strategy, making wealth creation not just a privilege of the rich, but a right of every individual.

# Getting Started
Clone [the github project](https://github.com/cfreundlich/portfolio-balancer/), `cd` to the root directory, and follow the directions in the README.
+++
title = 'Saffron.Finance (SFI) and A Post-Hype Crypto Project'
date = 2024-06-25T20:42:19-04:00
draft = true
summary = "Here I dive into what I found out after reading about the SFI token, which exhibits the same problem that seems to plague the cryptocurrency industry in general."
description = "Here I talk about the SFI token."
toc = false
readTime = true
autonumber = false
math = false
tags = ["crypto", "finance"]
showTags = false
hideBackToTop = false
+++
## Crypto
I remember when I first heard about Bitcoin, when in 2013 the FBI arrested [Ross Ulbririch](https://en.wikipedia.org/wiki/Silk_Road_marketplace) a.k.a *Dread Pirate Roberts* in a library, for running the darknet marketplace *Silk Road*. 

You see, buying drugs online with government backed currency like the US dollar is easily traceable by federal agencies and banks, especially due to the Bank Secrecy Act and AML/ATF regulations. The Silk Road solved that issue by allowing users to buy drugs using Bitcoin, a cryptocurrency. The fact that this currency allowed users to circumvent government sensorship and transact on these darknet markets provided a solid use-case.

This happened a solid 7 years before the huge crypto boom that occured in 2021. Between 2013 and 2021, the price of Bitcoin went from around \$1100 to about \$64,000 USD. Which means that anyone who spend their Bitcoin on drugs in 2013 likely cried themselves to sleep in 2021. But this also highlights a fundamental issue I have with cryptocurrency. The primary reason most people buy cryptocurrency is as an investment. The primary use-case for cryptocurrency is as a *currency*. A deflationary economy incentivises hoarding; why would you want to spend your money on something today if you could buy twice of that same thing tomorrow without lifting a finger?

As a result, crypto has essentially gone from a project to create  decentralized currency to an instrument of greed. Now when you pitch into a fledgling crypto project, chances are you are doing it in the hopes that it will pump to 10%, 30%, 500% of its original value (provided you got in early enough). So what you end up seeing are projects such as influence Wizard of Soho's [TARD coin](https://www.coinscan.com/tokens/eth/0x899124ce2f766ed32e9375045c24db512dd4265c) (haha, get it?) or such technological wonders as [MEME coin](https://coinmarketcap.com/currencies/meme/).

The way a lot of these schemes operate is as follows:
- The founders generate hype before the launch of the currency using discord, telegram, reddit and other forums.
- Early members join these closed forums and are given early access to the tokens
- Given enough hype, when the token gets released, the value of the token skyrockets and new money pours in from the hype generated on reddit etc.
- The founders and early buyers dump their tokens and exit. Some people are left holding the bag.
- Hype dies down and the project is forgotten

And throughout this whole experience, there is nothing of value generated, no use-case, no promises fullfilled; only that money has changed hands from some people to other people. 

## Saffron

Recently I became aware of a cryptocurrency called Saffron.Finance (SFI) running on the Ethereum chain that its website claims is a "...peer to peer risk adjustment protocol. Users customize their risk and return profiles by selecting their own degree of exposure to underlying platforms."

The project seems to be run by a person who goes by the psudonym 'Dingo' and from initial appearances seems like a sophisticated cryptocurrency project with hefty ambitions. The website contains a [governance forum](https://gov.saffron.finance/), [a github page showing the source code](https://github.com/saffron-finance/saffron) and what seems to be great documentation on its goals and intents. There is even a "Saffron Academy Podcast" where host Dingo interviews prominent cryptocurrency figures.

The first [commit](https://github.com/saffron-finance/saffron/commit/01daed0c4a8d589cc6f28c2a023bde5dd30d7b4c) to the Saffron github was on October 9, 2020, deep into the pandemic era, when many people had stimulus checks hitting their bank accounts and were bored at home. This was when a huge crypto boom was occuring, and NFTs were all the hype (which are curiously nowhere to be found now). 

The first commit was by the token's founded 'psykeeper', whos last commit to the project was 3 years ago in January 2021. There has been no development on the github repository since this last commit. At the time of writing this, SFI can currently be exchanged for \$21.81 per token, there are currently 92,000 tokens in circulation.

## The Whitepaper
The latest activity I can find for this token without joining their Telegram or Discord channels is an article posted by *Dingo* on Medium titled [Introducing Saffron Lido Vaults](https://medium.com/saffron-finance/introducing-saffron-lido-vaults-b3ac6b529023) and a [whitepaper](https://github.com/saffron-finance/papers/blob/main/SaffronFixedIncomeVault.pdf) released on Github. 'Whitepapers' are used extensively in the crypto industry as promotional memos to present their product to potential investors. They also serve another purpose of giving the project some modicum of professionalism and legitimacy. 

The Saffron Finance whitepaper on first glance is an impressive piece of work. Written by authors *Rx3A97* and *Psy Keeper*, it clocks in at an impressive 17 pages complete with mathamatical formulas as well as citations. 

The whitepaper describes Saffron Finance's attempt at implementing a *zero-oupon swap* into their crypto ecosystem. According to [Investopedia](https://www.investopedia.com/terms/z/zero-coupon-swap.asp) a ".. zero-coupon swap is a derivative contract entered into by two parties. One party makes floating payments which changes according to the future publication of the interest rate index (e.g. LIBOR, EURIBOR, etc.) upon which the rate is benchmarked. The other party makes payments to the other based on an agreed fixed interest rate".

The whitepaper attempts to explain how Saffron Finance will replicate a zero coupon swap with a smart contract and how this is a profitable strategy. Now I'm not a financial professional so I will not attempt to decipher this strategy or the viability of it. However, there are some other things in the whitepaper that give me pause and are worth highlighting. 

The whitepaper has a *methods* section which is supposed to point the reader to how the authors arrived to their conclusions. However, the authors seemed to not have double checked what they wrote and/or are not expecting any investors to actually read the paper. his is what they have to say about their calculation script: 
> Simulation of Saffron Fixed Income Vaults performance and calculations of study case

> To make all the simulations we build a simplified library that mimics the Saffron Fixed Income Vault operation called Dashi. The library is written in typescript and is available [URL ObservableHQ or NPM?]. These tow sections were coded in ObservableHQ Notebooks and canal so be accessed at https://observablehq.com/collection/@rx3a97/saffron-fixed-income-vault-paper

As you might have guessed, this URL leads to nothing and they forgot to delete the part where they debate whether the code should be hosted on NPM or observableHQ. That is not to say that this library does not exist, merely to point out the attention to detail that went into this whitepaper that seems to be several years in the making. 

One last thing I want to highlight in the whitepaper is the following sentence:
>Although the first implementations of the protocol lack some features described here, they could be prioritized and implemented upon request via governance.

## Governance
The Saffron Finance website contains a [governance](https://gov.saffron.finance/) section where community members can pitch proposals for the direction of the project. Since the beginning of the project in April 2021, there have been a total of 22 posts to this forum, where users have pitched ideas such as [a potential binance listing](https://gov.saffron.finance/t/binance-to-get-listing/96) (a platform that is now banned in ontario and whose founder took a plea deal and got 4 months in prison for money laundering) and granting the SFI foundation 250 SFI per quarter to conduct marketing for the chain. 

The most interesting proposal I found was to grant Dingo 20 SFI per quarter to conduct marketing activites. This proposal generated active discussion in the comments, where one user by the name of *rayraspberry* argues:
>80 SFI at \$\1500/SFI is \$120,000 which is 0.1\% of the entire market cap per cycle. I don’t think anyone is expecting SFI to sit at \$1500 for another year.

He then goes on further to ask how Dingo's contract will be managed, who is responsible for additional expenses, how do they ensure the money is spent wisely. This discussed caused *Dingo* to close the discussion. Months later, in september, a second proposal was pitched now asking for 250 SFI per quarter (the price of SFI/USD had dropped by around 50% from all time highs at this point). This proposal passed by 100% yes and 0% no votes with 24 users participating where the top 2 voters are actually the same person under two different [wallets](https://vote.saffron.finance/#/proposal/QmRDf9LAW1cDhjSM9CoXc8HjQcmsKgYtY8keGioptAJP2F). 

None of these proposals contain anything substantial, they tend to receive very little engagement, and since votes are weighed based on the voters crypto porfolio, the whales tend to decide the end result of the proposal.

## Ghost Town
Like many crypto projects, Saffron Finance is very devoid of any activity. The all time highs for this project occured in 2021, and since then it has been on a constant downward decline. This does not tend to lend well to engagement in the crypto space, where investors are on the hunt for *moonshots* and trying to ride the line up. The [reddit](https://www.reddit.com/r/SaffronFinance/) page for Saffron Finance received its last post 3 years ago where a user asked an apt question: "Why is the reddit page so dead?". The Safrron Finance reddit page is just one of hundreds if not thousands of other dead reddit pages in a graveyard of crypto projects. The marketing lead *Dingo* has his reddit account suspended for some unknown reason and there seems to be no admins for the page. Where did those 250 SFI per quarter for marketing dissapear off to?

I also joined their discord page to see if anything exciting was happening there, but that also seems to be scarcely populated and lacks moderation. The welcome page of the discord features messages from NSFW bots pitching Onlyfans content and scammers trying to steal information from naive users. The latest post in the general page is from a blockchain developer looking for a job, who seems to have posted the same message in multiple channels. 

User @dishy on the discord posted in February 2024:
>@psykeeper , do you have any plans to change your style of running this project? It's clearly not working... apologies if that comes off a little harsh. marketing? changes to tokenomics? anything?

Someone should tell dishy this ship has long sailed.

## Indodax
The entity holding the most amount of SFI at 17% of the total supply is Indodax 3, an Indonesian crypto exchange who also owns more than $300 million worth of other tokens in its portfolio. The website of this exchange shows the [transactions](https://indodax.com/market/SFIIDR) in SFI to Indonesian Rupiah. This leads me to conclude that this currency is quite popular in Indonesia.

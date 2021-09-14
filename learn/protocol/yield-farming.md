---
description: >-
  Here, you will be able to find the most relevant information about yield
  farming.
---

# Yield farming

The decentralized finance \(DeFi\) movement has been at the forefront of innovation in the blockchain space. What makes DeFi applications unique? They are permissionless, meaning that anyone \(or anything, like a smart contract\) with an internet connection and a supported wallet can interact with them. In addition, they typically don’t require trust in any custodians or middlemen. In other words: they are trustless. 

{% hint style="success" %}
**Yield farming** is a new way to earn rewards with cryptocurrency holdings using permissionless liquidity protocols. It allows anyone to earn passive income using a decentralized ecosystem. Yield farming \(also known as liquidity mining\) is a way to generate rewards with cryptocurrency holdings. In simple terms, it means locking up cryptocurrencies and getting rewards.
{% endhint %}

## How it works in DEIP infrastructure

Each F-NFT has **metadata**. One of the metadata attributes is a **category/segment** of an underlying intangible asset. 

> For example, there could be a “technology” category, and the sub-category of “biotech”, “nanotech” or “green tech”.

Every account in the network can stake **DEIP** [**tokens** ](../token.md)on a specific category to increase the amount of funding allocated from the **Ecosystem Fund** to a specific category of F-NFT. The distribution of capital in the Ecosystem Fund is proportional to the amount of **DEIP tokens** staked on each specific category. 

One of the metadata attributes in every F-NFT is a category/segment of an underlying intangible asset and each F-NFT has a metadata attribute that specifies the platform it is issued on. The metadata attributes allow you to stake DEIP tokens on a particular category to increase the number of funding allocated from the Ecosystem Fund to a specific category of F-NFT. This means that you can stake DEIP tokens to change the distribution of capital allocated for each issuance platform and this increases the platform’s chances of receiving investment from the fund.

Since every F-NFT also has a metadata attribute that specifies the platform it is issued on, it’s possible to stake DEIP tokens to change the distribution of capital allocated for each issuance platform. After network participants have staked their tokens, the Ecosystem Fund will have a special allocation to spend on investments in specific issuance platforms. By default, 5% of the profit from the Ecosystem Fund's investment activities is distributed among those who staked in the category which made this profit.

This creates an incentive to stake DEIP tokens in categories/segments of F-NFTs which will generate the most profits. However, the Council investment decisions and the eventual capital distribution differ from the distribution staked by F-NFT segments. It is like a competition in token staking between the Council and yield farmers. The result of this "competition" is to get investments from the fund and tells us who was better at investment decisions — the Council or the Community of yield farmers. 

If the performance of the community is better by {delta} then the next allocation of the DEIP Ecosystem Fund for the community-driven investments will be increased. The initial and minimum percentage of allocated capital for community-driven investment decisions is 20% and the maximum allocation is 80%.

![Yield farming by asset segments](../../.gitbook/assets/assets_wiki_-mzbonxaba-qbxpdued0_-mzbp6b9kaz21e1dvszk_7.jpeg)

The profit from yield farming $$P_{ki}$$ for an account i from all accounts \[1,N\] staked stakes $$ST_i$$ with a total amount $$ST$$ total on a segment $$k$$ is calculated with the formula:

$$
P_{ki} = \frac{ST_{ki}*\underset{d=day(now)-30}\Sigma P_{kd}}{\sum_{j=1}^{j=N}{ST_{kj}}}
$$

### Segment Liquidity Pools and AMM

At some point after the network launch when each segment has a considerable amount of DEIP tokens staked on it, the protocol will be updated to convert DEIP tokens staked on a specific segment of assets into a **Segment Liquidity Pool** \(SLP\). 

Once SLPs are introduced, they will enable additional liquidity for the assets in this segment via automatic market making. An **automated market maker** \(AMM\) is a type of decentralized exchange \(DEX\) protocol that relies on a mathematical formula to price assets. Instead of using an order book like a traditional exchange, assets are priced according to a pricing algorithm.


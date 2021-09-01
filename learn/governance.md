---
description: >-
  Read on to learn about the governance model of the DEIP infrastructure, its
  key stakeholders, and mechanisms.
---

# Governance

Due to their decentralized nature, blockchain protocols typically have no central governing entity. This requires independent individuals to participate in the maintenance, development, and security of the protocol and the network. 

Protocol participants must be motivated to perform these important tasks, and cryptocurrency tokens are used to financially compensate them for their efforts. As such, the design of the token economic model is critical to incentivize individuals to maximize the security, growth, and success of the protocol. In addition, a clear and transparent governance process is also crucial for the success of the blockchain protocol. Lack of central authority means no decisions can be made and implemented unilaterally. Hence, network participants must have a structured approach to collaborating and achieving consensus on which changes need to be made, plus when, how, and by whom.

## Council

**DEIP Council** is the main governance body of DEIP infrastructure.

### How to become a council member?

To become a council member, any account in the network can:

* Participate in an auction  
* Take over a seat from someone 

The initial 12 seats are allocated via the first staking competition. Each seat is granted for 12 months before becoming available for another staking competition. Every 12 months, 3 more seats will be created in the Council and are allocated via a staking competition. The total number of seats in the Council is limited to 30. Therefore, 6 years after the network launch, all 30 seats will be allocated and the protocol will stop creating new ones. 

![Council model, seat competition, and seat contender.](../.gitbook/assets/assets_wiki_-mzbonxaba-qbxpdued0_-mzbp6b81m3qsvazlflt_6.png)

For those who’ve got a seat, their stake is frozen for the next 12 months and unlocks gradually. 

### Council member election: staking auction

Every year there is an election for Council members. An account that wants to become a Council member needs to stake DEIP tokens during the voting period. The top 12 accounts by amount staked receive a seat on the DEIP Council. The staked amount is released over the period the member has a seat.

### Council member election: taking over a seat

At any time, any account can compete for a council seat by staking an amount \($$CST_n$$\) that is X times more \( $$X=>2$$\) than the current stake \($$ST_n$$\) of the current council member. When this amount is staked, it reduces the tenure of the seat incumbents by X times and accelerates the vesting schedule.

The account that competes for the seat is called a **contender**, and the stake \( $$CST_n$$\) this account makes reduces the time the incumbent has by X times and accelerates vesting, where $$X_n=\frac{CSTn}{ST_n}$$ . The example of the Council state and contender model is illustrated in the Image _Council model, seat competition, and seat contender_. 

In the example, council seat number 2 has a contender with a stake two times more than the current seat owner \(council member\). The formula for the time remaining $$t_n$$ for the council member in where it has a contender is:

$$
t_n = t_n^` \frac{ST_n}{CST_n}
$$

Therefore, the final formula of time remaining \($$t_n$$\) for the council member _n_ is:

$$
t_n = \frac {(t_{max}-(now-t_{n,init}))}{max(1_,\frac{CST_n}{ST_n})}
$$

## Ecosystem Fund \(Treasury\)

**DEIP Ecosystem Fund** is a DAO in the network governed by the Council. 

{% hint style="info" %}
The Ecosystem Fund accumulates a part of investment transaction fees to be further invested in F-NFT in DEIP infrastructure. 
{% endhint %}

The initial capital of the DEIP Ecosystem Fund is allocated during the TGE and consists of 25% of all DEIP tokens issued. All funds in the Ecosystem Fund are vested over 10 years with a 3 months' lockup cliff period. 

The DEIP Council can invest the capital of the DEIP Ecosystem Fund in other assets in DEIP Infrastructure. The major investment purpose of the DEIP Ecosystem Fund is F-NFTs issued in the DEIP infrastructure. Each investment decision must be approved by 2 council members to be processed. 

To liquidate a position, 3 Council members must approve the transaction. After the liquidation of a position, 20% of the profit goes to the Council members who performed the initial investment transaction. The rest of the profit goes back to the DEIP Ecosystem Fund for further investment in F-NFTs.


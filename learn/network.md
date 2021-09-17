---
description: Read on to learn about DEIP Network.
---

# Network

DEIP Network is an open-source network of [Portals](portals.md) \(projects, businesses\) that are built using DEIP technologies. Anyone is welcome to create their own portal which should have a specific theme to it. Portals are gateways to DEIP infrastructure and provide all of the necessary underlying features \(e.g. user interface, off-chain data, regulation compliance, KYC/AML\) and services required to interact with the network.

![DEIP Network overview](../.gitbook/assets/group-13.png)

## Validators and consensus

The DEIP Network is secured by the **Hybrid Nominated-Proof-of-Stake Consensus algorithm**. In order to add additional security and integrate with other Polkadot Parachains, the DEIP Network will secure a **Parachain Slot** in the **Polkadot Relay Chain**. 

DEIP Network utilizes a default consensus mechanism for Substrate-based chain: **Hybrid NPoS consensus BABE/GRANDPA**. 

**Validators** in the DEIP Network are rewarded from the **Validator Rewards Pool**. Reward amounts depend on the current circulating supply and are dynamically adjusted in a way that ensures the total annual validator reward is equal to 5% of the current circulating supply, and can’t exceed 20% of the Validators Rewards Pool. 

The Validator Reward Pool can also be replenished from a fraction of transaction fees. The exact percentage of the transaction fee that goes to Validator Reward Pools is set by the Council. By default, this parameter is set to 0%.

## Transactions fees and free transaction model

Every permissionless blockchain needs a mechanism to protect the chain against spam attacks. Within the DEIP Network, there are two ways for protecting the network against spam: 

* **The transaction-fee model**, which is used for the financial transactions in the network 
* **Free-transaction model**, which is used for non-financial transactions

### The transaction-fee model

The transaction-fee model means charging a fee for each financial transaction. By financial transaction, we mean transactions such as token swaps, exchange, investment/licensing/purchase of F-NFT in the network. The fee for each transaction is determined by the DEIP Council and can be changed via voting. The fees from all financial transactions go to the DEIP Ecosystem Fund.

### Free-transaction model

The free-transaction model allow to perform transactions within the network without paying transaction fees. It is used for transactions that don’t involve the transfer/exchange of value or assets. 

For example, if we want to add a hash of an IP asset to the IP-assets bucket on the network or invite a new member to a DAO, this would not require a transaction fee. This reduces barriers to using DEIP Network and makes the user experience seamless.


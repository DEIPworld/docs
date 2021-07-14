# Network

DEIP Network is an application-specific Substrate 3.0 based Polkadot Parachain that implements a number of protocols for the creative economy: the core protocol is Intellectual Capital Protocol. On top of the Intellectual Capital Protocol, the network implements the Collective Intelligence Protocol, the Dynamic Liquidity Protocol, and others.

## Validators and consensus

The DEIP Network is secured by the **Hybrid Nominated-Proof-of-Stake Consensus algorithm**. In order to add additional security and integrate with other Polkadot Parachains, the DEIP Network will secure a **Parachain Slot** in the **Polkadot Relay Chain**. 

DEIP Network utilizes default consensus mechanism for Substrate-based Parachain - **Hybrid NPoS consensus BABE/GRANDPA**. 

**Validators** in the DEIP Network are rewarded from the **Validator Rewards Pool**. Reward amount depends on the current circulating supply and dynamically adjusted in a way to ensure that total validators reward per year is equal to 5% of the current circulating supply, but it can’t exceed 20% of the Validators Rewards Pool. The Validators Reward Pool can also be replenished from a fraction of transaction fees. The exact percentage of the transaction fee that goes to Validators Reward Pools is set by the Council. By default, this parameter is set to 0%.

## Transactions fees and free transaction model

Every permissionless blockchain needs a mechanism to protect the chain against spam attacks. Within the DEIP Network, there are two ways for protecting the network against spam: 

* **The transaction fee model**, which is used for the financial transactions in the network, and 
* **Free Transaction model**, which is used for non-financial transactions.

### The transaction fee model

The transaction fee model is **self-explanatory** and means charging a fee for each financial transaction. By financial transaction, we mean transactions such as token swaps, exchange, investment/licensing/purchase of F-NFT in the network. The fee for each transaction is determined by the DEIP Council and can be changed via voting. The fee from all financial transactions goes to the DEIP Ecosystem Fund.

### Free Transaction model

The free transaction model allows performing transactions within the network without paying transaction fees. It is used for transactions that don’t involve the transfer/exchange of money or assets. 

For example, if we want to add a hash of an IP asset to the IP-assets bucket on the network or invite a new member to a DAO it would not require paying a transaction fee. This reduces barriers to using the DEIP Network and makes the user experience seamless.


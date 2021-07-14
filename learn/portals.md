# Portals

## What is it?

**Portals** are gateways to the DEIP Infrastructure and provide all necessary basement \(e.g. user interface, off-chain data, regulation compliance, KYC/AML\) and services required to interact with the network.

Usually, a portal focuses on a specific **intangible asset class**, such as invention/patents, movies script, tokenized talent, etc. This allows each portal to better address the needs of a specific customer segment, tune portal UI and functionality to these needs, and even provide some additional functionality beyond the protocol. 

Portal owner is represented in the network as DAO and its role in the protocol is called Bramnik \(“gatekeeper” from Belarusian\).

## Security deposit

Each portal must fulfill specific requirements to ensure that the assets approved to be registered by a portal have a high value and are authenticated. For this purpose, the incentive model of the protocol introduces a **security deposit** concept, which is designed to incentivize portals to register only high-value assets. 

Portals make security deposits by staking the DEIP Token as a guarantee of the quality of assets it brings to the network. Each asset needs to satisfy minimal requirements according to the rules set by the Council. Portals can charge a **portal fee** for the asset registration in the network, it can be a one-time fee or/an additional “curation fee” to a tokenized intangible asset and earn a fee from all the future transactions from this asset.

## Portals Profitability Index \(PPI\)

For each portal, the protocol calculates a **Portal Profitability Index \(PPI\)**, which is based on the **average CAGR** of all the assets registered through the portal, **average APY** of yield farmers from the segments, **a portal address**, and **total aggregated revenue** from portal fee for the last period. 

**Portal Profitability Index \(PPI\)** provides transparency on the performance of the portal, and therefore the performance of the assets registered by the portal. If the **Portal Profitability Index \(PPI\)** of a specific portal drops below a threshold then a corresponding part of the portal security deposit is burned to compensate the network. This is one of the mechanisms designed to protect the network from low-value assets being registered by a portal.

## Portal specific smart-contracts

Once the portal is in operation for a while and has registered enough intangibles with total value above the threshold \(specific parameters like **min\_opration\_period, min\_assets\_registred, min\_assets\_registred\_total\_value** is set by the Council\) it can also deploy portal specific smart-contracts for yield farming, dynamic liquidity, and AMM protocols. This allows better tune price discovery and risks assessment smart contracts to the assets registered by a specific portal and utilizes additional metadata and insights provided by the portal. 

> For example yield farming smart-contract allows sharing a part of the profit from the portal fee or any other portal revenue stream with the network community. This yield farming smart contract can be customized for a specific asset class from this portal and provide a better risk/profit profile for potential yield farmers.

Custom AMM smart contracts can be restricted to the assets just registered from the portal and provide better terms for asset holders or liquidity pool providers.


---
description: >-
  Read this brief introduction to the creator economy protocol to learn about
  its implementation.
---

# Operations

An operation is the smallest unit of the protocol dedicated to modify the state of a blockchain relying on predefined rules. Multiple operations can be combined into a transaction to be executed atomically. A composition of operations inside a transaction can reflect a specific business process. This allows Portals to set up and build services to achieve their special goals.

## Operations

Every operation is designed with a built-in authorization layer, which defines what accounts are permitted to execute it. An account can belong either to a person or an organization \(DAO\) with multi-signature mode, as well as other governance models.

The list below describes supported operations and will receive ongoing updates as the protocol evolves.

### Account operations

| Operation | Definition |
| :--- | :--- |
| `CREATE_ACCOUNT` | An operation that allows to create a new account. It is used to register a new user or DAO in the network with a set of keys, options, and metadata. This operation requires a fee from the creator. |
| `UPDATE_ACCOUNT` | An operation that allows to update existing account options, metadata, and keys set. |

### Project operations

| Operation | Definition |
| :--- | :--- |
| `CREATE_PROJECT` | An operation that allows to create a new project. The project is the central entity in the protocol which aggregates intangible asset content. It provides opportunities to discover, manage, and work on intangible assets. Projects can be owned and governed by assigned teams that may include DAOs and individual accounts. |
| `UPDATE_PROJECT` | An operation that allows to update existing project options and metadata. |
| `ADD_PROJECT_CONTENT` | An operation that allows to add new segregated content to an intangible asset. Evaluation of an intangible asset depends on how valuable its content is. Measurement of this value is one of the main challenges of the DEIP assessment system \(DAS\). |
| `START_PROJECT_FUNDRAISING` | An operation that allows intangible asset owners to start a fundraising campaign and attract investment for further activities in exchange for project NFT/F-NFT assets. Each fundraising campaign may use one of the supported models that describes applicable rules such as who is permitted to contribute the fundraising, tokens distribution model, soft/hard cap, refund policy, and more. |
| `CONTRIBUTE_PROJECT_FUNDRAISING` | An operation that allows to contribute to project fundraising campaigns and make investments. Depending on the fundraising campaign model, the execution of this operation may be narrowed down to a limited number of accounts. |
| `CREATE_PROJECT_LICENSE` | An operation that allows to create a license for an intangible asset to give the licensee the right to use it for commercial or other purposes. |
| `CREATE_PROJECT_NDA` | An operation that allows to create a non-disclosure agreement \(NDA\) for an intangible asset between involved parties. This operation gives the opportunity to establish a channel for sharing confidential information about an intangible asset and its content according to specified conditions. |
| `CREATE_PROJECT_CONTENT_REVIEW` | An operation that allows to make an assessment of an intangible asset and helps to define its value. The assessment model is customizable and represents a set of criteria that a reviewer addresses during their assessment. This operation is an essential unit of the DEIP assessment system \(DAS\) |
| `SUPPORT_PROJECT_CONTENT_REVIEW` | An operation that allows to support an existing assessment of an intangible asset and hence increase or decrease its value index. This operation is used by curators that help to justify the correctness of the assessment. As in the previous operation, this is an important part of the DEIP assessment system \(DAS\) |

### Asset operations

| Operation | **Definition** |
| :--- | :--- |
| `CREATE_ASSET` | An operation that allows to create an asset of a specific type. The type of asset must be specified while its creation and can not be changed. This operation gives opportunities to: tokenize an intangible asset or DAO by issuing non-fungible tokens \(NFT/F-NFT\); register an asset-backed token or dX stablecoin; or create a custom token to ​facilitate business models for custom services. Every asset has a set of options that may enable or disable specific actions for the asset such as transfer restrictions and others |
| `ISSUE_ASSET` | An operation that allows to issue previously created assets in a specific account. The amount of assets that can be issued is limited by the MAX amount value specified during asset creation and may be limited by additional options. |
| `RESERVE_ASSET` | An operation that allows to burn previously issued assets according to the rules specified during asset creation. This operation may be restricted depending on asset options. |
| `TRANSFER` | An operation that allows to transfer assets between accounts. Depending on the asset, the operation may require a fee from the sender. |

### Proposal operations

| **Operation** | **Definition** |
| :--- | :--- |
| `CREATE_PROPOSAL` | An operation that allows to create a postponed on-chain transaction. As mentioned previously, a transaction can be composed of an arbitrary number of operations that may require approval from multiple accounts. To address complex workflows, where approval of a transaction may last for a long time while all required signatures are being collected, DEIP protocol provides the ability to keep such a transaction in a pending state until its execution. |
| `UPDATE_PROPOSAL` | An operation that allows to add or revoke approval of a specific account for a specified proposal. Once all required approvals are collected, the proposed transaction is executed. |
| `DELETE_PROPOSAL` | An operation that allows to reject a proposed transaction and delete it from the pending transactions pool. This operation may only be executed by an account whose approval is required for the proposed transaction. |


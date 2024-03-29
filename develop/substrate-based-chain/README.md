---
description: Uses WASM and Rust.
---

# Substrate-based chain

## Quickstart

Follow our [Polkadot GitHub repository](https://github.com/DEIPworld/deip-polkadot) to get started 🛠️

## Rust Setup

First, complete the basic Rust setup instructions [doc/rust-setup.md](https://github.com/DEIPworld/deip-polkadot/blob/main/doc/rust-setup.md):

{% page-ref page="rust-setup.md" %}

### Run

Use Rust's native `cargo` command to build and launch the node:

```text
cargo run --release -- --dev --tmp
```

or use `make` alias

### Build

The `cargo run` command will perform an initial build. Use the following command to build the node without launching it:

### Test

The `make tests` command will launch comprehensive test suite.

### Embedded docs

Once the project has been built, the following command can be used to explore all parameters and subcommands:

```text
./target/release/node-template -h
```

To build and open a rust doc:

```text
cargo doc --package <spec> --open
```

Replacing with one of the included pallets \(i.e. `cargo doc --package pallet-deip --open`\).

## Run

The provided `cargo run` command will launch a temporary node and its state will be discarded after you terminate the process. After the project has been built, there are other ways to launch the node.

## Connect UI

There are 2 options:

* Use a [Substrate Front End Template](https://github.com/substrate-developer-hub/substrate-front-end-template). Follow the instructions in the repo
* Use this [link](https://polkadot.js.org/apps/#/extrinsics?rpc=ws://127.0.0.1:9944) to open the Polkadot JS Apps UI and automatically configure the UI to connect to the local node

## Tools

* [Utilities and libraries](https://polkadot.js.org/docs/) for interacting with the Polkadot/Parachains/Substrate network from JavaScript
* [Substrate utilities](https://www.shawntabrizi.com/substrate-js-utilities/)

### Single-node development chain

This command will start the single-node development chain with persistent state:

```text
./target/release/node-template --dev
```

Purge the development chain's state:

```text
./target/release/node-template purge-chain --dev
```

Start the development chain with detailed logging:

```text
RUST_LOG=debug RUST_BACKTRACE=1 ./target/release/node-template -lruntime=debug --dev
```

### Multi-node local testnet

If you want to see the multi-node consensus algorithm in action, refer to [our Start a Private Network tutorial](https://substrate.dev/docs/en/tutorials/start-a-private-network/).

## Template structure

A Substrate project such as this consists of a number of components that are spread across a few directories.

### Node

A blockchain node is an application that allows users to participate in a blockchain network. Substrate-based blockchain nodes expose a number of capabilities:

* **Networking**: Substrate nodes use the [`libp2p`](https://libp2p.io/) networking stack to allow the nodes in the network to communicate with one another
* **Consensus**: Blockchains must have a way to come to [consensus](https://substrate.dev/docs/en/knowledgebase/advanced/consensus) on the state of the network; Substrate makes it possible to supply custom consensus engines and also ships with several consensus mechanisms that have been built on top of [Web3 Foundation research](https://research.web3.foundation/en/latest/polkadot/NPoS/index.html)
* **RPC Server**: A remote procedure call \(RPC\) server is used to interact with Substrate nodes

There are several files in the `node` directory - take special note of the following:

* [`chain_spec.rs`](https://github.com/DEIPworld/deip-polkadot/blob/main/node/src/chain_spec.rs): A [chain specification](https://substrate.dev/docs/en/knowledgebase/integrate/chain-spec) is a source code file that defines a Substrate chain's initial \(genesis\) state; chain specifications are useful for development and testing, and critical when architecting the launch of a production chain; take note of the `development_config` and `testnet_genesis` functions, which are used to define the genesis state for the local development chain configuration; these functions identify some [well-known accounts](https://substrate.dev/docs/en/knowledgebase/integrate/subkey#well-known-keys) and use them to configure the blockchain's initial state
* [`service.rs`](https://github.com/DEIPworld/deip-polkadot/blob/main/node/src/service.rs): This file defines the node implementation; take note of the libraries that this file imports and the names of the functions it invokes; in particular, there are references to consensus-related topics, such as the [longest chain rule](https://substrate.dev/docs/en/knowledgebase/advanced/consensus#longest-chain-rule), the [Aura](https://substrate.dev/docs/en/knowledgebase/advanced/consensus#aura) block authoring mechanism and the [GRANDPA](https://substrate.dev/docs/en/knowledgebase/advanced/consensus#grandpa) finality gadget

After the node has been [built](./#build), refer to the embedded documentation to learn more about the capabilities and configuration parameters that it exposes:

```text
./target/release/node-template --help
```

### Runtime

In Substrate, the terms "[runtime](https://substrate.dev/docs/en/knowledgebase/getting-started/glossary#runtime)" and "[state transition function](https://substrate.dev/docs/en/knowledgebase/getting-started/glossary#stf-state-transition-function)" are analogous - they refer to the core logic of the blockchain that is responsible for validating blocks and executing the state changes they define. The Substrate project in this repository uses the [FRAME](https://substrate.dev/docs/en/knowledgebase/runtime/frame) framework to construct a blockchain runtime. FRAME allows runtime developers to declare domain-specific logic in modules called "pallets". At the heart of FRAME is a helpful [macro language](https://substrate.dev/docs/en/knowledgebase/runtime/macros) that makes it easy to create pallets and flexibly compose them to create blockchains that can address [a variety of needs](https://www.substrate.io/substrate-users/).

Review the [FRAME runtime implementation](https://github.com/DEIPworld/deip-polkadot/blob/main/runtime/src/lib.rs) included in this template and note the following:

* This file configures several pallets to include in the runtime; each pallet configuration is defined by a code block that begins with `impl $PALLET_NAME::Config for Runtime`
* The pallets are composed into a single runtime by way of the [`construct_runtime!`](https://crates.parity.io/frame_support/macro.construct_runtime.html) macro, which is part of the core [FRAME Support](https://substrate.dev/docs/en/knowledgebase/runtime/frame#support-library) library

### Pallets

The runtime in this project is constructed using many FRAME pallets that ship with the [core Substrate repository](https://github.com/paritytech/substrate/tree/master/frame) and a template pallet that is [defined in the `pallets`](https://github.com/DEIPworld/deip-polkadot/blob/main/pallets/template/src/lib.rs) directory.

A FRAME pallet is compromised of a number of blockchain primitives:

* **Storage**: FRAME defines a rich set of powerful [storage abstractions](https://substrate.dev/docs/en/knowledgebase/runtime/storage) that makes it easy to use Substrate's efficient key-value database to manage the evolving state of a blockchain
* **Dispatchables**: FRAME pallets define special types of functions that can be invoked \(dispatched\) from outside of the runtime in order to update its state
* **Events**: Substrate uses [events](https://substrate.dev/docs/en/knowledgebase/runtime/events) to notify users of important changes in the runtime
* **Errors**: When a dispatchable fails, it returns an error
* **Config**: The `Config` configuration interface is used to define the types and parameters upon which a FRAME pallet depends

### Run in Docker

First, install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/).

Then run the following command to start a single node development chain.

This command will firstly compile your code, and then start a local development network. You can also replace the default command \(`cargo build --release && ./target/release/node-template --dev --ws-external`\) by appending your own. A few useful ones are as follow.

```text
# Run Substrate node without re-compiling
./scripts/docker_run.sh ./target/release/node-template --dev --ws-external

# Purge the local dev chain
./scripts/docker_run.sh ./target/release/node-template purge-chain --dev

# Check whether the code is compilable
./scripts/docker_run.sh cargo check
```


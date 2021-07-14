# Proposal testing guide

### CREATE\_PROPOSAL

The `CREATE_PROPOSAL` DEIP protocol operation is Implemented as `propose(batch)` extrinsic from the `deipProposal` pallet \(runtime module\).

In the [Polkadot JS App](https://polkadot.js.org/apps) click on "[Developer -&gt; Extrinsics](https://polkadot.js.org/apps/#/extrinsics)" at menu bar and select the target extrinsic as a Pallet-&gt;Call pair:

| deipProposal | propose\(batch\) |
| :--- | :--- |


Then click the "+ Add item" button to add the proposal _batch_ _items_.

> Total number of batch items is NOT LIMITED yet but we are going to perform some kinds of benchmarking to extract the optimal batch size constraints soon.

> Proposal may have other CREATE\_PROPOSAL operations as a batch items thus we got some constraints on the _**nested proposals**_:
>
> * Now the _depth_ of nested proposals is set to **max 2**
> * We must to check that proposal batch has no UPDATE\_PROPOPSAL operations that refers to the parent proposal via `proposal_id` call arg. Because of proposal ID is a hash of \[BlockNumber;ExtrinsicId\] pair \(where the ExtrinsicId is an ID of the currently executed CREATE\_PROPOSAL operation on a Block\) then it may be predicted in some cases \(for example: if we have no transactions on the network in the current time then we can predict the next BlockNumber and suggest that ExtrinsicID will be "1", then we can potentially create a self-referential proposal\).

### UPDATE\_PROPOSAL

The `UPDATE_PROPOSAL` DEIP protocol operation is implemented as `decide(proposal_id, decision)` extrinsic from the `deipProposal` pallet.

In the [Polkadot JS App](https://polkadot.js.org/apps) click on "[Developer -&gt; Extrinsics](https://polkadot.js.org/apps/#/extrinsics)" at menu bar and select the target extrinsic as a Pallet-&gt;Call pair:

| deipProposal | decide\(proposal\_id, decision\) |
| :--- | :--- |


> To obtain a `proposal_id` of the _pending_ _proposal_ you should perform some Storage API queries \(see "Storage API" section\). Also `CREATE_PROPOSAL` emits a **Proposed\(AccountId, ProposalId\)** event where `AccountId` is a proposal author account ID.

Fill up fields and submit transaction. If you make "Approve" decision then state of a proposal member decision updates from "Pending" to "Approved" state in the proposal object. When the all members of proposal make "Approve" decision the batch will be executed as a single transaction and proposal state will updates from "Pending" to "Done" in the case of the successful batch execution or "Fail" in the case of batch execution error. If only one member make "Decline" decision then proposal state will be immediately updated from "Pending" to "Rejected" state.

### DELETE\_PROPOSAL

_Not implemented_

## Storage API

### PENDING\_PROPOSALS

The `PENDING_PROPOSALS` storage query is implemented as `pendingProposals(AccountId)` query from the `deipProposal` pallet.

In the [Polkadot JS App](https://polkadot.js.org/apps) click on "[Developer -&gt; Chain state -&gt; Storage](https://polkadot.js.org/apps/#/chainstate)" at menu bar and select the target storage query as Pallet-&gt;Query pair:

| deipProposal | pendingProposals\(AccountId\): PendingProposalsMap |
| :--- | :--- |


The `pendingProposals` query accept an AccountId and returns a hash-map where keys of hash-map is an IDs of _pending proposals_ with corresponding values which are _proposal_ _author_ AccountId.

```text
{
  "0x2e3e498716c2ad1e9544fd77e4e98aa41513e9dda58494af1b8160d11c5bb704":"5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY"
}
```

### PROPOSAL\_STORAGE

In the [Polkadot JS App](https://polkadot.js.org/apps) click on "[Developer -&gt; Chain state -&gt; Storage](https://polkadot.js.org/apps/#/chainstate)" at menu bar.

Select the `proposalStorage` storage query from the `deipProposal` pallet to explore the proposal _state_:

| deipProposal | proposalStorage\(AccountId, ProposalId\): Option |
| :--- | :--- |


The `proposalStorage` accept an AccountId which is a proposal author's account ID and ProposalId as proposal ID and returns a proposal object:

```text
{
  "id": "0x2e3e498716c2ad1e9544fd77e4e98aa41513e9dda58494af1b8160d11c5bb704",
  "batch": [
    {
      "account": "5FLSigC9HGRKVhB9FiEo4Y3koPsNmBmLJbpXg2mp1hXcS59Y",
      "call": {
        "args": [
          "somedomainsomedomain"
        ],
        "method": "addDomain",
        "section": "deip"
      }
    }
  ],
  "decisions": {
    "5FLSigC9HGRKVhB9FiEo4Y3koPsNmBmLJbpXg2mp1hXcS59Y": "Pending"
  },
  "state": "Pending",
  "author": "5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY"
}
```


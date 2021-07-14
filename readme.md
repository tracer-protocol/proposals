# Tracer Proposals
This repo contains all implementation details for specific proposals. This ensures the implementation of a specific proposal is transparent and public to the entire Tracer community before it is pushed on chain.

# Proposal Workflow
Before opening an issue on this repo, please adhere to the proper Tracer proposal workflow outlined [here](discourse.tracer.finance)

If your proposal has not
- Passed a temperature check on Discourse
- Passed an offchain vote on Snapshot

Then please do not open an issue. Any issues that have not met the above two criteria will be deleted.

## Creating an Issue
When creating an issue in this repo, please include
- a link to the proposal on snapshot
- a link / links to the proposal on Discourse
- any other relevant implementation details.

## Producing the proposal
You may use the DAOCheck tool (WIP) or simply generate the bytecode required for the proposal yourself (Mycelium recommends using hardhat or Truffle for this).

In order for a proposal to be considered complete, you must have produced
- a list of targets
- a list of data

Where each data is the corresponding function call on a specific target.

Wrap this up in a PR. Add each proposal as a .md file under the proposals folder using the following proposal template.

## Proposal Template
```
# Proposal Title
Description

## Implementation
Targets: []
Data: []

## Generation
insert either web3js, ethersjs, or links to how the proposal data was generated.
```
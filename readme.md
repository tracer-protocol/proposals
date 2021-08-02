# Tracer Proposals
This repo contains all implementation details for specific proposals. This ensures the implementation of a specific proposal is transparent and public to the entire Tracer community before it is pushed on chain.

# Proposal Workflow
Before opening an issue on this repo, please adhere to the proper Tracer proposal workflow
- Open a EOI for the proposal on Discourse
- Open a temperature check on Discourse in the proposal lobby
- Open a proposal on Discourse
- Push the proposal to Snapshot for offchain voting

If you have not already gone through these steps, then please do not open an issue on this repo. Any issues that have not met the above two criteria will be deleted.

## Creating an Issue
When creating an issue in this repo, use the [issue template](./issue_template.md)

## Producing the proposal
In order to produce a proposal, you must generate a list of targets (Ethereum addresses) and data (data to be executed on each target) that will be passed to the DAO.

Each data will be executed against its target, and most commonly each piece of data is simply calling a specific function with certain parameters.

You may generate the bytecode required for the proposal yourself (Mycelium recommends using Hardhat or Truffle for this).

In order for a proposal to be considered complete, you must have produced
- a list of targets
- a list of data

Use the [implementation_template](implementation_template.md) for the actual file produced that contains the implementation.

## Opening a PR
Once you have produced the implementation file, open a PR using the [PR template](pr_template.md).

Make sure your PR includes the produced implementation file. Add your produced file to the proposals folder, with the filename being in the format of `NUMBER-NAME.md`

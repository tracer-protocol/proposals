# Proposal 16 - Tracer Growth Fund
Create fund of 280,000 TCR for an unknown address via the `FundManagement` contract.

(The unknown address will be a multisig for the Growth Fund Managers)

## Issue Link
https://github.com/tracer-protocol/proposals/issues/18

## Implementation Discussion
### Steps:
1. `transfer()` 280,000 TCR to the `FundManagement` contract
2. `createFund()` with 280,000 TCR for the growth fund's multisig address

### Notes:

- I'll create a function capable of implementing this proposal with any address for the `growthFund` multisig, and the `FundManagement` contract (because both are currently unknown).
- `FundManagement` contract: https://github.com/tracer-protocol/vesting/blob/fundmanage/contracts/FundManagement.sol

## Implementation
Targets: [0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050, 0x460896bb4Ec40d0D7a75a388e1aef3CfaCFEB8ea]

Data: [0xa9059cbb000000000000000000000000460896bb4ec40d0d7a75a388e1aef3cfacfeb8ea000000000000000000000000000000000000000000003b4ad496106b7f000000, 0x3a4a2a8f000000000000000000000000c023ca822d7aabbb4675e3e6f0935d9d1ae2ee8b000000000000000000000000000000000000000000003b4ad496106b7f0000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f050]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const tcr = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"; // tcr address
const pAmount = 280_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

const getProposal16 = (fundManagement, growthFund) => {
    
    // Transfer 280,000 TCR to Fund Management Contract
    const call1Target = tcr;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' }, // fundManagement
            { type: 'uint256', name: 'amount' }, // amount
        ]
    }, [fundManagement, amount]);
    
    // Create Fund with 280,000 TCR for Growth Fund
    const call2Target = fundManagement;
    const call2Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'createFund',
        inputs: [
            { type: 'address', name: 'account' }, // growthFund
            { type: 'uint256', name: 'amount' }, // amount
            { type: 'address', name: 'asset' } // tcr
        ]
    }, [growthFund, amount, tcr]);
    
    console.log(`targets: ${[call1Target, call2Target]}`);
    console.log(`proposalData: ${[call1Data, call2Data]}`);
}

const fundManagement = "0x460896bb4Ec40d0D7a75a388e1aef3CfaCFEB8ea" // fund management contract address (dummy)
const growthFund = "0xC023CA822d7aabBB4675e3E6F0935D9d1Ae2EE8b" // growth fund's multisig address (dummy)

getProposal16(fundManagement, growthFund);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Tracer Growth Fund",
    "calls": [
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x460896bb4Ec40d0D7a75a388e1aef3CfaCFEB8ea" },
                { "type": "uint256", "name": "amount", "value": "280000000000000000000000" }
            ]
        },
        {
            "target": "0x460896bb4Ec40d0D7a75a388e1aef3CfaCFEB8ea",
            "name": "createFund",
            "parameters": [
                { "type": "address", "name": "account", "value": "0xC023CA822d7aabBB4675e3E6F0935D9d1Ae2EE8b" },
                { "type": "uint256", "name": "amount", "value": "280000000000000000000000" },
                { "type": "address", "name": "asset", "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050" }
            ]
        }
    ]
}
```

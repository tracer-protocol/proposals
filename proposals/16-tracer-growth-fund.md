# Proposal 16 - Tracer Growth Fund
Create fund of 275,731,020 TCR for Growth Fund Managers multisig address via the `FundManagement` contract.

## Issue Link
https://github.com/tracer-protocol/proposals/issues/18

## Implementation Discussion
### Steps:
1. `transfer()` 275,731,020 TCR to the `FundManagement` contract
2. `createFund()` with 275,731,020 TCR for the growth fund manager's multisig address

### Notes:

- Growth Fund Manager's multisig address: 0x1C315Ae20c758d8Dc9B56415566c82F9085478a8
- `FundManagement` contract: https://etherscan.io/address/0x83181d41b3203651216065f5f5601295e8e45da4#code

## Implementation
Targets: [0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050,0x83181d41b3203651216065F5F5601295E8e45DA4]

Data: [0xa9059cbb00000000000000000000000083181d41b3203651216065f5f5601295e8e45da4000000000000000000000000000000000000000000e414508b979d4fb9b00000,0x3a4a2a8f0000000000000000000000001c315ae20c758d8dc9b56415566c82f9085478a8000000000000000000000000000000000000000000e414508b979d4fb9b000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f050]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const growthFund = "0x1C315Ae20c758d8Dc9B56415566c82F9085478a8" // growth fund's multisig address
const fundManagement = "0x83181d41b3203651216065F5F5601295E8e45DA4" // fund management contract address
const tcr = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"; // tcr address

const pAmount = 275_731_020; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

const getProposal16 = () => {
    
    // Transfer 275,731,020 TCR to Fund Management Contract
    const call1Target = tcr;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' }, // fundManagement
            { type: 'uint256', name: 'amount' }, // amount
        ]
    }, [fundManagement, amount]);
    
    // Create Fund with 275,731,020 TCR for Growth Fund
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

getProposal16();
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
                { "type": "address", "name": "recipient", "value": "0x83181d41b3203651216065F5F5601295E8e45DA4" },
                { "type": "uint256", "name": "amount", "value": "275731020000000000000000000" }
            ]
        },
        {
            "target": "0x83181d41b3203651216065F5F5601295E8e45DA4",
            "name": "createFund",
            "parameters": [
                { "type": "address", "name": "account", "value": "0x1C315Ae20c758d8Dc9B56415566c82F9085478a8" },
                { "type": "uint256", "name": "amount", "value": "275731020000000000000000000" },
                { "type": "address", "name": "asset", "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050" }
            ]
        }
    ]
}
```

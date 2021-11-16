# Non Proposal (No offchain voting process required) - Reward Wayne (Fix Governors Airdrop)
Call `bail` on Airdrop contract, and send 49k TCR to Wayne.

- Airdrop Contract: https://etherscan.io/address/0x45eca81a5bfbdd58cafb225bd4c9c49c8db99754#code
- Wayne's Address: `0x6e3674ab23fea3968e0e859Ff89c2667c9C4cC74`

## Implementation
Targets: [0x45eca81a5bfbDd58cafB225bD4C9c49c8DB99754,0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050]

Data: [0x906597b9,0xa9059cbb0000000000000000000000006e3674ab23fea3968e0e859ff89c2667c9c4cc74000000000000000000000000000000000000000000000a604b9a42df9ca00000]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const airdrop = "0x45eca81a5bfbDd58cafB225bD4C9c49c8DB99754";
const wayne = "0x6e3674ab23fea3968e0e859Ff89c2667c9C4cC74";
const tcr = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050";

const pAmount = 49_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

// Call bail on Airdrop Contract
const call1Target = airdrop;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'bail',
    inputs: []
}, []);

// Transfer 49k TCR to Wayne
const call2Target = tcr;
const call2Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // wayne
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [wayne, amount]);

console.log(`targets: ${[call1Target, call2Target]}`);
console.log(`proposalData: ${[call1Data, call2Data]}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Reward Wayne",
    "calls": [
        {
            "target": "0x45eca81a5bfbDd58cafB225bD4C9c49c8DB99754",
            "name": "bail",
            "parameters": []
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x6e3674ab23fea3968e0e859Ff89c2667c9C4cC74" },
                { "type": "uint256", "name": "amount", "value": "49000000000000000000000" }
            ]
        }
    ]
}
```

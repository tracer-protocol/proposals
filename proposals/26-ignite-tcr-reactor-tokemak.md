# Proposal 26 - Ignite TCR Reactor in Tokemak
Send 1.5 million TCR to Tokemak.

## Issue Link
https://github.com/tracer-protocol/proposals/issues/28

## Implementation Discussion
Tokemak Address: `0x8b4334d4812C530574Bd4F2763FcD22dE94A969B`

## Implementation
Targets: [0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050]

Data: [0xa9059cbb0000000000000000000000008b4334d4812c530574bd4f2763fcd22de94a969b000000000000000000000000000000000000000000013da329b6336471800000]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const tokemak = "0x8b4334d4812C530574Bd4F2763FcD22dE94A969B";
const tcr = "0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050";
const pAmount = 1_500_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

const call1Target = tcr;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // tokemak
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [tokemak, amount]);

console.log(`targets: ${call1Target}`);
console.log(`proposalData: ${call1Data}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Ignite TCR Reactor in Tokemak",
    "calls": [
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x8b4334d4812C530574Bd4F2763FcD22dE94A969B" },
                { "type": "uint256", "name": "amount", "value": "1500000000000000000000000" }
            ]
        }
    ]
}
```

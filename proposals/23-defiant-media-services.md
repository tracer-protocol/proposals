# Proposal 23 - The Defiant - Media Services
Send 11k USDC to The Defiant.
(5k for Podcast Shout Outs + 6k for Video Shout Outs)

## Issue Link
https://github.com/tracer-protocol/proposals/issues/26

## Implementation Discussion
The Defiant address: `0x46b676303ebC5699BF47e416677A57A89c70a015`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb00000000000000000000000046b676303ebc5699bf47e416677a57a89c70a015000000000000000000000000000000000000000000000000000000028fa6ae00]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const defiant = "0x46b676303ebC5699BF47e416677A57A89c70a015"
const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
const pAmount = 11_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 6); // usdc has 6 decimals

const call1Target = usdc;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // defiant
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [defiant, amount]);

console.log(`targets: ${call1Target}`);
console.log(`proposalData: ${call1Data}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "The Defiant - Media Services",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x46b676303ebC5699BF47e416677A57A89c70a015" },
                { "type": "uint256", "name": "amount", "value": "11000000000" }
            ]
        }
    ]
}
```

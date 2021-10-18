# Proposal 25 - Code 423n4 (Arena) Audit - Bug Bounty #2
Send 30k USDC to Mycelium

## Issue Link
https://github.com/tracer-protocol/proposals/issues/24

## Implementation Discussion
@raymogg told me to send the 30k in USDC to Mycelium's Multisig: `0xa6a006c12338cdcdbc882c6ab97e4f9f82340651`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f8234065100000000000000000000000000000000000000000000000000000006fc23ac00]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const mycelium = "0xa6a006c12338cdcdbc882c6ab97e4f9f82340651" // mycelium's multisig
const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
const pAmount = 30_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 6); // usdc has 6 decimals

const call1Target = usdc;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // mycelium
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [mycelium, amount]);

console.log(`targets: [${call1Target}]`);
console.log(`proposalData: [${call1Data}]`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Code 423n4 (Arena) Audit - Bug Bounty #2",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0xa6a006c12338cdcdbc882c6ab97e4f9f82340651" },
                { "type": "uint256", "name": "amount", "value": "30000000000" }
            ]
        }
    ]
}
```

# Proposal 22A - Runtime Verification Perpetual Pools Audit
Transfer 105,000 USDC to Runtime Verification immediately.

## Issue Link
https://github.com/tracer-protocol/proposals/issues/20

## Implementation Discussion
This is will be the first transfer (22A).
Runtime Verification Address: `0xA3250Ab6292F2aAe7DE2DE5dC46Ba0D24dcf699E`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000a3250ab6292f2aae7de2de5dc46ba0d24dcf699e00000000000000000000000000000000000000000000000000000018727cda00]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const runtimeVerfication = "0xA3250Ab6292F2aAe7DE2DE5dC46Ba0D24dcf699E"
const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
const pAmount = 105_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 6); // usdc has 6 decimals

const callTarget = usdc;
const callData = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // runtimeVerfication
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [runtimeVerfication, amount]);

console.log(`targets: ${callTarget}`);
console.log(`proposalData: ${callData}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Runtime Verification Perpetual Pools Audit",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0xA3250Ab6292F2aAe7DE2DE5dC46Ba0D24dcf699E" },
                { "type": "uint256", "name": "amount", "value": "105000000000" }
            ]
        }
    ]
}
```

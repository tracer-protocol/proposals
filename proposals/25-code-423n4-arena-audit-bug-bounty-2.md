# Proposal 25 - Code 423n4 (Arena) Audit - Bug Bounty #2
1. Send 30k USDC to Code 423n4
2. Send 20k USDC (in TCR) to Code 423n4
3. Send 6k USDC to Mycelium
4. Send 8k USDC (in TCR) to Mycelium

## Issue Link
https://github.com/tracer-protocol/proposals/issues/24

## Implementation Discussion
- Code 423n4 Address: `0xC2bc2F890067C511215f9463a064221577a53E10`
- Mycelium Multisig: `0xa6a006c12338cdcdbc882c6ab97e4f9f82340651`
- Current TCR price: 0.328708$ (CoinGecko)

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050,0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050]

Data: [0xa9059cbb000000000000000000000000c2bc2f890067c511215f9463a064221577a53e1000000000000000000000000000000000000000000000000000000006fc23ac00,0xa9059cbb000000000000000000000000c2bc2f890067c511215f9463a064221577a53e10000000000000000000000000000000000000000000000a156e60abb99e2c0000,0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f823406510000000000000000000000000000000000000000000000000000000165a0bc00,0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f82340651000000000000000000000000000000000000000000000408981a275ee8a00000]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // remove scientific notation & return str (to prevent overflow)
    return noOverflowRealAmount;
}

const code423n4 = "0xC2bc2F890067C511215f9463a064221577a53E10";
const mycelium = "0xa6a006c12338cdcdbc882c6ab97e4f9f82340651";

const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
const tcr = "0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050";

const tcrUsdcPrice = 0.42; // from CoinGecko

// Send 30k USDC to Code 423n4
const call1Target = usdc;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' },
        { type: 'uint256', name: 'amount' },
    ]
}, [code423n4, toDecimalsExpanded(30_000, 6)]); // usdc has 6 decimals

// Send 20k USDC (in TCR) to Code 423n4
const call2Target = tcr;
const call2Amount = Math.round(20_000 / tcrUsdcPrice) // 47619 TCR
const call2Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' },
        { type: 'uint256', name: 'amount' },
    ]
}, [code423n4, toDecimalsExpanded(call2Amount, 18)]); // tcr has 18 decimals

// Send 6k USDC to Mycelium
const call3Target = usdc;
const call3Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' },
        { type: 'uint256', name: 'amount' },
    ]
}, [mycelium, toDecimalsExpanded(6_000, 6)]); // usdc has 6 decimals

// Send 8k USDC (in TCR) to Mycelium
const call4Target = tcr;
const call4Amount = Math.round(8_000 / tcrUsdcPrice); // 19048 TCR
const call4Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' },
        { type: 'uint256', name: 'amount' },
    ]
}, [mycelium, toDecimalsExpanded(call4Amount, 18)]); // tcr has 18 decimals

console.log(`targets: ${call1Target},${call2Target},${call3Target},${call4Target}`);
console.log(`proposalData: ${call1Data},${call2Data},${call3Data},${call4Data}`);
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
                { "type": "address", "name": "recipient", "value": "0xC2bc2F890067C511215f9463a064221577a53E10" },
                { "type": "uint256", "name": "amount", "value": "30000000000" }
            ]
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0xC2bc2F890067C511215f9463a064221577a53E10" },
                { "type": "uint256", "name": "amount", "value": "47619000000000000000000" }
            ]
        },
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0xa6a006c12338cdcdbc882c6ab97e4f9f82340651" },
                { "type": "uint256", "name": "amount", "value": "6000000000" }
            ]
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0xa6a006c12338cdcdbc882c6ab97e4f9f82340651" },
                { "type": "uint256", "name": "amount", "value": "19048000000000000000000" }
            ]
        }
    ]
}
```

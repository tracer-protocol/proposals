# Non Proposal (No offchain voting process required) - Mycelium Monthly Fund Withdraw (October)
Implementation for proposal, transferring 500k USDC to `Mycelium Multisig` (`0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`)

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f82340651000000000000000000000000000000000000000000000000000000746a528800]

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"
const amount = 500_000;
const multisig = "0xa6a006C12338cdcDbC882c6ab97E4F9F82340651";

const call1Target = usdc;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // multisig
        { type: 'uint256', name: 'amount' }, // toDecimalsExpanded(amount, 6) - USDC has 6 decimals
    ]
}, [ multisig, toDecimalsExpanded(amount, 6) ]);

console.log(`targets: ${call1Target}`);
console.log(`proposalData: ${call1Data}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "name": "recipient",
                    "type": "address",
                    "value": "0xa6a006C12338cdcDbC882c6ab97E4F9F82340651"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "500000000000"
                }
            ]
        }
    ]
}
```

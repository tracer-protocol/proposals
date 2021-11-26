# 32 - Permissionless Conference 2022
Send 98k USDC from DAO to Multisig

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/36

## Implementation Discussion
- `multisig`: `0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`
- `USDC`: `0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`
- `USDC` has 6 decimals

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f8234065100000000000000000000000000000000000000000000000000000016d1415400]

## Generation Code
```javascript
function implement() {
    const Web3 = require("web3");
    const web3 = new Web3();

    const toDecimalsExpanded = (amount, decimals) => {
        const realAmount = amount * 10 ** decimals; // apply decimals
        const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
        return noOverflowRealAmount;
    }

    const multisig = "0xa6a006C12338cdcDbC882c6ab97E4F9F82340651"
    const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
    const amount = 98_000;

    const callTarget = usdc;
    const callData = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [multisig, toDecimalsExpanded(amount, 6)]); // usdc has 6 decimals

    console.log(`targets: ${callTarget}`);
    console.log(`data: ${callData}`);

    return {
        targets: callTarget,
        data: callData
    }
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "Permissionless Conference 2022",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0xa6a006C12338cdcDbC882c6ab97E4F9F82340651"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "98000000000"
                }
            ]
        }
    ]
}
```

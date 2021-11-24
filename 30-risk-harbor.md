# 30 - Risk Harbor
Send 400k USDC to Risk Harbor

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/38

## Implementation Discussion
- `Risk Harbor Address`: `0x340b65f00bcA63EEfe7336f30290e1039EDe754F`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000340b65f00bca63eefe7336f30290e1039ede754f0000000000000000000000000000000000000000000000000000005d21dba000]

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

    const riskHarbor = "0x340b65f00bcA63EEfe7336f30290e1039EDe754F";
    const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
    const amount = 400_000;

    const target1 = usdc;
    const data1 = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [riskHarbor, toDecimalsExpanded(amount, 6)]); // usdc has 6 decimals

    console.log(`targets: ${target1}`);
    console.log(`data: ${data1}`);

    return {
        targets: target1,
        data: data1
    }
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "Risk Harbor",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0x340b65f00bcA63EEfe7336f30290e1039EDe754F"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "400000000000"
                }
            ]
        }
    ]
}
```
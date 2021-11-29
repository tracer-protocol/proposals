# N/A - GitHub Bot Test
Send 17.5k USDC to EthDenver

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/48

## Implementation Discussion
- `ethDenver`: `0xbD61Ef27f0793cC3A4A0AfbEb00b206FC5C89c2C`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]

Data: [0xa9059cbb000000000000000000000000bd61ef27f0793cc3a4a0afbeb00b206fc5c89c2c000000000000000000000000000000000000000000000000000000041314cf00]

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

    const ethDenver = "0xbD61Ef27f0793cC3A4A0AfbEb00b206FC5C89c2C";
    const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
    const amount = 17_500;

    const call1Target = usdc;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [ethDenver, toDecimalsExpanded(amount, 6)]); // usdc has 6 decimals

    console.log(`targets: ${call1Target}`);
    console.log(`data: ${call1Data}`);

    return {
        targets: call1Target,
        data: call1Data
    }
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "GitHub Bot Test",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0xbD61Ef27f0793cC3A4A0AfbEb00b206FC5C89c2C"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "17500000000"
                }
            ]
        }
    ]
}
```
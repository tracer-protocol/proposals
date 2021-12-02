# 00 - Bug Bounty Payout
Send 1k USD (in TCR) to bug finder.

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/53

## Implementation Discussion
- `bugFinder`: `0x8efE50a4b8c8B64FDC93a5b1712Fd735d8223cD5`

## Implementation
Targets: [0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050]

Data: [0xa9059cbb0000000000000000000000008efe50a4b8c8b64fdc93a5b1712fd735d8223cd50000000000000000000000000000000000000000000000c8cb53775deee00000]

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

    const bugFinder = "0x8efE50a4b8c8B64FDC93a5b1712Fd735d8223cD5";
    const tcr = "0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050";
    const amount = 1_000; // amount is 1k USD
    const tcrUsdcPrice = 0.27; // from CoinGecko

    const call1Target = tcr;
    const call1Amount = Math.round(amount / tcrUsdcPrice);
    console.log(`call 1 amount: ${call1Amount} TCR`); // to use in DAOCheckTool
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [bugFinder, toDecimalsExpanded(call1Amount, 18)]); // tcr has 18 decimals

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
    "name": "Bug Bounty Payout",
    "calls": [
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0x8efE50a4b8c8B64FDC93a5b1712Fd735d8223cD5"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "3704000000000000000000"
                }
            ]
        }
    ]
}
```
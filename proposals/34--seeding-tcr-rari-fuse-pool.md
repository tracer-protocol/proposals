# 34 -  Seeding TCR Rari Fuse Pool
1. Give 33,334 USDC allowance to USDC Pool
2. Mint 33,334 USDC on USDC Pool

3. Give 33,333 USDC (in TCR) allowance to TCR pool
4. Mint 33,333 USDC (in TCR) on TCR Pool

5. Mint 33,333 USDC (in ETH) on ETH Pool

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/43

## Implementation Discussion
- `usdcPool`: `0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`
- `tcrPool`: `0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`
- `ethPool`: `0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`

## Implementation
Targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0xa76D892F318C524A46C320EAb7867eF09F85f221,0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050,0xC12BB8773894B0D4CC7F9Df230C84206deAd2216,0x49E06B878f788810A15a9174d2Ec3f614dEB9451]

Data: [0x095ea7b3000000000000000000000000a76d892f318c524a46c320eab7867ef09f85f22100000000000000000000000000000000000000000000000000000007c2dc7980,0xa0712d6800000000000000000000000000000000000000000000000000000007c2dc7980,0x095ea7b3000000000000000000000000c12bb8773894b0d4cc7f9df230c84206dead2216000000000000000000000000000000000000000000001d6922316bd6a5200000,0xa0712d68000000000000000000000000000000000000000000001d6922316bd6a5200000,0x1249c58b]

## Generation Code
```javascript
function implement() {
    const Web3 = require("web3");
    const web3 = new Web3();

    const toDecimalsExpanded = (amount, decimals) => {
        const realAmount = amount * 10 ** decimals; // apply decimals
        const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // remove scientific notation & return str (to prevent overflow)
        return noOverflowRealAmount;
    }

    const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
    const tcr = "0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050";

    const usdcPool = "0xa76D892F318C524A46C320EAb7867eF09F85f221";
    const tcrPool = "0xC12BB8773894B0D4CC7F9Df230C84206deAd2216";
    const ethPool = "0x49E06B878f788810A15a9174d2Ec3f614dEB9451";

    const tcrUsdcPrice = 0.24; // from CoinGecko
    const ethUsdcPrice = 4080; // from CoinGecko

    // Give 33,334 USDC allowance and mint
    const call1Target = usdc;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'approve',
        inputs: [
            { type: 'address', name: 'spender' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [usdcPool, toDecimalsExpanded(33_334, 6)]); // usdc has 6 decimals

    const call2Target = usdcPool;
    const call2Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'mint',
        inputs: [
            { type: 'uint256', name: 'amount' }
        ]
    }, [toDecimalsExpanded(33_334, 6)]); // usdc has 6 decimals


    // Give 33,333 USDC (in TCR) allowance and mint
    const call3Target = tcr;
    const call3Amount = Math.round(33_333 / tcrUsdcPrice);
    console.log(`call 3 amount: ${call3Amount} TCR`); // to use in DAOCheckTool
    const call3Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'approve',
        inputs: [
            { type: 'address', name: 'spender' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [tcrPool, toDecimalsExpanded(call3Amount, 18)]); // tcr has 18 decimals

    const call4Target = tcrPool;
    const call4Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'mint',
        inputs: [
            { type: 'uint256', name: 'amount' }
        ]
    }, [toDecimalsExpanded(call3Amount, 18)]); // tcr has 18 decimals


    // Mint 33,333 USDC (in ETH)
    const call5Target = ethPool;
    const call5Amount = Math.round(33_333 / ethUsdcPrice);
    console.log(`call 5 amount: ${call5Amount} ETH`); // to use in DAOCheckTool
    const call5Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        payable: true,
        name: 'mint',
        inputs: [],
        value: web3.utils.toWei("8", "ether")
    }, []);

    console.log(`targets: ${call1Target},${call2Target},${call3Target},${call4Target},${call5Target}`);
    console.log(`proposalData: ${call1Data},${call2Data},${call3Data},${call4Data},${call5Data}`);

    return {
        targets: [call1Target, call2Target, call3Target, call4Target, call5Target],
        data: [call1Data, call2Data, call3Data, call4Data, call5Data]
    }
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": " Seeding TCR Rari Fuse Pool",
    "calls": [
        {
            "target": "USDC",
            "name": "approve",
            "parameters": [
                {
                    "type": "address",
                    "name": "spender",
                    "value": "0xa76D892F318C524A46C320EAb7867eF09F85f221"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "33334000000"
                }
            ]
        },
        {
            "target": "0xa76D892F318C524A46C320EAb7867eF09F85f221",
            "name": "mint",
            "parameters": [
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "33334000000"
                }
            ]
        },
        {
            "target": "TCR",
            "name": "approve",
            "parameters": [
                {
                    "type": "address",
                    "name": "spender",
                    "value": "0xC12BB8773894B0D4CC7F9Df230C84206deAd2216"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "138888000000000000000000"
                }
            ]
        },
        {
            "target": "0xC12BB8773894B0D4CC7F9Df230C84206deAd2216",
            "name": "mint",
            "parameters": [
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "138888000000000000000000"
                }
            ]
        },
        {
            "target": "0x49E06B878f788810A15a9174d2Ec3f614dEB9451",
            "name": "mint",
            "parameters": [],
            "value": "8000000000000000000"
        }
    ]
}
```
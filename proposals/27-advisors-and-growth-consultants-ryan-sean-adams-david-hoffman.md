# 27 - Advisors and Growth Consultants Ryan Sean Adams David Hoffman
Vest 3.5 million TCR over 91 weeks, no cliff (half to rsa, half to david)

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/51

## Implementation Discussion
- `rsa`: `0xe9d18dbfd105155eb367fcfef87eaaafd15ea4b2`
- `david`: `0x9f8D8096489d7d0e1A1051ABa87D34024447b7e3`

## Implementation
Targets: [0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050,0x707b6be09028e78d2a667db7596b2803c112f9b2]

Data: [0xa9059cbb000000000000000000000000707b6be09028e78d2a667db7596b2803c112f9b200000000000000000000000000000000000000000002e5276153cd3fb3800000,0x2976113600000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000000000000000000000001400000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000616fb0600000000000000000000000000000000000000000000000000000000000000002000000000000000000000000e9d18dbfd105155eb367fcfef87eaaafd15ea4b20000000000000000000000009f8d8096489d7d0e1a1051aba87d34024447b7e30000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000017293b0a9e69fd9c00000000000000000000000000000000000000000000000017293b0a9e69fd9c00000]

## Generation Code
```javascript
function implement() {
    const Web3 = require("web3");
    const web3 = new Web3();

    const toUnixEpoch = (year, month, day, hour, minutes) => {
        const monthIndex = month - 1;
        const dateObj = new Date(year, monthIndex, day, hour, minutes)
        console.log(`\nDate Obj: ${dateObj}`);
        const blockTimestamp = Math.floor(dateObj.getTime() / 1000);
        console.log(`\nBlock Timestamp: ${blockTimestamp}`);
        return blockTimestamp;
    }

    const toDecimalsExpanded = (amount, decimals) => {
        const realAmount = amount * 10 ** decimals; // apply decimals
        const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
        console.log(`\nAmount: ${noOverflowRealAmount}`);
        return noOverflowRealAmount;
    }

    const tcr = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"; // tcr address
    const vesting = "0x707b6be09028e78d2a667db7596b2803c112f9b2"; // vesting contract address
    const amount = 3_500_000; // proposal amount is 3.5 million TCR
    const startTime = toUnixEpoch(2021, 10, 20, 7, 0); // Snapshot Vote ended on October 20th, 2021 (7 AM)
    const vestingWeeks = 91;
    const cliffWeeks = 0;
    const rsa = "0xe9d18dbfd105155eb367fcfef87eaaafd15ea4b2";
    const david = "0x9f8D8096489d7d0e1A1051ABa87D34024447b7e3";

    // STEP 1: Transfer TCR to Vesting Contract (25k * address count)
    const call1Target = tcr;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' },
            { type: 'uint256', name: 'amount' },
        ]
    }, [vesting, toDecimalsExpanded(amount, 18)]); // tcr has 18 decimals

    // STEP 2: Create Vesting Schedule for each address
    const call2Target = vesting;
    const call2Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'multiVest',
        inputs: [
            { type: 'address[]', name: 'accounts' },
            { type: 'uint256[]', name: 'amount' },
            { type: 'address', name: 'asset' },
            { type: 'bool', name: 'isFixed' }, // false
            { type: 'uint256', name: 'cliffWeeks' },
            { type: 'uint256', name: 'vestingWeeks' },
            { type: 'uint256', name: 'startTime' }
        ]
    }, [[rsa, david], Array(2).fill(toDecimalsExpanded(amount / 2, 18)), tcr, false, cliffWeeks, vestingWeeks, startTime]);

    console.log(`\ntargets: ${[call1Target, call2Target]}`);
    console.log(`\ndata: ${[call1Data, call2Data]}`);

    return {
        targets: [call1Target, call2Target],
        data: [call1Data, call2Data]
    }   
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "Advisors and Growth Consultants Ryan Sean Adams David Hoffman",
    "calls": [
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0x707b6be09028e78d2a667db7596b2803c112f9b2"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "3500000000000000000000000"
                }
            ]
        },
        {
            "target": "0x707b6be09028e78d2a667db7596b2803c112f9b2",
            "name": "multiVest",
            "parameters": [
                {
                    "type": "address[]",
                    "name": "accounts",
                    "value": [
                        "0xe9d18dbfd105155eb367fcfef87eaaafd15ea4b2",
                        "0x9f8D8096489d7d0e1A1051ABa87D34024447b7e3"
                    ]
                },
                {
                    "type": "uint256[]",
                    "name": "amount",
                    "value": [
                        "1750000000000000000000000",
                        "1750000000000000000000000"
                    ]
                },
                {
                    "type": "address",
                    "name": "asset",
                    "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"
                },
                {
                    "type": "bool",
                    "name": "isFixed",
                    "value": false
                },
                {
                    "type": "uint256",
                    "name": "cliffWeeks",
                    "value": 0
                },
                {
                    "type": "uint256",
                    "name": "vestingWeeks",
                    "value": 91
                },
                {
                    "type": "uint256",
                    "name": "startTime",
                    "value": 1634709600
                }
            ]
        }
    ]
}
```
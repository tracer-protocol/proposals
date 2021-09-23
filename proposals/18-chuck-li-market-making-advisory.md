# Proposal 18 - Chuck Li - Market Making & Advisory
Vest 3,000,000 TCR to Chuck Li's EOA (`0x7c1b4b31fd641E1Ea73E895b3656D93a659f0D0D`) over 102 weeks (no cliff).

## Issue Link
https://github.com/tracer-protocol/proposals/issues/16

## Implementation Discussion
N/A

## Implementation
Targets: [0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050]

Data: [0x0d5358830000000000000000000000007c1b4b31fd641e1ea73e895b3656d93a659f0d0d000000000000000000000000000000000000000000027b46536c66c8e30000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006600000000000000000000000000000000000000000000000000000000613b4fc8]

## Generation Code
Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Chuck Li - Market Making & Advisory",
    "calls": [
        {
            "target": "TCR",
            "name": "vest",
            "parameters": [
                { "type": "address", "name": "account", "value": "0x7c1b4b31fd641E1Ea73E895b3656D93a659f0D0D" },
                { "type": "uint256", "name": "amount", "value": "3000000000000000000000000" },
                { "type": "address", "name": "asset", "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050" },
                { "type": "bool", "name": "isFixed", "value": false },
                { "type": "uint256", "name": "cliffWeeks", "value": 0 },
                { "type": "uint256", "name": "vestingWeeks", "value": 102 },
                { "type": "uint256", "name": "startTime", "value": 1631277000 }
            ]
        }
    ]
}
```
The following code was used to double-check `Data` (it requires `web3`):
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toUnixEpoch = dateObj => {
    return Math.floor(dateObj.getTime() / 1000);
}

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const account = "0x7c1b4b31fd641E1Ea73E895b3656D93a659f0D0D"; // proposal account
const asset = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"; // tcr address

const pAmount = 3_000_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

/*
    Snapshot End Time: Sep 10, 2021, 1:30 PM
    Snapshot converts dates to my system time, but Date constructor converts from system back to UTC
*/

const snapshotEndTime = new Date(2021, 8, 10, 13, 30); // september's monthIndex = 8
const startTime = toUnixEpoch(snapshotEndTime);

const proposal18 = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'vest',
    inputs: [
        { type: 'address', name: 'account' },
        { type: 'uint256', name: 'amount' },
        { type: 'address', name: 'asset' },
        { type: 'bool', name: 'isFixed' }, // false
        { type: 'uint256', name: 'cliffWeeks' }, // 0
        { type: 'uint256', name: 'vestingWeeks' }, // 102
        { type: 'uint256', name: 'startTime' }
    ]
}, [account, amount, asset, false, 0, 102, startTime]);

console.log("DATA:", proposal18);
```

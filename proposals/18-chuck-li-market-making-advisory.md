# Proposal 18 - Chuck Li - Market Making & Advisory
Vest 3,000,000 TCR to Chuck Li's EOA (`0x7c1b4b31fd641E1Ea73E895b3656D93a659f0D0D`) over 102 weeks (no cliff).

## Issue Link
https://github.com/tracer-protocol/proposals/issues/16

## Implementation Discussion
Had a quick chat with @mynameuhh, and he advised me to set the `startTime` parameter in the `vest()` function as the time when the Snapshot Proposal passed.

The time when the Snapshot Proposal passed, should be "End date":
<img width="979" alt="Screenshot 2021-09-23 at 14 32 41" src="https://user-images.githubusercontent.com/44982443/134516398-c974a29c-cce2-4880-8d50-951bbed7059a.png">

However, I'm in Lisbon (currently UTC+1).
Is "End time" in UTC? Or was it adapted to my timezone?
<img width="671" alt="Screenshot 2021-09-23 at 14 37 56" src="https://user-images.githubusercontent.com/44982443/134517671-15dbf365-0378-45be-8aab-b7ea494b01be.png">

If I change my timezone to Brisbane (UTC+10), the "End date" also changes:
<img width="671" alt="Screenshot 2021-09-23 at 23 42 20" src="https://user-images.githubusercontent.com/44982443/134518468-e3ca77ed-2618-4807-a26f-46b5161d9271.png">
<img width="976" alt="Screenshot 2021-09-23 at 23 44 32" src="https://user-images.githubusercontent.com/44982443/134518316-0ebfe5b6-c4fe-41da-a064-8494bf96bb59.png">

Therefore, I can conclude that "End date" is being converted to my timezone.
If "End date" is `Sep 10, 2021, 1:30 PM` (when my timezone is UTC+1), then it's UTC time is `Sep 10, 2021, 12:30 PM`

I'll be using UTC time, as EVM's `block.timestamp` is seconds since unix epoch (https://docs.soliditylang.org/en/latest/units-and-global-variables.html#block-and-transaction-properties), and unix epoch is in UTC.

## Implementation
Targets: [0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050, 0x707b6be09028e78d2a667db7596b2803c112f9b2]

Data: [0xa9059cbb000000000000000000000000707b6be09028e78d2a667db7596b2803c112f9b2000000000000000000000000000000000000000000027b46536c66c8e3000000, 0x0d5358830000000000000000000000007c1b4b31fd641e1ea73e895b3656d93a659f0d0d000000000000000000000000000000000000000000027b46536c66c8e30000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006600000000000000000000000000000000000000000000000000000000613b4fc8]

## Generation Code
The following code was used to get the value of `startTime` (and to double-check DAOCheck tool's `Data`). It requires `web3`.

(Could have used less code, but decided to implement more generally applicable functions to improve future output)
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

const tcr = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"; // tcr address
const vesting = "0x707b6be09028e78d2a667db7596b2803c112f9b2"; // vesting contract address
const chuckLi = "0x7c1b4b31fd641E1Ea73E895b3656D93a659f0D0D"; // chuck li's address

const pAmount = 3_000_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 18); // tcr has 18 decimals

/*
    Snapshot End Time: Sep 10, 2021, 1:30 PM
    Snapshot converts dates to my system time, but Date constructor converts from system back to UTC
*/
const snapshotEndTime = new Date(2021, 8, 10, 13, 30); // september's monthIndex = 8
const startTime = toUnixEpoch(snapshotEndTime);

// MAKE CALL FROM GROWTH FUND (NOT DAO)

const call1Target = tcr;
const call1Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'transfer',
    inputs: [
        { type: 'address', name: 'recipient' }, // vesting
        { type: 'uint256', name: 'amount' }, // amount
    ]
}, [vesting, amount]);

const call2Target = vesting;
const call2Data = web3.eth.abi.encodeFunctionCall({
    type: 'function',
    name: 'vest',
    inputs: [
        { type: 'address', name: 'account' }, // chuckLi
        { type: 'uint256', name: 'amount' }, // amount
        { type: 'address', name: 'asset' }, // tcr
        { type: 'bool', name: 'isFixed' }, // false
        { type: 'uint256', name: 'cliffWeeks' }, // 0
        { type: 'uint256', name: 'vestingWeeks' }, // 102
        { type: 'uint256', name: 'startTime' } // startTime
    ]
}, [chuckLi, amount, tcr, false, 0, 102, startTime]);

console.log("Snapshot UTC End Time:", snapshotEndTime) // should be at 12:30 PM
console.log("START TIME:", startTime) // will use in DAOCheck tool as "startTime"

console.log(`targets: ${[call1Target, call2Target]}`);
console.log(`proposalData: ${[call1Data, call2Data]}`);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Chuck Li - Market Making & Advisory",
    "calls": [
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x707b6be09028e78d2a667db7596b2803c112f9b2" },
                { "type": "uint256", "name": "amount", "value": "3000000000000000000000000" }
            ]
        },
        {
            "target": "0x707b6be09028e78d2a667db7596b2803c112f9b2",
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

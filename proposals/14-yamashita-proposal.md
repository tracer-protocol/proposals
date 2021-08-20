# 14 - Advisor and Financial Engineer: Yamashita
Cause a total of 10,000,000 TCR tokens to vest to Yamashita's designated EOA ([`0x87c2f090997b0E158c10399605d19C41eC47b49b`](https://etherscan.io/address/0x87c2f090997b0E158c10399605d19C41eC47b49b)) linearly over a 91 week duration with no cliff. See below for important details regarding this proposal specifically.

## Issue Link
[#7](https://github.com/tracer-protocol/proposals/issues/7)

## Implementation Discussion
As discussed in the associated issue, this proposal is interesting in that the vesting agreement is rather strange: half of the 10,000,000 TCR total vested is cancellable while the other half isn't.

To avoid modifying the (very sensitive) vesting logic, we'll achieve this by creating two vesting schedules for Yamashita: one cancellable; the other not.

## Implementation
Targets: [`0x707b6be09028e78d2a667db7596b2803c112f9b2`, `0x707b6be09028e78d2a667db7596b2803c112f9b2`]
Data: [`0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70`,`0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70`]

## Generation Code
The following proposal plan was provided to [DAOCheck](https://github.com/tracer-protocol/daocheck):

```json
{
    "name": "Yamashita",
    "calls": [
        {
            "target": "0x707b6be09028e78d2a667db7596b2803c112f9b2",
            "name": "vest",
            "parameters": [
                {
                    "name": "account",
                    "type": "address",
                    "value": "0x87c2f090997b0E158c10399605d19C41eC47b49b"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "5000000000000000000000000"
                },
                {
                    "name": "asset",
                    "type": "address",
                    "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"
                },
                {
                    "name": "isFixed",
                    "type": "bool",
                    "value": "false"
                },
                {
                    "name": "cliffWeeks",
                    "type": "uint256",
                    "value": "0"
                },
                {
                    "name": "vestingWeeks",
                    "type": "uint256",
                    "value": "91"
                },
                {
                    "name": "startTime",
                    "type": "uint256",
                    "value": "1628146800"
                }
            ]
        },
        {
            "target": "0x707b6be09028e78d2a667db7596b2803c112f9b2",
            "name": "vest",
            "parameters": [
                {
                    "name": "account",
                    "type": "address",
                    "value": "0x87c2f090997b0E158c10399605d19C41eC47b49b"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "5000000000000000000000000"
                },
                {
                    "name": "asset",
                    "type": "address",
                    "value": "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050"
                },
                {
                    "name": "isFixed",
                    "type": "bool",
                    "value": "true"
                },
                {
                    "name": "cliffWeeks",
                    "type": "uint256",
                    "value": "0"
                },
                {
                    "name": "vestingWeeks",
                    "type": "uint256",
                    "value": "91"
                },
                {
                    "name": "startTime",
                    "type": "uint256",
                    "value": "1628146800"
                }
            ]
        }
    ]
}
```

It produced the following output:

```
$ yarn run start yamashita.json
============ Call 0 ============
TARGET:
    0x707b6be09028e78d2a667db7596b2803c112f9b2 (https://etherscan.io/address/0x707b6be09028e78d2a667db7596b2803c112f9b2)
DATA:
    0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70

============ Call 1 ============
TARGET:
    0x707b6be09028e78d2a667db7596b2803c112f9b2 (https://etherscan.io/address/0x707b6be09028e78d2a667db7596b2803c112f9b2)
DATA:
    0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70

============ Final Proposal ============
targets: [0x707b6be09028e78d2a667db7596b2803c112f9b2,0x707b6be09028e78d2a667db7596b2803c112f9b2]
proposalData: [0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70,0x0d53588300000000000000000000000087c2f090997b0e158c10399605d19c41ec47b49b0000000000000000000000000000000000000000000422ca8b0a00a4250000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b00000000000000000000000000000000000000000000000000000000610b8c70]
```


# 14 - Advisor and Financial Engineer: Yamashita
Pay 30,000 USDC to Flex Dapps and cause 2,000,000 TCR to vest linearly over 3 years with no cliff to Flex Dapps.

## Issue Link
[#10](https://github.com/tracer-protocol/proposals/issues/10)

## Implementation Discussion
N/A

## Implementation
Targets: [`0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`,`0x707b6be09028e78d2a667db7596b2803c112f9b2`]
Data: [`0xa9059cbb000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000000000000000006fc23ac00`,`0x0d535883000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000001a784379d99db420000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000009c0000000000000000000000000000000000000000000000000000000060a5c2a0`]

## Generation Code
The following proposal plan was provided to [DAOCheck](https://github.com/mycelium-ethereum/daocheck):

```json
{
    "name": "Flex Dapps",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "name": "to",
                    "type": "address",
                    "value": "0xDD140cB2847F6186A9Df3B25Ae1E135052b09321"
                },
                {
                    "name": "value",
                    "type": "uint256",
                    "value": "30000000000"
                }
            ]
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                {
                    "name": "to",
                    "type": "address",
                    "value": "0x707b6be09028e78d2a667db7596b2803c112f9b2"
                },
                {
                    "name": "value",
                    "type": "uint256",
                    "value": "2000000000000000000000000"
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
                    "value": "0xDD140cB2847F6186A9Df3B25Ae1E135052b09321"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "2000000000000000000000000"
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
                    "value": "156"
                },
                {
                    "name": "startTime",
                    "type": "uint256",
                    "value": "1621476000"
                }
            ]
        }
    ]
}
```

It produced the following output:

```
============ Call 0 ============
TARGET:
    0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 (https://etherscan.io/address/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
DATA:
    0xa9059cbb000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000000000000000006fc23ac00

============ Call 1 ============
TARGET:
    0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050 (https://etherscan.io/address/0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050)
DATA:
    0xa9059cbb000000000000000000000000707b6be09028e78d2a667db7596b2803c112f9b200000000000000000000000000000000000000000001a784379d99db42000000

============ Call 2 ============
TARGET:
    0x707b6be09028e78d2a667db7596b2803c112f9b2 (https://etherscan.io/address/0x707b6be09028e78d2a667db7596b2803c112f9b2)
DATA:
    0x0d535883000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000001a784379d99db420000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000009c0000000000000000000000000000000000000000000000000000000060a5c2a0

============ Final Proposal ============
targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050,0x707b6be09028e78d2a667db7596b2803c112f9b2]
proposalData: [0xa9059cbb000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000000000000000006fc23ac00,0xa9059cbb000000000000000000000000707b6be09028e78d2a667db7596b2803c112f9b200000000000000000000000000000000000000000001a784379d99db42000000,0x0d535883000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000001a784379d99db420000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000009c0000000000000000000000000000000000000000000000000000000060a5c2a0]
```

This was then checked against a manual implementation:

```typescript
import * as fs from "fs";
import { ethers } from "ethers";

/* build contract handles */
let usdcAbi: string = fs.readFileSync("USDC.json","utf8");
let tcrAbi: string = fs.readFileSync("TCR.json","utf8");
let vestingAbi: string = fs.readFileSync("vesting.json","utf8");

let usdcContract: ethers.utils.Interface = new ethers.utils.Interface(usdcAbi);
let tcrContract: ethers.utils.Interface = new ethers.utils.Interface(tcrAbi);
let vestingContract: ethers.utils.Interface = new ethers.utils.Interface(vestingAbi);

/* proposal parameters */
let flexAddress: string = "0xDD140cB2847F6186A9Df3B25Ae1E135052b09321";
let usdcAddress: string = "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48";
let tcrAddress: string = "0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050";
let vestingAddress: string = "0x707b6Be09028e78D2A667Db7596b2803C112F9b2";
let usdcAmount: number = 30000;
let tcrAmount: number = 2000000;
let proposalStart: number = 1621476000;
let vestingYears: number = 3;
let WEEKS_PER_YEAR: number = 52;

/* actual proposal logic follows */
let payloads = [
    usdcContract.encodeFunctionData("transfer", [
        flexAddress,
        ethers.BigNumber.from(usdcAmount).mul(ethers.BigNumber.from("1000000"))
    ]),
    tcrContract.encodeFunctionData("transfer", [
        vestingAddress,
        ethers.BigNumber.from(tcrAmount)
    ]),
    vestingContract.encodeFunctionData("vest", [
        flexAddress,
        ethers.BigNumber.from(tcrAmount).mul(ethers.BigNumber.from("1000000000000000000")),
        tcrAddress,
        false,
        ethers.constants.Zero,
        ethers.BigNumber.from(vestingYears)
            .mul(ethers.BigNumber.from(WEEKS_PER_YEAR)),
        ethers.BigNumber.from(proposalStart)
    ])
];

let targets = [usdcAddress, tcrAddress, vestingAddress];

console.log(targets, payloads);
```

Which produced the output:

```
$ ts-node flex.ts
[
  '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48',
  '0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050',
  '0x707b6Be09028e78D2A667Db7596b2803C112F9b2'
] [
  '0xa9059cbb000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000000000000000006fc23ac00',
  '0xa9059cbb000000000000000000000000707b6be09028e78d2a667db7596b2803c112f9b200000000000000000000000000000000000000000000000000000000001e8480',
  '0x0d535883000000000000000000000000dd140cb2847f6186a9df3b25ae1e135052b0932100000000000000000000000000000000000000000001a784379d99db420000000000000000000000000000009c4a4204b79dd291d6b6571c5be8bbcd0622f05000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000009c0000000000000000000000000000000000000000000000000000000060a5c2a0'
]
```

Conceptually, there are three steps:

 1. Transfer USDC directly to Flex
 2. Transfer TCR to vesting contract
 3. Create vesting schedule with vesting contract


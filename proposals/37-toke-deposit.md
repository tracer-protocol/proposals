# 37 - Toke Deposit
Deposit 27406 TOKE into Toke reactors

## Issue Link
Issue: 

## Implementation Discussion
- `Toke`: `0x2e9d63788249371f1dfc918a52f8d799f4a38c94`
- `tToke `: `0xa760e26aA76747020171fCF8BdA108dFdE8Eb930`
- `Toke` has 18 decimals

## Implementation
targets: ["0x2e9d63788249371f1dfc918a52f8d799f4a38c94","0xa760e26aA76747020171fCF8BdA108dFdE8Eb930"]
proposalData: [0x095ea7b3000000000000000000000000a760e26aa76747020171fcf8bda108dfde8eb93000000000000000000000000000000000000000000000d3c21bcecceda1000000,0xb6b55f250000000000000000000000000000000000000000000005cdb66c99d265b00000]

## Generation Code

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "Deposit TOKE into the reactor",
    "calls": [
        {
            "target": "0x2e9d63788249371f1dfc918a52f8d799f4a38c94",
            "name": "approve",
            "parameters": [
                { "type": "address", "name": "spender", "value": "0xa760e26aA76747020171fCF8BdA108dFdE8Eb930" },
                { "type": "uint256", "name": "amount", "value": "1000000000000000000000000" }
            ]
        },
        {
            "target": "0xa760e26aA76747020171fCF8BdA108dFdE8Eb930",
            "name": "deposit",
            "parameters": [
                { "type": "uint256", "name": "amount", "value": "27406560000000000000000" }
            ]
        }
    ]
}
```

# 21 - TCR-ETH Uniswap v3 Liquidity Pool Proposal - Visor Finance
Implementation for the TCR Liquidity proposal with Visor Finance

## Issue Link


## Implementation Discussion
The implementation will transfer $500,000 USD worth of TCR and USDC to a multisig owned by Visor Finance (`0x59D01Cc35d72d1c20Bda86A8130D7e0eFa4844d9`). They are then conducting the setup of the vault and will return LP tokens to the DAO.

TCR will be valued at $0.34 USD for the sake of this proposal, meaning 1470589 TCR will be transfered.

## Implementation
Targets: [`0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`,`0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050`]
Data: [`0xa9059cbb00000000000000000000000059d01cc35d72d1c20bda86a8130d7e0efa4844d9000000000000000000000000000000000000000000000000000000746a528800`,`0xa9059cbb00000000000000000000000059d01cc35d72d1c20bda86a8130d7e0efa4844d9000000000000000000000000000000000000000000013768ca18318c7bd40000`]

## Generation Code
DAOCheck JSON file used to generate payload

```json
{
    "name": "Visor Finance Transfer",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "name": "recipient",
                    "type": "address",
                    "value": "0x59D01Cc35d72d1c20Bda86A8130D7e0eFa4844d9"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "500000000000"
                }
            ]
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                {
                    "name": "recipient",
                    "type": "address",
                    "value": "0x59D01Cc35d72d1c20Bda86A8130D7e0eFa4844d9"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "1470589000000000000000000"
                }
            ]
        }
    ]
}
```

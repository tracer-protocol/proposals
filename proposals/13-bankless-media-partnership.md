# Proposal 13 - Bankless Media Partnership
Implementation for Proposal 13, transferring 30,000 USDC to `bankless.eth` (`0x844e211e291077B11221c0F18615a64F2Ff19c26`)

## Implementation
| field | value |
| :------------- | :-------------: |
| targets | [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]
| proposalData | [0xa9059cbb000000000000000000000000844e211e291077b11221c0f18615a64f2ff19c2600000000000000000000000000000000000000000000000000000006fc23ac00]

## Generation
Generated using the following function call(s) and the DAOCheck tool
```json
"calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "name": "recipient",
                    "type": "address",
                    "value": "0x844e211e291077B11221c0F18615a64F2Ff19c26"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "30000000000"
                }
            ]
        }
    ]
```
Note that USDC uses 6 decimals and hence `amount = 30,000 * 10^6`. The USDC address being used is `0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`.
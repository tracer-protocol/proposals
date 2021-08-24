# Non Proposal (No offchain voting process required) - Mycelium Monthly Fund Withdraw
Implementation for proposal, transferring 250,000 USDC to `Mycelium Multisig` (`0xa6a006C12338cdcDbC882c6ab97E4F9F82340651`)

## Implementation
| field | value |
| :------------- | :-------------: |
| targets | [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]
| proposalData | [0xa9059cbb000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f823406510000000000000000000000000000000000000000000000000000003a35294400]

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
                    "value": "0xa6a006C12338cdcDbC882c6ab97E4F9F82340651"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "250000000000"
                }
            ]
        }
    ]
```
Note that USDC uses 6 decimals and hence `amount = 250,000 * 10^6`. The USDC address being used is `0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`.

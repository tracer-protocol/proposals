# Proposal Title
Implementation for proposal 12, transferring 471k USDC to the Mycelium Multisig (0xa6a006C12338cdcDbC882c6ab97E4F9F82340651)

## Implementation
targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48]
proposalData: [0x91ddeef8000000000000000000000000a6a006c12338cdcdbc882c6ab97e4f9f823406510000000000000000000000000000000000000000000000000000006da9c9a600]

## Generation
Generated using the following function call(s) and the DAOCheck tool
```
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
                    "value": "471000000000"
                }
            ]
        }
    ]
```
Note that USDC uses 6 decimals and hence amount = 471000 * 10^6. The USDC address being used is 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48
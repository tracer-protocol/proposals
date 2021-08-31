# Proposal 15 - Maple Pools Treasury Diversification
1. Approve 1,250,000 USDC spending from Orthogonal Trading Maple Pool.
2. Deposit 1,250,000 USDC to Orthogonal Trading Maple Pool. We should recieve 1,250,000 MPTs (Maple Pool Token) in return. (`0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27`)
3. Approve 1,250,000 MPT spending from MPL Rewards smart contract.
4. Stake 1,250,000 MPT to MPL Rewards smart contract. (`0x7869D7a3B074b5fa484dc04798E254c9C06A5e90`)


## Implementation
| field | value |
| :------------- | :-------------: |
| targets | [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27,0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27,0x7869D7a3B074b5fa484dc04798E254c9C06A5e90]
| proposalData | [0x095ea7b3000000000000000000000000febd6f15df3b73dc4307b1d7e65d46413e710c270000000000000000000000000000000000000000000000000000012309ce5400,0xb6b55f250000000000000000000000000000000000000000000000000000012309ce5400,0x095ea7b30000000000000000000000007869d7a3b074b5fa484dc04798e254c9c06a5e900000000000000000000000000000000000000000000108b2a2c2802909400000,0xa694fc3a0000000000000000000000000000000000000000000108b2a2c2802909400000]


## Generation
Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Maple Pools - Treasury diversification",
    "calls": [
        {
            "target": "USDC",
            "name": "approve",
            "parameters": [
                {
                    "name": "spender",
                    "type": "address",
                    "value": "0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27"
                },
                {
                    "name": "value",
                    "type": "uint256",
                    "value": "1250000000000"
                }
            ]
        },
        {
            "target": "0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27",
            "name": "deposit",
            "parameters": [
                {
                    "name": "amt",
                    "type": "uint256",
                    "value": "1250000000000"
                }
            ]
        },
        {
            "target": "0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27",
            "name": "approve",
            "parameters": [
                {
                    "name": "spender",
                    "type": "address",
                    "value": "0x7869D7a3B074b5fa484dc04798E254c9C06A5e90"
                },
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "1250000000000000000000000"
                }
            ]
        },
        {
            "target": "0x7869D7a3B074b5fa484dc04798E254c9C06A5e90",
            "name": "stake",
            "parameters": [
                {
                    "name": "amount",
                    "type": "uint256",
                    "value": "1250000000000000000000000"
                }
            ]
        }
    ]
}
```

It produced the following output:

============ Call 0 ============
TARGET:
    0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 (https://etherscan.io/address/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48)
DATA:
    0x095ea7b3000000000000000000000000febd6f15df3b73dc4307b1d7e65d46413e710c270000000000000000000000000000000000000000000000000000012309ce5400

============ Call 1 ============
TARGET:
    0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27 (https://etherscan.io/address/0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27)
DATA:
    0xb6b55f250000000000000000000000000000000000000000000000000000012309ce5400

============ Call 2 ============
TARGET:
    0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27 (https://etherscan.io/address/0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27)
DATA:
    0x095ea7b30000000000000000000000007869d7a3b074b5fa484dc04798e254c9c06a5e900000000000000000000000000000000000000000000108b2a2c2802909400000

============ Call 3 ============
TARGET:
    0x7869D7a3B074b5fa484dc04798E254c9C06A5e90 (https://etherscan.io/address/0x7869D7a3B074b5fa484dc04798E254c9C06A5e90)
DATA:
    0xa694fc3a0000000000000000000000000000000000000000000108b2a2c2802909400000

============ Final Proposal ============
targets: [0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48,0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27,0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27,0x7869D7a3B074b5fa484dc04798E254c9C06A5e90]
proposalData: [0x095ea7b3000000000000000000000000febd6f15df3b73dc4307b1d7e65d46413e710c270000000000000000000000000000000000000000000000000000012309ce5400,0xb6b55f250000000000000000000000000000000000000000000000000000012309ce5400,0x095ea7b30000000000000000000000007869d7a3b074b5fa484dc04798e254c9c06a5e900000000000000000000000000000000000000000000108b2a2c2802909400000,0xa694fc3a0000000000000000000000000000000000000000000108b2a2c2802909400000]

Note that USDC uses 6 decimals and hence `amount = 1,250,000 * 10^6`. The USDC address being used is `0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48`.

The MPT token uses 18 decimals and hence `amount = 1,250,000 * 10^18`. The MPT address being used is `0xFeBd6F15Df3B73DC4307B1d7E65D46413e710C27`.
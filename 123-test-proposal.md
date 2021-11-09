# 123 - Test Proposal
Deploy Fund byb at address 0x000
- Address A: `0xE94A8d2eda89866C628AfF5Ff1461DFD22fC5DcD`
- Amount B: `50_000`

## Issue Link
Issue: https://github.com/tracer-protocol/proposals/issues/32

## Implementation Discussion
- Address A: `0xE94A8d2eda89866C628AfF5Ff1461DFD22fC5DcD`
- Amount B: `50_000`

## Implementation
Targets: [1,2,3]

Data: [a,b,c]

## Generation Code
```javascript
function implement() {

    // ----- EDIT HERE -----
    const targets = [1, 2, 3];
    const data = ["a", "b", "c"];
    // ----- STOP EDITING -----

    return {
        targets: targets,
        data: data
    }
}
```

Generated using the following function call(s) and the DAOCheck tool:
```json
{
    "name": "Test Proposal",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0xC2bc2F890067C511215f9463a064221577a53E10"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "30000000000"
                }
            ]
        },
        {
            "target": "TCR",
            "name": "transfer",
            "parameters": [
                {
                    "type": "address",
                    "name": "recipient",
                    "value": "0xC2bc2F890067C511215f9463a064221577a53E10"
                },
                {
                    "type": "uint256",
                    "name": "amount",
                    "value": "32258000000000000000000"
                }
            ]
        }
    ]
}
```
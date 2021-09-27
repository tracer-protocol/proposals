# Runtime Verification Perpetual Pools Audit
Make 2 transfers of 105,000 USDC to Runtime Verification

## Issue Link
https://github.com/tracer-protocol/proposals/issues/20

## Implementation Discussion
N/A

## Implementation
Targets: []

Data: []

### GENERATED USING DUMMY DATA! SHOULD BE UPDATED ONCE RUNTIME VERIFICATION ADDRESS IS KNOWN!

## Generation Code
```javascript
const Web3 = require("web3");
const web3 = new Web3();

const toDecimalsExpanded = (amount, decimals) => {
    const realAmount = amount * 10 ** decimals; // apply decimals
    const noOverflowRealAmount = realAmount.toLocaleString('fullwide', {useGrouping:false}); // return str (to prevent overflow) & remove scientific notation
    return noOverflowRealAmount;
}

const usdc = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"; // usdc address
const pAmount = 105_000; // proposal amount
const amount = toDecimalsExpanded(pAmount, 6); // usdc has 6 decimals

const getProposalImplementation = runtimeVerfication => {

    const call1Target = usdc;
    const call1Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' }, // runtime verfication
            { type: 'uint256', name: 'amount' }, // amount
        ]
    }, [runtimeVerfication, amount]);

    const call2Target = usdc;
    const call2Data = web3.eth.abi.encodeFunctionCall({
        type: 'function',
        name: 'transfer',
        inputs: [
            { type: 'address', name: 'recipient' }, // runtime verification
            { type: 'uint256', name: 'amount' }, // amount
        ]
    }, [runtimeVerfication, amount]);

    console.log(`targets: ${[call1Target, call2Target]}`);
    console.log(`proposalData: ${[call1Data, call2Data]}`);
}

const runtimeVerfication = "0x24f8c382bc3F8Abcb47FAECec2267eA401b09531" // runtime verification's address (dummy)
getProposalImplementation(runtimeVerfication);
```

Generated using the following function call(s) and the DAOCheck tool
```json
{
    "name": "Runtime Verification Perpetual Pools Audit",
    "calls": [
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x24f8c382bc3F8Abcb47FAECec2267eA401b09531" },
                { "type": "uint256", "name": "amount", "value": "105000000000" }
            ]
        },
        {
            "target": "USDC",
            "name": "transfer",
            "parameters": [
                { "type": "address", "name": "recipient", "value": "0x24f8c382bc3F8Abcb47FAECec2267eA401b09531" },
                { "type": "uint256", "name": "amount", "value": "105000000000" }
            ]
        }
    ]
}
```

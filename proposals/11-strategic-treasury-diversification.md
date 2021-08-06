# 11 - Strategic Treasury Diversification
This proposal would diversify a portion of the TCR governance tokens held in the Tracer DAO treasury into USDC via a direct TCR acquisition by strategic investors

## Issue Link
https://github.com/tracer-protocol/proposals/issues/3

## Implementation Discussion
The list of strategic investors and their associated token allocations can be found on the [Discourse Proposal](https://discourse.tracer.finance/t/proposal-strategic-treasury-diversification/286).

All vesting schedules will be started as of June 26th 8:50am EST (unix: 1624711800), and will vest linearly for two years with no cliff. The vesting schedules will be fixed, meaning they are unable to be cancelled by the DAO.

The following are the steps for this proposal to be executed

1. Transfer 100,000,000 TCR (0x9c4a4204b79dd291d6b6571c5be8bbcd0622f050) to the vesting contract (0x707b6be09028e78d2a667db7596b2803c112f9b2) 
   
2. Set vesting for the strategic partners

The function to be called by this proposal on the vesting contract to set vesting is 
```
function multiVest(
    address[] calldata accounts,
    uint256[] calldata amount,
    address asset,
    bool isFixed,
    uint256 cliffWeeks,
    uint256 vestingWeeks,
    uint256 startTime
) 
```

The following is the data for this function call
accounts: `[]`
amount: `[]`
asset: `0x9C4A4204B79dd291D6b6571C5BE8BbcD0622F050`
isFixed: `true`
cliffWeeks: `0`
vestingWeeks: `104`
startTime: `1624711800`




## Implementation
Targets: []
Data: []

## Generation Code


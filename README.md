# gesha17 - Smart Contract Security Researcher - Intro

**Breaking code to make it stronger.**

I hunt bugs, tear apart smart contracts, and expose vulnerabilities before the bad guys do.  
Deep into EVM internals, weird chains, DeFi protocols, and the occasional zero-day.  
Here you'll find my research, findings, audit reports, and war stories from the frontlines of Web3 security.

> Trust nothing. Verify everything.

4 times top 3 placement in competitive audits.
🛠️ Found **50+ High/Medium severity bugs** during audits.
Targets ranged across staking protocols, lending platforms, bridges, and cross-chain messaging systems.  

Below you can find links to my public profiles and some of my best findings. 👇

# Links

I am currently open for booking private audits. Get in touch with me on [X](https://x.com/shishgeor).

Here are my public profiles on the popular plaftorms:

- [C4 profile](https://code4rena.com/@gesha17)
- [Cantina profile](https://cantina.xyz/u/gesha17)
- [Sherlock profile](https://audits.sherlock.xyz/watson/gesha17)

Note that these profiles do not represent the complete list of my security findings, as some findings will remain private or are just not yet published.

# Some of my best findings(to be updated further)

## [C4 - SecondSwap audit - Solo finding](https://code4rena.com/reports/2024-12-secondswap#m-19-large-number-of-steps-in-a-vesting-may-lead-to-loss-of-beneficiary-funds-or-uneven-vesting-distribution)

### [M-19] Large number of steps in a vesting may lead to loss of beneficiary funds or uneven vesting distribution

Some token owners may create StepVesting contracts with very large numbers of steps, to simulate a continous vesting. This can lead to two edge cases for the releaseRate of a beneficiary:

- Consider a scenario where a vesting is created that has less tokens than there are number of steps in the plan. Then the releaseRate would be calculated to 0, so users will essentially lose their vestings. The severity of this would depend on how many steps there are and how much the vesting is. Suppose there are 100000000 steps in a vesting plan with duration 1 year. A user receives a vesting for 90e6 USDC. So the releaseRate will be calculated as 90e6/100000000 = 0.9, which is rounded down to 0. So the user will lose his tokens.
- This can also lead to a situation where the release rate becomes 1 and a large amount of the tokens get vested at the very last step, creating a very uneven vesting distribution. A requirement is that the number of steps is more than tokenAmount/2. So if the amount of steps is say 10000000 USDC or 10e6 USDC, the number of steps has to be more than 5e6 USDC for the bug to occur. So likelihood is very low.

...
  
  Read the full description [here](https://code4rena.com/reports/2024-12-secondswap#m-19-large-number-of-steps-in-a-vesting-may-lead-to-loss-of-beneficiary-funds-or-uneven-vesting-distribution)

## [C4 - Size audit - Selected for report](https://code4rena.com/reports/2024-06-size#m-08-sandwich-attack-on-loan-fulfillment-will-temporarily-prevent-users-from-accessing-their-borrowed-funds)

### [M-08] Sandwich attack on loan fulfillment will temporarily prevent users from accessing their borrowed funds

The protocol does not remove borrowed token liquidity from the aave pool once a loan is initiated. It only checks if there is enough available liquidity via the validateVariablePoolHasEnoughLiquidity() function. A user is expected to withdraw their funds after the loan is created. This means that a malicious user can sandwich loans that exceed the available liquidity in aave by depositing liquidity in a frontrun transaction and removing it in a backrun transaction. This way a user that takes out a loan will not be able to remove their funds until there is enough available liquidity in the pool.

Also note that liquidity may become unavailable via other factors, like external users removing liquidity from aave.

...

  Read the full description [here](https://code4rena.com/reports/2024-06-size#m-08-sandwich-attack-on-loan-fulfillment-will-temporarily-prevent-users-from-accessing-their-borrowed-funds)

## [C4 - Liquid Ron Audit - I found all HM bugs in this audit](https://code4rena.com/reports/2025-01-liquid-ron#m-01-user-can-earn-rewards-by-frontrunning-the-new-rewards-accumulation-in-ron-staking-without-actually-delegating-his-tokens)

### [M-01] User can earn rewards by frontrunning the new rewards accumulation in Ron staking without actually delegating his tokens

The Ron staking contract let us earn rewards by delegating our tokens to a validator. But you will only earn rewards on the lowest balance of the day (source). So if you delegate your tokens on the first day, you are going to earn 0 rewards for that day as your lowest balance was 0 on that day. This will happens with every new delegator.

...

  Read the full description [here](https://code4rena.com/reports/2025-01-liquid-ron#m-01-user-can-earn-rewards-by-frontrunning-the-new-rewards-accumulation-in-ron-staking-without-actually-delegating-his-tokens)

## [C4 - Chakra Audit - Cross chain protocol - High severity finding](https://code4rena.com/reports/2024-08-chakra#h-14-malicious-actors-can-manipulate-the-cross_chain_callback-callback)

### [H-14] Malicious actors can manipulate the cross_chain_callback callback

Because the validator’s signature message does not include the from_chain field, a malicious actor can preemptively execute the validator’s transaction with an incorrect from_chain field. This can cause the status of create_cross_txs[txid] to become a Failed state, preventing it from being executed again.

...

  Read the full description [here](https://code4rena.com/reports/2024-08-chakra#h-14-malicious-actors-can-manipulate-the-cross_chain_callback-callback)

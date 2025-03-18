---
sponsor: "Liquid Ron"
slug: "2025-01-liquid-ron"
date: "2025-03-18"
title: "Liquid Ron"
findings: "https://code4rena.com/audits/2025-01-liquid-ron/submissions"
contest: 486
---

# Overview
## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the Liquid Ron smart contract system. The audit took place from January 28 to February 04, 2025.

Following the C4 audit, 3 wardens ([Aamir](https://code4rena.com/@Aamir), [ilchovski](https://code4rena.com/@ilchovski), and [0rpse](https://code4rena.com/@0rpse)) reviewed the mitigations implemented by the Liquid Ron team; the [mitigation review report](#mitigation-review) is appended below the audit report.

The audit and mitigation review were judged by [0xsomeone](https://code4rena.com/@0xsomeone).

Final report assembled by Code4rena.

# Summary

The C4 analysis yielded an aggregated total of 3 unique vulnerabilities. Of these vulnerabilities, 1 received a risk rating in the category of HIGH severity and 2 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 17 reports detailing issues with a risk rating of LOW severity or non-critical. 

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 Liquid Ron repository](https://github.com/code-423n4/2025-01-liquid-ron), and is composed of 6 smart contracts written in the Solidity programming language and includes 386 lines of Solidity code.

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (1)

## [[H-01] The calculation of `totalAssets()` could be wrong if `operatorFeeAmount > 0`, this can cause potential loss for the new depositors](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-3)
*Submitted by [0x04bytes](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-960), also found by [056Security](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-990), 0rpse ([1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1128), [2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1136)), 0x0bserver ([1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1091), [2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1102)), [0x0dd](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-493), [0x23r0](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-97), [0xAlix2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-371), [0xDemon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-788), [0xG0P1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-761), [0xRajkumar](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-894), [0xrex](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-107), [0xvd](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1132), [Aamir](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-473), [aariiif](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-61), [Adotsam](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-957), [air\_0x](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-745), [aldarion](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-258), [Alekso](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-492), [arman](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1183), [attentioniayn](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-67), [Bauchibred](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-292), [bigbear1229](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-941), [BlackAdam](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-909), Breeje ([1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-936), [2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-939)), [ccvascocc](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-569), [csanuragjain](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-324), [curly](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-623), [Darinrikusham](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1036), [DemoreX](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1067), [DoD4uFN](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-439), [ElCid](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-911), [emerald7017](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-988), [EPSec](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-708), [eta](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-391), [Fitro](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-499), [future2\_22](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-625), [gesha17](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-185), [grearlake](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1267), [harry\_cryptodev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1106), [hrmneffdii](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-425), [hyuunn](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-563), [ilchovski](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1265), [IlIlHunterlIlI](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-46), [JCN](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-63), [Josh4324](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1042), [jsonDoge](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-796), [klau5](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-970), [muncentu](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-489), [nnez](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-401), oakcobalt ([1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-684), [2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-698)), [PabloPerez](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1203), [peanuts](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1165), [phoenixV110](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-133), [roccomania](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-726), [rudhra](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-163), [Ryonen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-200), [santiellena](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1134), [serial-coder](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1179), [Shahil\_Hussain](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-895), [silver\_eth](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-497), [sl1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-644), [spuriousdragon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1046), [stuart\_the\_minion](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-174), t0x1c ([1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-116), [2](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-118)), [Tadev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-353), [udogodwin](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1011), [valy001](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-912), [victortheoracle](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-924), [wellbyt3](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-953), [y4y](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-470), [YouCrossTheLineAlfie](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-379), [zainab\_ou](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-100), and [zraxx](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-811)*

[LiquidRon.sol#L293-L295](https://github.com/code-423n4/2025-01-liquid-ron/blob/e4b0b7c256bb2fe73b4a9c945415c3dcc935b61d/src/LiquidRon.sol#L293-L295)<br>
[LiquidRon.sol#L121-L126](https://github.com/code-423n4/2025-01-liquid-ron/blob/e4b0b7c256bb2fe73b4a9c945415c3dcc935b61d/src/LiquidRon.sol#L121-L126)

### Description

The fee accumulated by operator is stored in `operatorFeeAmount`. The amount is directly recorded based on the number of actual assets accumulated, not the portion of shares. The problem is, this fee is stored in the vault contract as WRON token balance together with the assets deposited by the users.

Because the calculation of `totalAssets()` will also depend on the WRON token balance owned by the vault contract, the fee withdrawn by the operator can decrease the total assets in circulation. It means that the users who withdraw their funds after the operator withdraw the fee will receive less assets than the users who withdraw before the fee withdrawal.

### Impact

Potential assets loss for the users who withdraw funds after operator withdraw the fee.

### Proof of Concept

To make things clear here, let's consider the following scenario. To make the scenario easier, just assume there is enough balance for the new user to withdraw.

1. The operator call `harvest()`. This will increase WRON balance owned by the vault and also increase `operatorFeeAmount`.
2. A new user deposit assets and receive shares. The calculation of `totalAssets()` will include the amount of operator's fee.
3. The operator withdraw the fee by calling `fetchOperatorFee()` function.
4. The new user withdraw his funds by calling `redeem()`. Now the user receives less assets because the calculation of `totalAssets()` will be based on the new WRON balance after fee withdrawal.

The detailed example:

**Initial state:**

```
totalBalance = 10000 // balance in all (vault, staked, rewards)
totalShares = s // just assume it is a variable `s` to make the calculation easier
operatorFeeAmount = 0
```

**Operator call `harvest()`:**

The state of vault now:

```
totalBalance = 10000 // the total balance is not changed, just the form is changed from rewards into actual WRON
totalShares = s
operatorFeeAmount = 10 // let's assume the operator get 10 units as fee
```

**New user deposit 100 units:**

The number of shares received by the new user:

`userShares = (100*totalShares)/totalBalance`<br>
`userShares = (100*s)/10000`<br>
`userShares = (1/100)s`<br>

The step above will increase the `totalShares`.

The state of vault now:

```
totalBalance = 10100 // including the deposit by new user
totalShares = s + s/100
operatorFeeAmount = 10
```

**Operator withdraws the fee:**

The state of vault now:

```
totalBalance = 10090 // total balance is decreased by 10 as operator withdraw the fee
totalShares = s + s/100
operatorFeeAmount = 0
```

**The user withdraw his funds:**

The assets received by the new user will be:

`userAsset = (userShares*totalBalance)/totalShares`<br>
`userAsset = ((s/100) * 10090)/(s + (s/100))`<br>
`userAsset = ((s/100) * 10090)/((101/100)s)`<br>
`userAsset = 10090/101`<br>
`userAsset = 99.9`<br>

After withdrawal, the new user will receive 99.9 units. The new user loss `0.1` units.

**POC Code**

Copy the POC code below to `LiquidRonTest` contract in `test/LiquidRon.t.sol` and then run the test.

```js
function test_withdraw_new_user() public {
        address user1 = address(0xf1);
        address user2 = address(0xf2);

        uint256 amount = 100000 ether;
        vm.deal(user1, amount);
        vm.deal(user2, amount);

        vm.prank(user1);
        liquidRon.deposit{value: amount}();

        uint256 delegateAmount = amount / 7;
        uint256[] memory amounts = new uint256[](5);
        for (uint256 i = 0; i < 5; i++) {
            amounts[i] = delegateAmount;
        }
        liquidRon.delegateAmount(0, amounts, consensusAddrs);

        skip(86400 * 365 + 2 + 1);
        // operator fee before harvest
        assertTrue(liquidRon.operatorFeeAmount() == 0);
        liquidRon.harvest(0, consensusAddrs);
        // operator fee after harvest
        assertTrue(liquidRon.operatorFeeAmount() > 0);

        // new user deposit
        vm.prank(user2);
        liquidRon.deposit{value: amount}();
        uint256 user2Shares = liquidRon.balanceOf(user2);
        uint256 expectedRedeemAmount = liquidRon.previewRedeem(user2Shares);

        // fee withdrawal by operator
        liquidRon.fetchOperatorFee();
        assertTrue(liquidRon.operatorFeeAmount() == 0);

        // user2 redeem all his shares
        vm.prank(user2);
        liquidRon.redeem(user2Shares, user2, user2);

        console.log(user2.balance);
        console.log(expectedRedeemAmount);
        assertTrue(user2.balance == expectedRedeemAmount);
    }
```

Based on the POC code above, the last assertion `assertTrue(user2.balance == expectedRedeemAmount);` will fail because the amount withdrawn is not equal to the expected withdrawn.

### Recommended Mitigation Steps

Change the formula that calculate `totalAssets()` to include `operatorFeeAmount` to subtract the total balance.

```diff
function totalAssets() public view override returns (uint256) {
-        return super.totalAssets() + getTotalStaked() + getTotalRewards();
+        return super.totalAssets() + getTotalStaked() + getTotalRewards() - operatorFeeAmount;
    }
```

**[Owl (Liquid Ron) confirmed and commented via duplicate issue S-174](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-174):**
> A simpler fix would be to include `operationFeeAmount` in total assets like such:
> ```sol
>     function totalAssets() public view override returns (uint256) {
>         return super.totalAssets() + getTotalStaked() + getTotalRewards() - operationFeeAmount;
>     }
> ```

**[0xsomeone (judge) increased severity to High and commented via duplicate issue S-174](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-174):**
> The finding and its duplicates outline that the accumulated operator fee is factored in total asset calculations despite being meant to be redeemed as a fee.
>
> Apart from contradicting the EIP-4626 standard, it allows the operator fee to be redeemed by users, undervalues deposits made when a non-zero operator fee exists, and abruptly reduces the total assets whenever the operator fee is claimed.
>
> I believe the consistent dilution of all incoming deposits whenever a non-zero operator fee is present to be a significant issue and one that would merit a high severity rating. Specifically:
> 
> - The vulnerability is consistently present whenever an operator fee is realized (i.e. `operatorFeeAmount` is non-zero) - Likelihood of High.
> - The impact of the vulnerability is significant as it devalues all incoming user deposits whenever a non-zero fee is present and can also result in the `operatorFeeAmount` becoming irredeemable in extreme circumstances (i.e. total withdrawal of vault) - Impact of Medium.
>
> Combining the likelihood and impact traits above, I believe that a severity level of high is better suited for this issue.

**[Liquid Ron mitigated](https://github.com/code-423n4/2025-02-liquid-ron-mitigation?tab=readme-ov-file#mitigation-of-high--medium-severity-issues):**
> Add `operatorFeeAmount` in `totalAssets` calculations.

**Status:** Mitigation confirmed. Full details in reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-1), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-32), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-11).


***

# Medium Risk Findings (2)

## [[M-01] User can earn rewards by frontrunning the new rewards accumulation in Ron staking without actually delegating his tokens](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-10)
*Submitted by [Aamir](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1252), also found by [0rpse](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1070), [0x0dd](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-366), [0xrex](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-631), [gesha17](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-352), [ilchovski](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1171), [KupiaSec](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-783), and [spuriousdragon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1056)*

[LiquidProxy.sol#L39](https://github.com/OwlOfMoistness/liquid_ron/blob/b9b462cb1f8554796b78ad81a935dbce19cce0c5/src/LiquidProxy.sol#L39)

### Finding Description and Impact

The Ron staking contract let us earn rewards by delegating our tokens to a validator. But you will only earn rewards on the lowest balance of the day ([source](https://docs.roninchain.com/protocol/delegators/claim-rewards#:~:text=Your%20rewards%20are,in%20your%20stake.)). So if you delegate your tokens on the first day, you are going to earn 0 rewards for that day as your lowest balance was 0 on that day. This will happens with every new delegator.

Now the issue with `LiquidRon` is that, there will be many users who will be depositing their tokens in it. And there is no such kind of time or amount restriction for new delegators if some people have already delegated before them. So with direct delegation, the new rewards flow will be this:

```
User -> delegate -> RonStaking -> Wait atleast a day -> New Rewards
```

But if we deposit through `LiquidRon` it has become this:

```
User -> LiquidRon -> LiquidProxy -> New Rewards
```

Now a user can earn rewards by just depositing the tokens into the `LiquidRon` by frontrunning the new rewards arrival and immediately withdraw them. But if a user try to do this by frontrunning the `LiquidRon::harvest(...)` call, this will not be possible. Because when he deposits, he will get shares in return which will already be accounting for any unclaimed rewards through `getTotalRewards(...)` in `LiqiuidRon::totalAssets(...)`:

```solidity
    function totalAssets() public view override returns (uint256) {
@>        return super.totalAssets() + getTotalStaked() + getTotalRewards();
    }
```

But instead of frontrunning this `harvest(...)` call, a user can just frontrun the new rewards arrival in the `RonStaking` contract itself. Because as per the Ronin staking docs, a user will be able to claim new rewards after every 24 hours.

Also, if we look at the `_getReward(...)` (used by claimRewards etc.) function of the Ronin staking contract, the rewards will be same as before as long as we are not in new period: 

```solidity
  function _getReward(
    address poolId,
    address user,
    uint256 latestPeriod,
    uint256 latestStakingAmount
  ) internal view returns (uint256) {
    UserRewardFields storage _reward = _userReward[poolId][user];

@>    if (_reward.lastPeriod == latestPeriod) {
@>      return _reward.debited;
    }
```

Github: [Link](https://github.com/ronin-chain/dpos-contract/blob/348e2e364fb9d63faa116dd61ea71a1161578fd7/contracts/ronin/staking/RewardCalculation.sol#L55C1-L65C6)

So if a user frontrun before this, the `getTotalRewards(...)` function will also not account for new rewards as long as we are not in new period.

Also note that, if a user frontruns and deposit, he didn't not actually delegated his tokens as the tokens are only delegated once the operator calls `LiquidRon::delegateAmount(...)` function:

```solidity
    function delegateAmount(uint256 _proxyIndex, uint256[] calldata _amounts, address[] calldata _consensusAddrs)
        external
        onlyOperator
        whenNotPaused
    {
        address stakingProxy = stakingProxies[_proxyIndex];
        uint256 total;

        if (stakingProxy == address(0)) revert ErrBadProxy();
        // @audit how many max validators can be there?
        for (uint256 i = 0; i < _amounts.length; i++) {
            if (_amounts[i] == 0) revert ErrNotZero();
            _tryPushValidator(_consensusAddrs[i]);
            total += _amounts[i];
        }
@>        _withdrawRONTo(stakingProxy, total);
@>        ILiquidProxy(stakingProxy).delegateAmount(_amounts, _consensusAddrs);
    }
```

So a user is just depositing, claiming and withdrawing his tokens but not actually delegating.

The following attack can be summarized like this:

1. There are currently millions of delegated tokens deposited into the `LiquidRon` which are delegated to many validators through `LiquidProxy`. And each day the `LiquidRon` is earning let's 1000 tokens as a reward.
2. But these rewards are only claimable in the new epoch. 
3. So a user keeps an eye on the new rewards arrival into the RonStaking for the `LiquidRon` and also on the new epoch update.
4. Once rewards are arrived he waits for the epoch update, and frontruns this epoch update and deposits into the `LiquidRon`.
5. Once this new epoch is updated, these new rewards will be starting to reflect into the the share price through `LiquidRon::totalAssets(...)`.
6. User withdraws immediately with the profit.

In the above case, the user didn't have to stake his tokens and still earns the share of the rewards. Also, this can be done each and every time to claim the rewards.

He also didn't have to bear any risk of loss in case something bad happens (maybe some kind of attack) and the share price value goes down; while others will also have to bear this loss.

### Recommended Mitigation Steps

Incorporate some kind of locking mechanism for new depositor like Ron staking contract does. Or, go for some alternate option.

**[Owl (Liquid Ron) confirmed and commented](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-10?commentParent=P9i7NzFyfP8):**
> Vampire attack as I like to call it. 
>
> Valid finding, definitely need to think of a viable mitigation solution. For now, adding a deposit fee seems the best solution I have found (deposit fee would be equivalent to 1 day worth of reward expected based on amount deposited).

**[0xsomeone (judge) commented](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-10?commentParent=bTmqobbjBFN):**
> The finding and its duplicates outline a valid attack path via which users are able to arbitrage upcoming reward updates to capture the rewards without actually staking their assets for a long period of time in the system.
> 
> I believe a medium-severity rating is justifiable, and mitigation for the vulnerability outlined will be hard to implement properly unless a simplistic measure such as a deposit fee is implemented. Alternatives would be to finalize deposits via operators or permit deposits to occur within a predefined time window of a reward issuance, ensuring new deposits are finalized after a reward update has occurred recently.

**[Liquid Ron mitigated](https://github.com/code-423n4/2025-02-liquid-ron-mitigation?tab=readme-ov-file#mitigation-of-high--medium-severity-issues):**
> Add a deposit fee that can be reset every period based on daily expected rewards.

**Status:** Mitigation confirmed. Full details in report from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-50).


***

## [[M-02] Operators are unable to perform any actions due to incorrect modifier implementation](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-23)
*Submitted by [zanderbyte](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-41), also found by [056Security](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-317), [0rpse](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-966), [0x0107](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-19), [0x0bserver](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1049), [0x0dd](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-303), [0x11singh99](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1032), [0x23r0](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-94), [0xAadi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-333), [0xAkira](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-901), [0xAlipede](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-162), [0xAsen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-151), [0xastronatey](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-350), [0xauditagent](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-741), [0xaudron](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-482), [0xAura](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1074), [0xfocusNode](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-886), [0xhuh2005](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1127), [0xiehnnkta](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-45), [0xLeveler](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1045), [0xMosh](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-330), [0xmujahid002](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-595), [0xnolo](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-584), [0xodus](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-969), [0xRajkumar](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-804), [0xrex](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-13), [0xterrah](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1025), [0xvd](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-914), [13u9](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-752), [4rdiii](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-208), [Aamir](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-466), [aariiif](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-59), [Adotsam](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-954), [Afriauditor](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1142), [Agontuk](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1069), [air\_0x](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-725), [Albort](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1010), [anonymousjoe](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1073), [arman](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1245), [aua\_oo7](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1079), [AvantGard](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1020), [axelot](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1194), [backboard9654](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-504), [Banditx0x](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-177), [bani](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-538), [Bauchibred](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-294), [Bbash](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-437), [Bluedragon101](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-614), [brevis](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-117), [BRONZEDISC](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-571), [BroRUok](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-717), [Bz](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-606), [ccvascocc](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-274), [ChainSentry](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-216), [Cli7max](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-838), [CrazyMoose](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-460), [crmx\_lom](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-748), [csanuragjain](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-320), [cylzxje](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1144), [CyXq](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-137), [d4r3d3v1l](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-522), [Daniel\_eth](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-356), [Daniel526](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-35), [dd0x7e8](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-815), [debo](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-104), [Dec3mber](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-828), [DemoreX](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-809), [den-sosnowsky](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-720), [dexcripter](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-307), [DharkArtz](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1023), [DoD4uFN](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-435), [dreamcoder](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-153), [edwardmintel](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1152), [ElCid](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-845), [elolpuer](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-249), [eLSeR17](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-148), [EPSec](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-675), [erictee](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-958), [eternal1328](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-445), [ewwrekt](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1159), [Falendar](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-62), [federodes](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-735), [Flare](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-339), [francoHacker](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1168), [fromeo\_016](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-189), [gesha17](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-247), [gregom](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-750), [gxh191](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-337), [HardlyDifficult](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-354), [harry\_cryptodev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-505), [HChang26](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-306), [holydevoti0n](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-166), [honey-k12](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1062), [hrmneffdii](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-550), [hyuunn](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-254), [IceBear](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-773), [ilchovski](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-975), [importDev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-340), [Incogknito](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-577), [inh3l](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-734), [interestingTimes](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-240), [itsabinashb](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-217), [JakeFromStateFarm](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-252), [JCN](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-25), [jesusrod15](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-968), [jkk812812](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-952), [Josh4324](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-997), [ka14ar](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-451), [Kalogerone](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-367), [Kek](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-666), [King\_9aimon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-994), [klau5](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-891), [KupiaSec](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-770), [kutugu](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-599), [Lamsy](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-187), [levi\_104](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-158), [linemi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-169), [LLakterian](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-23), [LonelyWolfDemon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-949), [Maglov](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-935), [mahdifa](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1238), [Mahi\_Vasisth](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-638), [marwen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-540), [miaowu](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-122), [mtberi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-977), [muellerberndt](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-134), [MukulKolpe](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1191), [muncentu](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-802), [mxteem](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1195), [N0nce](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-50), [newspacexyz](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-537), [NexusAudits](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-821), [nnez](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-409), [noured23](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-21), [oakcobalt](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-669), [octeezy](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-724), [ok567](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1121), [Olugbenga](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1254), [oxelmiguel12](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1189), [p\_crypt0](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-20), [peanuts](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1232), [persik228](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1149), [pfapostol](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-780), [phoenixV110](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-125), [Prestige](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-450), [pulse](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1000), [PumpkingWok](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-213), [Punith](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-864), [queen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-142), [RaOne](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-43), [rare\_one](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-716), [rbserver](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1204), [Rhaydden](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-357), [Riceee](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-915), [rishab](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-810), [robertauditor](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-858), [Rolando](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-272), [rudhra](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-69), [Ryonen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-198), [sabanaku77](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-799), [safie](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-180), [sajeevan\_58356](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-795), [Samueltroydomi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-101), [seerether](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-963), [serial-coder](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1175), [Shahil\_Hussain](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-892), [shaka](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-578), [Shinobi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-737), [Shipkata494](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-257), [silver\_eth](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-491), [sl1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-646), [SmartAuditPro](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-11), [sohrabhind](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-774), [Sparrow](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1153), [spuriousdragon](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1048), [stuart\_the\_minion](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-171), [t0x1c](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-28), [tachida2k](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-342), [Tadev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-164), [Tamer](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-635), [teoslaf](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-227), [Tiannah](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1156), [Tigerfrake](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-168), [Timeless](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-256), [tonitonitoni](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-689), [Topmark](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-79), [tpiliposian](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-594), [Trepid](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-731), [typicalHuman](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-553), [udo](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1060), [udogodwin](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-926), [Udsen](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1085), [unique](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-808), [unnamed](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-383), [vahdrak1](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-124), [verboten\_viking](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-645), [victortheoracle](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-937), [vladi319](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-181), [vulkan\_xx](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-384), [wellbyt3](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-967), [Xcrypt](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1099), [XDZIBECX](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-545), [YouCrossTheLineAlfie](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-374), [Z-bra](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-395), [zraxx](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-419), [zubyoz](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-223), and [ZZhelev](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-687)*

[LiquidRon.sol#L91](https://github.com/code-423n4/2025-01-liquid-ron/blob/e4b0b7c256bb2fe73b4a9c945415c3dcc935b61d/src/LiquidRon.sol#L91)

### Finding Description and Impact

The `onlyOperator` modifier in `LiquidRon` contract is intended to restrict access to specific functions to either the `owner` or `operator`. Functions like `harvest`, `delegateAmount`, and `harvestAndDelegateRewards` rely on this modifier for access control.  

However, the modifier implementation is incorrect and will always revert when called by any address other than the owner, even if the caller is a valid operator. As a result, operators are completely unable to perform any of their intended actions.

As we can see, if `msg.sender` is not the owner, the first condition evaluates to true, triggering a revert. Even if we ignore the first condition, when an operator calls a function using this modifier, `operator[msg.sender]` evaluates to true, causing the revert to be triggered again.

```solidity
    /// @dev Modifier to restrict access of a function to an operator or owner
    modifier onlyOperator() {
        if (msg.sender != owner() || operator[msg.sender]) revert ErrInvalidOperator();
        _;
    }
```

### Proof of Concept

Paste the following test in `LquidRon.operator.t.sol`:

```solidity
    function test_wronModifierIImplementation() public {
        address operator = makeAddr("operator");
        liquidRon.updateOperator(operator, true);

        assertTrue(liquidRon.operator(operator));

        vm.startPrank(operator);
        vm.expectRevert(LiquidRon.ErrInvalidOperator.selector);
        liquidRon.harvest(1, consensusAddrs);
    }
```

### Recommended Mitigation Steps

The modifier should revert only if the `msg.sender` is neither the owner nor an operator:

```diff
    /// @dev Modifier to restrict access of a function to an operator or owner
    modifier onlyOperator() {
-       if (msg.sender != owner() || operator[msg.sender]) revert ErrInvalidOperator();
+       if (msg.sender != owner() && !operator[msg.sender]) revert ErrInvalidOperator();
        _;
    }
```

**[Owl (Liquid Ron) confirmed and commented](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-23?commentParent=pfQ2wL54gWV):**
> I agree that the finding is valid, I simply wonder if the severity is justified. 
>
> The modifier doesn't permit for anyone to call the operator functions, which for me is a high severity. With this reasoning, the finding could be of medium severity as workarounds external to the contract are possible (owner is a contract with actual correct usage of the operator finding if such code was live).

**[0xsomeone (judge) decreased severity to Medium and commented](https://code4rena.com/audits/2025-01-liquid-ron/submissions/F-23?commentParent=yXrLNTLtpkL):**
> The submission details an incorrect code implementation that effectively increases the level of access control for functions that utilize the `onlyOperator` modifier as operators are not able to access those functions and the owner is the only one capable of invoking them.
> 
> I believe that such a finding does not result in a material vulnerability and instead falls under the "self-evident code mistake" clause of the relevant Supreme Court verdicts. In such instances, mistakes in code that are clear yet do not result in a significant vulnerability would be considered medium severity and I consider this approach to apply here, thus downgrading the issue to medium severity.

**[Liquid Ron mitigated](https://github.com/code-423n4/2025-02-liquid-ron-mitigation?tab=readme-ov-file#mitigation-of-high--medium-severity-issues):**
> Bad operator modifer.

**Status:** Mitigation confirmed. Full details in reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-2), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-33), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-12).


***

# Low Risk and Non-Critical Issues

For this audit, 17 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-304) by **IlIlHunterlIlI** received the top score from the judge.

*The following wardens also submitted reports: [0x23r0](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-536), [0xAadi](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-908), [0xodus](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1103), [0xrex](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-496), [atoko](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-596), [Bauchibred](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-296), [Bigsam](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-775), [Daniel526](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-36), [inh3l](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1018), [K42](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-736), [Kalogerone](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-603), [magiccentaur](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-618), [pfapostol](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-798), [rbserver](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1241), [Rhaydden](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-363), and [Sparrow](https://code4rena.com/audits/2025-01-liquid-ron/submissions/S-1269).*

## Summary

| ID   | Title                                                                           |
| ----- | ------------------------------------------------------------------------------- |
| [01] | Risk `Out-Of-Gas` reverts during deposit and withdraw in reasonable circumstances |
| [04]&nbsp; | Some users can deposit but can never withdraw                                   |

*Note: findings `02` (redundant with H-01) and `03` (judged invalid) from IlIlHunterlIlI's submission have been omitted from this section of the report. The original numbering has been kept for ease of reference.*

## [01] Risk `Out-Of-Gas` reverts during deposit and withdraw in reasonable circumstances

The `totalAssets()` function in `LiquidRon.sol` iterates over all staking proxies and consensus addresses to calculate the total assets controlled by the contract. This function is called during critical operations such as deposits and withdrawals. However, if the number of staking proxies or consensus addresses is large, the function can consume excessive gas, potentially exceeding the Ethereum block gas limit (30M gas). This can lead to out-of-gas (OOG) reverts, rendering the contract unusable for deposits and withdrawals in high-scale scenarios.

The most reasonable numbers I could come across are 60 validator and 100 staking proxy deployed: 
- While this seems large:
   - The nature of staking protocols usually involve more than 100 validators.
   - If the TVL of the LiquidRonin is increasing and multiple user interactions are happening daily, they will need to deploy more proxies.
- The above two points make the bug more likely to rise.
  
### Impact

- **Denial of Service (DoS)**: If `totalAssets()` reverts due to OOG, users will be unable to deposit or withdraw funds, effectively freezing the contract temporarily till the operator claim and undelegate from number of operators to delete some them to decrease the iteration numbers on consensus adresses.
- **Scalability issues**: The contract cannot handle a large number of staking proxies or consensus addresses, limiting its scalability.
- **User funds at risk**: If withdrawals are blocked due to OOG reverts, users may be unable to access their funds. (same as first point).

### Proof of Concept

Paste this in `LiquidRon.t.sol`:

```solidity
    function test_totalAssets_OOG() public {
    // Deploy multiple staking proxies
    uint256 proxyCount = 100; // Adjust this number to test different scenarios
    for (uint256 i = 0; i < proxyCount; i++) {
        liquidRon.deployStakingProxy();
    }

    // Add a large number of consensus addresses
    uint256 consensusCount = 60; // Adjust this number to test different scenarios
    address[] memory consensusAddrs = new address[](consensusCount);
    for (uint256 i = 0; i < consensusCount; i++) {
        consensusAddrs[i] = address(uint160(i + 1)); // Generate unique addresses
    }

    // Deposit some RON to initialize the system
    uint256 depositAmount = 1000000000000000000000000000000 ether;

    deal(address(this), depositAmount * 10);
    
    liquidRon.deposit{value: depositAmount * 10}();

    // Delegate amounts to consensus addresses
    uint256[] memory amounts = new uint256[](consensusCount);
    for (uint256 i = 0; i < consensusCount; i++) {
        amounts[i] = 1;
    }
    for (uint256 i = 0; i < proxyCount; i++) {
        liquidRon.delegateAmount(i, amounts, consensusAddrs);
    }

    // Call totalAssets() and check for OOG reverts
    uint256 blockGasLimit = 30_000_000;
    uint256 totalAssets;
    // passing the block gas limit as a parameter to simulate a real environment block limit
    try liquidRon.totalAssets{gas: blockGasLimit}() returns (uint256 _totalAssets) {
        totalAssets = _totalAssets;
    } catch {
        revert("OOG in totalAssets()");
    }

    // Assert that totalAssets is greater than 0
    assertTrue(totalAssets > 0, "totalAssets should be greater than 0");
}
```

The test fails with an `OutOfGas` error, demonstrating that `totalAssets()` consumes excessive gas and reverts when the number of staking proxies and consensus addresses is large.

### Recommended Mitigation Steps

1. **Optimize `totalAssets()` function**:

- **Cache results**: Cache the results of expensive operations (e.g., staked amounts and rewards) to avoid recalculating them on every call.
- **Batch processing**: Process staking proxies and consensus addresses in batches to reduce gas consumption per transaction.
- **Off-chain calculation**: Use an off-chain service to calculate total assets and provide the result to the contract via a trusted oracle.

2. **Limit the number of proxies and consensus addresses**:

- **Enforce limits**: Set a maximum limit on the number of staking proxies and consensus addresses that can be added to the contract.
- **Prune inactive addresses**: Regularly prune inactive consensus addresses to reduce the number of iterations in `totalAssets()`.

## [04] Some users can deposit but can never withdraw

In `LiquidRon`, the contract allow users to `deposit()` or `mint()` using the `wRON` token, but during `withdraw()` or `burn()` users are forced to receive native `RON` or the txn will revert:
- This is a problem cause the depositor may have been a contract that doesn't implement `receive()` or payable functions.
- The depositor may have been a protocol that is building on top of `liquidRon` too.

This makes the above two cases to never be able to get back any tokens and have their funds stuck.

### Proof of Concept

1. A contract not having receive or payable functions deposit in `liquidRon` using `wRON`.
2. Time passes and he wants to withdraw.
3. Any call to `withdraw()` or `redeem()` will revert during `_withdrawRONTo()` call.

```solidity
File: RonHelper.sol
38:     function _withdrawRONTo(address to, uint256 amount) internal {
39:         IWRON(wron).withdraw(amount);
40:         (bool success, ) = to.call{value: amount}("");
41:         if (!success) revert ErrWithdrawFailed();
42:     }
```

4. Funds are stuck forever.

### Recommended Mitigation Steps

Wrap the native call that if failed, wrap the native tokens and send them to the receiver as `wRON`.


***

# [Mitigation Review](#mitigation-review)

## Introduction

Following the C4 audit, 3 wardens ([Aamir](https://code4rena.com/@Aamir), [ilchovski](https://code4rena.com/@ilchovski), and [0rpse](https://code4rena.com/@0rpse)) reviewed the mitigations implemented by the Liquid Ron team. Additional details can be found within the [C4 Liquid Ron Mitigation Review repository](https://github.com/code-423n4/2025-02-liquid-ron-mitigation).

## Mitigation Review Scope

### Branch
- Branch: https://github.com/OwlOfMoistness/liquid_ron/tree/ca4-mitigation
- Commits: https://github.com/OwlOfMoistness/liquid_ron/compare/main...ca4-mitigation

### Mitigation of High & Medium Severity Issues
| Mitigation | Mitigation<br>of | Purpose | 
| --------- | --------------- | ----------- |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/c30c35b1b5a4adcc46f1d20506a9816f1fec275c) | H&#8209;01<br>(aka&nbsp;F&#8209;3) | Add operatorFeeAmount in totalAssets calculations | 
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/3eb49f91241ef3bf1c8bedda4180ac1c36e80995) | M&#8209;01<br>(aka&nbsp;F&#8209;10) | Add a deposit fee that can be reset every period based on daily expected rewards | 
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/af83a41854f38a7defef97dde2e8a5a97a0f13d1) | M&#8209;02<br>(aka&nbsp;F&#8209;23) | Bad operator modifer | 

### Additional Scope to be Reviewed
These are additional changes that were in scope.

| Mitigation | RefID | Purpose | 
| --------- | --------------- | ----------- |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/14fd27de293430d97aab2b5fe746d2513426dc05) | FX-1&ast; | Update flow of withdrawal to add changeable receiver |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/0d4844c9697a9365760c7eb1673f5e51c37281b2) | F-25 | Replace validator data storage from consensus addresses to IDs which never change |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/ea748e02c9dbf700d24e28db1fb9a586ffc24c87) | F-2 | Add start index to start loop on specif validator and length of computation |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/15ef42af4bd5391b43824b262affe605176b3aa4) | F-45 | QA, remove unused mapping |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/c3b19f0c0ffb5a9cfbf56859a35e3e672bf0cb0d) | F-32 | Fix wrong event emission |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/1780ebde0ec92c1c9523dd56bb72960ef8f9f169) | F-156 | Clear validator Index when removing it |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/af2165659f4c721e9caa91df8f69db4859360955) | F-22 | Remove for loop |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/64a6dfed2ba5691a492883b1efe60f5b7814690e) | F-1 | Prevent native deposits when paused |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/e275282e9365e7b2e0295c464d69197f272c0338) | S&#8209;736:<br>Low&#8209;4&ast;&ast;| Improve getTotalStaked() to prevent recomputing state each call by tracking internally |
| [Link&nbsp;1](https://github.com/OwlOfMoistness/liquid_ron/commit/08cf347939feafca4681469a2a33606ca826c055),<br>[Link&nbsp;2](https://github.com/OwlOfMoistness/liquid_ron/commit/415665dcd7b8cac90b3540c90c3bc32ceaec9121) | ADD-01 | QAs: getValidator func, payable withdraw ron, remove _checkIfPaused, immutable proxy var, check src/dst in proxy, remove dead code, deposit payable has receiver param |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/be97c210ae421bc0e9a5147c2ede584caea0bb53) | ADD&#8209;02 | Fix test |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/354c741e989f5d27a2f55b68b190a7fc71b26135) | ADD&#8209;03 | Add forge lib |
| [Link](https://github.com/OwlOfMoistness/liquid_ron/commit/017f2bb1e2d7de54726969529eec1f3be9cc4329) | ADD&#8209;04 | Add periodStartVariable for external data tracking |

&ast;*`FX-1` represents multiple findings from the initial audit: F-18, F-17, and F-27. These have all been fixed by omitting the `_checkUserCanReceiveRon` implementation and replacing it with the capability to specify a different `receiver` when performing withdrawal requests as well as deposits.*

&ast;&ast;*Commit title incorrectly mentions `S-726`.*

## Mitigation Review Summary

During the review, all in-scope mitigations were confirmed, and no new high- or medium-risk issues were discovered by the wardens. The table below provides further detail.

| Original Issue | Status | Full Details |
| ----------- | ------------- | ----------- |
| H&#8209;01&nbsp;(F&#8209;3) | 🟢 Mitigation Confirmed | Reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-1), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-32), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-11) |
| M&#8209;01&nbsp;(F&#8209;10) | 🟢 Mitigation Confirmed | Report from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-50) |
| M-02&nbsp;(F-23) | 🟢 Mitigation Confirmed | Reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-2), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-33), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-12) |
| FX-1 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-43), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-20), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-8) |
| F-25 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-35), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-14), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-49) |
| F-2 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-34), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-13), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-3) |
| F-45 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-47), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-15), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-5) |
| F-32 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-46), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-16), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-4) |
| F-156 | 🟢 Mitigation Confirmed | Reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-6), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-42), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-17) |
| F-22 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-45), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-18), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-7) |
| F-1 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-41), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-19), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-9) |
| S&#8209;736:&nbsp;Low&#8209;4| 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-37), [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-21), and [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-10) |
| ADD-01 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-36), [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-48), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-22) |
| ADD-02 | 🟢 Mitigation Confirmed | Reports from [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-27), [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-38), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-23) |
| ADD-03 | 🟢 Mitigation Confirmed | Reports from [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-39), [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-44), and [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-24) |
| ADD-04 | 🟢 Mitigation Confirmed | Reports from [ilchovski](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-25), [Aamir](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-26), and [0rpse](https://code4rena.com/audits/2025-02-liquid-ron-mitigation-review/submissions/S-40) |


***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.

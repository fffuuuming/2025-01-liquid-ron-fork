# Report

- [Report](#report)
  - [Gas Optimizations](#gas-optimizations)
    - [\[GAS-1\] `a = a + b` is more gas effective than `a += b` for state variables (excluding arrays and mappings)](#gas-1-a--a--b-is-more-gas-effective-than-a--b-for-state-variables-excluding-arrays-and-mappings)
    - [\[GAS-2\] Use assembly to check for `address(0)`](#gas-2-use-assembly-to-check-for-address0)
    - [\[GAS-3\] Using bools for storage incurs overhead](#gas-3-using-bools-for-storage-incurs-overhead)
    - [\[GAS-4\] Cache array length outside of loop](#gas-4-cache-array-length-outside-of-loop)
    - [\[GAS-5\] State variables should be cached in stack variables rather than re-reading them from storage](#gas-5-state-variables-should-be-cached-in-stack-variables-rather-than-re-reading-them-from-storage)
    - [\[GAS-6\] For Operations that will not overflow, you could use unchecked](#gas-6-for-operations-that-will-not-overflow-you-could-use-unchecked)
    - [\[GAS-7\] Use Custom Errors instead of Revert Strings to save Gas](#gas-7-use-custom-errors-instead-of-revert-strings-to-save-gas)
    - [\[GAS-8\] Avoid contract existence checks by using low level calls](#gas-8-avoid-contract-existence-checks-by-using-low-level-calls)
    - [\[GAS-9\] Stack variable used as a cheaper cache for a state variable is only used once](#gas-9-stack-variable-used-as-a-cheaper-cache-for-a-state-variable-is-only-used-once)
    - [\[GAS-10\] State variables only set in the constructor should be declared `immutable`](#gas-10-state-variables-only-set-in-the-constructor-should-be-declared-immutable)
    - [\[GAS-11\] Functions guaranteed to revert when called by normal users can be marked `payable`](#gas-11-functions-guaranteed-to-revert-when-called-by-normal-users-can-be-marked-payable)
    - [\[GAS-12\] `++i` costs less gas compared to `i++` or `i += 1` (same for `--i` vs `i--` or `i -= 1`)](#gas-12-i-costs-less-gas-compared-to-i-or-i--1-same-for---i-vs-i---or-i---1)
    - [\[GAS-13\] Using `private` rather than `public` for constants, saves gas](#gas-13-using-private-rather-than-public-for-constants-saves-gas)
    - [\[GAS-14\] Increments/decrements can be unchecked in for-loops](#gas-14-incrementsdecrements-can-be-unchecked-in-for-loops)
  - [Non Critical Issues](#non-critical-issues)
    - [\[NC-1\] Missing checks for `address(0)` when assigning values to address state variables](#nc-1-missing-checks-for-address0-when-assigning-values-to-address-state-variables)
    - [\[NC-2\] `constant`s should be defined rather than using magic numbers](#nc-2-constants-should-be-defined-rather-than-using-magic-numbers)
    - [\[NC-3\] Control structures do not follow the Solidity Style Guide](#nc-3-control-structures-do-not-follow-the-solidity-style-guide)
    - [\[NC-4\] Consider disabling `renounceOwnership()`](#nc-4-consider-disabling-renounceownership)
    - [\[NC-5\] Function ordering does not follow the Solidity style guide](#nc-5-function-ordering-does-not-follow-the-solidity-style-guide)
    - [\[NC-6\] Functions should not be longer than 50 lines](#nc-6-functions-should-not-be-longer-than-50-lines)
    - [\[NC-7\] Interfaces should be defined in separate files from their usage](#nc-7-interfaces-should-be-defined-in-separate-files-from-their-usage)
    - [\[NC-8\] Lack of checks in setters](#nc-8-lack-of-checks-in-setters)
    - [\[NC-9\] Missing Event for critical parameters change](#nc-9-missing-event-for-critical-parameters-change)
    - [\[NC-10\] NatSpec is completely non-existent on functions that should have them](#nc-10-natspec-is-completely-non-existent-on-functions-that-should-have-them)
    - [\[NC-11\] Incomplete NatSpec: `@param` is missing on actually documented functions](#nc-11-incomplete-natspec-param-is-missing-on-actually-documented-functions)
    - [\[NC-12\] Incomplete NatSpec: `@return` is missing on actually documented functions](#nc-12-incomplete-natspec-return-is-missing-on-actually-documented-functions)
    - [\[NC-13\] Use a `modifier` instead of a `require/if` statement for a special `msg.sender` actor](#nc-13-use-a-modifier-instead-of-a-requireif-statement-for-a-special-msgsender-actor)
    - [\[NC-14\] Consider using named mappings](#nc-14-consider-using-named-mappings)
    - [\[NC-15\] Owner can renounce while system is paused](#nc-15-owner-can-renounce-while-system-is-paused)
    - [\[NC-16\] Take advantage of Custom Error's return value property](#nc-16-take-advantage-of-custom-errors-return-value-property)
    - [\[NC-17\] Contract does not follow the Solidity style guide's suggested layout ordering](#nc-17-contract-does-not-follow-the-solidity-style-guides-suggested-layout-ordering)
    - [\[NC-18\] Use Underscores for Number Literals (add an underscore every 3 digits)](#nc-18-use-underscores-for-number-literals-add-an-underscore-every-3-digits)
    - [\[NC-19\] Internal and private variables and functions names should begin with an underscore](#nc-19-internal-and-private-variables-and-functions-names-should-begin-with-an-underscore)
    - [\[NC-20\] Event is missing `indexed` fields](#nc-20-event-is-missing-indexed-fields)
    - [\[NC-21\] `public` functions not called by the contract should be declared `external` instead](#nc-21-public-functions-not-called-by-the-contract-should-be-declared-external-instead)
    - [\[NC-22\] Variables need not be initialized to zero](#nc-22-variables-need-not-be-initialized-to-zero)
  - [Low Issues](#low-issues)
    - [\[L-1\] `approve()`/`safeApprove()` may revert if the current approval is not zero](#l-1-approvesafeapprove-may-revert-if-the-current-approval-is-not-zero)
    - [\[L-2\] Use a 2-step ownership transfer pattern](#l-2-use-a-2-step-ownership-transfer-pattern)
    - [\[L-3\] Some tokens may revert when zero value transfers are made](#l-3-some-tokens-may-revert-when-zero-value-transfers-are-made)
    - [\[L-4\] Missing checks for `address(0)` when assigning values to address state variables](#l-4-missing-checks-for-address0-when-assigning-values-to-address-state-variables)
    - [\[L-5\] Empty `receive()/payable fallback()` function does not authenticate requests](#l-5-empty-receivepayable-fallback-function-does-not-authenticate-requests)
    - [\[L-6\] External call recipient may consume all transaction gas](#l-6-external-call-recipient-may-consume-all-transaction-gas)
    - [\[L-7\] Prevent accidentally burning tokens](#l-7-prevent-accidentally-burning-tokens)
    - [\[L-8\] Owner can renounce while system is paused](#l-8-owner-can-renounce-while-system-is-paused)
    - [\[L-9\] Loss of precision](#l-9-loss-of-precision)
    - [\[L-10\] Solidity version 0.8.20+ may not work on other chains due to `PUSH0`](#l-10-solidity-version-0820-may-not-work-on-other-chains-due-to-push0)
    - [\[L-11\] Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership`](#l-11-use-ownable2steptransferownership-instead-of-ownabletransferownership)
    - [\[L-12\] Unsafe ERC20 operation(s)](#l-12-unsafe-erc20-operations)
  - [Medium Issues](#medium-issues)
    - [\[M-1\] Contracts are vulnerable to fee-on-transfer accounting-related issues](#m-1-contracts-are-vulnerable-to-fee-on-transfer-accounting-related-issues)
    - [\[M-2\] Centralization Risk for trusted owners](#m-2-centralization-risk-for-trusted-owners)
      - [Impact](#impact)
    - [\[M-3\] Return values of `transfer()`/`transferFrom()` not checked](#m-3-return-values-of-transfertransferfrom-not-checked)
    - [\[M-4\] Unsafe use of `transfer()`/`transferFrom()`/`approve()`/ with `IERC20`](#m-4-unsafe-use-of-transfertransferfromapprove-with-ierc20)

## Gas Optimizations

| |Issue|Instances|
|-|:-|:-:|
| [GAS-1](#GAS-1) | `a = a + b` is more gas effective than `a += b` for state variables (excluding arrays and mappings) | 10 |
| [GAS-2](#GAS-2) | Use assembly to check for `address(0)` | 1 |
| [GAS-3](#GAS-3) | Using bools for storage incurs overhead | 3 |
| [GAS-4](#GAS-4) | Cache array length outside of loop | 12 |
| [GAS-5](#GAS-5) | State variables should be cached in stack variables rather than re-reading them from storage | 4 |
| [GAS-6](#GAS-6) | For Operations that will not overflow, you could use unchecked | 46 |
| [GAS-7](#GAS-7) | Use Custom Errors instead of Revert Strings to save Gas | 1 |
| [GAS-8](#GAS-8) | Avoid contract existence checks by using low level calls | 1 |
| [GAS-9](#GAS-9) | Stack variable used as a cheaper cache for a state variable is only used once | 4 |
| [GAS-10](#GAS-10) | State variables only set in the constructor should be declared `immutable` | 6 |
| [GAS-11](#GAS-11) | Functions guaranteed to revert when called by normal users can be marked `payable` | 11 |
| [GAS-12](#GAS-12) | `++i` costs less gas compared to `i++` or `i += 1` (same for `--i` vs `i--` or `i -= 1`) | 16 |
| [GAS-13](#GAS-13) | Using `private` rather than `public` for constants, saves gas | 1 |
| [GAS-14](#GAS-14) | Increments/decrements can be unchecked in for-loops | 15 |

### <a name="GAS-1"></a>[GAS-1] `a = a + b` is more gas effective than `a += b` for state variables (excluding arrays and mappings)

This saves **16 gas per instance.**

*Instances (10)*:

```solidity
File: src/LiquidProxy.sol

87:             totalUndelegated += _amounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

137:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

155:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

175:             total += _amounts[i];

267:         for (uint256 i = 0; i < proxyCount; i++) totalStaked += _getTotalStakedInProxy(i, consensusAddrs);

282:         for (uint256 i = 0; i < proxyCount; i++) totalRewards += _getTotalRewardsInProxy(i, consensusAddrs);

353:         request.shares += _shares;

354:         lockedSharesPerEpoch[epoch] += _shares;

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-2"></a>[GAS-2] Use assembly to check for `address(0)`

*Saves 6 gas per instance*

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

171:         if (stakingProxy == address(0)) revert ErrBadProxy();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-3"></a>[GAS-3] Using bools for storage incurs overhead

Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’, after having been ‘true’ in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

*Instances (3)*:

```solidity
File: src/LiquidRon.sol

52:     mapping(address => bool) public operator;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

14:     bool public paused;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/ValidatorTracker.sol

17:     mapping(address => bool) public validatorStakeActive;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/ValidatorTracker.sol)

### <a name="GAS-4"></a>[GAS-4] Cache array length outside of loop

If not cached, the solidity compiler will always read the length of the array during each iteration. That is, if it is a storage array, this is an extra sload operation (100 additional extra gas for each iteration except for the first) and if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

*Instances (12)*:

```solidity
File: src/LiquidProxy.sol

38:         for (uint256 i = 0; i < _consensusAddrs.length; i++) {

62:         for (uint256 i = 0; i < _amounts.length; i++) {

76:         for (uint256 i = 0; i < _amounts.length; i++) {

86:         for (uint256 i = 0; i < _amounts.length; i++) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

172:         for (uint256 i = 0; i < _amounts.length; i++) {

194:         for (uint256 i = 0; i < _consensusAddrsSrc.length; i++) {

218:         for (uint256 i = 0; i < proxies.length; i++) proxies[i] = stakingProxies[i];

223:             for (uint256 j = 0; j < proxies.length; j++) {

229:             for (uint256 j = 0; j < proxies.length; j++)

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

408:         for (uint256 i = 0; i < _consensusAddrs.length; i++) users[i] = user;

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-5"></a>[GAS-5] State variables should be cached in stack variables rather than re-reading them from storage

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*Saves 100 gas per instance*

*Instances (4)*:

```solidity
File: src/LiquidRon.sol

227:             uint256[] memory stakingTotals = IRoninValidator(roninStaking).getManyStakingAmounts(valis, proxies);

341:         Escrow(escrow).deposit(msg.value, msg.sender);

464:             Escrow(escrow).deposit(msg.value, msg.sender);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

32:         IWRON(wron).transfer(to, amount);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="GAS-6"></a>[GAS-6] For Operations that will not overflow, you could use unchecked

*Instances (46)*:

```solidity
File: src/Escrow.sol

10: import "@openzeppelin/token/ERC20/IERC20.sol";

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

10: import {IRoninValidator} from "./interfaces/IRoninValidators.sol";

11: import {ILiquidProxy} from "./interfaces/ILiquidProxy.sol";

12: import {RonHelper} from "./RonHelper.sol";

38:         for (uint256 i = 0; i < _consensusAddrs.length; i++) {

62:         for (uint256 i = 0; i < _amounts.length; i++) {

76:         for (uint256 i = 0; i < _amounts.length; i++) {

86:         for (uint256 i = 0; i < _amounts.length; i++) {

87:             totalUndelegated += _amounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

10: import {IRoninValidator} from "./interfaces/IRoninValidators.sol";

11: import {ILiquidProxy} from "./interfaces/ILiquidProxy.sol";

12: import "@openzeppelin/token/ERC20/extensions/ERC4626.sol";

13: import "@openzeppelin/token/ERC20/IERC20.sol";

14: import "@openzeppelin/utils/math/Math.sol";

15: import {Ownable} from "@openzeppelin/access/Ownable.sol";

16: import {Pausable} from "./Pausable.sol";

17: import {RonHelper} from "./RonHelper.sol";

18: import {Escrow} from "./Escrow.sol";

19: import {LiquidProxy} from "./LiquidProxy.sol";

20: import {ValidatorTracker} from "./ValidatorTracker.sol";

117:         stakingProxies[stakingProxyCount++] = address(new LiquidProxy(roninStaking, asset(), address(this)));

137:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

155:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

172:         for (uint256 i = 0; i < _amounts.length; i++) {

175:             total += _amounts[i];

194:         for (uint256 i = 0; i < _consensusAddrsSrc.length; i++) {

218:         for (uint256 i = 0; i < proxies.length; i++) proxies[i] = stakingProxies[i];

219:         for (uint256 i = 0; i < listCount; i++) {

220:             address vali = validators[listCount - 1 - i];

223:             for (uint256 j = 0; j < proxies.length; j++) {

229:             for (uint256 j = 0; j < proxies.length; j++)

249:         statusPerEpoch[withdrawalEpoch++] = WithdrawalStatus.FINALISED;

267:         for (uint256 i = 0; i < proxyCount; i++) totalStaked += _getTotalStakedInProxy(i, consensusAddrs);

282:         for (uint256 i = 0; i < proxyCount; i++) totalRewards += _getTotalRewardsInProxy(i, consensusAddrs);

283:         totalFees = (totalRewards * operatorFee) / BIPS;

284:         return totalRewards - totalFees;

294:         return super.totalAssets() + getTotalStaked() + getTotalRewards();

353:         request.shares += _shares;

354:         lockedSharesPerEpoch[epoch] += _shares;

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

408:         for (uint256 i = 0; i < _consensusAddrs.length; i++) users[i] = user;

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

424:         return _shares.mulDiv(_totalAssets + 1, _totalShares + 10 ** _decimalsOffset(), Math.Rounding.Floor);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

10: import "@openzeppelin/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/ValidatorTracker.sol

39:             validatorIndex[_validator] = validatorCount++;

48:             address lastValidator = validators[--validatorCount];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/ValidatorTracker.sol)

### <a name="GAS-7"></a>[GAS-7] Use Custom Errors instead of Revert Strings to save Gas

Custom errors are available from solidity version 0.8.4. Custom errors save [**~50 gas**](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) each time they're hit by [avoiding having to allocate and store the revert string](https://blog.soliditylang.org/2021/04/21/custom-errors/#errors-in-depth). Not defining the strings also save deployment gas

Additionally, custom errors can be used inside and outside of contracts (including interfaces and libraries).

Source: <https://blog.soliditylang.org/2021/04/21/custom-errors/>:

> Starting from [Solidity v0.8.4](https://github.com/ethereum/solidity/releases/tag/v0.8.4), there is a convenient and gas-efficient way to explain to users why an operation failed through the use of custom errors. Until now, you could already use strings to give more information about failures (e.g., `revert("Insufficient funds.");`), but they are rather expensive, especially when it comes to deploy cost, and it is difficult to use dynamic information in them.

Consider replacing **all revert strings** with custom errors in the solution, and particularly those that have multiple occurrences:

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

111:         require(_fee < 1000, "LiquidRon: Invalid fee");

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-8"></a>[GAS-8] Avoid contract existence checks by using low level calls

Prior to 0.8.10 the compiler inserted extra code, including `EXTCODESIZE` (**100 gas**), to check for contract existence for external function calls. In more recent solidity versions, the compiler will not insert these checks if the external call has a return value. Similar behavior can be achieved in earlier versions by using low-level calls, since low level calls never check for contract existence

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

289:         return IERC20(asset()).balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-9"></a>[GAS-9] Stack variable used as a cheaper cache for a state variable is only used once

If the variable is only accessed once, it's cheaper to use the state variable directly that one time, and save the **3 gas** the extra stack assignment would spend

*Instances (4)*:

```solidity
File: src/LiquidRon.sol

123:         uint256 amount = operatorFeeAmount;

264:         uint256 proxyCount = stakingProxyCount;

278:         uint256 proxyCount = stakingProxyCount;

363:         uint256 epoch = withdrawalEpoch;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-10"></a>[GAS-10] State variables only set in the constructor should be declared `immutable`

Variables only set in the constructor and never edited afterwards should be marked as immutable, as it would avoid the expensive storage-writing operation in the constructor (around **20 000 gas** per variable) and replace the expensive storage-reading operations (around **2100 gas** per reading) to a less expensive value reading (**3 gas**)

*Instances (6)*:

```solidity
File: src/Escrow.sol

24:         _vault = msg.sender;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

24:         vault = _vault;

25:         roninStaking = _roninStaking;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

82:         roninStaking = _roninStaking;

83:         escrow = address(new Escrow(_wron));

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

24:         wron = _wron;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="GAS-11"></a>[GAS-11] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

*Instances (11)*:

```solidity
File: src/LiquidProxy.sol

37:     function harvest(address[] calldata _consensusAddrs) external onlyVault returns (uint256) {

61:     function delegateAmount(uint256[] calldata _amounts, address[] calldata _consensusAddrs) external onlyVault {

84:     function undelegateAmount(uint256[] calldata _amounts, address[] calldata _consensusAddrs) external onlyVault {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

97:     function updateFeeRecipient(address _feeRecipient) external onlyOwner {

104:     function updateOperator(address _operator, bool _value) external onlyOwner {

110:     function setOperatorFee(uint256 _fee) external onlyOwner {

116:     function deployStakingProxy() external onlyOwner {

135:     function harvest(uint256 _proxyIndex, address[] calldata _consensusAddrs) external onlyOperator whenNotPaused {

245:     function finaliseRonRewardsForEpoch() external onlyOperator whenNotPaused {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

21:     function pause() external onlyOwner {

25:     function unpause() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="GAS-12"></a>[GAS-12] `++i` costs less gas compared to `i++` or `i += 1` (same for `--i` vs `i--` or `i -= 1`)

Pre-increments and pre-decrements are cheaper.

For a `uint256 i` variable, the following is true with the Optimizer enabled at 10k:

**Increment:**

- `i += 1` is the most expensive form
- `i++` costs 6 gas less than `i += 1`
- `++i` costs 5 gas less than `i++` (11 gas less than `i += 1`)

**Decrement:**

- `i -= 1` is the most expensive form
- `i--` costs 11 gas less than `i -= 1`
- `--i` costs 5 gas less than `i--` (16 gas less than `i -= 1`)

Note that post-increments (or post-decrements) return the old value before incrementing or decrementing, hence the name *post-increment*:

```solidity
uint i = 1;  
uint j = 2;
require(j == i++, "This will be false as i is incremented after the comparison");
```
  
However, pre-increments (or pre-decrements) return the new value:
  
```solidity
uint i = 1;  
uint j = 2;
require(j == ++i, "This will be true as i is incremented before the comparison");
```

In the pre-increment case, the compiler has to create a temporary variable (when used) for returning `1` instead of `2`.

Consider using pre-increments and pre-decrements where they are relevant (meaning: not where post-increments/decrements logic are relevant).

*Saves 5 gas per instance*

*Instances (16)*:

```solidity
File: src/LiquidProxy.sol

38:         for (uint256 i = 0; i < _consensusAddrs.length; i++) {

62:         for (uint256 i = 0; i < _amounts.length; i++) {

76:         for (uint256 i = 0; i < _amounts.length; i++) {

86:         for (uint256 i = 0; i < _amounts.length; i++) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

172:         for (uint256 i = 0; i < _amounts.length; i++) {

194:         for (uint256 i = 0; i < _consensusAddrsSrc.length; i++) {

218:         for (uint256 i = 0; i < proxies.length; i++) proxies[i] = stakingProxies[i];

219:         for (uint256 i = 0; i < listCount; i++) {

223:             for (uint256 j = 0; j < proxies.length; j++) {

229:             for (uint256 j = 0; j < proxies.length; j++)

267:         for (uint256 i = 0; i < proxyCount; i++) totalStaked += _getTotalStakedInProxy(i, consensusAddrs);

282:         for (uint256 i = 0; i < proxyCount; i++) totalRewards += _getTotalRewardsInProxy(i, consensusAddrs);

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

408:         for (uint256 i = 0; i < _consensusAddrs.length; i++) users[i] = user;

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/ValidatorTracker.sol

48:             address lastValidator = validators[--validatorCount];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/ValidatorTracker.sol)

### <a name="GAS-13"></a>[GAS-13] Using `private` rather than `public` for constants, saves gas

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

50:     uint256 public constant BIPS = 10_000;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="GAS-14"></a>[GAS-14] Increments/decrements can be unchecked in for-loops

In Solidity 0.8+, there's a default overflow check on unsigned integers. It's possible to uncheck this in for-loops and save some gas at each iteration, but at the cost of some code readability, as this uncheck cannot be made inline.

[ethereum/solidity#10695](https://github.com/ethereum/solidity/issues/10695)

The change would be:

```diff
- for (uint256 i; i < numIterations; i++) {
+ for (uint256 i; i < numIterations;) {
 // ...  
+   unchecked { ++i; }
}  
```

These save around **25 gas saved** per instance.

The same can be applied with decrements (which should use `break` when `i == 0`).

The risk of overflow is non-existent for `uint256`.

*Instances (15)*:

```solidity
File: src/LiquidProxy.sol

38:         for (uint256 i = 0; i < _consensusAddrs.length; i++) {

62:         for (uint256 i = 0; i < _amounts.length; i++) {

76:         for (uint256 i = 0; i < _amounts.length; i++) {

86:         for (uint256 i = 0; i < _amounts.length; i++) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

172:         for (uint256 i = 0; i < _amounts.length; i++) {

194:         for (uint256 i = 0; i < _consensusAddrsSrc.length; i++) {

218:         for (uint256 i = 0; i < proxies.length; i++) proxies[i] = stakingProxies[i];

219:         for (uint256 i = 0; i < listCount; i++) {

223:             for (uint256 j = 0; j < proxies.length; j++) {

229:             for (uint256 j = 0; j < proxies.length; j++)

267:         for (uint256 i = 0; i < proxyCount; i++) totalStaked += _getTotalStakedInProxy(i, consensusAddrs);

282:         for (uint256 i = 0; i < proxyCount; i++) totalRewards += _getTotalRewardsInProxy(i, consensusAddrs);

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

408:         for (uint256 i = 0; i < _consensusAddrs.length; i++) users[i] = user;

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

## Non Critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | Missing checks for `address(0)` when assigning values to address state variables | 6 |
| [NC-2](#NC-2) | `constant`s should be defined rather than using magic numbers | 2 |
| [NC-3](#NC-3) | Control structures do not follow the Solidity Style Guide | 13 |
| [NC-4](#NC-4) | Consider disabling `renounceOwnership()` | 1 |
| [NC-5](#NC-5) | Function ordering does not follow the Solidity style guide | 1 |
| [NC-6](#NC-6) | Functions should not be longer than 50 lines | 27 |
| [NC-7](#NC-7) | Interfaces should be defined in separate files from their usage | 2 |
| [NC-8](#NC-8) | Lack of checks in setters | 2 |
| [NC-9](#NC-9) | Missing Event for critical parameters change | 3 |
| [NC-10](#NC-10) | NatSpec is completely non-existent on functions that should have them | 6 |
| [NC-11](#NC-11) | Incomplete NatSpec: `@param` is missing on actually documented functions | 4 |
| [NC-12](#NC-12) | Incomplete NatSpec: `@return` is missing on actually documented functions | 4 |
| [NC-13](#NC-13) | Use a `modifier` instead of a `require/if` statement for a special `msg.sender` actor | 5 |
| [NC-14](#NC-14) | Consider using named mappings | 9 |
| [NC-15](#NC-15) | Owner can renounce while system is paused | 2 |
| [NC-16](#NC-16) | Take advantage of Custom Error's return value property | 12 |
| [NC-17](#NC-17) | Contract does not follow the Solidity style guide's suggested layout ordering | 5 |
| [NC-18](#NC-18) | Use Underscores for Number Literals (add an underscore every 3 digits) | 1 |
| [NC-19](#NC-19) | Internal and private variables and functions names should begin with an underscore | 1 |
| [NC-20](#NC-20) | Event is missing `indexed` fields | 4 |
| [NC-21](#NC-21) | `public` functions not called by the contract should be declared `external` instead | 1 |
| [NC-22](#NC-22) | Variables need not be initialized to zero | 15 |

### <a name="NC-1"></a>[NC-1] Missing checks for `address(0)` when assigning values to address state variables

*Instances (6)*:

```solidity
File: src/LiquidProxy.sol

24:         vault = _vault;

25:         roninStaking = _roninStaking;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

82:         roninStaking = _roninStaking;

85:         feeRecipient = _feeRecipient;

98:         feeRecipient = _feeRecipient;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

24:         wron = _wron;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-2"></a>[NC-2] `constant`s should be defined rather than using magic numbers

Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

*Instances (2)*:

```solidity
File: src/LiquidRon.sol

111:         require(_fee < 1000, "LiquidRon: Invalid fee");

424:         return _shares.mulDiv(_totalAssets + 1, _totalShares + 10 ** _decimalsOffset(), Math.Rounding.Floor);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-3"></a>[NC-3] Control structures do not follow the Solidity Style Guide

See the [control structures](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) section of the Solidity Style Guide

*Instances (13)*:

```solidity
File: src/Escrow.sol

34:         if (msg.sender != _vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

30:         if (msg.sender != vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

91:         if (msg.sender != owner() || operator[msg.sender]) revert ErrInvalidOperator();

122:         if (msg.sender != feeRecipient) revert ErrNotFeeRecipient();

171:         if (stakingProxy == address(0)) revert ErrBadProxy();

173:             if (_amounts[i] == 0) revert ErrNotZero();

195:             if (_amounts[i] == 0) revert ErrNotZero();

234:             if (canPrune) _removeValidator(vali);

365:         if (request.fulfilled) revert ErrRequestFulfilled();

366:         if (statusPerEpoch[_epoch] != WithdrawalStatus.FINALISED) revert ErrWithdrawalProcessNotFinalised();

431:         if (!success) revert ErrCannotReceiveRon();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

17:         if (paused) revert ErrPaused();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/RonHelper.sol

41:         if (!success) revert ErrWithdrawFailed();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-4"></a>[NC-4] Consider disabling `renounceOwnership()`

If the plan for your project does not include eventually giving up all ownership control, consider overwriting OpenZeppelin's `Ownable`'s `renounceOwnership()` function in order to disable it.

*Instances (1)*:

```solidity
File: src/Pausable.sol

12: abstract contract Pausable is Ownable {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="NC-5"></a>[NC-5] Function ordering does not follow the Solidity style guide

According to the [Solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

1: 
   Current order:
   external updateFeeRecipient
   external updateOperator
   external setOperatorFee
   external deployStakingProxy
   external fetchOperatorFee
   external harvest
   external harvestAndDelegateRewards
   external delegateAmount
   external redelegateAmount
   external undelegateAmount
   external pruneValidatorList
   external finaliseRonRewardsForEpoch
   public getTotalStaked
   public getTotalRewards
   public getAssetsInVault
   public totalAssets
   public withdraw
   public redeem
   public deposit
   public mint
   external deposit
   external requestWithdrawal
   external redeem
   internal _getTotalRewardsInProxy
   internal _getTotalStakedInProxy
   internal _convertToAssets
   internal _checkUserCanReceiveRon
   internal _withdraw
   
   Suggested order:
   external updateFeeRecipient
   external updateOperator
   external setOperatorFee
   external deployStakingProxy
   external fetchOperatorFee
   external harvest
   external harvestAndDelegateRewards
   external delegateAmount
   external redelegateAmount
   external undelegateAmount
   external pruneValidatorList
   external finaliseRonRewardsForEpoch
   external deposit
   external requestWithdrawal
   external redeem
   public getTotalStaked
   public getTotalRewards
   public getAssetsInVault
   public totalAssets
   public withdraw
   public redeem
   public deposit
   public mint
   internal _getTotalRewardsInProxy
   internal _getTotalStakedInProxy
   internal _convertToAssets
   internal _checkUserCanReceiveRon
   internal _withdraw

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-6"></a>[NC-6] Functions should not be longer than 50 lines

Overly complex code can make understanding functionality more difficult, try to further modularize your code to ensure readability

*Instances (27)*:

```solidity
File: src/Escrow.sol

13:     function deposit(uint256 _amount, address _receiver) external payable;

33:     function deposit(uint256 _amount, address _receiver) external {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

37:     function harvest(address[] calldata _consensusAddrs) external onlyVault returns (uint256) {

61:     function delegateAmount(uint256[] calldata _amounts, address[] calldata _consensusAddrs) external onlyVault {

84:     function undelegateAmount(uint256[] calldata _amounts, address[] calldata _consensusAddrs) external onlyVault {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

97:     function updateFeeRecipient(address _feeRecipient) external onlyOwner {

104:     function updateOperator(address _operator, bool _value) external onlyOwner {

110:     function setOperatorFee(uint256 _fee) external onlyOwner {

116:     function deployStakingProxy() external onlyOwner {

135:     function harvest(uint256 _proxyIndex, address[] calldata _consensusAddrs) external onlyOperator whenNotPaused {

245:     function finaliseRonRewardsForEpoch() external onlyOperator whenNotPaused {

262:     function getTotalStaked() public view returns (uint256) {

276:     function getTotalRewards() public view returns (uint256) {

288:     function getAssetsInVault() public view returns (uint256) {

293:     function totalAssets() public view override returns (uint256) {

328:     function deposit(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

333:     function mint(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

339:     function deposit() external payable whenNotPaused {

348:     function requestWithdrawal(uint256 _shares) external whenNotPaused {

362:     function redeem(uint256 _epoch) external whenNotPaused {

429:     function _checkUserCanReceiveRon(address _user) internal {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

30:     function _depositRONTo(address to, uint256 amount) internal {

38:     function _withdrawRONTo(address to, uint256 amount) internal {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

```solidity
File: src/ValidatorTracker.sol

24:     function getValidators() external view returns (address[] memory) {

30:     function _getValidators() internal view returns (address[] memory) {

36:     function _tryPushValidator(address _validator) internal {

45:     function _removeValidator(address _validator) internal {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/ValidatorTracker.sol)

### <a name="NC-7"></a>[NC-7] Interfaces should be defined in separate files from their usage

The interfaces below should be defined in separate files, so that it's easier for future projects to import them, and to avoid duplication later on if they need to be used elsewhere in the project

*Instances (2)*:

```solidity
File: src/Escrow.sol

12: interface IVault {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/RonHelper.sol

10: interface IWRON {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-8"></a>[NC-8] Lack of checks in setters

Be it sanity checks (like checks against `0`-values) or initial setting checks: it's best for Setter functions to have them

*Instances (2)*:

```solidity
File: src/LiquidRon.sol

97:     function updateFeeRecipient(address _feeRecipient) external onlyOwner {
            feeRecipient = _feeRecipient;

104:     function updateOperator(address _operator, bool _value) external onlyOwner {
             operator[_operator] = _value;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-9"></a>[NC-9] Missing Event for critical parameters change

Events help non-contract tools to track changes, and events prevent users from being surprised by changes.

*Instances (3)*:

```solidity
File: src/LiquidRon.sol

97:     function updateFeeRecipient(address _feeRecipient) external onlyOwner {
            feeRecipient = _feeRecipient;

104:     function updateOperator(address _operator, bool _value) external onlyOwner {
             operator[_operator] = _value;

110:     function setOperatorFee(uint256 _fee) external onlyOwner {
             require(_fee < 1000, "LiquidRon: Invalid fee");
             operatorFee = _fee;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-10"></a>[NC-10] NatSpec is completely non-existent on functions that should have them

Public and external functions that aren't view or pure should have NatSpec comments

*Instances (6)*:

```solidity
File: src/Escrow.sol

13:     function deposit(uint256 _amount, address _receiver) external payable;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/Pausable.sol

21:     function pause() external onlyOwner {

25:     function unpause() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/RonHelper.sol

11:     function deposit() external payable;

12:     function withdraw(uint256) external;

13:     function transfer(address, uint256) external;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-11"></a>[NC-11] Incomplete NatSpec: `@param` is missing on actually documented functions

The following functions are missing `@param` NatSpec comments.

*Instances (4)*:

```solidity
File: src/LiquidRon.sol

301:     /// @dev We override to prevent wrong event emission and send native ron back to user
         ///   Acts as the ERC4626 withdraw function
         function withdraw(
             uint256 _assets,
             address _receiver,
             address _owner

314:     /// @dev We override to prevent wrong event emission and send native ron back to user
         ///   Acts as the ERC4626 redeem function
         function redeem(
             uint256 _shares,
             address _receiver,
             address _owner

327:     /// @dev We override to add the pause check
         function deposit(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

332:     /// @dev We override to add the pause check
         function mint(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-12"></a>[NC-12] Incomplete NatSpec: `@return` is missing on actually documented functions

The following functions are missing `@return` NatSpec comments.

*Instances (4)*:

```solidity
File: src/LiquidRon.sol

301:     /// @dev We override to prevent wrong event emission and send native ron back to user
         ///   Acts as the ERC4626 withdraw function
         function withdraw(
             uint256 _assets,
             address _receiver,
             address _owner
         ) public override whenNotPaused returns (uint256) {

314:     /// @dev We override to prevent wrong event emission and send native ron back to user
         ///   Acts as the ERC4626 redeem function
         function redeem(
             uint256 _shares,
             address _receiver,
             address _owner
         ) public override whenNotPaused returns (uint256) {

327:     /// @dev We override to add the pause check
         function deposit(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

332:     /// @dev We override to add the pause check
         function mint(uint256 _assets, address _receiver) public override whenNotPaused returns (uint256) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-13"></a>[NC-13] Use a `modifier` instead of a `require/if` statement for a special `msg.sender` actor

If a function is supposed to be access-controlled, a `modifier` should be used instead of a `require/if` statement for more readability.

*Instances (5)*:

```solidity
File: src/Escrow.sol

34:         if (msg.sender != _vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

30:         if (msg.sender != vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

91:         if (msg.sender != owner() || operator[msg.sender]) revert ErrInvalidOperator();

122:         if (msg.sender != feeRecipient) revert ErrNotFeeRecipient();

462:         if (msg.sender != asset()) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-14"></a>[NC-14] Consider using named mappings

Consider moving to solidity version 0.8.18 or later, and using [named mappings](https://ethereum.stackexchange.com/questions/51629/how-to-name-the-arguments-in-mapping/145555#145555) to make it easier to understand the purpose of each mapping

*Instances (9)*:

```solidity
File: src/LiquidRon.sol

52:     mapping(address => bool) public operator;

53:     mapping(uint256 => LockedPricePerShare) public lockedPricePerSharePerEpoch;

54:     mapping(uint256 => mapping(address => WithdrawalRequest)) public withdrawalRequestsPerEpoch;

55:     mapping(uint256 => uint256) public lockedSharesPerEpoch;

56:     mapping(uint256 => WithdrawalStatus) public statusPerEpoch;

58:     mapping(uint256 => address) public stakingProxies;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/ValidatorTracker.sol

17:     mapping(address => bool) public validatorStakeActive;

18:     mapping(address => uint256) public validatorStakeCount;

19:     mapping(address => uint256) public validatorIndex;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/ValidatorTracker.sol)

### <a name="NC-15"></a>[NC-15] Owner can renounce while system is paused

The contract owner or single user with a role is not prevented from renouncing the role/ownership while the contract is paused, which would cause any user assets stored in the protocol, to be locked indefinitely.

*Instances (2)*:

```solidity
File: src/Pausable.sol

21:     function pause() external onlyOwner {

25:     function unpause() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="NC-16"></a>[NC-16] Take advantage of Custom Error's return value property

An important feature of Custom Error is that values such as address, tokenID, msg.value can be written inside the () sign, this kind of approach provides a serious advantage in debugging and examining the revert details of dapps such as tenderly.

*Instances (12)*:

```solidity
File: src/Escrow.sol

34:         if (msg.sender != _vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

30:         if (msg.sender != vault) revert ErrNotVault();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

91:         if (msg.sender != owner() || operator[msg.sender]) revert ErrInvalidOperator();

122:         if (msg.sender != feeRecipient) revert ErrNotFeeRecipient();

171:         if (stakingProxy == address(0)) revert ErrBadProxy();

173:             if (_amounts[i] == 0) revert ErrNotZero();

195:             if (_amounts[i] == 0) revert ErrNotZero();

365:         if (request.fulfilled) revert ErrRequestFulfilled();

366:         if (statusPerEpoch[_epoch] != WithdrawalStatus.FINALISED) revert ErrWithdrawalProcessNotFinalised();

431:         if (!success) revert ErrCannotReceiveRon();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

17:         if (paused) revert ErrPaused();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/RonHelper.sol

41:         if (!success) revert ErrWithdrawFailed();

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-17"></a>[NC-17] Contract does not follow the Solidity style guide's suggested layout ordering

The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be:

1) Type declarations
2) State variables
3) Events
4) Modifiers
5) Functions

However, the contract(s) below do not follow this ordering

*Instances (5)*:

```solidity
File: src/Escrow.sol

1: 
   Current order:
   FunctionDefinition.deposit
   ErrorDefinition.ErrNotVault
   VariableDeclaration._vault
   FunctionDefinition.constructor
   FunctionDefinition.deposit
   
   Suggested order:
   VariableDeclaration._vault
   ErrorDefinition.ErrNotVault
   FunctionDefinition.deposit
   FunctionDefinition.constructor
   FunctionDefinition.deposit

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidProxy.sol

1: 
   Current order:
   ErrorDefinition.ErrNotVault
   VariableDeclaration.vault
   VariableDeclaration.roninStaking
   FunctionDefinition.constructor
   ModifierDefinition.onlyVault
   FunctionDefinition.harvest
   FunctionDefinition.harvestAndDelegateRewards
   FunctionDefinition.delegateAmount
   FunctionDefinition.redelegateAmount
   FunctionDefinition.undelegateAmount
   FunctionDefinition.receive
   
   Suggested order:
   VariableDeclaration.vault
   VariableDeclaration.roninStaking
   ErrorDefinition.ErrNotVault
   ModifierDefinition.onlyVault
   FunctionDefinition.constructor
   FunctionDefinition.harvest
   FunctionDefinition.harvestAndDelegateRewards
   FunctionDefinition.delegateAmount
   FunctionDefinition.redelegateAmount
   FunctionDefinition.undelegateAmount
   FunctionDefinition.receive

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

1: 
   Current order:
   UsingForDirective.Math
   ErrorDefinition.ErrRequestFulfilled
   ErrorDefinition.ErrWithdrawalProcessNotFinalised
   ErrorDefinition.ErrInvalidOperator
   ErrorDefinition.ErrBadProxy
   ErrorDefinition.ErrCannotReceiveRon
   ErrorDefinition.ErrNotZero
   ErrorDefinition.ErrNotFeeRecipient
   StructDefinition.WithdrawalRequest
   StructDefinition.LockedPricePerShare
   VariableDeclaration.BIPS
   VariableDeclaration.operator
   VariableDeclaration.lockedPricePerSharePerEpoch
   VariableDeclaration.withdrawalRequestsPerEpoch
   VariableDeclaration.lockedSharesPerEpoch
   VariableDeclaration.statusPerEpoch
   VariableDeclaration.stakingProxies
   VariableDeclaration.stakingProxyCount
   VariableDeclaration.escrow
   VariableDeclaration.roninStaking
   VariableDeclaration.feeRecipient
   VariableDeclaration.withdrawalEpoch
   VariableDeclaration.operatorFee
   VariableDeclaration.operatorFeeAmount
   EventDefinition.WithdrawalRequested
   EventDefinition.WithdrawalClaimed
   EventDefinition.WithdrawalProcessFinalised
   EventDefinition.Harvest
   FunctionDefinition.constructor
   ModifierDefinition.onlyOperator
   FunctionDefinition.updateFeeRecipient
   FunctionDefinition.updateOperator
   FunctionDefinition.setOperatorFee
   FunctionDefinition.deployStakingProxy
   FunctionDefinition.fetchOperatorFee
   FunctionDefinition.harvest
   FunctionDefinition.harvestAndDelegateRewards
   FunctionDefinition.delegateAmount
   FunctionDefinition.redelegateAmount
   FunctionDefinition.undelegateAmount
   FunctionDefinition.pruneValidatorList
   FunctionDefinition.finaliseRonRewardsForEpoch
   FunctionDefinition.getTotalStaked
   FunctionDefinition.getTotalRewards
   FunctionDefinition.getAssetsInVault
   FunctionDefinition.totalAssets
   FunctionDefinition.withdraw
   FunctionDefinition.redeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.deposit
   FunctionDefinition.requestWithdrawal
   FunctionDefinition.redeem
   FunctionDefinition._getTotalRewardsInProxy
   FunctionDefinition._getTotalStakedInProxy
   FunctionDefinition._convertToAssets
   FunctionDefinition._checkUserCanReceiveRon
   FunctionDefinition._withdraw
   FunctionDefinition.receive
   
   Suggested order:
   UsingForDirective.Math
   VariableDeclaration.BIPS
   VariableDeclaration.operator
   VariableDeclaration.lockedPricePerSharePerEpoch
   VariableDeclaration.withdrawalRequestsPerEpoch
   VariableDeclaration.lockedSharesPerEpoch
   VariableDeclaration.statusPerEpoch
   VariableDeclaration.stakingProxies
   VariableDeclaration.stakingProxyCount
   VariableDeclaration.escrow
   VariableDeclaration.roninStaking
   VariableDeclaration.feeRecipient
   VariableDeclaration.withdrawalEpoch
   VariableDeclaration.operatorFee
   VariableDeclaration.operatorFeeAmount
   StructDefinition.WithdrawalRequest
   StructDefinition.LockedPricePerShare
   ErrorDefinition.ErrRequestFulfilled
   ErrorDefinition.ErrWithdrawalProcessNotFinalised
   ErrorDefinition.ErrInvalidOperator
   ErrorDefinition.ErrBadProxy
   ErrorDefinition.ErrCannotReceiveRon
   ErrorDefinition.ErrNotZero
   ErrorDefinition.ErrNotFeeRecipient
   EventDefinition.WithdrawalRequested
   EventDefinition.WithdrawalClaimed
   EventDefinition.WithdrawalProcessFinalised
   EventDefinition.Harvest
   ModifierDefinition.onlyOperator
   FunctionDefinition.constructor
   FunctionDefinition.updateFeeRecipient
   FunctionDefinition.updateOperator
   FunctionDefinition.setOperatorFee
   FunctionDefinition.deployStakingProxy
   FunctionDefinition.fetchOperatorFee
   FunctionDefinition.harvest
   FunctionDefinition.harvestAndDelegateRewards
   FunctionDefinition.delegateAmount
   FunctionDefinition.redelegateAmount
   FunctionDefinition.undelegateAmount
   FunctionDefinition.pruneValidatorList
   FunctionDefinition.finaliseRonRewardsForEpoch
   FunctionDefinition.getTotalStaked
   FunctionDefinition.getTotalRewards
   FunctionDefinition.getAssetsInVault
   FunctionDefinition.totalAssets
   FunctionDefinition.withdraw
   FunctionDefinition.redeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.deposit
   FunctionDefinition.requestWithdrawal
   FunctionDefinition.redeem
   FunctionDefinition._getTotalRewardsInProxy
   FunctionDefinition._getTotalStakedInProxy
   FunctionDefinition._convertToAssets
   FunctionDefinition._checkUserCanReceiveRon
   FunctionDefinition._withdraw
   FunctionDefinition.receive

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

1: 
   Current order:
   ErrorDefinition.ErrPaused
   VariableDeclaration.paused
   ModifierDefinition.whenNotPaused
   FunctionDefinition.pause
   FunctionDefinition.unpause
   
   Suggested order:
   VariableDeclaration.paused
   ErrorDefinition.ErrPaused
   ModifierDefinition.whenNotPaused
   FunctionDefinition.pause
   FunctionDefinition.unpause

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

```solidity
File: src/RonHelper.sol

1: 
   Current order:
   FunctionDefinition.deposit
   FunctionDefinition.withdraw
   FunctionDefinition.transfer
   ErrorDefinition.ErrWithdrawFailed
   VariableDeclaration.wron
   FunctionDefinition.constructor
   FunctionDefinition._depositRONTo
   FunctionDefinition._withdrawRONTo
   
   Suggested order:
   VariableDeclaration.wron
   ErrorDefinition.ErrWithdrawFailed
   FunctionDefinition.deposit
   FunctionDefinition.withdraw
   FunctionDefinition.transfer
   FunctionDefinition.constructor
   FunctionDefinition._depositRONTo
   FunctionDefinition._withdrawRONTo

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-18"></a>[NC-18] Use Underscores for Number Literals (add an underscore every 3 digits)

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

111:         require(_fee < 1000, "LiquidRon: Invalid fee");

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-19"></a>[NC-19] Internal and private variables and functions names should begin with an underscore

According to the Solidity Style Guide, Non-`external` variable and function names should begin with an [underscore](https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)

*Instances (1)*:

```solidity
File: src/RonHelper.sol

21:     address wron;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="NC-20"></a>[NC-20] Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

*Instances (4)*:

```solidity
File: src/LiquidRon.sol

69:     event WithdrawalRequested(address indexed requester, uint256 indexed epoch, uint256 shareAmount);

70:     event WithdrawalClaimed(address indexed claimer, uint256 indexed epoch, uint256 shareAmount, uint256 assetAmount);

71:     event WithdrawalProcessFinalised(uint256 indexed epoch, uint256 shares, uint256 assets);

72:     event Harvest(uint256 indexed proxyIndex, uint256 amount);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-21"></a>[NC-21] `public` functions not called by the contract should be declared `external` instead

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

288:     function getAssetsInVault() public view returns (uint256) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="NC-22"></a>[NC-22] Variables need not be initialized to zero

The default value for variables is zero, so initializing them to zero is superfluous.

*Instances (15)*:

```solidity
File: src/LiquidProxy.sol

38:         for (uint256 i = 0; i < _consensusAddrs.length; i++) {

62:         for (uint256 i = 0; i < _amounts.length; i++) {

76:         for (uint256 i = 0; i < _amounts.length; i++) {

86:         for (uint256 i = 0; i < _amounts.length; i++) {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

172:         for (uint256 i = 0; i < _amounts.length; i++) {

194:         for (uint256 i = 0; i < _consensusAddrsSrc.length; i++) {

218:         for (uint256 i = 0; i < proxies.length; i++) proxies[i] = stakingProxies[i];

219:         for (uint256 i = 0; i < listCount; i++) {

223:             for (uint256 j = 0; j < proxies.length; j++) {

229:             for (uint256 j = 0; j < proxies.length; j++)

267:         for (uint256 i = 0; i < proxyCount; i++) totalStaked += _getTotalStakedInProxy(i, consensusAddrs);

282:         for (uint256 i = 0; i < proxyCount; i++) totalRewards += _getTotalRewardsInProxy(i, consensusAddrs);

392:         for (uint256 i = 0; i < rewards.length; i++) totalRewards += rewards[i];

408:         for (uint256 i = 0; i < _consensusAddrs.length; i++) users[i] = user;

410:         for (uint256 i = 0; i < stakedAmounts.length; i++) totalStaked += stakedAmounts[i];

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

## Low Issues

| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | `approve()`/`safeApprove()` may revert if the current approval is not zero | 2 |
| [L-2](#L-2) | Use a 2-step ownership transfer pattern | 1 |
| [L-3](#L-3) | Some tokens may revert when zero value transfers are made | 2 |
| [L-4](#L-4) | Missing checks for `address(0)` when assigning values to address state variables | 6 |
| [L-5](#L-5) | Empty `receive()/payable fallback()` function does not authenticate requests | 1 |
| [L-6](#L-6) | External call recipient may consume all transaction gas | 2 |
| [L-7](#L-7) | Prevent accidentally burning tokens | 1 |
| [L-8](#L-8) | Owner can renounce while system is paused | 2 |
| [L-9](#L-9) | Loss of precision | 3 |
| [L-10](#L-10) | Solidity version 0.8.20+ may not work on other chains due to `PUSH0` | 2 |
| [L-11](#L-11) | Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership` | 2 |
| [L-12](#L-12) | Unsafe ERC20 operation(s) | 4 |

### <a name="L-1"></a>[L-1] `approve()`/`safeApprove()` may revert if the current approval is not zero

- Some tokens (like the *very popular* USDT) do not work when changing the allowance from an existing non-zero allowance value (it will revert if the current approval is not zero to protect against front-running changes of approvals). These tokens must first be approved for zero and then the actual allowance can be approved.
- Furthermore, OZ's implementation of safeApprove would throw an error if an approve is attempted from a non-zero value (`"SafeERC20: approve from non-zero to non-zero allowance"`)

Set the allowance to zero immediately before each of the existing allowance calls

*Instances (2)*:

```solidity
File: src/Escrow.sol

25:         IERC20(_token).approve(msg.sender, type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidRon.sol

86:         IERC20(_wron).approve(address(this), type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="L-2"></a>[L-2] Use a 2-step ownership transfer pattern

Recommend considering implementing a two step process where the owner or admin nominates an account and the nominated account needs to call an `acceptOwnership()` function for the transfer of ownership to fully succeed. This ensures the nominated EOA account is a valid and active account. Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*Instances (1)*:

```solidity
File: src/Pausable.sol

12: abstract contract Pausable is Ownable {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="L-3"></a>[L-3] Some tokens may revert when zero value transfers are made

Example: <https://github.com/d-xo/weird-erc20#revert-on-zero-value-transfers>.

In spite of the fact that EIP-20 [states](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) that zero-valued transfers must be accepted, some tokens, such as LEND will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

*Instances (2)*:

```solidity
File: src/LiquidRon.sol

372:         IERC20(asset()).transferFrom(escrow, address(this), assets);

454:         SafeERC20.safeTransfer(IERC20(asset()), receiver, assets);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="L-4"></a>[L-4] Missing checks for `address(0)` when assigning values to address state variables

*Instances (6)*:

```solidity
File: src/LiquidProxy.sol

24:         vault = _vault;

25:         roninStaking = _roninStaking;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

82:         roninStaking = _roninStaking;

85:         feeRecipient = _feeRecipient;

98:         feeRecipient = _feeRecipient;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

24:         wron = _wron;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="L-5"></a>[L-5] Empty `receive()/payable fallback()` function does not authenticate requests

If the intention is for the Ether to be used, the function should call another function, otherwise it should revert (e.g. require(msg.sender == address(weth))). Having no access control on the function means that someone may send Ether to the contract, and have no way to get anything back out, which is a loss of funds. If the concern is having to spend a small amount of gas to check the sender against an immutable address, the code should at least have a function to rescue unused Ether.

*Instances (1)*:

```solidity
File: src/LiquidProxy.sol

94:     receive() external payable {}

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

### <a name="L-6"></a>[L-6] External call recipient may consume all transaction gas

There is no limit specified on the amount of gas used, so the recipient can use up all of the transaction's gas, causing it to revert. Use `addr.call{gas: <amount>}("")` or [this](https://github.com/nomad-xyz/ExcessivelySafeCall) library instead.

*Instances (2)*:

```solidity
File: src/LiquidRon.sol

430:         (bool success, ) = payable(_user).call{value: 0}("");

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

40:         (bool success, ) = to.call{value: amount}("");

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

### <a name="L-7"></a>[L-7] Prevent accidentally burning tokens

Minting and burning tokens to address(0) prevention

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

453:         _burn(owner, shares);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="L-8"></a>[L-8] Owner can renounce while system is paused

The contract owner or single user with a role is not prevented from renouncing the role/ownership while the contract is paused, which would cause any user assets stored in the protocol, to be locked indefinitely.

*Instances (2)*:

```solidity
File: src/Pausable.sol

21:     function pause() external onlyOwner {

25:     function unpause() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="L-9"></a>[L-9] Loss of precision

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator

*Instances (3)*:

```solidity
File: src/LiquidRon.sol

137:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

155:         operatorFeeAmount += (harvestedAmount * operatorFee) / BIPS;

283:         totalFees = (totalRewards * operatorFee) / BIPS;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="L-10"></a>[L-10] Solidity version 0.8.20+ may not work on other chains due to `PUSH0`

The compiler for Solidity 0.8.20 switches the default target EVM version to [Shanghai](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/#important-note), which includes the new `PUSH0` op code. This op code may not yet be implemented on all L2s, so deployment on these chains will fail. To work around this issue, use an earlier [EVM](https://docs.soliditylang.org/en/v0.8.20/using-the-compiler.html?ref=zaryabs.com#setting-the-evm-version-to-target) [version](https://book.getfoundry.sh/reference/config/solidity-compiler#evm_version). While the project itself may or may not compile with 0.8.20, other projects with which it integrates, or which extend this project may, and those projects will have problems deploying these contracts/libraries.

*Instances (2)*:

```solidity
File: src/LiquidProxy.sol

2: pragma solidity ^0.8.20;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidProxy.sol)

```solidity
File: src/LiquidRon.sol

2: pragma solidity ^0.8.20;

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="L-11"></a>[L-11] Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership`

Use [Ownable2Step.transferOwnership](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol) which is safer. Use it as it is more secure due to 2-stage ownership transfer.

**Recommended Mitigation Steps**

Use <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol">Ownable2Step.sol</a>
  
  ```solidity
      function acceptOwnership() external {
          address sender = _msgSender();
          require(pendingOwner() == sender, "Ownable2Step: caller is not the new owner");
          _transferOwnership(sender);
      }
```

*Instances (2)*:

```solidity
File: src/LiquidRon.sol

15: import {Ownable} from "@openzeppelin/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

10: import "@openzeppelin/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="L-12"></a>[L-12] Unsafe ERC20 operation(s)

*Instances (4)*:

```solidity
File: src/Escrow.sol

25:         IERC20(_token).approve(msg.sender, type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidRon.sol

86:         IERC20(_wron).approve(address(this), type(uint256).max);

372:         IERC20(asset()).transferFrom(escrow, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/RonHelper.sol

32:         IWRON(wron).transfer(to, amount);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/RonHelper.sol)

## Medium Issues

| |Issue|Instances|
|-|:-|:-:|
| [M-1](#M-1) | Contracts are vulnerable to fee-on-transfer accounting-related issues | 1 |
| [M-2](#M-2) | Centralization Risk for trusted owners | 8 |
| [M-3](#M-3) | Return values of `transfer()`/`transferFrom()` not checked | 1 |
| [M-4](#M-4) | Unsafe use of `transfer()`/`transferFrom()`/`approve()`/ with `IERC20` | 3 |

### <a name="M-1"></a>[M-1] Contracts are vulnerable to fee-on-transfer accounting-related issues

Consistently check account balance before and after transfers for Fee-On-Transfer discrepancies. As arbitrary ERC20 tokens can be used, the amount here should be calculated every time to take into consideration a possible fee-on-transfer or deflation.
Also, it's a good practice for the future of the solution.

Use the balance before and after the transfer to calculate the received amount instead of assuming that it would be equal to the amount passed as a parameter. Or explicitly document that such tokens shouldn't be used and won't be supported

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

372:         IERC20(asset()).transferFrom(escrow, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="M-2"></a>[M-2] Centralization Risk for trusted owners

#### Impact

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*Instances (8)*:

```solidity
File: src/LiquidRon.sol

81:     ) ERC4626(IERC20(_wron)) ERC20(_name, _symbol) RonHelper(_wron) Ownable(msg.sender) {

97:     function updateFeeRecipient(address _feeRecipient) external onlyOwner {

104:     function updateOperator(address _operator, bool _value) external onlyOwner {

110:     function setOperatorFee(uint256 _fee) external onlyOwner {

116:     function deployStakingProxy() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

```solidity
File: src/Pausable.sol

12: abstract contract Pausable is Ownable {

21:     function pause() external onlyOwner {

25:     function unpause() external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Pausable.sol)

### <a name="M-3"></a>[M-3] Return values of `transfer()`/`transferFrom()` not checked

Not all `IERC20` implementations `revert()` when there's a failure in `transfer()`/`transferFrom()`. The function signature has a `boolean` return value and they indicate errors that way instead. By not checking the return value, operations that should have marked as failed, may potentially go through without actually making a payment

*Instances (1)*:

```solidity
File: src/LiquidRon.sol

372:         IERC20(asset()).transferFrom(escrow, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

### <a name="M-4"></a>[M-4] Unsafe use of `transfer()`/`transferFrom()`/`approve()`/ with `IERC20`

Some tokens do not implement the ERC20 standard properly but are still accepted by most code that accepts ERC20 tokens.  For example Tether (USDT)'s `transfer()` and `transferFrom()` functions on L1 do not return booleans as the specification requires, and instead have no return value. When these sorts of tokens are cast to `IERC20`, their [function signatures](https://medium.com/coinmonks/missing-return-value-bug-at-least-130-tokens-affected-d67bf08521ca) do not match and therefore the calls made, revert (see [this](https://gist.github.com/IllIllI000/2b00a32e8f0559e8f386ea4f1800abc5) link for a test case). Use OpenZeppelin's `SafeERC20`'s `safeTransfer()`/`safeTransferFrom()` instead

*Instances (3)*:

```solidity
File: src/Escrow.sol

25:         IERC20(_token).approve(msg.sender, type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/Escrow.sol)

```solidity
File: src/LiquidRon.sol

86:         IERC20(_wron).approve(address(this), type(uint256).max);

372:         IERC20(asset()).transferFrom(escrow, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2025-01-liquid-ron/blob/main/src/LiquidRon.sol)

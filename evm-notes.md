# EVM / Solidity notes

## Checks-effects-interactions

The classic. If a state change that determines a balance happens after an external call, the callee can re-enter and read stale state. Look for state that is written *after* `transfer`, `transferFrom`, `safeTransfer`, a `call{value:}`, or any `safeApplyAllowance` style hook. Read-only reentrancy (oracle or view functions that read the stale state) is the quieter variant.

## Recorded-but-unpaid desync

A counter advances before value moves, and a branch commits the advance without moving anything. The tell: a cumulative counter compared against an elapsed schedule, with an early return for dust. It never over-pays, but the beneficiary is permanently underpaid and the residue sits in the contract. Search for `+=` that happens before the transfer, then look for a branch that returns without transferring.

## Share inflation and donation

First depositor mints a huge share count, or donates tokens directly to the vault so the share price diverges from the deposited amount. Check the mint formula against `totalSupply` and the vault balance at the same block.

## Oracle

Spot price or a thin TWAP, no staleness check, no fallback. Confirm the exact read site and whether anything bounds the age of the update. Then ask what a same-block swap does to it.

## Token edge cases

Fee-on-transfer and rebasing tokens make `amount` a lie. Reflection tokens change balances without transfers. ERC-777 and ERC-1155 hooks re-enter. Weird decimals break every multiplication. Pin the token, then check the maths.

## Proxy storage

Storage collisions between implementation and proxy, uninitialized implementation, admin role in a single-key wallet, `upgradeTo` without a timelock. Compare the storage layout across versions.

## Signature paths

Replaying a signature across chains or contracts, missing deadline, missing EIP-712 domain, malleable `s` and `v`, and signatures that sign a constant string instead of the action. The last one turns the signature into a bearer token.

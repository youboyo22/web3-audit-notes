# Solana / Anchor and Soroban / Rust notes

## Anchor: signer and constraint checks

An instruction that takes an account without `has_one`, `constraint`, or `seeds` can be called with a substitute. Check every account argument: is it the expected owner, is it seeded correctly, and is the signer check present. Sibling instructions are the best reference — when one sibling enforces a check and another does not, the gap is the finding.

## CPI ordering and accounting

A cumulative counter that advances before a CPI transfer, plus an early return for a dust amount, records value that never moves. Solana programs usually have `overflow-checks = true` in release, so the failure mode is a recorded-but-unpaid desync rather than a wraparound drain. Look for the counter and the early return together.

##PDA derivation

Hard-coded program IDs, a single static seed, or a bump stored in the wrong account lets one pool impersonate another. Confirm the seeds match the account being written.

## Upgradeable programs

On Solana every program is upgradeable. The upgrade authority is the whole game: who holds it, is it a multisig, and can a program be upgraded to malicious code without a review. Not a bug on its own, but it frames the severity of everything else you find.

## Soroban / Rust

Contract size and entry caps matter (an enum with more variants than the XDR limit will not compile). Storage-key collisions between two contracts sharing an instance, auth scopes that are broader than the action, and `try_` helpers that swallow a failure are the recurring shapes. Because the toolchain is young, a non-compiling HEAD is itself worth reporting.

## Cross-chain bridges

Conservation first: does burn-on-source equal mint-on-destination? Then message authentication: who can call the receive path, is the peer and source chain checked, and is a replay or a forged return bounded by an outstanding balance?

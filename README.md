# web3-audit-notes

Field notes on vulnerability classes across chains. Written for reviewers who already read the code once and want a second pass to catch what the first one missed.

## Contents

- `evm-notes.md` — Solidity and EVM patterns: reentrancy, accounting desync, oracle and token edge cases, proxy storage.
- `solana-soroban-notes.md` — Solana/Anchor and Soroban/Rust patterns: CPI ordering, signer checks, integer checks, upgradeable program risk.
- `triage.md` — how to move from a candidate to a proven finding: build the fork, write the test, rate the money path.

## How to use these

These are patterns, not findings. A pattern only becomes a finding when you point at the exact lines in the target and prove the impact with a runnable test. If you cannot prove the movement of funds or state, you have an opinion, not a report.

## Contributing

Corrections and additions welcome. Keep entries tied to a real, verifiable mechanism and name the code shape rather than a specific target.

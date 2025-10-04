# hybrid-chaos-quantum-rng (public, sanitized)

**Designed for post-quantum Ethereum randomness (Falcon / Keccak compatible).**

This repository provides a **public, sanitized** specification and a short whitepaper for a hybrid RNG architecture targeted at high-assurance use cases (post-quantum signing seeds, verifiable on-chain randomness, secure key generation). The public content is intentionally high-level; the full implementation, private parameters, test logs, and production artifacts are held in a private repository and available under NDA or commercial licensing.

## What this repo contains (public)
- `WHITEPAPER.md` — a 1–2 page technical brief (sanitized) describing architecture, high-level math, and recommended integration patterns.
- `demo/simulated_rng_demo.py` — a safe demo that shows an off-chain commit/reveal flow using OS-provided entropy. **This demo is intentionally simplified and does not contain secret parameters.**
- `SECURITY.md` — instructions for requesting private access, reporting issues, and requesting an NDA.

## Why this design
The architecture combines multiple orthogonal entropy and mixing mechanisms to reduce predictability and provide verifiable audit trails:
- hardware seed layer (TRNG/QRNG recommended),
- chaotic amplifiers (deterministic maps used to amplify small irreducible entropy),
- topological mixers to remove simple algebraic structure,
- cryptographic mixing (a provable, public-key style component such as BBS used privately),
- a cryptographic extractor (SHAKE family recommended) and Keccak-based commit for on-chain verification,
- and a hash-based ratchet for forward/backward secrecy.

Publication here is **sanitized** — implementation-level parameters (private BBS primes, exact bit-extraction windows, raw TRNG outputs) are intentionally omitted. These will be shared under NDA for trusted audits or licensing.

## Intended integrations
- Falcon-based account-abstract wallets (ERC-4337) as a seed/nonce provider.
- On-chain commit/reveal or VRF oracle adapters (off-chain compute + on-chain verification).
- Secure key generation inside HSMs / KMS where deterministic seeding must be avoided.

## Contact & licensing
To request NDA access, private repo access, or licensing/purchase discussions, follow the instructions in `SECURITY.md`.

**Disclaimer:** This repo is research/marketing material and not a production-ready cryptographic library. Do not use these materials for production key generation without independent auditing.

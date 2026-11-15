# Appendix A

I kept the chapters light on purpose, so here is the heavier version of the details, the parts I simplified or skipped to keep the book readable. Nothing here is required to understand the rest of the book; it is just for the people who want to open the hood and see the machinery. If something below does not make sense yet, reread the related chapter and come back.

## Consensus Mechanisms in Detail

### Proof of Work

**The puzzle itself:** miners keep incrementing a number called the nonce inside the block header until the hash of the header falls below the network's current target. In its simplest form:

```
H(block header + nonce) < target
```

Since a hash function's output is uniformly distributed, every attempt is an independent lottery ticket. The target is recalibrated periodically (every 2016 blocks in Bitcoin, about two weeks) so that blocks keep arriving at the intended pace regardless of how much hash power joined or left the network. Less target means more difficulty.

**Why KDFs instead of plain hash functions:** SHA-256 is so cheap in hardware that ASICs turned mining into an arms race. KDFs like scrypt and Argon2 are memory-hard, which means the cost is dominated by memory, and memory is expensive to shrink into a chip. scrypt takes three parameters (N, r, p), and its memory need is roughly:

```
memory ≈ 128 × N × r bytes
```

Dial N up and every parallel evaluation needs that much fast memory on the die, which raises ASIC costs much faster than it raises CPU costs. That is the whole trick: not making mining impossible for machines, just making specialization unprofitable for long enough.

**Selfish mining:** an attacker with a private fork can withhold blocks and release them strategically to make honest miners waste work. The classic analysis by Eyal and Sirer put the profitable threshold at roughly a quarter of the total hash power, which is uncomfortably low, and it is one more reason hash power concentration matters.

### Proof of Stake

**Selection and finality:** validators lock coins, get pseudo-randomly chosen to propose blocks, and the rest of the committee attests. When a supermajority (commonly two thirds) of the stake attests to a checkpoint, that checkpoint becomes finalized and can no longer be reverted without a hard fork. This is why PoS chains can have economic finality in minutes while PoW finality is only probabilistic and grows with confirmations.

**Slashing:** validators who sign conflicting blocks or stay offline lose part of their stake. The penalties are usually correlated, meaning the more validators misbehave at the same time, the more each one loses. That gradient is deliberate; it makes coordinated attacks expensive and honest operation boring and profitable.

**The known weaknesses:** nothing-at-stake (voting on every fork costs nothing unless slashing punishes it) and long-range attacks (rewriting history using old, long-unstaked keys) are the two classics. Chains mitigate them with finality gadgets, checkpointing, and weak subjectivity assumptions, meaning new nodes need a recent trusted checkpoint to know they are on the real chain. It is a real trade-off against PoW, where the heaviest chain is self-evident from the data alone.

### Proof of History

PoH is not consensus on its own, it is a clock. It hashes input after input, where each output feeds into the next hash:

```
h1 = H(seed, data1)
h2 = H(h1, data2)
h3 = H(h2, data3)
```

Creating the chain is necessarily sequential, but verifying any single transition is a single hash computation, so verification parallelizes across cores. The result is a cryptographic timestamp: everyone can later prove that event B happened after event A without anyone agreeing on wall-clock time. Solana pairs it with PoS, where PoH orders events and PoS does the actual validation.

## Hash Functions and KDFs

**The properties that matter:** for an n-bit hash function, finding a preimage costs about 2^n operations, but finding any collision only costs about 2^(n/2) because of the birthday paradox. This is why a 256-bit hash gives you roughly 128-bit collision resistance, and why we consider hash functions "broken" long before preimages become feasible.

**Avalanche effect:** flip one input bit and about half of the output bits flip. This is what makes hash chaining work as a tamper detector; there is no such thing as a small change in the output.

**Memory-hardness:** scrypt and Argon2id were built to make password cracking expensive in hardware, and blockchains borrowed them for the same reason. Argon2id won the Password Hashing Competition in 2015 and combines resistance to both GPU and side-channel attacks, which is why newer chains and newer KDF-based PoW schemes prefer it.

## Signature Schemes

**ECDSA on secp256k1:** the classic Bitcoin and Ethereum scheme. Its most dangerous practical weakness is the nonce; if the random number k used in a signature repeats or leaks even once, the private key can be computed from two signatures. RFC 6979 fixes this by deriving k deterministically from the key and the message, and most modern implementations do exactly that.

**EdDSA on Ed25519:** signatures and keys are 32 bytes, signing is deterministic by design, verification is fast and can be batched, and there is no nonce to misuse. This is why newer chains (Solana, Cardano, Polkadot) picked it.

**Key sizes:** elliptic curve cryptography gets its security from the discrete logarithm problem, so a 256-bit curve gives roughly the same security as a 3072-bit RSA key. On a blockchain where every signature lives forever in every node's storage, that difference is not a detail, it is the reason ECC won.

**Schnorr signatures:** mathematically simpler than ECDSA and linear, which means multiple signatures can be aggregated into one that verifies against the combined key. That is the foundation of signature aggregation and smaller multi-party transactions.

## Zero-Knowledge Proof Systems

All ZK systems share three properties: completeness (a true statement can always be proven), soundness (a false statement cannot be proven except with negligible probability), and zero-knowledge (the verifier learns nothing beyond the truth of the statement). The families differ in how they get there:

- **zk-SNARKs:** proofs of a few hundred bytes, verifiable in milliseconds. Pairing-based constructions like Groth16 need a circuit-specific trusted setup; the ceremony's "toxic waste" parameters must be destroyed, and if they are not, someone holding them can forge proofs. Newer setups (Powers of Tau with many participants, or KZG ceremonies with thousands of contributions) make sabotage practically impossible, but the assumption remains.
- **zk-STARKs:** no trusted setup at all, built from hashes and polynomial commitments with the FRI protocol. Proofs are much larger (tens of kilobytes), but the construction is transparent and post-quantum secure, since it relies only on hash assumptions.
- **Bulletproofs:** no setup, logarithmic-size range proofs, slower to verify. Monero uses them to prove that hidden transaction amounts are non-negative without revealing the amounts.

The practical pattern: SNARKs when you need tiny proofs on a chain where every byte costs gas, STARKs when you need transparency and quantum resistance, Bulletproofs when you just need to hide amounts.

## Monero's Privacy Stack

**Stealth addresses:** the sender generates a one-time public key for each output using the recipient's public view key and a random value. Only the recipient, holding the matching private view key, can scan the chain and recognize which outputs belong to them. The chain never shows a repeated receiving address in the first place.

**RingCT:** amounts are hidden inside Pedersen commitments, cryptographic promises of the form `C = aG + bH` where a is the amount and b is a blinding factor. The network can verify that the sum of input commitments equals the sum of output commitments plus the fee without ever learning any of the amounts. Range proofs (Bulletproofs) guarantee the hidden values are not negative.

**Ring signatures and FCMP++:** ring signatures place the real input among decoys, so a verifier knows one of N outputs funded the transaction but not which one. The weakness was statistical; decoys that look unusual compared to the real input leak hints. FCMP++ (Full Chain Membership Proofs) replaces the small ring with a proof of membership over the entire set of outputs on the chain, which moves the anonymity set from "sixteen possible senders" to "every output that exists". That is the biggest single jump in Monero's design so far.

## The EVM and Gas

**The machine:** the EVM is a 256-bit stack machine with a small instruction set, ephemeral memory, and persistent storage. Storage is the expensive part because every storage slot must stay in consensus, while memory and stack are wiped after the transaction.

**The price list:** simple arithmetic costs single digits of gas (an ADD has been 3 gas since genesis), while touching a cold storage slot costs thousands. Storage writes cost more than reads and clearing a slot actually refunds gas, which nudges developers toward cleaning up after themselves.

**The fee market:** since EIP-1559 every transaction pays a base fee, which the protocol adjusts block by block toward the network's gas target (15 million gas), plus an optional tip for the validator. The base fee adjustment is capped at 12.5% per block, so fees cannot spiral out of control in a single step. Base fees are burned, not paid to validators, which ties ETH's supply to how much the network is actually used.

```
base_fee_next ≈ base_fee × (1 + 0.125 × (gas_used - target) / target)
```

**Why the determinism matters:** every node must reach the same post-state after every transaction, so the EVM forbids anything nondeterministic. No current time, no random numbers, no network access. Oracles exist precisely because the EVM is deaf to the outside world.

## UTXO vs Accounts (Technical Notes)

**UTXO:** the global state is just a set of unspent outputs, each with a locking script that describes who may spend it. Transactions consume whole outputs and create new ones, including the change output sent back to the sender. Since outputs are independent, transaction validation parallelizes beautifully and there is no shared mutable state to fight over. The privacy cost is that outputs form a graph; if you merge coins from two sources in one transaction, everyone sees it.

**Accounts:** a global map from addresses to balances, nonces, and (for contracts) code and storage. The nonce enforces ordering and replay protection: every transaction must spend the next unused nonce of its sender. State lives in Merkle Patricia tries so a light client can verify a single account's balance with a short proof. Shared state is what makes composability easy and parallel execution hard, the exact opposite of UTXO.

## P2P Networking Internals

**Discovery:** new nodes bootstrap through DNS seeds, hardcoded peer lists, or peers they have saved, then exchange addresses to fill their peer tables. Kademlia-style DHTs (used by libp2p and Ethereum 2) place records in a keyspace where distance is XOR of node IDs, so lookup takes a logarithmic number of hops.

**Gossip:** when a node learns a new transaction or block, it announces the hash to a random subset of peers, who request the full payload only if they do not have it. This deduplication is what keeps floods from doubling the bandwidth of the network on every hop.

**Eclipse defense:** if an attacker controls all of your peers, they can feed you a fictional version of the chain. Mitigations include diversifying peer selection, scoring misbehaving peers, and keeping some persistent connections across restarts, and none of them are perfect. It is an uncomfortable truth that your view of a decentralized network is only as honest as the peers you happen to be connected to.

## Threshold Signatures and MPC

A t-of-n threshold signature scheme lets any t participants jointly produce one signature that verifies as a single normal signature, while any t-1 of them learn nothing usable. Distributed Key Generation creates the shared key so that no single party ever holds it in full.

Compared to on-chain multisig, the difference is on-chain footprint: a multisig transaction lists every signer and their weights for the whole world to catalog, while a TSS transaction looks like any single-key transaction. That is why TSS shows up both in privacy-preserving compliance committees (a threshold of members must agree before anything is revealed) and in custody products that do not want to advertise their signer sets.

## A Field Guide to Attacks

- **51% attack:** control a majority of hash power or stake and you can reorganize recent history and double-spend. You cannot invent coins from nothing or rewrite old finalized history, you can only reorder the recent past, which is usually enough.
- **Selfish mining:** withhold and strategically release blocks to waste the honest network's work; profitable from roughly a quarter of the hash power under the classic analysis.
- **Eclipse attack:** isolate one node by controlling all its peers and feed it a fabricated view of the network; often a stepping stone to double-spends against that specific victim.
- **Sybil attack:** create thousands of fake identities to overweight voting, peer selection, or governance. Any system counting "people" without a cost per identity is vulnerable.
- **Long-range attack:** buy old validator keys and rewrite history from far back; only works against nodes that sync without a trusted checkpoint.
- **Nothing-at-stake:** validate on every fork because it is free, keeping useless forks alive; mitigated by slashing.
- **MEV (front-running and sandwiching):** bots watch the mempool, buy before your trade and sell right after it, profiting from the price movement your own transaction causes. Private transaction relays and slippage limits are the usual defenses.
- **Flash loan attacks:** borrow enormous value with zero collateral inside a single transaction, use it to distort a price feed or governance vote, and repay it before the transaction ends. The attack is atomic, so it requires no capital at all, just a vulnerable protocol.

## A Short Note on Post-Quantum

Two quantum algorithms matter here. Shor's algorithm breaks the math behind ECDSA, EdDSA, and RSA entirely, meaning every blockchain signature scheme in wide use today eventually fails to a sufficiently large quantum computer. Grover's algorithm only gives a quadratic speedup against symmetric primitives, so AES-256 and SHA-256 keep roughly 128-bit security, which is why hashes and symmetric encryption survive the quantum era mostly intact.

Post-quantum signature schemes (ML-DSA/Dilithium, SPHINCS+, and friends) exist and are standardized, but their signatures and keys are measured in kilobytes instead of bytes, and blockchains feel that cost on every transaction forever. That mismatch, not lack of research, is why chains are experimenting with signature aggregation, hybrid schemes, and migration plans instead of switching overnight. The honest summary is that quantum computers do not threaten blockchains today, but they threaten them on a timeline longer than the lifetime of this book, and migration is a decade-scale project that has not started in earnest.


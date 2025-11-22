# Chapter 4

Now that we went through the history of decentralization and ideology behind this movement, we should take a look at the actual technology behind it to understand the underlying mechanisms that power these decentralized networks.

## Blockchains

The most important thing that comes to mind is the blockchain itself, apart from its usage in decentralized systems.

A blockchain is a database that many computers keep together. Everyone with access has the same copy. When new information is added, all copies update the same way. Entries are placed in blocks. Each block is linked to the previous one by a mathematical fingerprint called a hash. If anyone tries to change an old block, its hash changes, which breaks the link. That broken link is easy for everyone to see.

Here is an example of how a single change can break a hash function output using SHA256:

```
"Hello": 66a045b452102c59d840ec097d59d9467e13a3f34f6494e539ffd32c1bb35f18
"hello": 5891b5b522d5df086d0ff0b110fbd9d21bb4fc7163af34d08286a2e846f6be03
```

With the smallest changes, a checksum hash function can break, and this is the most resilient linking system for a decentralized blockchain because it mathematically prevents tampering.

Which is the most important feature of it. This resilience to tampering is what prevents fraud in decentralized systems.

Normally you trust a bank, company, or government office to keep the records. A blockchain replaces that central authority with a network of independent computers that check each other's work.

Since no single party can change the data by themselves, trust comes from the group rather than a leader.

Blockchains shift the trust from an authority to keep the records correctly to the hash function that links the chains together and the rules of the network which verify the integrity of the blockchain.

## Consensus Mechanisms

When someone wants to add information, such as transferring a cryptocurrency, the request is broadcast to the network. The network then uses a consensus mechanism to decide whether the request is valid. Two common mechanisms:

**Proof of Work**  
Computers compete to solve a hard math puzzle (usually using hash functions or KDFs). The winner earns the right to add the block. This uses a large amount of electricity. The high cost is what discourages bad actors. This process is called mining.

KDFs and custom hash functions are preferred for PoW systems because of the ASIC devices.

ASICs (Application-Specific Integrated Circuits) are chips built to do one thing extremely efficiently, and in the case of PoW, the hashing function PoW mining.

This leads to centralization of mining power, which weakens the network since big players can afford farms of ASIC devices and gain a lot of mining power, making the network more prone to 51% attacks.

51% attacks happen when a single miner or group controls most of the network's power, allowing them to rewrite recent transactions or double-spend coins. KDFs (Key Derivation Functions) make PoW memory or computation-heavy in ways that limit ASIC advantages, helping keep mining more accessible and the network more decentralized.

**Proof of Stake**  
Participants lock up (staking) some of their own coins to earn the right to validate blocks. Validators are selected to propose or confirm new blocks based on the amount of stake they hold and sometimes randomization.

If they validate fraudulent or incorrect data, part or all of their staked coins can be confiscated (slashing).

PoS uses far less energy than PoW because it does not rely on intense computation. However, wealthier participants naturally have more influence, which can centralize control over block production.

PoS also introduces potential attacks like long-range attacks, nothing-at-stake behavior, and validator collusion, which require additional mechanisms such as finality gadgets or checkpointing to mitigate.

Long-range attacks happen when an attacker tries to rewrite old blocks using previously staked coins.

Nothing-at-stake happens when validators cheaply build on multiple forks, risking chain instability.

Validator collusion occurs when a group coordinates to control block production or censor transactions. Networks defend against these using finality gadgets, slashing rules, and randomized validator selection.

So Proof of Stake is not perfect as well. Finding the perfect consensus mechanism has always been a big problem in decentralized blockchains.

**Proof of Capacity**  
In Proof of Capacity, validators allocate unused disk space instead of computing power. More space means higher chance of producing a block. This mechanism uses much lower energy than PoW.

PoC also introduces risks that need extra rules.

Storage grinding happens when attackers try to generate or tweak plots repeatedly to gain an unfair advantage.

Plot compression lets specialized hardware reduce storage needs while keeping high block‑winning odds, creating centralization pressure.

Farm centralization also happens when large operators build massive storage farms.

Networks usually counter these with plot verification rules, time‑costly plotting algorithms, and hardware‑neutral designs to keep participation fair.

**Proof of History**

Proof of History is an interesting one; it was first used in the Solana blockchain.

Proof of History is a mechanism that provides a cryptographic timestamp to prove that events happened in a specific order, without requiring every node to agree on time.

It is not a full consensus mechanism on its own but is usually combined with Proof of Stake for final block validation.

PoH uses a verifiable delay function (VDF) that produces a sequence of outputs that can only be computed in order.

Each output depends on the previous one, creating a chain of cryptographic timestamps. When a validator proposes a block, it includes these timestamps, proving the order and passage of time for transactions.

This way, nodes can verify transaction order quickly without waiting for traditional consensus steps. Validators can agree on transaction order more efficiently, increasing network speed, while other nodes can check timestamps without doing all the computation.

The main limitation of PoH is that it does not prevent malicious block proposals on its own; it still relies on PoS or another consensus mechanism to finalize blocks.

For example, Solana combines PoH with PoS. PoH orders transactions while PoS validators confirm blocks and maintain network integrity.

---

Neither system is perfect. Proof of Work wastes energy. Proof of Stake can drift toward oligarchy, where a small group of people holds most of the power. And Proof of Capacity encourages large farms of hard drives, which can still become resource races.

There are a lot more consensus mechanisms. Explaining them all wouldn't fit in this book, and many new mechanisms will come into play in the future.

Because of how fast this space moves, it's best to always stay on top of the new technologies that are introduced.

## Hash and Signatures

Hash functions and public key signatures are a fundamental part of any blockchain.

**Hash Functions**  
Hash functions verify integrity, they provide a mathematical challenge for PoW consensus mechanisms. It would be impossible to have a tamper-proof blockchain without them.

A hash function takes any input and produces a fixed-size output called a hash. You cannot recover the original data from the hash. It should be extremely hard to find two different inputs that produce the same hash. A tiny change in input creates a completely different output. Nodes must calculate them at high speed.

This means hash functions are one-way, collision-resistant, tamper-proof (Avalanche Effect), and fast to compute.

These properties allow blockchains to link blocks together through block headers. Each block includes the hash of the previous block. Any attempt to alter past data produces a different hash, which breaks the entire chain. This makes tampering obvious to all nodes.

Hash functions also form the difficulty puzzle used in Proof of Work. But in this case, KDFs (Key Derivation Functions) are more suited, because we don't need the hash to be fast to compute; rather the opposite. KDFs are made exactly for this purpose, to be very computationally expensive to compute.

Some KDFs force the miner to store and repeatedly access large amounts of memory. Memory is expensive to scale in custom chips, which helps reduce ASIC advantage, making the network more fair and resistant to attacks like 51% attacks.

The core idea of using KDFs is that the cost to compute the function should be consistent for everyone, so no one gets an unexpected shortcut. This is achievable with KDFs.

For example, scrypt, Argon2, and other memory-hard functions were originally developed to protect passwords because attackers with GPUs or ASICs could crack fast hashes too easily. Blockchains adopted the same idea to preserve decentralization.

KDFs are not perfect. ASICs can still be built for them, but the cost of doing so rises very sharply. This slows centralization and makes mining more accessible to regular users.

**Digital Signatures**  
Public-key cryptography, especially ECCs (Elliptic Curves), provides short private and public keys, unlike RSA which had very long keys, to be used as a user's identity and proof of their actions.

Public key cryptography lets users prove ownership and authorize actions on a blockchain.

Each user controls a private key that only they have and shares a matching public key with the network. When a user signs a transaction with their private key, anyone can verify the signature using the public key. This proves that the transaction is legitimate and that the sender actually intended to move their funds.

Without this, it would be impossible to verify users' actions on blockchains.

Most blockchains rely heavily on elliptic curve cryptography (ECC), which provides strong security with much shorter keys and signatures than older systems like RSA.

Shorter keys save space in each transaction and reduce bandwidth requirements, while allowing nodes to verify signatures more quickly. This matters because blockchains must validate a large volume of transactions across many nodes.

Different blockchains use different elliptic curves depending on their security goals, performance needs, and signature schemes.

For example, secp256k1 is used by Bitcoin, Ethereum, Litecoin, Dogecoin, and most early blockchains. It is paired with ECDSA signatures. Its main advantage is simplicity and widespread support.

Solana, Cardano, Polkadot, Algorand, and many newer chains use Ed25519. It provides faster signature verification, stronger default security properties, and is less error-prone for developers. It uses the EdDSA signature scheme.

We know that these elliptic curve schemes are prone to post-quantum attacks and will eventually be broken if quantum computers advance enough. Because of that, several blockchains and research networks are experimenting with quantum-resistant signature systems.

Post-quantum signatures are not yet mainstream because they require much more storage, more bandwidth, and far more complex key management.

## UTXO vs Accounts

Blockchains use two main models to represent ownership and track state updates.

The UTXO model treats funds as discrete, spendable outputs, while the account model tracks balances and state directly. Both approaches provide security and determinism, but they differ fundamentally in structure, expressiveness, and the ease of building smart contract logic.

**UTXO Model**  
A UTXO (Unspent Transaction Output) is a small chunk of value that can be spent exactly once. A transaction takes some UTXOs as inputs and creates new UTXOs as outputs. The blockchain never updates a balance in place. It only consumes old outputs and creates new ones.

In this model, there is no “account balance.” Your wallet just tracks which UTXOs you control. Old UTXOs never change. They are either unspent or spent. This makes verification very simple. Each UTXO can be checked on its own. Nodes can validate many inputs in parallel because they do not touch shared state. Every UTXO can contain a locking script that says how it can be spent. When you spend it, you must provide a script that satisfies the conditions. A UTXO can be spent once. If a node sees it used twice, it rejects the second attempt.

The UTXO model is mostly used in early blockchains like Bitcoin, Litecoin, and most Bitcoin forks.

The UTXO model is very simple and straightforward, and easy to verify, but building smart contracts is harder because state must be represented as UTXOs. Privacy is also limited because spending patterns reveal links.

**Account Model**  
To fix the problems of the UTXO model, people came up with the account model. The account model keeps a global map of accounts, where each account has a balance and possibly contract code and storage. Transactions directly modify these balances and storage entries.

Balances and contract storage change over time. The blockchain updates existing entries instead of creating new ones. Because balances change, the system uses nonces to stop old transactions from being replayed.

This way, contracts can store and modify data, making complex applications easier to build. For example, the EVM in Ethereum and Sealevel in Solana.

Smart contracts are easier to write, it provides a natural way to express shared global state, it’s easier for developers to develop contracts, and it provides a simpler UX for wallets and explorers.

But one of the problems with the account model is that it’s harder to parallelize and it introduces more complex gas and storage accounting.

I will walk through these concepts like gas and smart contracts in the next chapter.

## Networking

Networking is a massive part of a blockchain system because nodes that hold and verify transactions need to communicate with each other. This is where networking comes into play.

The networking layer allows thousands of independent nodes to spread transactions, blocks, and consensus messages across the system. Most blockchains use a peer-to-peer (P2P) network with no central server, which creates its own set of challenges and design requirements.

**Peer-to-Peer Networks**  
In P2P networks, nodes connect directly to each other instead of relying on a central hub. Each node keeps a list of peers and shares data with them. This avoids single points of failure and allows the network to stay online even if many nodes drop out.

A P2P network always has these key elements:

**Discovery:** Nodes must find peers to connect to. Chains use bootstrapping methods such as DNS seeds, hardcoded nodes, or peer advertisement protocols.

**Random connections:** Nodes connect to several peers chosen at random. This prevents attackers from controlling information flow.

**Openness:** Anyone can join and leave the network. The protocol must handle churn, unreliable peers, and nodes behind NAT or firewalls.

One of the protocols that is used is the gossip protocol. Blockchains use gossip-based spreading. When a node learns new information, it quickly forwards it to its peers, who forward it again, creating a flood-like distribution.

But gossip also creates overhead because the same data travels multiple times. Efficient gossip protocols add techniques like inventory messages, compression, and deduplication to reduce bandwidth.

Another tool used by many blockchains and other decentralized systems is libp2p, a modular networking stack originally developed by the IPFS team.

Libp2p provides a framework for building P2P networks, handling:

- Peer discovery: Nodes can find each other dynamically using DHTs (Distributed Hash Tables), DNS, or bootstrap nodes.
    
- Transport abstraction: Libp2p supports TCP, WebSockets, QUIC, and other transports, allowing nodes behind firewalls or NATs to connect.
    
- Multiplexing and streams: Nodes can maintain multiple logical connections over a single transport, supporting parallel communication for blocks, transactions, and gossip.
    
- Encryption and identity: Each node has a cryptographic identity to ensure authenticated connections and protect against man-in-the-middle attacks.
    
- Gossip protocols and PubSub: Efficient message dissemination to all or selected peers, reducing bandwidth and latency.
    

Libp2p has been used by Ethereum (2.0), Filecoin, Polkadot, Solana, and many more networks. It is not limited to blockchains; decentralized messaging services, web-like networks, and federated platforms can all use this framework to build their networking layer.

**Node Types**

Different nodes participate in networking differently.

Full nodes store the full blockchain, verify every block and transaction, provide data to the rest of the network, and help enforce consensus rules.

Archival nodes store all historical data, not just the necessary states. They're used by explorers and analytics tools.

Light clients do not store the full chain. They just verify headers and use Merkle proofs or similar methods to check data, relying on full nodes for state queries.

**Propagation and Latency**

Propagation in decentralized networks is the act of spreading information. When a node receives a new transaction or new block, it doesn’t just keep it for itself; it forwards the information to its peers. Those peers then forward it to their peers, and so on. Eventually, the information reaches all nodes in the network.

This is how the network stays synchronized and ensures that every node agrees on the current state of the blockchain.

Slow propagation increases the likelihood of forks or competing blocks, creating valid blocks that lose the race to the main chain. Delays and poor connectivity can also increase double-spend risk and favor miners or validators with better network access.

So the latency and efficiency of propagation in these networks really matters.

**Network Threats**

Decentralized networks come with their own vulnerabilities, for example:

- Eclipse attacks: Isolate a node by controlling its peers, feeding it false data.
    
- Sybil attacks: An attacker introduces many fake nodes to manipulate peer selection.
    
- Partitioning attacks: Network splits can cause temporary forks and inconsistent views.
    

Mitigating these attacks is really important for the integrity and security of the system.

By combining randomized peer connections, cryptographic verification of identities, computational costs to participate, and redundant communication paths, decentralized networks can maintain resilience against these attacks. These mitigation strategies are critical to ensure that the system remains secure, censorship-resistant, and capable of reaching consensus.

---

There were a lot of other related concepts on blockchains which were mostly related to blockchains as an infrastructure, which I will cover in a separate chapter. Things like smart contracts, gas, EVMs, and more.


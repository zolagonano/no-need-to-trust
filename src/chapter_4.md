# Chapter 4

Now that we went through the history of decentralization and ideology behind this movement, we can take a look at the actual technology behind it to understand the underlying mechanisms that power these decentralized networks.

Understanding these mechanisms often makes it more clear why these systems behave the way they do, why they have certain limitations, and what is actually powering them.
## Blockchains

The most important thing that comes to mind is the blockchain itself, apart from its usage in decentralized systems it is basically a database.

A database that many computers keep together. Everyone with access has the same copy. When new information is added, all copies update the same way. Entries are placed in blocks. Each block is linked to the previous one by a mathematical fingerprint called a hash. If anyone tries to change an old block, its hash changes, which breaks the link. That broken link is easy for everyone to see.

Checksum hash functions are particularly important in decentralized systems because they are the mathematical algorithm behind integrity checks, making sure data isn't corrupted or changed while transmitting. When input data of a checksum hash function changes, even a bit, it changes the whole output result.

Here is an example of how a single change can break a hash function output using SHA256 (a very commonly used hash function):

```
"Hello": 66a045b452102c59d840ec097d59d9467e13a3f34f6494e539ffd32c1bb35f18
"hello": 5891b5b522d5df086d0ff0b110fbd9d21bb4fc7163af34d08286a2e846f6be03
```

As shown above, even with the smallest changes, a checksum hash function can break, and this makes it the most resilient linking system for a decentralized blockchain because it mathematically prevents tampering. This resilience to tampering is what prevents fraud in decentralized systems.

Normally you trust a bank, company, or government office to keep the records. A blockchain replaces that central authority with a network of independent computers that check each other's work by comparing checksum outputs against the real data.

Since no single party can change the data by themselves, trust comes from the group rather than a leader.

Blockchains shift the trust from an authority to keep the records correctly to the hash function that links the chains together and the rules of the network which verify the integrity of the blockchain.

## Consensus Mechanisms

In decentralized systems, when someone wants to add information to the blockchain, such as transferring a cryptocurrency, the request is broadcasted to the network. The network then uses a consensus mechanism to decide whether the request is valid.

There are a lot of different consensus mechanisms and they get more and more innovative and efficient year by year. But some of the most commonly used consensus mechanisms are:

**Proof of Work**  
Computers compete to solve a hard math puzzle (usually using hash functions or KDFs). The winner earns the right to add the block. This uses a large amount of electricity. The high cost is what discourages bad actors. The whole process of solving and submitting these math puzzles is called mining.

Bitcoin was the first successful cryptocurrency that used Proof of Work using a normal checksum hash function like SHA256. These days KDFs and custom hash functions are preferred for PoW systems because of the ASIC devices.

ASICs (Application-Specific Integrated Circuits) are chips built to do one thing extremely efficiently, and in the case of PoW, the hashing function PoW mining.

This leads to centralization of mining power, which weakens the network since big players can afford farms of ASIC devices and gain a lot of mining power, making the network more prone to 51% attacks.

51% attacks happen when a single miner or group controls most of the network's power, allowing them to rewrite recent transactions or double-spend coins. 

KDFs (Key Derivation Functions) are essentially hash functions but more computationally expensive to perform. They make calculating PoW puzzles memory or computation-heavy in ways that limit ASIC advantages, helping keep mining more accessible and the network more decentralized.

An example of this being Litecoin that used the scrypt KDF algorithm instead of standard checksum hash functions, which requires RAM to calculate, and RAM is not something that an ASIC-like device can bypass. Making it much more expensive and much more fair for everyone else mining Litecoin.

**Proof of Stake**  
Participants lock up (stake) some of their own coins to earn the right to validate other blocks on the blockchains. Validators are selected to propose or confirm new blocks based on the amount of stake they hold and sometimes randomization.

If they validate fraudulent or incorrect data, part or all of their staked coins can be confiscated (slashing). This makes cheating financially expensive without needing to rely on cryptographic puzzles and computational power.

Because PoS doesn't rely on solving complex problems, it uses far less energy than PoW. However, wealthier participants naturally have more influence, which can centralize control over block production.

PoS is not perfect and it also introduces new potential attacks like long-range attacks, nothing-at-stake behavior, and validator collusion, which require additional mechanisms such as finality gadgets or checkpointing to mitigate.

Long-range attacks happen when an attacker tries to rewrite old blocks using previously staked coins.

Nothing-at-stake happens when validators cheaply build on multiple forks, risking chain instability.

Validator collusion occurs when a group coordinates to control block production or censor transactions. Networks defend against these using finality gadgets, slashing rules, and randomized validator selection.

Solving all of these problems produces more complexity to the system and puts PoS mechanism far from perfect. Finding the perfect consensus mechanism has always been a big problem in decentralized blockchains and it might always be because improvements can be endless.

**Proof of Capacity**  
In Proof of Capacity, validators allocate unused disk space instead of computing power. More space means higher chance of producing a block. This mechanism uses much lower energy than PoW.

But PoC is also far from perfect and introduces several risks that need extra rules. Risks such as storage grinding, plot compression and farm centralization that, like PoS, fixing them makes the system more complex and harder to implement.

Storage grinding happens when attackers try to generate or tweak plots repeatedly to gain an unfair advantage.

Plot compression lets specialized hardware reduce storage needs while keeping high block‑winning odds, creating centralization pressure.

Farm centralization also happens when large operators build massive storage farms.

Networks usually counter these with plot verification rules, time‑costly plotting algorithms, and hardware‑neutral designs to keep participation fair.

Chia Coin is a famous example that implemented this consensus mechanism successfully and gained a lot of attention because it allowed a lot of people to use the disks that they had lying around for mining coins.

**Proof of History**

Proof of History is an interesting one; it was first used in the Solana blockchain alongside the PoS as a dual mechanism.

Proof of History is a mechanism that provides a cryptographic timestamp to prove that events happened in a specific order, without requiring every node to agree on time.

It is not a full consensus mechanism on its own because it doesn't prove the validity of the block but the correctness of the order of those blocks, and because of that it is often combined with Proof of Stake for final block validation.

PoH uses a verifiable delay function (VDF) that produces a sequence of outputs that can only be computed in order.

Each output depends on the previous one, creating a chain of cryptographic timestamps. When a validator proposes a block, it includes these timestamps, proving the order and passage of time for transactions.

This way, nodes can verify transaction order quickly without waiting for traditional consensus steps. Validators can agree on transaction order more efficiently, increasing network speed, while other nodes can check timestamps without doing all the computation.

The main limitation of PoH is that it does not prevent malicious block proposals on its own; it still relies on PoS or another consensus mechanism to finalize blocks.

For example, in Solana, PoH orders transactions while PoS validators confirm blocks and maintain network integrity.

---

What we know is that neither system is perfect. Proof of Work wastes energy. Proof of Stake can drift toward oligarchy, where a small group of people holds most of the power. And Proof of Capacity encourages large farms of hard drives, which can still become resource races.

There are a lot more consensus mechanisms. Explaining them all wouldn't fit in this book, and many new mechanisms will come into play in the future.

Because of how fast this space moves, it's best to always stay on top of the new technologies that are introduced.

## Hash and Signatures

Hash functions and public key signatures are a fundamental part of any blockchain, as they're responsible for validating and proving legitimacy of transactions on the chain.

Without hash functions or signatures nobody would be able to validate if a block is not tampered or if someone is actually the owner of an account when transferring funds and information on the blockchain.


**Hash Functions**  
Hash functions verify integrity, they provide a mathematical challenge for PoW consensus mechanisms. It would be impossible to have a tamper-proof blockchain without them.

A hash function takes any input and produces a fixed-size output called a hash. You cannot recover the original data from the hash. It should be extremely hard to find two different inputs that produce the same hash because even a tiny change in input creates a completely different output.

A good hash function for a blockchain consensus should be something that nodes can calculate at high speed but it wouldn't be too fast to calculate for malicious actors, and it shouldn't produce the same output with different inputs.

This means hash functions are one-way, collision-resistant, tamper-proof (Avalanche Effect), and fast to compute.

These properties allow blockchains to link blocks together through block headers. Each block includes the hash of the previous block. Any attempt to alter past data produces a different hash, which breaks the entire chain. This makes tampering obvious to all nodes.

Hash functions also form the difficulty puzzle used in Proof of Work. But in this case, KDFs (Key Derivation Functions) are more suited, because we don't need the hash to be too fast to compute; rather the opposite. KDFs are made exactly for this purpose, to be very computationally expensive to compute.

Originally KDFs have been developed to generate a fixed-length cryptographic key from a password and because of that use case they had to be expensive to compute so if someone would want to calculate millions of possibilities to crack a password they would have to either spend an unreal amount of time or spend an unreal amount of computer power to do so but someone with the correct password would only need to do this once to get the same key from the same password.

And that is the feature that makes KDFs superior to checksum hash functions in a PoW blockchain consensus mechanism, because they take a lot of resources to find the PoW puzzle but a fraction of those resources to validate that puzzle by other nodes on the network.

KDFs use different approaches to achieve this effect. Some KDFs force the miner to store and repeatedly access large amounts of memory while some iterate the same checksum functions thousands to millions of times to make calculation more expensive. KDFs that require memory to calculate are often favored because memory is expensive to scale in custom chips, which helps reduce ASIC advantage, making the network more fair and resistant to attacks like 51% attacks.

The core idea of using KDFs is that the cost to compute the function should be consistent for everyone, so no one gets an unexpected shortcut. This is achievable with KDFs.

For example, scrypt, Argon2, and other memory-hard functions were originally developed to protect passwords because attackers with GPUs or ASICs could crack fast hashes too easily. Blockchains adopted the same idea to preserve decentralization.

This doesn't mean that KDFs are perfect. ASICs can still be built for them, but the cost of doing so rises very sharply. This slows centralization and makes mining more accessible to regular users.

**Digital Signatures**  
Public-key cryptography, especially ECCs (Elliptic Curves), are what make it possible for users to prove their identities, sign their transactions, and receive funds on blockchains.

ECCs are especially important in decentralized systems, because in these systems public keys are the user's identities and they should be within a reasonable length to be able to share and store easily, and ECCs provide exactly that.

Unlike the older public-key cryptography algorithm, RSA, which had thousands of bytes of length for both its private key and public key, ECCs provide the same amount of security for a fraction of that length.

Public key cryptography is what lets users prove ownership and authorize actions on a blockchain.

In decentralized systems, each user controls a private key that only they have and shares a matching public key with the network. When a user signs a transaction with their private key, anyone can verify the signature using the public key. This proves that the transaction is legitimate and that the sender actually intended to move their funds.

Without this, it would be impossible to verify users' actions on blockchains.

Because of the amount of reliance and relevance of public key cryptography in these systems, having a short and strong public-key cryptography algorithm is essential. Shorter keys save space in each transaction and reduce bandwidth requirements, while allowing nodes to verify signatures more quickly. This matters because blockchains must validate a large volume of transactions across many nodes and large keys could easily pile up.

Different blockchains use different elliptic curves depending on their security goals, performance needs, and signature schemes.

For example, secp256k1 is used by Bitcoin, Ethereum, Litecoin, Dogecoin, and most early blockchains. It is paired with ECDSA signatures. Its main advantage is simplicity and widespread support.

Solana, Cardano, Polkadot, Algorand, and many newer chains use Ed25519. It provides faster signature verification, stronger default security properties, and is less error-prone for developers. It uses the EdDSA signature scheme.

We know that these elliptic curve schemes are prone to post-quantum attacks and will eventually be broken if quantum computers advance enough. Because of that, several blockchains and research networks are experimenting with quantum-resistant signature systems.

But post-quantum signatures are not yet mainstream because they require much more storage, more bandwidth, and far more complex key management, which is not simply worth implementing at the time.

## UTXO vs Accounts

Blockchains usually use two main models to represent ownership and track state updates. The UTXO model and the Accounts Model.

The UTXO model treats funds as discrete, spendable outputs, while the account model tracks balances and state directly. Both approaches provide security and determinism, but they differ fundamentally in structure, expressiveness, and the ease of building smart contract logic.

**UTXO Model**  
A UTXO (Unspent Transaction Output) is a small chunk of value that can be spent exactly once. A transaction takes some UTXOs as inputs and creates new UTXOs as outputs. The blockchain never updates a balance in place. It only consumes old outputs and creates new ones.

Think of a UTXO like a physical coin. If someone sends you 2 BTC, the blockchain doesn't increase a number called “your balance.” Instead, you receive a specific 2 BTC output that belongs to you.

In this model, there is no “account balance.” Your wallet just tracks which UTXOs you control. Old UTXOs never change. They are either unspent or spent. This makes verification very simple. Each UTXO can be checked on its own. Nodes can validate many inputs in parallel because they do not touch shared state. Every UTXO can contain a locking script that says how it can be spent. When you spend it, you must provide a script that satisfies the conditions. A UTXO can be spent once. If a node sees it used twice, it rejects the second attempt.

If you later want to spend 1.5 BTC, you can't partially modify that 2 BTC output. You consume the entire 2 BTC UTXO and create new outputs: one sending 1.5 BTC to someone else and another sending 0.5 BTC back to yourself as change.

So the old coins are permanently marked as spent, and the new ones become available to spend.

The UTXO model is mostly used in early blockchains like Bitcoin, Litecoin, and most Bitcoin forks.

The UTXO model is very simple and straightforward, and easy to verify, but building smart contracts is harder because state must be represented as UTXOs. Privacy is also limited because spending patterns reveal links.

**Account Model**  
To fix the problems of the UTXO model, people came up with the account model. The account model keeps a global map of accounts, where each account has a balance and possibly contract code and storage. Transactions directly modify these balances and storage entries.

Balances and contract storage change over time. The blockchain updates existing entries instead of creating new ones. Because balances change, the system uses nonces to stop old transactions from being replayed.

In accounts model, when a transaction is executed, it can directly modify this existing state. If Alice has 5 ETH and sends 2 ETH to Bob, the blockchain doesn't consume a 5 ETH object and create two new ones. It simply changes Alice's balance from 5 ETH to 3 ETH and Bob's balance increases by 2 ETH.

This way, contracts can store and modify data, making complex applications easier to build. For example, Ethereum's EVM and Solana's Sealevel execution environment use account-based state models.

Smart contracts are easier to write, it provides a natural way to express shared global state, it’s easier for developers to develop contracts, and it provides a simpler UX for wallets and explorers.

In Accounts model, a smart contract can have its own balance, code, and storage, and transactions can modify that storage over time. This makes applications with complex, persistent state much more natural to build.

But one of the problems with the account model is that it’s harder to parallelize and it introduces more complex gas and storage accounting. If two transactions modify the same account or storage location, they cannot always be executed independently.

I will walk through these concepts like gas and smart contracts in the next chapter.

## Networking

Networking is a massive part of a blockchain system because nodes that hold and verify transactions need to communicate with each other. This is where networking comes into play.

The networking layer allows thousands of independent nodes to spread transactions, blocks, and consensus messages across the system. Most blockchains use a peer-to-peer (P2P) network with no central server, which creates its own set of challenges and design requirements.

But this design is crucial to make sure no one controls the network and everything remains fully decentralized and transparent even at the network layer.

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

In decentralized networks there are various types of nodes and different nodes participate in networking differently.

Full nodes store the full blockchain, verify every block and transaction, provide data to the rest of the network, and help enforce consensus rules.

Archival nodes store all historical data, not just the necessary states. They're used by explorers and analytics tools.

Light clients do not store the full chain. They just verify headers and use Merkle proofs or similar methods to check data, relying on full nodes for state queries.

**Propagation and Latency**

Propagation in decentralized networks is the act of spreading information. When a node receives a new transaction or new block, it doesn’t just keep it for itself; it forwards the information to its peers. Those peers then forward it to their peers, and so on. Eventually, the information reaches all nodes in the network.

This is how the network stays synchronized and ensures that every node agrees on the current state of the blockchain.

Slow propagation increases the likelihood of forks or competing blocks, creating valid blocks that lose the race to the main chain. Delays and poor connectivity can also increase double-spend risk and favor miners or validators with better network access.

So the latency and efficiency of propagation in these networks really matters for both efficiency and integrity.

**Network Threats**

Every network has security issues and it's the same for decentralized networks, these networks come with their own vulnerabilities as well, for example:

- Eclipse attacks: Isolate a node by controlling its peers, feeding it false data.
    
- Sybil attacks: An attacker introduces many fake nodes to manipulate peer selection.
    
- Partitioning attacks: Network splits can cause temporary forks and inconsistent views.
    

Mitigating these attacks is really important for the integrity and security of the system.

By combining randomized peer connections, cryptographic verification of identities, computational costs to participate, and redundant communication paths, decentralized networks can maintain resilience against these attacks. These mitigation strategies are critical to ensure that the system remains secure, censorship-resistant, and capable of reaching consensus.

---

There were a lot of other related concepts on blockchains which were mostly related to blockchains as an infrastructure, which I will cover in a separate chapter. Things like smart contracts, gas, EVMs, and more.


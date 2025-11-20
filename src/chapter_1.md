# Chapter 1

The first usable decentralized system ever built was Bitcoin in 2008 by Satoshi Nakamoto. There had been many attempts before that to create digital money, but they failed.

In 1976, Diffie and Hellman introduced the idea that two parties could communicate securely without sharing a secret key beforehand. This was the foundation of public key cryptography and made later digital money systems possible.

Two decades later, in 1991 and 1992, Haber and Stornetta focused on document authenticity. They faced the problem that digital documents could be changed at will, with no reliable way to prove when a document was created. Their solution was to chain blocks of hashed documents together so that tampering with one block breaks the chain. This created one of the earliest forms of blockchain style timestamping.

In the 1980s, David Chaum proposed eCash. As far as we know, this was the first attempt at digital money. Its goals were similar to Bitcoin's: privacy preserving and untraceable transactions between users and banks. eCash relied on blind signatures to allow users to withdraw digital coins from a bank and spend them anonymously. But eCash was not decentralized. Its trust model depended entirely on banks.

In 1998, Wei Dai, a computer scientist, wanted a system where money could exist without any bank. He wrote the b money proposal. His idea was that participants would maintain records of each other's balances, and money creation could be tied to computational work. b money introduced the concept of distributed consensus and digital scarcity without a central authority. But the design was entirely theoretical. No one had implemented it, and there was no practical method for participants to agree on the ledger reliably.

Around the same time, Nick Szabo expanded on the ideas of b money. He suggested the use of proof of work puzzles to create scarce digital tokens. Each token would be tied to a chain of previous proofs, creating a tamper evident ledger. This was effectively an early blockchain concept. But it also never got implemented and relied on people voluntarily following the rules, since the consensus problem was still unsolved.

Satoshi saw all of these attempts and innovations as the missing pieces of the puzzle for digital trustless money. Satoshi did not invent everything, but they combined cryptography, economics, and distributed computing in a way no one else had. The pieces existed, but no one had solved the double spending problem in a decentralized setting until Bitcoin.

After Bitcoin, many pre existing ideas and innovations were implemented in decentralized systems.

For example, before Solana, verifiable delay functions existed in cryptography research but had not been used to construct blockchain consensus. Solana used them in 2017 to create a cryptographic timestamp of events. This provided a sequential ordering of events without relying on external clocks and reduced coordination overhead in a distributed network.

The main issue that Bitcoin solved was double spending.

Double spending in digital currencies was a major problem because a digital file can be copied perfectly. If you send someone a digital token, nothing stops you from sending an identical copy to someone else unless a trusted party checks every transaction. Traditional systems solve this by relying on a central ledger managed by a bank. The bank’s ledger decides which transaction is valid and which is rejected.

Bitcoin removed the central authority by distributing the ledger across thousands of nodes and adding rules that prevent conflicting transactions from being accepted.

In Bitcoin, every node keeps a copy of the blockchain. If you try to spend the same coins twice, the network will see that one of the transactions does not match the current state of the ledger.

Miners collect pending transactions and attempt to publish the next block. Only one block wins at a time because of proof of work.

Miners must commit significant computational effort to create each block. This cost discourages rewriting history. If someone wants to double spend, they need to create an alternative chain that outpaces the honest chain, which is impractical when the honest network has more hash power.

Nodes follow the valid chain with the most accumulated proof of work. A conflicting transaction that appears in a shorter chain gets ignored. This rule is central because it coordinates agreement without trusted intermediaries.

Even if an attacker temporarily produces a competing block, the chance that they can keep extending their fork drops quickly as more blocks are added on top of the honest chain.

A common misunderstanding is that cryptography alone solves double spending. It does not. Signatures prove ownership, but they do not choose between two conflicting transactions signed by the same key. The consensus mechanism is what resolves conflicts, and this will be covered in more detail in later chapters.

And after Bitcoin, there were still a lot of issues left to solve. For example, Bitcoin's PoW consensus mechanism was computationally cheap to perform because it used the SHA-2 hash algorithm, which is a cryptographic checksum function. SHA-2 was not designed to be computationally expensive; rather, the opposite. As a result, people and companies started building ASIC devices that were made solely to perform SHA-2 computations, and that became a problem. It weakened the network and made it less fair. Originally, anyone with a CPU could mine Bitcoin, but now anyone with farms filled with specialized devices could mine. Since not everyone could do this fairly, some people could gain a lot more hash rate and therefore more control over the network.

This led to many new innovations around consensus mechanisms, such as using KDFs (Key Derivation Functions), which are designed to be computationally expensive for deriving passwords instead of using checksum hash functions as a PoW algorithm. For example, Litecoin uses scrypt. Scrypt requires not only CPU but also memory, and memory is very expensive to scale and expand. Unlike purely computational hash functions, there are not many workarounds.

People even went beyond the idea of computationally expensive work as a consensus mechanism. We now have PoS (Proof of Stake) for consensus in Ethereum, which fully removed the need for computational work. This was a great innovation in many ways, since mining farms require a lot of electricity and energy. PoS made cryptocurrencies much more eco-friendly and scalable.

In PoS consensus, instead of solving a mathematical puzzle, participants lock up a certain amount of the blockchain’s native token. The more you stake, the higher your chance of being selected to propose the next block. Validators are typically chosen pseudo-randomly, weighted by stake. Some systems also add factors like time staked or reputation. This randomness reduces predictability, which helps prevent attacks like long-range or nothing-at-stake attacks.

Once a validator proposes a block, other validators attest to its validity. If a supermajority, often two thirds, of validators agree, the block is finalized. This is faster than PoW’s probabilistic finality. Validators can lose part of their staked funds if they act maliciously, for example signing conflicting blocks, or fail to participate. Slashing enforces honesty economically, creating a system of rewards and punishments to maintain the integrity of the chain.

This was a major step toward the scalability of crypto since transaction confirmation times were heavily reduced. Blocks no longer needed to be mined, which would take several minutes. Although there were attempts to make this issue more tolerable, for example Bitcoin Cash was a fork of Bitcoin created for this exact reason. The solution they used was increasing the block size so that more transactions could be confirmed in each mined block.

There have also been more innovative consensus mechanisms after PoS, like Hybrid PoW/PoS, Proof of Capacity, Avalanche, and more, which will be covered in later chapters.

Decentralization has always been about more than just money or finance. It is about building systems where control and access are shared rather than concentrated. Long before Bitcoin, there were pioneering networks exploring this idea in the context of data and communication.

It started with BitTorrent in 2001, which reimagined file sharing. Instead of relying on a central server, BitTorrent allowed users to download pieces of a file from many peers simultaneously, forming a decentralized “swarm.” This approach made file distribution faster and more resilient while demonstrating the power of cooperative, peer-to-peer networks.

Around the same time, Freenet was exploring decentralization from a privacy-focused angle. It provided a platform for anonymous, distributed storage and communication, allowing users to share information without centralized control or fear of censorship. Freenet showed that decentralization could protect not only efficiency but also freedom of expression and personal privacy.

Building on these ideas, projects like ZeroNet came to life. ZeroNet created the first fully functional web-like network where websites themselves could exist in a decentralized way. Each site was signed and distributed among its visitors, making censorship very difficult and putting control directly into users’ hands.

Finally, IPFS (InterPlanetary File System) took the concept further. Inspired by BitTorrent and Freenet, it introduced content-addressed storage, immutable data, and efficient peer-to-peer retrieval, turning decentralized file sharing into a backbone platform for modern web applications. Unlike previous systems, IPFS made it possible to think about a web where files are identified by what they are, not where they are stored, creating a foundation for a truly distributed internet. Which later become a building block for many Web3 applications.

From BitTorrent’s swarm networks to IPFS’s content-addressed web, this evolution shows that decentralization has always been about freedom, preventing censorship, protecting privacy, and making things trustless, laying the groundwork for everything from decentralized websites to cryptocurrencies.

---

Now that we have a rough understanding of the history of decentralization and how things stood on each other's shoulders to build the Web3 we know, the next chapter will cover the cypherpunk philosophy, cryptoanarchism, and the ideology and motives behind this whole movement.

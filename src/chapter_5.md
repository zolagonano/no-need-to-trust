# Chapter 5

Bitcoin had major limitations. Perhaps Satoshi never thought it would blow up this much. Slow transactions, not the best PoW algorithm, not the best blocksize for scaling, and certainly not the best model for scripting and supporting complex applications. These prevented Bitcoin and Bitcoin forks from scaling beyond just a transfer of value.

Finance is far broader than cash or gold. It includes loans, trading, investments, credit creation, assets, liabilities, insurance, derivatives, and more. If decentralization were to evolve beyond currency and penetrate broader financial systems (or even governance, identity, and digital assets), it needed to become more than a transactional protocol. It had to be a scalable infrastructure capable of executing programmable logic.

This is where Vitalik Buterin’s Ethereum came into play. In 2013, Buterin proposed a new blockchain designed to go beyond the limitations of Bitcoin. Ethereum was crowdfunded in 2014 and launched in 2015, providing a platform for decentralized governance, applications, finance, NFTs, and digital identity. Its goal was ambitious: to create a programmable world computer capable of supporting virtually any decentralized application. And in many ways, it succeeded.

At the core of Ethereum is the Ethereum Virtual Machine (EVM). The EVM executes smart contracts, self-executing code deployed on the blockchain, and ensures deterministic outcomes across all nodes. “Code is law” is truly implemented in this system: every transaction is validated by the network, and contracts execute exactly as programmed. The EVM can perform any computation, given enough resources. Its gas system incentivizes efficient computation and prevents abuse, ensuring that the network is not overwhelmed by infinite loops or excessively complex calculations.

Smart contracts are also composable, meaning they can interact with one another, forming complex decentralized systems. This modularity was what allowed Ethereum to scale beyond simple finance, enabling the creation of applications ranging from decentralized exchanges to NFTs and identity systems. The EVM’s universality also became a standard that inspired entire ecosystems of smart contract development.

At the same time, other blockchains looked into alternatives to the EVM. Non-EVM chains such as Solana, with its parallelized Sealevel runtime, Cardano with its formally verified KEVM framework, and NEAR Protocol with a WASM-based VM, were designed to address limitations in speed, efficiency, or developer accessibility. These chains offered higher throughput or language flexibility but often lacked Ethereum’s depth of composable contracts and developer ecosystem, highlighting a trade-off between performance and network effects.

Ethereum itself has evolved technically as well. At first, it relied on proof-of-work (PoW), similar to Bitcoin, to secure the network. While PoW provided security, it was energy-intensive, slow, and limited scalability. To address these issues, Ethereum transitioned to proof-of-stake (PoS) with the Merge.

PoS heavily reduced energy consumption and allowed validators to secure the network by staking ETH rather than expending computational work. This shift also opened the door for improved scalability, paving the way for layer-2 solutions and future sharding implementations, without compromising decentralization.

Ethereum was designed to be more than a currency. And it became just that.

It is infrastructure. A programmable, decentralized platform that enables finance, governance, identity, and complex applications.

## Smart Contracts and Composability

Composability is the ability of one contract to interact seamlessly with others, which enables modular, complex systems. For example, in DeFi, a lending protocol can use an automated market maker to determine collateral values, or a yield aggregator can pull liquidity from multiple protocols to maximize returns for users. This stacking of protocols on top of each other creates a network effect: each new contract can benefit from existing protocols, accelerating innovation exponentially.

This was huge, because it allowed rapid experimentation and iteration. Developers didn’t need to reinvent the wheel. They could simply build on top of existing protocols, improving them or combining them in new and innovative ways. Entire ecosystems of applications could grow in a relatively short time, producing complex financial primitives like flash loans, synthetic assets, or composable insurance products. The modularity also meant users could mix and match protocols to create personalized financial strategies, something impossible in traditional finance.

Although this wasn’t a perfect system. Complex networks of interacting contracts can create cascading failures if one contract fails, like dominos. Or if a vulnerability is exploited in one protocol that others rely on. Events like the 2020 bZx exploit or the repeated failures of poorly audited lending protocols show how interconnected these systems can become a source of systemic risk.

Composability along with privacy is an extremely challenging thing to do. Most composable contracts rely on public state to function, which means privacy-preserving mechanisms are very difficult to implement without breaking interoperability. Only a handful of projects have managed to combine composability with privacy in a meaningful way, often using advanced cryptography or layer-2 solutions, but these usually remain experimental.

Despite its risks, composability is one of Ethereum’s most defining features. It’s what allows the blockchain to scale beyond single-purpose financial applications into entire ecosystems of interoperable services.

Without composability, DeFi would be siloed, innovation would move slower, and the idea of a programmable, modular financial system wouldn’t even exist.

## DeFi: What It Is and How It Differs from Decentralized Currency

To understand DeFi (Decentralized Finance), we first need to differentiate Finance from money.

Money is simply a medium of exchange, a store of value, and a unit of account. Physical cash, bank deposits, and digital currencies like Bitcoin all serve this purpose. Bitcoin, in particular, is a decentralized, digital form of money: it allows peer-to-peer transfers without intermediaries, with transparency and limited supply. But Bitcoin alone does not provide tools for lending, trading, or complex financial management. It is primarily a tool for value transfer and wealth storage.

Finance, on the other hand, is much broader. It is the management, creation, and study of money, investments, banking, credit, assets, and liabilities. Finance encompasses personal, corporate, and public domains which range from savings and loans to trading in stocks, bonds, derivatives, and insurance. It includes complex mechanisms and systems that allow wealth to be leveraged, allocated, and managed efficiently. Essentially, finance is the infrastructure that makes money productive, rather than just something that changes hands.

DeFi, or Decentralized Finance, is finance but rebuilt on blockchain. It replicates the functions of traditional financial systems like lending, borrowing, trading, investing, and insurance but without relying on banks or centralized intermediaries and in a trustless manner.

Smart contracts are the backbone of DeFi: self-executing programs on Ethereum (and other chains) that enforce rules and handle assets autonomously.

Bitcoin primarily moves and stores value. DeFi enables the creation, allocation, and management of value in sophisticated ways.

Smart contracts automate financial operations, such as automatically liquidating undercollateralized loans or executing trades based on pre-defined conditions.

Anyone with an internet connection can interact with DeFi protocols, bypassing traditional geographic and regulatory barriers.

DeFi protocols can integrate with one another, allowing complex financial products to be built on top of existing ones. For example, a user can deposit collateral in one protocol, borrow assets from another, and then supply liquidity to a third, all without intermediaries.

Platforms like Aave and Compound allow users to lend assets to earn interest or borrow against their holdings.

Uniswap, Sushiswap, and others enable peer-to-peer trading without a centralized order book.

Decentralized alternatives to fiat, pegged to value-stable assets.

Although DeFi opens unprecedented opportunities, it comes with unique risks: smart contract vulnerabilities, cascading liquidations, impermanent loss in liquidity pools, and governance risks. Unlike banks, there is no safety net; users have to bear the full consequences of protocol failures or exploits.

DeFi is essentially the full stack of finance but rebuilt in a decentralized, permissionless, and programmable form. It is the next step beyond Bitcoin, making it not just digital money, but digital financial infrastructure that anyone can access, build on, and innovate with.

## Decentralized Infrastructure

Ethereum exists as part of a layered, decentralized infrastructure.

It is designed to distribute responsibilities across multiple actors while minimizing reliance on centralized intermediaries.

Understanding these layers helps us understand how decentralized applications operate and why infrastructure matters for the security, efficiency, and scalability of the network.

**Network Layer:** This is the foundation. Nodes communicate, propagate transactions, validate blocks, and maintain consensus across the network. Each full node keeps a copy of the blockchain, ensuring redundancy and resilience. The decentralized nature of this layer prevents any single actor from controlling transaction history or censoring activity, but it also introduces latency and computational overhead compared to centralized systems.

**Protocol Layer:** On top of the network layer sits the protocol, the ruleset governing state changes. Smart contracts execute here, and the blockchain enforces deterministic outcomes. The protocol layer ensures consistency across nodes: every transaction, contract execution, or state update follows the same rules. Ethereum’s protocol also manages gas fees, which incentivize efficient computation and prevent network abuse.

**Application Layer:** This is where users interact with the blockchain. Decentralized applications (dApps), wallets, marketplaces, and other tools provide functionality without intermediaries. While the underlying network and protocol are decentralized, the application layer determines usability, accessibility, and how effectively users can use the underlying infrastructure.

Beyond Ethereum itself, decentralized infrastructure extends to supporting technologies that enhance storage, computation, and data reliability:

**IPFS (InterPlanetary File System) and Filecoin:** These protocols provide decentralized storage, removing dependence on centralized cloud providers and ensuring files remain accessible even if individual nodes go offline.

**Decentralized Oracles:** Services like Chainlink feed real-world data into smart contracts, enabling them to act on external events without relying on a single source.

**Layer-2 Solutions:** Optimistic rollups, zk-rollups, and sidechains help scale Ethereum by processing transactions off-chain while still relying on the main chain for security. These solutions reduce congestion, lower fees, and improve throughput without compromising decentralization.

These decentralized infrastructures were built to minimize single points of failure, increase trustlessness, and distribute power among participants.

However, there are always trade-offs. Higher decentralization often reduces throughput and increases latency. Layer-2 solutions and alternative protocols can improve scalability but sometimes at the cost of composability or security. Balancing these factors (decentralization, scalability, and security) is a constant challenge for any blockchain system.

Decentralized infrastructure is about creating systems resilient to censorship, single points of failure, and centralized control, while enabling a flexible foundation for applications, finance, and digital governance.

## Single-Chain to Multi-Chain Infrastructure

Ethereum started as a single, dominant chain, serving as the primary platform for smart contracts, decentralized applications, and DeFi. In its early years, most of the blockchain ecosystem was concentrated on Ethereum, benefiting from network effects, developer attention, and liquidity. However, as adoption grew, so did the limitations of a single-chain model.

Congestion, high gas fees, and scalability issues showed the practical limits of relying on one chain for a growing movement.

This led to the rise of multi-chain infrastructure, where different blockchains coexist and interact to serve specialized purposes:

Not all chains are built the same. Some prioritize high throughput and low latency for trading applications (like Solana), others focus on minimal fees and efficient computation for small-scale dApps (like Polygon), while privacy-focused chains (like Secret Network or Oasis) enable confidential smart contracts. This specialization allows developers to choose the platform that best fits the requirements of their application, rather than being limited by a one-size-fits-all environment.

Multi-chain ecosystems require communication across chains. Bridges, wrapped tokens, and cross-chain protocols enable assets, data, and smart contract interactions to flow between chains. For example, a token minted on Ethereum can be used in a DeFi protocol on Avalanche or Solana through a bridge. Interoperability opens the door for larger, integrated ecosystems, where composability and liquidity can extend beyond the boundaries of a single chain.

But multi-chain systems are not without risks. Liquidity can become heavily fragmented and complex, making it harder to move large amounts of capital efficiently. Security is more complex: bridges and cross-chain mechanisms are frequent targets for hacks as they spread the attack surface area, as seen in several high-profile exploits. Governance also becomes more complicated. Protocol upgrades and consensus decisions must consider interactions across chains, and coordination between different communities is often difficult.

Despite all risks, interconnected blockchains promise greater scalability, specialization, and resilience, but they also require more sophisticated tools and methods for interoperability, risk management, and governance coordination.

## NFTs, Soulbound Tokens, and Decentralized IDs

Non-Fungible Tokens (NFTs), Soulbound Tokens (SBTs), and Decentralized IDs (DIDs) represent some of the most significant innovations in bridging the decentralized blockchain world with real-life identity, ownership, and personal reputation.

They move beyond money and finance, extending Ethereum and other blockchains into social, cultural, and personal worlds.

### Digital Ownership

NFTs are unique, indivisible tokens representing ownership of a digital or physical asset. Unlike cryptocurrencies, which are fungible and identical, each NFT is distinct and verifiable on-chain. This uniqueness allows them to represent art, music, collectibles, real estate, intellectual property, or even digital event tickets.

The importance of NFTs lies in their ability to create provable ownership and scarcity in a digital environment. In traditional systems, ownership is often centralized, recorded in databases controlled by authorities. NFTs, on the other hand, make ownership trustless and portable, allowing a user to prove control of an asset anywhere in the digital ecosystem without relying on any centralized system.

Beyond simple ownership, NFTs also allow composability. A single NFT can carry metadata, programmable royalties, or permissions that interact with other smart contracts. For example, an NFT representing a concert ticket could automatically grant access to an event, trigger a royalty payout to the artist, or unlock additional digital content.

NFTs are more than just meme collectibles; they are programmable assets that can link the digital and physical worlds.

### Identity and Reputation on Chain

Soulbound Tokens extend the idea of NFTs into the world of personal identity and reputation.

Unlike NFTs, SBTs are non-transferable, tied permanently to a specific wallet or individual. This makes them ideal for representing personal credentials, achievements, or affiliations, things that should not be sold or traded.

SBTs can serve as proof of education, professional experience, memberships, certifications, and anything imaginable.

By storing this information on-chain, they create a decentralized, verifiable record of personal accomplishments, which could replace centralized systems like diplomas, licenses, or professional endorsements.

### Digital Identity

Unlike centralized identity providers, DIDs give individuals full control over their personal information, allowing selective disclosure without relying on intermediaries.

DIDs can interact with SBTs and NFTs to form a broader digital identity ecosystem. For example, a decentralized identity could prove that the holder owns a specific NFT or that they have certain credentials without revealing unrelated personal data.

NFTs, SBTs, and DIDs collectively serve as bridges between physical reality and decentralized networks. They enable:

**Ownership Verification:** Proof of property or rights without centralized registries.

**Digital Reputation:** Portable records of achievements, trustworthiness, and more.

**Programmable Interaction:** Smart contracts that respond automatically to token ownership or identity credentials.

**Access Control:** NFT or SBT-based permissions for events, memberships, or services.

One challenge with NFTs, SBTs, and DIDs is that blockchain data is public by default. Every token and transaction can be seen, creating potential privacy issues for users who may not want their assets or identity fully exposed.

Zero-knowledge proofs (zk-proofs) provide a solution. Again, using zk-proofs, it is possible to prove ownership of an NFT, a credential, or an identity without revealing the underlying data. For instance, a user could prove they hold a specific SBT representing a professional certification without revealing their name or the issuing institution. Technical details of zk-proofs will be explained in later chapters.

NFTs, Soulbound Tokens, and Decentralized IDs expand blockchain’s potential far beyond money. They allow digital assets to mirror real-life ownership, reputation, and identity, creating a more integrated, programmable world.

## Centralization Problems

Decentralization, in practice, is rarely absolute.

Even networks like Ethereum, which are designed to minimize central points of control, remain connected to centralized systems in critical ways.

While thousands of nodes exist globally, staking and validator power is often concentrated among a relatively small number of people.

For example, in proof-of-stake systems, a few large validators or staking pools can control a significant portion of the total staked tokens, giving them disproportionate influence over block production and consensus.

Many projects rely on a core team or foundation to develop and maintain the protocol. Decisions on upgrades, security patches, and governance rules often come from a concentrated group of developers, creating potential points of influence or bias.

And even in DeFi ecosystems, centralized exchanges and custodians hold large volumes of user assets. Users trusting these platforms reintroduce centralized risk, from censorship and withdrawal freezes to outright hacks and mismanagement.

Token-based voting systems often favor large holders, meaning major decisions can be disproportionately influenced by whales and early investors.

Most DeFis and DApps rely on centralized network infrastructures to work, like cloud services, RPC servers, centralized websites, and databases.

And most stablecoins and real-life assets need to be managed by a centralized institution. For example, USDT is managed by the Tether company, which ensures it stays pegged to 1 US dollar at all times. And we still have to trust one company to do its job right. These things are essentially sugar-coated centralization wrapped in decentralized solutions.

While blockchain design aims to distribute control, practical realities often reintroduce centralized influence.

Ultimately, understanding centralization problems is critical because decentralization is not binary. It is a spectrum.

Every blockchain faces trade-offs between security, efficiency, and the ideal of distributed control. What matters is moving toward a fairer decentralization and constantly reducing the reliance on centralized systems.

## Roles in Autonomy

Autonomy in decentralized systems is not absolute either. It is distributed across various actors who collectively maintain, govern, and use the network. Each role comes with distinct responsibilities and influence:

Users drive adoption and liquidity. They interact with protocols, supply assets, vote in governance mechanisms, and provide feedback. In many DeFi applications, users’ decisions directly affect protocol behavior, such as lending pool utilization or liquidity incentives.

Validators and miners maintain consensus, validate transactions, and secure the network. Their autonomy is constrained by protocol rules, but they influence which transactions are included in blocks and help enforce network integrity.

Developers, core teams, independent contributors, and community developers create, maintain, and upgrade protocols. While decentralized contributions are possible, early design choices and governance frameworks often give significant influence to developers or foundations.

Token holders or DAO participants vote on protocol upgrades, parameter changes, or fund allocations. This collective decision-making provides distributed control but is often weighted by stake, creating the potential for imbalance between large holders and smaller participants.

Autonomy in blockchain systems exists on a spectrum as well. Full decentralization is idealized, but practical systems must balance control, efficiency, and security.

Understanding how power and responsibility are distributed helps us see why decentralization is not just technical; rather, it is social, economic, and political.

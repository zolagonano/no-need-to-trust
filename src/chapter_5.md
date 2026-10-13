# Chapter 5

Bitcoin had major limitations. Perhaps Satoshi never thought it would blow up this much. Slow transactions, not the best PoW algorithm, not the best blocksize for scaling, and certainly not the best model for scripting and supporting complex applications. These prevented Bitcoin and Bitcoin forks from scaling beyond just a transfer of value.

These limitations are very important since finance is far broader than cash or gold. It includes loans, trading, investments, credit creation, assets, liabilities, insurance, derivatives, and more. If decentralization were to evolve beyond currency and penetrate broader financial systems (or even governance, identity, and digital assets), it needed to become more than a transactional protocol. It had to be a scalable infrastructure capable of executing programmable logic.

This is where Vitalik Buterin’s Ethereum came into play. In 2013, Buterin proposed a new blockchain designed to go beyond the limitations of Bitcoin. Ethereum was crowdfunded in 2014 and launched in 2015, providing a platform for decentralized governance, applications, finance, NFTs, and digital identity. Its goal was ambitious: to create a programmable world computer capable of supporting virtually any decentralized application. And in many ways, it succeeded.

Buterin introduced something that had long existed in the world of computers into Ethereum: a virtual machine (VM) named the EVM (Ethereum Virtual Machine).

Think of a VM as an imaginary computer defined by software. For example, a very simplified VM might look something like this:

```
Registers: A, B, C
Memory: 0..65535
Instructions:
    PUSH 5
    ADD
    STORE
    JUMP
```

A program written for that imaginary computer can run on your real computer because a VM implementation interprets or executes those instructions.

But that is a full VM. Ethereum's EVM is much smaller than that; it is much closer to a software-defined CPU, which has certain specifications and instructions. Code written in Solidity (EVM's programming language) compiles to EVM bytecode, and the Ethereum client executes that bytecode according to the EVM specification.

This code written in Solidity is called a smart contract, which is self-executing code deployed on the blockchain. The EVM executes smart contracts and ensures deterministic outcomes across all nodes.

This deterministic nature of the EVM is very important for the integrity of the blockchain. And that's what makes it different from a normal VM, because in most VMs, determinism is not guaranteed, but in the EVM, it is.

Here is an example of a VirtualBox machine (a VM) vs. the EVM. I know this is not the most relevant comparison because these two are very different, but it helps explain the difference better:

The main difference is that a normal VM deliberately connects to the outside world: in a VirtualBox machine, you can inspect hardware information, get the current time, or interact with devices. All of these things can produce different results on different machines, and that's perfectly fine for a normal VM because determinism doesn't need to be guaranteed.

But the EVM is not a full VM and doesn't need to be; it's more like a computational environment. The EVM controls the inputs that a smart contract can see and defines exactly how those inputs are processed, like a calculator:

```
Same inputs + Same rules = Same answer
```

This is why all Ethereum nodes first agree on the current blockchain state:

```
Alice balance = 10 ETH
Contract storage[0] = 50
```

And they receive the same transaction:

```
call contract.increment()
```

And they all execute the same contract bytecode and follow the same rules because the EVM specifies exactly what every operation means.

```
ADD -> addition
SLOAD -> read storage
SSTORE -> write storage
MUL -> multiplication
```

This way, different EVM implementations must follow the same rules. A contract can't simply say, 'Read my computer's clock, read my filesystem, fetch a URL, or generate a random number,' because then different nodes could get different answers.

Because the state, transaction, code, environment, and execution rules are the same, every Ethereum client that executes a smart contract gets the same result.

This way, “Code is law” is truly implemented in this system: every transaction is validated by the network, and contracts execute exactly as programmed. The EVM can perform any computation, given enough resources.

Even though the EVM is a very simple VM, the smart contracts on it are composable, meaning they can interact with one another, forming complex decentralized systems. This modularity was what allowed Ethereum to scale beyond simple finance, enabling the creation of applications ranging from decentralized exchanges to NFTs and identity systems. The EVM’s universality also became a standard that inspired entire ecosystems of smart contract development.

But there was still a big issue: Ethereum allows anyone to execute code on its clients, and that introduces malicious actors. Someone could simply write a smart contract like this:

```solidity
while (true) {
    // keep computing forever
}
```

This code is a simple infinite loop that runs forever and takes unlimited CPU and resources.

To solve this problem, Ethereum introduced gas, which puts a limit on computation. A transaction gets a finite gas allowance, so an infinite loop can't run forever. It also makes resource usage costly by making different operations consume different amounts of gas. For example, simple arithmetic is cheap, but reading and writing storage are expensive.

This discourages people from filling Ethereum with unnecessarily expensive computation and uses some of that gas to reward the validators who execute the code for the resources involved. Some of that gas is also burned, permanently removing it from circulation.

This burning mechanism was also introduced to prevent malicious validators from creating artificial transactions that increase fees, and it has now been adopted by most modern blockchains that support smart contracts. Burning the fees also makes ETH supply responsive to its usage: the more the network is used, the more ETH is burned, and it may even result in more ETH being burned than issued, which can make it scarcer and more valuable.

Essentially, the gas system incentivizes efficient computation and prevents abuse, ensuring that the network is not overwhelmed by infinite loops or excessively complex calculations.

These innovative approaches from Ethereum were very inspiring to other blockchains, and they led other blockchains to look into even better alternatives to the EVM. Non-EVM chains such as Solana, with its parallelized Sealevel runtime; Cardano, with its formally verified KEVM framework; and NEAR Protocol, with a WASM-based VM, were designed to address limitations in speed, efficiency, or developer accessibility. These chains offered higher throughput or language flexibility but often lacked Ethereum’s depth of composable contracts and developer ecosystem, highlighting a trade-off between performance and network effects.

I am not going to explain all of these novel non-EVM approaches because that would be out of the scope of this book. But I encourage you to take your time and read about them. They are truly innovative and amazing mechanisms that make a fully scalable decentralized financial system something feasible.

Alongside these new approaches, Ethereum itself has evolved technically as well. At first, it relied on proof-of-work (PoW), similar to Bitcoin, to secure the network. While PoW provided security, it was energy-intensive, slow, and limited scalability. To address these issues, Ethereum transitioned to proof-of-stake (PoS) with the Merge.

PoS heavily reduced energy consumption and allowed validators to secure the network by staking ETH rather than expending computational work. This shift also opened the door for improved scalability, paving the way for layer-2 solutions and future sharding implementations, without compromising decentralization.

And other than that, Ethereum is constantly evolving with new upgrades that improve efficiency, security, and scalability.

Ethereum was designed to be more than a currency. And it became just that.

It became an infrastructure: a programmable, decentralized platform that enables finance, governance, identity, and complex applications. And because it was the first one to successfully do this, I thought it was almost necessary to understand its mechanism that allows all that to happen.

## Smart Contracts and Composability

In the previous section, I briefly mentioned composability in smart contracts and how they allow complex systems to form. Here, I want to go a little deeper into this concept because it is such an important part of decentralized applications and systems.

Composability is the ability of one contract to interact seamlessly with others, which enables modular, complex systems. For example, in DeFi, a lending protocol can use an automated market maker to determine collateral values, or a yield aggregator can pull liquidity from multiple protocols to maximize returns for users. This stacking of protocols on top of each other creates a network effect: each new contract can benefit from existing protocols, accelerating innovation exponentially.

This was huge because it allowed rapid experimentation and iteration. Since developers didn’t need to reinvent the wheel, they could simply build on top of existing protocols, improving them or combining them in new and innovative ways. Entire ecosystems of applications could grow in a relatively short time, leading to complex financial primitives like flash loans, synthetic assets, and so on. The modularity also meant users could mix and match protocols to create personalized financial strategies, something that was previously impossible in traditional finance.

It all sounds great on paper, but this is also far from a perfect system. Complex networks of interacting contracts can create cascading failures, like dominoes, if one contract fails or if a vulnerability is exploited in one protocol that others rely on. Events like the 2020 bZx exploit or the repeated failures of poorly audited lending protocols show how the interconnectedness of these systems can become a source of systemic risk.

Another issue is that composability, along with privacy, is extremely challenging. Most composable contracts rely on public state to function, which means privacy-preserving mechanisms are very difficult to implement without breaking interoperability. Only a handful of projects have managed to combine composability with privacy in a meaningful way, often using advanced cryptography or layer-2 solutions, but these usually remain experimental.

I used to work at a company that did just that, but unfortunately, it never took off. The way it worked was to keep the user's sensitive state private while letting the actual target application continue operating on the normal public Ethereum state. And it required a lot of complex and cryptographically heavy mechanisms to achieve that.

Still, despite its risks, composability is one of Ethereum’s most defining features. It’s what allows the blockchain to scale beyond single-purpose financial applications into entire ecosystems of interoperable services.

Without composability, DeFi would be siloed, innovation would move slower, and the idea of a programmable, modular financial system wouldn’t even exist.

## DeFi: What It Is and How It Differs from Decentralized Currency

I have mentioned multiple times in this book that finance is something much broader than currency, and Decentralized Finance, commonly known as DeFi, is what allows us to have that broader finance in a trustless and decentralized environment.

To understand DeFi, we first need to differentiate Finance from money.

Money is simply a medium of exchange, a store of value, and a unit of account. Physical cash, bank deposits, and digital currencies like Bitcoin all serve this purpose. Bitcoin, in particular, is a decentralized, digital form of money: it allows peer-to-peer transfers without intermediaries, with transparency and limited supply. But Bitcoin alone does not provide tools for lending, trading, or complex financial management. It is primarily a tool for value transfer and wealth storage.

Finance, on the other hand, is much broader. It is the management, creation, and study of money, investments, banking, credit, assets, and liabilities. Finance includes personal, corporate, and public domains which range from savings and loans to trading in stocks, bonds, derivatives, and insurance. It includes complex mechanisms and systems that allow wealth to be leveraged, allocated, and managed efficiently. Essentially, finance is the infrastructure that makes money productive, rather than just something that changes hands.

DeFi, or Decentralized Finance, is finance but rebuilt on blockchain. It replicates the functions of traditional financial systems like lending, borrowing, trading, investing, and insurance but without relying on banks or centralized intermediaries and in a trustless manner.

For example, Bitcoin primarily moves and stores value. On the other hand, DeFi enables the creation, allocation, and management of value in sophisticated ways.

And what makes DeFi possible are smart contracts. They are the backbone of DeFi: self-executing programs on blockchains that enforce rules and handle assets autonomously. These smart contracts automate all of the financial operations, such as automatically liquidating poorly backed loans or executing trades based on predefined conditions.

And these DeFi protocols are borderless too, similar to how decentralized currencies are. Anyone with an internet connection can interact with DeFi protocols, bypassing traditional geographic and regulatory barriers.

DeFi protocols can integrate with one another because of the composable nature of smart contracts, allowing complex financial products to be built on top of existing ones. For example, a user can deposit collateral in one protocol, borrow assets from another, and then supply liquidity to a third, all without intermediaries.

Examples of successful DeFi protocols that solve financial problems in the decentralized world are endless, but these are some well-known examples:

- Platforms like Aave and Compound allow users to lend assets to earn interest or borrow against their holdings.
- Uniswap, Sushiswap, and others enable peer-to-peer trading without a centralized order book.
- Decentralized alternatives to fiat, pegged to value-stable assets.

Although DeFi opens unique opportunities, it also comes with unique risks: smart contract vulnerabilities, cascading liquidations, impermanent loss in liquidity pools, and governance risks are a few that I can recall off the top of my head. And here, unlike banks, there is no safety net; users have to bear the full consequences of protocol failures or exploits.

DeFi is essentially the full stack of finance but rebuilt in a decentralized, permissionless, and programmable form. It is the next step beyond Bitcoin, making it not just digital money, but digital financial infrastructure that anyone can access, build on, and innovate with.

## Decentralized Infrastructure

I said before that Ethereum is not just a currency, but a decentralized infrastructure, and here is what I mean by that.

Ethereum and other programmable blockchains are designed to distribute responsibilities across multiple actors (nodes that run blockchain clients as validators) while minimizing reliance on centralized intermediaries.

Ethereum and many other programmable blockchains exist as part of a layered, decentralized infrastructure.

Understanding these layers helps us understand how decentralized applications operate and why infrastructure matters for the security, efficiency, and scalability of the network. Here are the layers that allow Ethereum to function as infrastructure:

**Network Layer:** This is the foundational layer. Nodes communicate, propagate transactions, validate blocks, and maintain consensus across the network. Each full node keeps a copy of the blockchain, ensuring redundancy and resilience. The decentralized nature of this layer prevents any single actor from controlling transaction history or censoring activity, but it also introduces latency and computational overhead compared to centralized systems.

**Protocol Layer:** On top of the network layer sits the protocol layer, the ruleset governing state changes. Smart contracts execute here, and the blockchain enforces deterministic outcomes. The protocol layer ensures consistency across nodes: every transaction, contract execution, or state update follows the same rules.

**Application Layer:** This is where users interact with the blockchain. Decentralized applications (dApps), wallets, marketplaces, and other tools. While the underlying network and protocol are decentralized, the application layer determines usability, accessibility, and how effectively users can use the underlying infrastructure.

Different blockchains might have different layers based on how they operate, but here I just focus on Ethereum to prevent any potential confusion.

Beyond Ethereum itself, decentralized infrastructure extends to supporting technologies that enhance storage, computation, and data reliability:

**IPFS (InterPlanetary File System) and Filecoin:** These protocols provide decentralized storage, removing dependence on centralized cloud providers and ensuring files remain accessible even if individual nodes go offline.

**Decentralized Oracles:** Services like Chainlink feed real-world data into smart contracts, enabling them to act on external events without relying on a single source.

**Layer-2 Solutions:** Optimistic rollups, zk-rollups, and sidechains help scale Ethereum by processing transactions off-chain while still relying on the main chain for security. These solutions reduce congestion, lower fees, and improve throughput without compromising decentralization.

These decentralized infrastEDITED: ructures were built to minimize single points of failure, increase trustlessness, and distribute power among participants.

However, there are always trade-offs. The more we decentralize, the more throughput often decreases and latency increases. Layer-2 solutions and alternative protocols can improve scalability, but sometimes at the cost of composability or security. Balancing these factors (decentralization, scalability, and security) is a constant challenge for any blockchain system.

Decentralized infrastructure is about creating systems resilient to censorship, single points of failure, and centralized control, while enabling a flexible foundation for applications, finance, and digital governance.

## Single-Chain to Multi-Chain Infrastructure

Ethereum started as a single, dominant chain, serving as the primary platform for smart contracts, decentralized applications, and DeFi. In its early years, most of the blockchain ecosystem was concentrated on Ethereum, benefiting from network effects, developer attention, and liquidity. However, as adoption grew, so did the limitations of a single-chain model.

But very soon, congestion, high gas fees, and scalability issues showed the practical limits of relying on one chain for a growing movement.

This led to the rise of multi-chain infrastructure, where different blockchains coexist and interact to serve specialized purposes:

Not all chains are built the same. Some prioritize high throughput and low latency for trading applications (like Solana), others focus on minimal fees and efficient computation for small-scale dApps (like Polygon), while privacy-focused chains (like Secret Network or Oasis) enable confidential smart contracts. This specialization allows developers to choose the platform that best fits the requirements of their application, rather than being limited by a one-size-fits-all environment.

But this makes it harder for the end user, since they would now have to use multiple chains with different fees, mechanisms, speeds, and wallets simultaneously. And one solution would be to have a multi-chain ecosystem.

Multi-chain ecosystems require communication across chains. Bridges, wrapped tokens, and cross-chain protocols enable assets, data, and smart contract interactions to flow between chains. For example, a token minted on Ethereum can be used in a DeFi protocol on Avalanche or Solana through a bridge. Interoperability opens the door for larger, integrated ecosystems, where composability and liquidity can extend beyond the boundaries of a single chain.

But multi-chain systems are not without risks. Liquidity can become heavily fragmented and complex, making it harder to move large amounts of capital efficiently. Security is more complex: bridges and cross-chain mechanisms are frequent targets for hacks as they spread the attack surface area, as seen in several high-profile exploits. Governance also becomes more complicated. Protocol upgrades and consensus decisions must consider interactions across chains, and coordination between different communities is often difficult.

Despite all risks, interconnected blockchains promise greater scalability, specialization, and resilience, but they also require more sophisticated tools and methods for interoperability, risk management, and governance coordination.

## NFTs, Soulbound Tokens, and Decentralized IDs

Non-Fungible Tokens (NFTs), Soulbound Tokens (SBTs), and Decentralized IDs (DIDs) represent some of the most significant innovations in bridging the decentralized blockchain world with real-life identity, ownership, and personal reputation.

They move beyond money and finance, extending blockchains into social, cultural, and personal worlds.

### Digital Ownership

NEW: one hard to solve problem of the internet has been proving your ownership of something digital, like a digital photo. And NFTs solve that problem. 

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

Zero-knowledge proofs (zk-proofs) provide a solution. Using zk-proofs, it is possible to prove ownership of an NFT, a credential, or an identity without revealing the underlying data. For instance, a user could prove they hold a specific SBT representing a professional certification without revealing their name or the issuing institution. Technical details of zk-proofs will be explained in later chapters.

NFTs, Soulbound Tokens, and Decentralized IDs expand blockchain’s  potential far beyond money. They allow digital assets to mirror real-life ownership, reputation, and identity, creating a more integrated, programmable world.

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

And a lot of these centralized influences are inevitable, at least right now. And this is why it's important to see decentralization as a spectrum, not a binary. Understanding and acknowledging these centralization problems is necessary to build better systems in the future that have fewer of these problems.

Every blockchain faces trade-offs between security, efficiency, and the ideal of distributed control. What matters is moving toward a fairer decentralization and constantly reducing the reliance on centralized systems.

## Roles in Autonomy

Autonomy in decentralized systems is not absolute either. It is distributed across various actors who collectively maintain, govern, and use the network. Each role comes with distinct responsibilities and influence:

Users drive adoption and liquidity. They interact with protocols, supply assets, vote in governance mechanisms, and provide feedback. In many DeFi applications, users’ decisions directly affect protocol behavior, such as lending pool utilization or liquidity incentives.

Validators and miners maintain consensus, validate transactions, and secure the network. Their autonomy is constrained by protocol rules, but they influence which transactions are included in blocks and help enforce network integrity.

Developers, core teams, independent contributors, and community developers create, maintain, and upgrade protocols. While decentralized contributions are possible, early design choices and governance frameworks often give significant influence to developers or foundations.

Token holders or DAO participants vote on protocol upgrades, parameter changes, or fund allocations. This collective decision-making provides distributed control but is often weighted by stake, creating the potential for imbalance between large holders and smaller participants.

Autonomy in blockchain systems exists on a spectrum as well. Full decentralization is idealized, but practical systems must balance control, efficiency, and security to be usable.

Understanding how power and responsibility are distributed helps us see why decentralization is not just a technical problem to solve; rather, it is social, economic, and political.

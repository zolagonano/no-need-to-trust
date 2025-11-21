# Chapter 3

Strong and secure cryptography before the 1960s was inseparable from state authority. It was almost considered a weapon. Governments treated secure cryptographic tools as instruments of war, and access to them was heavily controlled. They could be exported only with permission, circulated only within approved circles, and developed primarily inside intelligence agencies.

Citizens, companies, scientists, and researchers had no practical way to protect their communications at a level that challenged government capabilities.

This began to change in the 1970s when Diffie and Hellman introduced the concept of public key exchange, and RSA soon provided a concrete method for asymmetric encryption. These were breakthroughs that did more than solve technical problems. They shattered the belief that only governments could produce cryptographic systems strong enough to stay secure.

Then in the 1990s, Phil Zimmermann released an easy-to-use tool named PGP that offered strong encryption to anyone with a computer. This really challenged the export controls because it showed that governments could not stop an algorithm that could be printed in a book, posted online, or simply reimplemented elsewhere. As soon as PGP gained global attention, the mental barriers that assumed cryptography was not for everyone vanished. PGP spread way faster than any regime or authority could stop it or adapt to it.

The larger consequence was a shift in the cost structure of surveillance. When only authorities possessed strong cryptography, targeted monitoring was straightforward. Once individuals gained access to the same level of protection, the economics changed. Intercepting communications required new methods that were more expensive, more intrusive, or more fragile. In other words, it became functionally impossible. Governments could still try to exploit implementation vulnerabilities, but these strategies did not scale the way passive interception had before.

This event was a redistribution of power in a measurable way. It gave ordinary individuals a form of protection that was previously reserved for states, and it still continues to define the politics of digital security. This is what this chapter is going to cover.

## Online Privacy as a Human Right

We have all heard, and most of us believe, that privacy is a human right and it is non-negotiable. In the online world or in real life, it does not matter.

Without private space for decision-making, people cannot form intentions that are truly their own. They act under the shadow of observation, adjusting behavior to the expectations of whoever is watching. In that setting, even apparent agreement is shaped by pressure, not choice. A society that normalizes constant monitoring violates the very idea of voluntary action.

Surveillance also creates a built-in power gap. The watcher collects information the watched cannot see, challenge, or limit. That information can be stored and used in ways that strengthen the watcher’s position. Any institution that can observe others without being observed gains the ability to predict behavior, make decisions, and enforce rules. Individuals have no similar tools, so the balance of power inevitably leans toward control.

This is not only a government problem. Major tech companies and data brokers run systems that track people at large scale. They study patterns, build profiles, and influence choices through automated tools that function like private governance. Collecting personal data for profit weakens autonomy just as much as political surveillance. The commercial framing does not erase the power imbalance.

Ensuring privacy on the internet is different. Its foundation is cryptography. We can say there will be no privacy online without cryptography. This becomes extremely challenging in decentralized systems.

Decentralization should shift trust from humans to math and code. The main way to do this is through transparency. Decentralized systems must be inspectable, predictable, and resistant to manipulation. But transparency and privacy pull in opposite directions. One demands that everything be visible so no one can cheat. The other demands that some things stay hidden so no one can control you.

Balancing these two forces is one of the core challenges of building decentralized technologies. If everything is transparent, users lose privacy and fall back into the same power dynamics that decentralization was meant to avoid. If everything is private, participants cannot verify the system and it becomes vulnerable to fraud and abuse.

The goal is to design mechanisms that let people prove what needs proving without revealing everything about themselves. Techniques like zero-knowledge proofs, multiparty computation, ring signatures, and private key cryptography exist because this balance is essential.

Privacy is not an obstacle to decentralization; it is one of the things that makes decentralization worth pursuing. A decentralized network that exposes all user activity is decentralization in name only. It removes central control while leaving surveillance intact, simply shifting it to whoever has the resources to analyze the data. Real decentralization must protect individuals not just from a central authority, but from any actor seeking to accumulate an unequal amount of information.

Cryptography is the only way to do this at scale. It lets individuals participate without being mapped. It ensures that power does not quietly return to whoever can observe the most. Without cryptography, decentralization cannot guarantee privacy. Without privacy, decentralization cannot lead to autonomy.

In the coming chapters, I will expand in more detail about the techniques we have, like zkProofs, how they work, and why they are so important for the future of decentralization.

## Code Replaces Law

Cypherpunks argue that the most effective way to defend freedom in a digital world is not by asking for better laws, but by building systems that make certain abuses impossible.

> Cypherpunks write code. We know that someone has to write software to defend privacy, and since we cannot get privacy unless we all do, we are going to write it. We publish our code so that our fellow cypherpunks may practice and play with it. Our code is free for all to use, worldwide. We do not much care if you do not approve of the software we write. We know that software cannot be destroyed and that a widely dispersed system cannot be shut down.
> 
> - A Cypherpunk's Manifesto
>     

A cryptographic protocol does not require belief in the good intentions of a government or a regulator. It requires only that the underlying assumptions hold and that the code is open for anyone to examine. When the system is transparent and the constraints are built into the protocol, the result is predictability that law never provides. Misconduct becomes technically impossible rather than illegal.

Examples of this approach are everywhere in modern privacy and security tools.

Tor routes traffic through many nodes so no one can trace who is speaking to whom.

PGP lets individuals encrypt messages without relying on a central authority.

Zcash and Monero provide financial privacy through cryptography.

Signal uses forward secrecy to make intercepted messages useless.

Bitcoin created a monetary system where the consensus rules govern the ledger, not a bank.

These tools succeed because they do not rely on promises. They rely on math and code, and math is sound and code is law.

Tor does not ask operators to behave. PGP does not require trust in anything. It gives each person their own keys. Privacy coins do not depend on regulations. They use proofs that reveal only what is necessary. Bitcoin does not rely on law to enforce its policy. The protocol enforces it block by block using math and cryptography.

In each case, the protocol replaces the legal guarantee and the system guarantees the outcome. The individual does not need to request rights from anyone. They use tools that make those rights real.

This was the cypherpunk vision: freedom that does not rely on permission, backed by math, not men.

## Parallel Systems Outside Authority's Control

The core idea of crypto-anarchism was to build systems that operate independently of governments, corporations, or centralized authorities. Cryptography is the essential tool that makes these systems possible. By removing the need for trust in intermediaries, encryption allows individuals to participate in networks that are voluntary, borderless, and resistant to censorship.

In finance, encryption provided parallel monetary systems. Bitcoin and other cryptocurrencies create digital money that functions without central banks.

Stablecoins peg value to real-world assets while remaining outside traditional banking rails.

Privacy coins like Monero or Zcash protect transactional anonymity, allowing participants to move value without exposing sensitive information.

These systems show that money, once entirely under state control, can now exist in autonomous, encrypted forms. This is why Bitcoin is historically important, because it showed what can be achieved through cryptography and decentralized systems. It broke a mental barrier that expanded our imagination far beyond money and finance.

Communication networks have been similarly transformed. End-to-end encrypted messaging apps such as Matrix, Jami, and Tox allow private conversation without relying on centralized servers that can be monitored by authorities.

Identity is another domain reshaped by cryptography. Pseudonyms, zero-knowledge identity proofs (zk-ID), and decentralized identifiers (DIDs) enable participants to interact and verify credentials without exposing unnecessary personal data. These systems allow people to assert authority over their own identities, walking away from the control imposed by governments or centralized platforms.

Cryptography also enables parallel economies. Decentralized exchanges (DEXs), peer-to-peer trade platforms, and other systems allow the exchange of goods and services.

All these show that encryption can make corruption and central control technically difficult, if not impossible.

## Crypto Wars

Cryptography has never been a neutral matter. Its ability to shift power from governments to individuals has made it a political issue. The history of government attempts to limit encryption is often called the Crypto Wars, and it stretches from the 1990s to today.

Phil Zimmermann’s PGP made strong encryption widely available, immediately triggering alarm at the U.S. government. The Clipper Chip, a government-backed encryption device, proposed mandatory key escrow, allowing authorities to decrypt communications at will. These conflicts made clear that encryption was not just a technical tool; it was a challenge to government power.

This battle continues today. Governments and regulators push companies to weaken or bypass end-to-end encryption, claiming they need access to private communications to fight crime or terrorism. Efforts to regulate stablecoins, ban transaction mixers, and delist privacy coins from exchanges are all attempts to bring decentralized finance under legal control.

Every attempted ban, backdoor, or restriction shows the stakes of these technologies.

The Crypto Wars are evidence that strong encryption enables autonomy in ways that authorities cannot easily tolerate.

## The Engine of Autonomy

Without cryptography, decentralization is impossible.

Blockchains, decentralized networks, and peer-to-peer systems can promise autonomy on paper, but they rely entirely on the underlying mathematics to enforce their rules.

Without encryption, everything is exposed. Every participant is exposed. Every message readable. Every transaction observable. Decentralization without cryptography is simply an illusion that will never happen.

Trustless systems exist because they replace trust in governments or institutions with mathematical guarantees. In centralized systems, people rely on intermediaries like banks, governments, or corporations to enforce rules and protect rights. Cryptography allows the same guarantees to exist independently. Protocols, algorithms, and proofs ensure integrity, authenticity, and privacy without requiring faith in any central authority.

Encryption gives individuals the power to communicate privately, transact securely, and assert control over their own identity.

This proves that cryptography is the engine of decentralization. Blockchains, tokens, and networks are tools built on top of it, but they are strong only because encryption enforces rules without relying on permission.

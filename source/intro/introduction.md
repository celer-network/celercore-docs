# Layer-2 Blockchain Scaling

Blockchain technologies offer a foundation to dramatically expand the scope and freedom of global information sharing and value transfer. We envision a future with blockchain-powered decentralized ecosystems where people, computers, mobile and IoT devices can perform secure, private, and trust-free interactions at a massive scale. However, just like how the 56Kbps dialup Internet in the 90s cannot possibly support 4K video streaming, the insufficient scalability of layer-1 blockchains is the key factor limiting its use cases.

Layer-1 blockchains such as Bitcoin and Ethereum are slow because each operation needs to be processed by most of the nodes to reach on-chain consensus, which is exactly "how to build a super slow distributed system" every CS student learned from their Computer Systems 101. On-chain consensus also has severe implications on privacy, because all transactions are permanently public. New on-chain consensus improvements such as sharding and various Proof-of-X mechanisms are continually getting proposed and developed. They make the layer-1 blockchains relatively faster with different tradeoffs but cannot change the fundamental limitations of on-chain consensus.

To enable Internet-scale blockchain systems with better privacy and no compromise on trust or decentralization, we have to look beyond on-chain consensus improvements. The core principle of designing a scalable distributed system is to make operations on different nodes mostly independent. This simple insight indicates that the only way to fully scale out decentralized applications is to bring most of the transactions off-chain, avoid on-chain consensus as much as possible and use it only as a last resort. Related solutions are often referred to as layer-2 scaling technologies, which include state channel, sidechain, rollup, etc.

## State Channel

A state channel allows mutually distrustful parties to execute a smart contract off-chain and quickly settle on the latest agreed states, with their security and finality guaranteed by on-chain bond contracts. Parties involved in the off-chain transactions cooperatively maintain a multi-signature fraud-proof replicated state machine, and only resort to on-chain consensus when absolutely necessary (e.g., when channel peers disagree on a state).

State channel was initially introduced by the [Lightning Network](https://lightning.network) to support high-throughput off-chain Bitcoin micropayments. Then the technology was extended on Ethereum (by [Celer](https://www.celer.network), [L4](https://l4.ventures/), [Magmo](https://magmo.com), [FunFair](https://funfair.io), etc.) to support arbitrary off-chain smart contract state transitions such as generic conditional payment, multi-party game move, second-price auction bid, high-frequency atomic token exchange, etc.

Previous works on state channel networks have been facing a few significant challenges in terms of performance, robustness, scalability, flexibility, and cost-efficiency. This site provides an in-depth description of how Celer Network meets these challenges and builds the first large scale state channel network in production.

## Sidechain

Another important off-chain scaling technique is the sidechain. The core idea is to run another more efficient decentralized system (with its own validators and operators) that can bridge assets to and from the mainchain. A sidechain can be either custodial (with its own decentralized trust) or non-custodial (such as [Plasma](https://www.learnplasma.org/en/)). The main benefits of sidechain over state channel include that it is more friendly to interactions among many participants, and it does not require significant liquidity lockup or high user availability for the security guarantee. The major downside of sidechain over state channel is longer latency and higher cost for off-chain transactions.

Sidechain and state channel are complementary to each other. This site will also describe how Celer Network uses sidechain technology to build highly reliable and decentralized services that eliminate the state channel security risks and usability hassles caused by the state channel off-chain user availability challenge.

## Rollup

Rollup is an emerging layer-2 scaling technology. In a rollup system, contract state hashes are stored on-chain, along with the transaction calls and arguments logged as calldata. The actual transaction computation happens off-chain. Rollup performance is gained by batching many off-chain transactions into a single on-chain state transition. Rollup security is guaranteed by the on-chain contract's ability to verify the correctness of state transitions. Two major rollup approaches are Optimistic Rollup and ZK-Rollup. 

In Optimistic Rollup, aggregators submit rollup blocks that summarize the off-chain transactions; anyone can check the validity of the rollup blocks and issue a dispute to let the on-chain contract execute the calldata to verify the rollup blocks. Optimistic Rollup can provide higher throughput, lower costs, mainchain-level security, and mainchain-like (e.g., “EVM-compatible”) execution environment, at the expense of higher transaction latency due to the nature of batching. Celer layer-2 system adopts the Optimistic Rollup approach and develops a hybrid Rollup sidechain with tunable options on different trust-level, feature, and performance tradeoffs. We will add more details on the Celer hybrid rollup sidechain in this site later.

ZK-Rollup is similar to Optimistic Rollup but relies on ZK-SNARKs for block verification instead of on-chain disputes. Creating the ZK proofs is extremely expensive, which makes ZK-Rollup not workable anytime soon for generalized applications. We keep a keen eye on the evolution of ZK-Rollup but do not include it in the Celer layer-2 scope for now.

# What is Celer?

Celer Network is an Internet-scale, trust-free, and privacy-preserving platform where everyone can quickly build, operate, and use highly scalable decentralized applications. It consists of a group of layer-2 scaling mechanisms running on top of existing and future blockchains. Celer provides unprecedented performance and flexibility through innovation in off-chain scaling techniques and incentive-aligned cryptoeconomics.

Celer Network embraces a coherent and loosely coupled architecture with clean abstractions that enable rapid evolution of each individual component, including a generalized state channel and sidechain suite that supports fast and generic off-chain state transitions; a highly efficient state channel payment routing protocol that achieves an order of magnitude higher throughput compared to state-of-the-art solutions; a hybrid rollup sidechain that offers user-tunable tradeoffs on trust, performance, and features; a powerful development framework and runtime for off-chain applications; and new cryptoeconomic models that provide strong security, high availability, stable liquidity, and network effect for the off-chain ecosystem.

This site currently covers the core architecture of Celer [state channel network](../channel/overview.md), [state guardian network](../sgn/architecture.md), and [liquidity backing](../liquidity/backing.md). It will be extended to also include Celer hybrid rollup sidechain later.

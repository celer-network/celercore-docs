# Off-Chain Availability Problem
Everything comes at a price. While state channel improves scalability, it imposes an impractical "always online" responsibility on the users, as the off-chain states need to be available against malicious on-chain disputes. Additionally, state channel also introduces various usability hassles because the channel off-chain states can only make progress when all participants are available online to sign new states. These security and usability issues can be categorized as the off-chain availability problem, which is the major challenge of state channel applications.

---
## Security Risks

#### What if I lost my off-chain state?

Unlike the blockchain where every node stores all the data, a state channel requires the users to be responsible for keeping their own off-chain state proof safe and available. This means if a client did not backup its off-chain state elsewhere and lost its local storage, then its fund security is at the channel peer's mercy.

#### What if my peer maliciously disputes while I am offline?

If one party tries to settle the payment channel on a state that is old but more favorable for itself, the counterparty must be able to respond by submitting the latest state within the pre-agreed *dispute time window* in order to guarantee its fund safety. A longer dispute window may mitigate the problem by allowing a user to stay offline safely for a longer period of time, but cannot eliminate this fundamental and unacceptable burden for ordinary (mobile) users.

---
## Usability Hassles

#### How do I send payments to someone who is offline?

Sending a payment through the blockchain is easy, which is just sending a request to alter the blockchain state. However, completing a payment through a state channel network has a much higher requirement: the receiver must be available online to sign the off-chain state. This is a huge usability burden for people who have used to how traditional mobile payments work nowadays.

#### How can I get rid of the need for on-chain game moves?

Playing an interactive state channel chess game is fast and fun until someone becomes unresponsive and the counterparty has to bring the game to the  blockchain, after which players have to make the moves on-chain, which is often unbearably slow and expensive for most players. On-chain play has to be supported because the state channel protocols cannot tell who is really the "bad guy" responsible for the dispute.

---
## Decentralized Solution

A straightforward solution to solve all the problems above is to have the users connected to services that are always online to continuously
- Backup users latest off-chain states.
- Watch on-chain dispute events and respond on behalf of offline users.
- Receive payments on behalf of offline users.
- Monitor and provide authentic proofs on app user off-chain actions.

These functionalities are not that complicated to be implemented as parts of a centralized service. However, this will break the promise of blockchain applications, since it implies a single point of trust or failure. Celer's approach is to develop and promote a highly scalable, available, and secure decentralized platform to provide these services. Our solution is an efficient *specialized sidechain* called **State Guardian Network** (SGN), which we detail in the following sections.

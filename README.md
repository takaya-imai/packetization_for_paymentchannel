# packetization_for_paymentchannel

```
Layer: Layer 2 ideas
Title: Multi-hop payment packetization on Lightning Network channel
Author: Takaya Imai <takaya.imai@unitedbitcoiners.com, takaya.imai@frontier-ptnrs.com>




[Abstract]

Lighting Network(LN) was invented by Joseph Poon and Thaddeus Dryja in 2015 \cite{ln}.
LN makes Bitcoin very scalable by lower transaction fee and rapid bitcoin transfer.
There are four major LN products \cite{products}, lit, lnd, c-lightning and eclair, and RFC \cite{bolt}. These has been developped steadily and LN can be extended and connected (atomic swap) to other blockchains simply.

LN Routing algorisms like flare \cite{flare} and gossip is proposed and developed but LN has two problems.
One is that it is easy to be centralized. Some whose channel has large money as a deposit can dominate a whole LN. This depends on routing algorism though.
Flare is one of proposals for a routing algorism but nothing about the centralization.
The other is that nodes in the middle have a possibility to take a long time to get money if a preimage does not propagate successfully.

I propose one solution. That is a packet-like payment.




[Anti-centralization]

This is a way to reduce centralization of LN and provide higher processing ability of payment by distributed nodes on whole LN.
Consider to send 10,000 satoshis from Alice to Bob on the following channel network.

Alice - Coulomb - Bob
      \         /
        Dirac
      \         /
        Einstein-
      \         /
        Faraday

Alice can send at once through Coulomb but this case promote a centralization because only nodes which have enough deposit on a channel can become one of nodes on a route.
So Alice divides a big payment into small payments such as 10,000 satoshis into 2,500 satoshis * 4 etc.

Even if a channel between Dirac and Bob has 4,000 satoshis as a direction of Dirac to Bob, this channel can join this payment.
I think smaller amount is better but it might need excess payments so it is important to keep a balance between process overhead loss and decentralization.




[Payment damage reduction]

This is a way to reduce damage in case that a preimage propagation problem occurs.
Consider to send 10,000 satoshis from Alice to Bob on the following channel network.

Alice - Coulomb - Dirac - Bob
                \       /
                  Einstein

One route is selected and Alice sends 10,000 satoshis through Dirac.
If Dirac does not return a preimage to Coulomb, Coulomb have to do one of the following ways.

1, wait that Dirac do unilateral close of a channel between Coulomb and Dirac and get the preimage from public Bitcoin blockchain
2, do unilateral close of a channel between Coulomb and Dirac to revoke a transaction to send 10,000 satoshis to Dirac.

It is possible to send 10,000 satoshis at once through Dirac but this case takes a long time for the payment for all amounts.
So Alice should divide a big payment into small payments such as 10,000 satoshis into 100 satoshis * 100 etc and then Bob can get parts of payment earlier.
Amount is smaller, damage is smaller even if problem occurs, for example, Bob can get 9,990 satoshis soon and just 10 satoshi is delayed.

And once a problem occurs, Alice changes the first route from "through Dirac" to "through Einstein".
Of course, Coulomb has to wait a preimage a bit before changing the first route because Dirac is honest and his node is down temporarily.




[pros and cons]

The following are pros and cons for my proposal.

* Pros
** to reduce damage in case of bad preimage propagation
** to promote to use many kinds of routes and decentralize
** to distribute points of failure and do payment processing in a whole network
** to get earlier to find bad nodes because of many trials for various nodes and routes

* Cons
** network must process many small payments
** to make payment time longer by overhead processes even if the payment has no problem
** to make route search time longer in case of finding multi-routes
** This is not a complete solution, just reducing damage




[References]

1, The Bitcoin Lightning Network: https://lightning.network/lightning-network-paper.pdf \bibitem{ln}
2, Basis of Lightning Technology(BOLT): https://github.com/lightningnetwork/lightning-rfc \bibitem{bolt}
3, Implementations: \bibitem{products}
  lit: https://github.com/mit-dci/lit
  eclair: https://github.com/ACINQ/eclair
  lnd: https://github.com/lightningnetwork/lnd
  c-lightning: https://github.com/ElementsProject/lightning
4, Flare: http://bitfury.com/content/5-white-papers-research/whitepaper_flare_an_approach_to_routing_in_lightning_network_7_7_2016.pdf \bibitem{flare}
```

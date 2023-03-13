# Ethereum Fork History

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span>Most
hard forks are planned as part of an upgrade roadmap and consist of
updates that the community generally agrees to (i.e., there is social
consensus). However, some hard forks lack consensus, which leads to
multiple distinct blockchains. The events that led to the
Ethereum/Ethereum Classic split are one such case, and are discussed in
this appendix.

# Ethereum Classic (ETC)

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span>Ethereum Classic came to be after members
of the Ethereum community implemented a time-sensitive hard fork
(codenamed “DAO”). On July 20, 2016, at a block height of 1.92 million,
Ethereum introduced an irregular state change via a hard fork in an
effort to return approximately 3.6 million ether that had been taken
from a smart contract known as The DAO. Almost everyone agreed that the
ether taken had been stolen and that leaving it all in the hands of the
thief would be of significant detriment to the development of the
Ethereum ecosystem as well as the platform itself.

Returning the ether to its respective owners as though The DAO had never
even existed was technically easy, if rather politically controversial.
A number of people in the ecosystem disagreed with this change,
believing immutability should be a fundamental principle of the Ethereum
blockchain without exception; they elected to continue the original
chain under the moniker of Ethereum Classic. While the split itself was
initially ideological, the two chains have since evolved into separate
entities.

# The Decentralized Autonomous Organization (The DAO)

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span>The <span class="indexterm"></span>DAO
was created by Slock.it, with the aim of providing community-based
funding and governance for projects. The core idea was that proposals
would be submitted, curators would manage proposals, funds would be
raised from investors within the Ethereum community, and, if the
projects proved successful, investors would receive a share of the
profits.

The DAO was also one of the first experiments in an Ethereum token.
Rather than funding projects directly with ether, participants would
trade their ether for DAO tokens, use them to vote on project funding,
and later be able to trade them back for ether.

DAO tokens were available to purchase in a crowdsale that ran from April
5 through April 30, 2016, amassing [nearly 14%](https://econ.st/2qfJO1g)
of the total ether in existence, which was worth ~\$150 million at the
time.

# The Reentrancy Bug

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>On June 9,
2016, developers Peter Vessenes and Chriseth reported that most
Ethereum-based contracts that managed funds were potentially [vulnerable
to an exploit](http://bit.ly/2AAaDmA) that could empty contract funds. A
few days later, on June 12, Stephen Tual (cofounder of Slock.it)
reported that [The DAO’s code was not vulnerable](http://bit.ly/2qmo3g1)
to the bug described by Peter and Chriseth. Worried DAO contributors
breathed a sigh of relief—until five days later, when an unknown
attacker started [draining The DAO](http://bit.ly/2Q7zR1h) using an
exploit similar to the one for which the warning had been issued.
Ultimately, the DAO attacker siphoned ~3.6 million ether out of The DAO.

Simultaneously, an assemblage of volunteers calling themselves the Robin
Hood Group (RHG) started using the same exploit to withdraw the
remaining funds in order to save them from being stolen by the DAO
attacker. On June 21, [the RHG announced](http://bit.ly/2PtX4xl) that
they had secured about 70% of The DAO’s funds (roughly 7.2 million
ether), with plans to return it to the community (which they
successfully did on the ETC network, and didn’t need to do on the
Ethereum network after the fork). Many thanks and commendations were
given to the RHG for their quick thinking and fast actions that helped
secure the bulk of the community’s ether.

## Technical Details

<span class="indexterm"></span> <span class="indexterm"></span>While a
more detailed and thorough explanation of the bug is given by [Phil
Daian](http://bit.ly/2EQaLCI), the short explanation is that a crucial
function in the DAO had two lines of code in the wrong order, meaning
that the attacker could have requests to withdraw ether acted upon
repeatedly, before the check of whether the attacker was entitled to the
withdrawal was completed. This type of vulnerability is described in
[???](#reentrancy_security).

## Attack Flow

<span class="indexterm"></span> <span class="indexterm"></span>Imagine
you had \$100 in your bank account and you could bring your bank teller
any number of withdrawal slips. The teller would give you money for each
slip in order, and only after processing all the slips would they record
your withdrawal. What if you brought them three slips, each requesting
withdraw \$100? What if you brought them three thousand?

The DAO attack worked like this:

1.  The DAO attacker asks the DAO contract to withdraw DAO tokens (DAO).

2.  The attacker asks the contract to withdraw DAO *again*, before the
    contract updates its records to show that DAO was withdrawn.

3.  The attacker repeats step 2 as many times as possible.

4.  The contract finally logs a single DAO withdrawal, losing track of
    the withdrawals that happened in the interim.

# The DAO Hard Fork

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>Fortunately,
there were several safeguards built into The DAO: notably, all
withdrawal requests were subject to a 28-day delay. This gave the
community a little while to discuss what to do about the exploit,
because from roughly June 17–July 20 the DAO attacker would be unable to
convert their DAO tokens into ether.

Several developers focused on finding a viable solution, and multiple
avenues were explored in this short space of time. Among them were a
[*DAO soft fork*](http://bit.ly/2qhruEK), announced on June 24, to delay
DAO withdrawals until consensus was reached, and a [*DAO hard
fork*](http://bit.ly/2AAGjIu), announced on July 15, to reverse the
effects of the DAO attack with an exceptional state change.

On June 28, developers discovered [a DoS exploit in the DAO soft
fork](http://bit.ly/2zgOxUn) and concluded that the DAO hard fork would
be the only viable option to fully resolve the situation. The DAO hard
fork would transfer all ether that had been invested in The DAO into a
new refund smart contract, allowing the original owners of the ether to
claim full refunds. This provided a solution for returning the hacked
funds, but also meant interfering with the balances of specific
addresses on the network, however isolated they were. There would also
be some leftover ether in portions of The DAO known as *childDAOs*. A
group of trustees would manually authorize the leftover ether, worth
[~\$6–7 million](http://bit.ly/2RuUrJh) at the time.

With time running out, multiple Ethereum development teams created
clients that allowed a user to decide whether they wanted to enable this
fork. However, the client creators wanted to decide whether to make this
choice opt-in (don’t fork by default) or opt-out (fork by default). On
July 15, a vote was opened on [*carbonvote.com*](http://bit.ly/2ABkTuV).
The next day, at block height [1,894,000](http://bit.ly/2yHb7Gl), it was
closed. Of the [5.5% of the total ether supply](http://bit.ly/2RuUrJh)
that voted, ~80% of the votes (~4.5% of the total ether supply) voted
for opt-out. One-quarter of the opt-out vote came from a single address.

Ultimately the decision became opt-out, so those who opposed the DAO
hard fork would need to explicitly state their opposition by changing a
configuration option in the software they were running.

On July 20, at block height [1,920,000](http://bit.ly/2zfaIKB), Ethereum
[implemented the DAO hard fork](http://bit.ly/2yJxZ83) and thus two
Ethereum networks were created: one including the state change, and the
other ignoring it.

<span class="indexterm"></span> <span class="indexterm"></span>When the
DAO hard-forked Ethereum (present-day Ethereum) gained a majority of the
mining power, many assumed that consensus was achieved and the minority
chain would fade away, as in previous forks. Despite this, a sizable
portion of the Ethereum community (roughly 10% by value and mining
power) started supporting the non-forked chain, which came to be known
as Ethereum Classic.

Within days of the fork, several exchanges began to list both Ethereum
("ETH") and Ethereum Classic ("ETC"). Due to the nature of hard forks,
all Ethereum users holding ether at the time of the split then held
funds on both of the chains, and a market value for ETC was soon
established with [Poloniex](http://bit.ly/2qhuNvP) listing ETC on July
24.

## Timeline of the DAO Hard Fork

- April 5, 2016: Slock.it [releases a security
  review](http://bit.ly/2Db4boE) of the generic DAO framework smart
  contracts by Deja Vu Security.

- April 30, 2016: The DAO crowdsale [launches](http://bit.ly/2qhwhpI).

- May 27, 2016: The DAO crowdsale ends.

- June 9, 2016: A generic [recursive call bug](http://bit.ly/2AAaDmA) is
  discovered and believed to affect many Solidity contracts that track
  users' balances.

- June 12, 2016: Stephen Tual [declares](http://bit.ly/2qmo3g1) that The
  DAO’s funds are not at risk.

- June 17, 2016: [The DAO is exploited](http://bit.ly/2EQaLCI) and a
  variant of the discovered bug (termed the "reentrancy bug") is used to
  start draining the funds, eventually nabbing ~30% of the ether.

- June 21, 2016: The RHG [announces](http://bit.ly/2zgl3Gk) it has
  secured the other ~70% of the ether stored within The DAO.

- June 24, 2016: A [soft fork vote](http://bit.ly/2qhruEK) is announced
  via opt-in signaling through Geth and Parity clients, designed to
  temporarily withhold funds until the community can better decide what
  to do.

- June 28, 2016: A [vulnerability](http://bit.ly/2zgOxUn) is discovered
  in the soft fork and it’s abandoned.

- June 28, 2016 to July 15: Users debate whether or not to hard fork;
  most of the vocal public debate occurs on the */r/ethereum* subreddit.

- July 15, 2016: The [DAO hard fork](http://bit.ly/2qmo3g1) is proposed,
  to return the funds taken in the DAO attack.

- July 15, 2016: A [vote is held](http://bit.ly/2ABkTuV) on CarbonVote
  to decide if the DAO hard fork will be opt-in (don’t fork by default)
  or opt-out (fork by default).

- July 16, 2016: [5.5% of the total ether supply
  votes](http://bit.ly/2RuUrJh); ~80% of the votes (~4.5% of the total
  supply) are pro the opt-out hard fork, with one-quarter of the
  pro-vote coming from a single address.

- July 20, 2016: The [hard fork](http://bit.ly/2yJxZ83) occurs at block
  1,920,000.

- July 20, 2016: Those against the DAO hard fork continue running the
  old client software; this leads to issues with [transactions being
  replayed on both chains](http://bit.ly/2qjJm27).

- July 24, 2016: [Poloniex lists](http://bit.ly/2qhuNvP) the original
  Ethereum chain under the ticker symbol ETC; it’s the first exchange to
  do so.

- August 10, 2016: The RHG [transfers 2.9](http://bit.ly/2JrLpK2)
  million of the recovered ETC to Poloniex in order to convert it to ETH
  on the advice of Bity SA; 14% of the total RHG holdings are converted
  from ETC to ETH and other cryptocurrencies, and [Poloniex
  freezes](http://bit.ly/2ETDdUc) the other 86% of deposited ETH.

- August 30, 2016: The frozen funds are sent by Poloniex back to the
  RHG, which then sets up a refund contract on the ETC chain.

- December 11, 2016: IOHK’s ETC development team forms, led by Ethereum
  founding member Charles Hoskinson.

- January 13, 2017: The ETC network is updated to resolve transaction
  replay issues; the chains are now functionally separate.

- February 20, 2017: The ETCDEVTeam forms, led by early ETC developer
  Igor Artamonov<span class="indexterm"></span>
  (splix).<span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span>

# Ethereum and Ethereum Classic

<span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span><span class="indexterm"></span>
<span class="indexterm"></span>While the initial split was centered
around The DAO, the two networks, Ethereum and Ethereum Classic, are now
separate projects, although most development is still done by the
Ethereum community and simply ported to Ethereum Classic codebases.
Nevertheless, the full set of differences is constantly evolving and too
extensive to cover in this appendix. However, it is worth noting that
the chains do differ significantly in their core development and
community structure. A few of the technical differences are discussed
next.

## The EVM

<span class="indexterm"></span>For the most part (at the time of
writing), the two networks remain highly compatible: contract code
produced for one chain runs as expected on the other; but there are some
small differences in EVM OPCODES (see EIPs [140](http://bit.ly/2yIajkF),
[145](http://bit.ly/2qhKz9Y), and [214](http://bit.ly/2SxsrFR)).

## Core Network Development

Being open projects, blockchain platforms often have many users and
contributors. However, the core network development (i.e., of the code
that runs the network) is often done by small groups due to the
expertise and knowledge required to develop this type of software. On
Ethereum, this work is done by the Ethereum Foundation and volunteers.
On Ethereum Classic, it’s done by ETCDEV, IOHK, and volunteers.

# Other Notable Ethereum Forks

<span class="indexterm"></span>[Ellaism](https://ellaism.org/about/) is
an Ethereum-based network that intends to use PoW exclusively to secure
the blockchain. It has no pre-mine and no mandatory developer fees, with
all support and development donated freely by the community. Its
developers believe this makes theirs “one of the most honest pure
Ethereum projects,” and one that is “uniquely interesting as a platform
for serious developers, educators, and enthusiasts. Ellaism is a pure
smart contract platform. Its goal is to create a smart contract platform
that is both fair and trustworthy.” The principles of the platform are
as follows:

> - All changes and upgrades to the protocol should strive to maintain
>   and reinforce these Principles of Ellaism.
>
> - Monetary Policy: 280 million coins.
>
> - No Censorship: Nobody should be able to prevent valid txs from being
>   confirmed.
>
> - Open-Source: Ellaism source code should always be open for anyone to
>   read, modify, copy, share.
>
> - Permissionless: No arbitrary gatekeepers should ever prevent anybody
>   from being part of the network (user, node, miner, etc).
>
> - Pseudonymous: No ID should be required to own, use Ellaism.
>
> - Fungible: All coins are equal and should be equally spendable.
>
> - Irreversible Transactions: Confirmed blocks should be set in stone.
>   Blockchain History should be immutable.
>
> - No Contentious Hard Forks: Never hard fork without consensus from
>   the whole community. Only break the existing consensus when
>   necessary.
>
> - Many feature upgrades can be carried out without a hard fork, such
>   as improving the performance of the EVM.

Several other forks have occurred on Ethereum as well. Some of these are
hard forks, in the sense that they split directly off of the preexisting
Ethereum network. Others are software forks: they use Ethereum’s
client/node software but run entirely separate networks without any
history shared with Ethereum. There will likely be more forks over the
life of Ethereum.

There are also several other projects that claim to be Ethereum forks
but are actually based on ERC20 tokens and run on the Ethereum network.
<span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span>Two
examples of these are EtherBTC (ETHB) and Ethereum Modification (EMOD).
These are not forks in the traditional sense, and may sometimes be
called “airdrops.”

Here’s a brief rundown of some of the more notable forks that have
occurred:

- <span class="indexterm"></span>*Expanse* was the first fork of the
  Ethereum blockchain to gain traction. It was announced via the Bitcoin
  Talk forum on September 7, 2015. The actual fork occurred a week later
  on September 14, 2015, at a block height of 800,000. It was originally
  founded by Christopher Franko and James Clayton. Their stated vision
  was to create an advanced chain for: "identity, governance, charity,
  commerce, and equity".

- <span class="indexterm"></span><span class="indexterm"></span>*EthereumFog*
  (ETF) was launched on December 14, 2017, and forked at a block height
  of 4,730,660. The project’s stated aim is to develop "world
  decentralized fog computing" by focusing on fog computing and
  decentralized storage. There is still little information on what this
  will actually entail.

- *EtherZero* (ETZ) <span class="indexterm"></span>was launched on
  January 19, 2018, at a block height of 4,936,270. Its notable
  innovations were the introduction of a masternode architecture and the
  removal of transaction fees for smart contracts to enable a wider
  diversity of DApps. There has been some criticism from some prominent
  members of the Ethereum community, MyEtherWallet, and MetaMask, due to
  the lack of clarity surrounding development and some accusations of
  possible phishing.

- <span class="indexterm"></span><span class="indexterm"></span>*EtherInc*
  (ETI) was launched on February 13, 2018, at a block height of
  5,078,585, with a focus on building decentralized organizations.
  Stated goals include the reduction of block times, increased miner
  rewards, the removal of uncle rewards, and setting a cap on mineable
  coins. EtherInc uses the same private keys as Ethereum and has
  implemented replay protection to protect ether on the original
  non-forked
  chain.<span class="indexterm"></span><span class="indexterm"></span><span class="indexterm"></span>

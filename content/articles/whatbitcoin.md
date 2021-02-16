---
title: "What actually is Bitcoin?"
date: 2021-02-11T10:04:18-08:00
draft: false
featured_image: "images/what_is_bitcoin.jpg"
---

Bitcoin is a peer-to-peer, distributed ledger. It's merely a large record of who has the right to spend what. The beauty lies in the simplicity.
<!--more-->

Bitcoin has three levels of trustlessness.

1. [Distributed information](#distributed-information)
2. [Digital Signatures](#digital-signatures)
3. [Proof of Work](#proof-of-work)



## Distributed information

The first important feature of Bitcoin is that it is distributed. Unlike VISA, PayPal, or even your Chase Checking account, the Bitcoin ledger is distributed around the world to anyone who is interested in running the Bitcoin software.

Running the Bitcoin software is called operating a "Bitcoin node." A Bitcoin node stores the record of every transaction that has ever occurred on the Bitcoin blockchain. There is no cost to do this, apart from a few hundred GB of disk space to store the Blockchain data. If space is limited, you are able to "prune" the history and only keep a copy of the last few weeks of transactions, as well as the list of all currently spendable coins, which is called the UTXO set.

This enables a Bitcoiner to check the balance of their wallets in complete privacy - no need to disclose to a third party what addresses you are looking up.

It also allows a Bitcoiner to validate that transactions are actually occurring on the network, without relying on a trusted third-party to tell them the state of the world.

Do you still reconcile your bank statements? If you are like most of us, you just trust that your bank isn't skimming money off the top and hoping that you don't notice. You are trusting companies which run by sinful corrupt humans to manage your money for you. They hold all the cards, and leave you with nothing more than a pat on the head and a bank statement as a consolation prize.

{{< giphy xUNd9JmsrWkrYnLcU8 >}}

## Digital Signatures

Bitcoin leverages public key cryptography extensively. For the sake of a simple analogy, think of the ubiquitous blue USPS drop boxes.

With the public key, you can drop mail into the box. Give your public key to anyone, and they can drop mail in the box. But only the mailman can open the drop box and take the mail back out (or even see what's in the box, for that matter!) The mailman is using the private key.

{{< figure src="/images/usps_dropbox.jpg" class="w-30 center" >}}

Bitcoin addresses are derived from a public key. When you spend bitcoin, your wallet software will sign the input of the transaction with your private key, proving that you have the authority to spend the bitcoin which was associated with that input.

What this means is that every single transaction on the Bitcoin network is guaranteed to be unforgeable - no person has ever spent any amount of bitcoin that they weren't authorized to spend.

## Proof of Work

In a centralized system, it's easy to determine the state of the world. When VISA says that the transaction has gone through, everyone accepts it as truth.

In a decentralized system, however, it's quite a bit trickier. What is to prevent me from taking some of my bitcoin and sending it to you, while simultaneously creating another transaction that sends the same bitcoin to someone else?

This is called the double-spend problem. It's also referred to as the [Byzantine Generals problem](https://coincentral.com/byzantine-generals-problem/).

In order to resolve this issue, Bitcoin leverages a simple but ingenious solution. Every signed transaction is valid (because of the digital signature), but it's not immediately committed.

### A brief interlude

Before we can explain how transactions are confirmed, we must quickly discuss hashing. Hashing is a process by which some amount of data is run through an algorithm, and out comes a string of characters.

Hashing is unpredictable, in that the output follows no pattern, and is not guessable without running the algorithm yourself.

Hashing is also a one-way function. Once given a hash, there's no way to determine what the original data was that created it. However it is trivial to generate the hash of any given piece of data.

By way of example, the SHA256 hashes of the words 'Bitcoin' (the network protocol) and 'bitcoin' (the monetary unit that is exists in that network) are completely different:

```
$ printf Bitcoin | sha256sum
6b88c087247aa2f07ee1c5956b8e1a9f4c7f892a70e324f1bb3d161e05ca107b  -
$ printf bitcoin | sha256sum
b4056df6691f8dc72e56302ddad345d65fead3ead9299609a826e2344eb63aa4  -
```

### Back to transactions, you blockhead!

Ah yes. Pending transactions on the bitcoin network go into a holding bucket called the mempool. Users who wish to participate in Bitcoin mining then take pending transactions and group them together into a block.

Miners must then take the contents of the entire block, the hash of the previous block, and find a number (called a nonce) which when all hashed together will result in a specified number of leading zeros.

Since there is no better way to find this nonce than blind trial and error, it Bitcoin miners work very hard to find this number.

The number of zeros they are looking for is determined automatically by the Bitcoin protocol, and is self-adjusting such that blocks are "solved" every 10 minutes, on average.

### How does the nonce solve the Byzantine Generals problem?

The Bitcoin protocol specifies that the longest chain of blocks represents the true state of the network.

Because of the tremendous amount of computational power required to solve the solution, it's not possible for someone to alter the state of a transaction once it has a few blocks mined on top of it.

Since every block references the previous block, if you changed any block in the past, it would invalidate the hashes of every subsequent block, and you would have to go back and re-mine them all.

Since the rest of the world will trust that the longest chain is true, you would need to be able to re-mine every subsequent block faster than the rest of the world's miners are producing regular blocks.

### Why would someone do all that work to mine?

It all comes down to money.

> “Show me the incentives and I will show you the outcome.”
>
>\- Charlie Munger

When you submit a transaction to the Bitcoin network, you offer a tip to whichever miner will include your transaction in a block. Space in the blockchain is precious, so there's always competition to get in. Miners will prioritize transactions that tip the best, at the cost of increased expense for the sender.

The other incentive for miners is also the mechanism by which new bitcoin is drip-fed into the system. Whichever miner solves the block is allowed to pay themselves a block reward.

This reward was 50 BTC. It is programmatically cut in half every 4 years (210,000 blocks), and is currently 6.25 BTC.

### Results

The result of this layered approach to security is a system whereby individual participants are empowered to be financially sovereign. They are not required to place any trust in any individual, and need not ask for permission to transfer their own money to anyone, anywhere, at any time.

Miners are compensated on the free market. They are paid for the work they do, and require no permission or consent to mine. Nobody directs them what transactions to include. If a miner doesn't include your transaction, then it creates an opportunity for someone else to earn your transaction fee. Unlike commodity mining in the physical world, all miners globally are in a winner-take-all competition for the same fees and block rewards. They have a tremendous investment in hardware, and thus are incentivized to not misbehave. If all miners colluded together to refuse to mine transactions, they would reduce the desirability of the network, and would thus be biting the hand that feeds them. They are employees of the network, not it's masters.

For a visual explanation of this process, check out this video:
{{< youtube bBC-nXj3Ng4 >}}


{{< tail >}}

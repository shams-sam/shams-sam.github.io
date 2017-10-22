---
layout: post
title: Blockchain
categories: []
tags: [concept, references]
description: A blockchain, originally termed as block chain, is a continuously growing distributed list of records, called blocks, that are linked using cryptographic security. 
cover: "/assets/images/blockchain.png"
cover_source: "https://d2v9y0dukr6mq2.cloudfront.net/video/thumbnail/rtcKLbaBipwaan5v/blockchain-title-in-matrix-space_sk78fvxp__F0000.png"
comments: true
---

### What is **blockchain** ?
* Originally developed as a part of digital currency [**Bitcoin**](https://bitcoin.org/){:target="_blank"}.
* Blockchain can support a wide variety of applications such as peer-to-peer payment services, supply chain tracking etc.
* **Digital Record**: A blockchain is a record of transactions like a traditional ledger, where a transaction can be any movement of money, goods or data.
* **Secure**: It stores data in a way that it is virtually impossible to tamper the data without being detected by other users.
* **Decentralized**: Blockchain uses decentralized verification systems that uses consensus of multiple users instead of traditional centralized ones regulated by a verified authority like a government or a credit card clearinghouse.

### How does it work ?
* Blockchain **Steps**:
  * First, gather and order data into blocks.
  * Second, chain them together securely using cryptography.
* **Recording** a Transaction:
  * Say A sells car to B. 
  * Transaction information is recorded and shared with other systems on the blockchain network.
* Building transactions into **Blocks**:
  * On the network, the record is combined with other transactions to form a block and each transaction is **time stamped**.
  * Upon completion, a block also gets a time stamp.
  * All the data is sequential which helps to avoid duplicate records.
* Connecting blocks into **Chains**:
  * Completed block is sent out across the network and appended to the chain.
  * Other participants may also be sending out their blocks but the time stamp ensures the correct order of blocks and participants have the latest versions.
* **Securing** the chain:
  * Security is maintained using a **hash** and the cryptographic math makes the links between blocks made using these hashes virtually unbreakable.
  * A **hash function** takes the information in the block to create the hash which is a unique string of characters easy to generate but almost impossible to back trace to original data.
* **Locking** it down:
  * The hash from one block is added to the data in the next block.
  * So, when the next block goes through the hash function a trace of hash from previous block is woven into the new hash.
  * The same is repeated further down the chain.
* Raising the **Alarm**:
  * So if there is any tampering with a previously created block the hash encoded in the next block will not match up anymore.
  * The mismatch will cascade through all subsequent blocks denoting an alteration in the chain.
* Establishing **Trust**:
  * Since all the participants have a copy of the block chain they can detect any data tampering.
  * If hashes match up across the chain, all parties know they can trust their records.

### Blockchain in Action (Examples)
* Enormous potential.
* Because they establish trust, they provide simple, paperless way to establish ownership of money, information and objects - like concert tickets.
* **Trusted Concert Tickets**:
  * Trusted Seller: It's hard to tell a real ticket from a counterfeit, especially if bought through a third-party website or a private individual.
  * Going Straight to the Source: Blockchain can help buyers quickly establish that a ticket (and its seller) can be trusted.
  * The event venue will register all tickets to a blockchain which would be accessible online.
  * When a ticket is sold it will be assigned an address - a string of data publically viewable on the blockchain.
  * Owner is given a private key which is a hash of the address data.
  * The key can be used to **unlock** the address. So by producing the correct key the buyer can prove that the item is theirs without checking with the event venue.
  * If they choose to sell it, it is assigned a new address, and new owner gets a new private key and the transaction is added to the blockchain.
  * The ticket can be sold multiple number of times and when a seller unlocks the ticket with their private key, the buyer knows that the ticket they are getting is authentic.
* **More Efficient Markets**:
  * Removing the Bottlenecks: In the financial markets the trade happens in a fraction of second, but the actual exchanging of assets and payments can take days, involving multiple banks and clearinghouses which can cause errors, delays and other unnecessary risks.
  * **Smart Contract**: A piece of computer code that describes a transaction step by step. It can connect to multiple blockchains, tracking multiple assets so it can swap those assets as needed to execute transactions.
  * A broker only needs to buy stock on behalf of a client. The order will be placed with the private keys of both the buyer and seller.
  * This will trigger the execution of a smart contract. It connects to multiple blockchains, verifies the availability of the stock and the payment and then makes the transfers between the seller and the buyer.
* **Digital ID**:
  * Digitally issued IDs via a blockchain would be more secure mechanism than the traditional ones issued by governments.
  * Internation ID Blockchain, accessible anywhere in the world, allows people to prove identity, connect with family member or receive money without a bank account.
  * A person is a fingerprint. Fingerprint is digitized and added to blockchain with other data like name etc.
  * To prove identity they need to give their fingerprint which can be used to unlock and verify their ID.

### Improvements Needed:
* Early stage of the technology.
* Has various hurdles to overcome:
  * Departure from manual work for businesses would add **new costs** and **new risks** which leads to reluctance to adopt the new tech.
  * Current blockchain technologies like bitcoin can support only **5-8 transactions per second** which cannot keep up with applications like credit card transactions which amount to be **around 10000 times** what is supported.
  * Even though its transparent in ledgering there are **no real standardization** of implementation, which is required for relaibility and other legal issues.
  * Even though it uses business grade cryptography, it is **not 100% secure**. Large sums of money transaction therefore would be reluctant to adopt this technology.

## REFERENCES:

<small>[Blockchain by Goldman Sachs](http://www.goldmansachs.com/our-thinking/pages/blockchain/){:target="_blank"}</small>

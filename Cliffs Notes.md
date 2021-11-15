# Cliffs Notes on Safecoin Program Library
The Safecoin (Solana) Program Library project is a goldmine and a grab bag of useful stuff, but as is the general style of rust projects the coders write functional well engineered code but they apparently think that the code is totally "self explanatory"; in the author's experience it is not. So what follows are some notes on what exactly the Safecoin Program Library contains with the hope that these note will be a sort of roadmap to save new developers time.  Note that Solana already provides documentation for this [project](https://spl.solana.com) and I simply, humbly hope to build on that information.

## Introduction To Sealevel
Solana has tried to rename "BPF programming" as "Sealevel Application Environment.  But you are building BPF code.  BPF is the acronym for BSD Packet Filtering.  In a nutshell all sealevel programming involves four activities:
* Creating accounts
* Changing the balance  of an account.
* Writing data into an account.
* Calling other sealevel programs.

## For Beginners

### Examples
The following examples are, logically enough, in a directory called `examples`. Each example program includes a test you can run. And for each example written in rust there is a corresponding example written in 'C'.

* The fundamental example is `transfer-lamports` and it shows exactly what you would expect a blockchain to be able to do easily: send some lamports (a lamport is a billionth of a Safecoin) from one account to another.  

* Because you are writing code that runs in a very inaccessible, rigorous environment you it will be important that you can log messages from your code, the `logging` example shows specific logging methods available to sealevel programs. Critically there is the `sol_log_params` method to dump the standard instruction parameters. 

* Next most simple example is called `sysvar` and it shows how a program can access [several pieces of cluster level information](https://docs.solana.com/developing/runtime-facilities/sysvars) such as the system clock and current slot.

* Lastly simple (and really, not simple at all is) is an example called `cross-program-invocation` demonstrates that sealevel (BPF) code can [call other sealevel code](https://docs.solana.com/developing/programming-model/calling-between-programs).

### Example 5: Shared Memory
 
The `shared-memory` program is not under `examples` but could have been. A Safecoin account has two fields and a program can use either the unsigned 64 bit balance which is used to store lamports (Safecoin). Or the other field which is `data` that can contain up to 10 megabytes of data (to be interpreted as the program so desires).  So it can be useful to treat this data field as "shared memory" within or even between programs. The comment in the code describes the program:
```
This program expects one account and writes instruction data into the
account's data.  The first 8 bytes of the instruction data contain the
little-endian offset into the account data.  The rest of the instruction
data is written into the account data starting at that offset.
```
Is this truly useful?  It seems pretty limiting that the biggest offset into possibly 10 megs of data is 256.  

## Low Intermediate
### Memo

A straightforward useful blockchain application is writing a cryptographically signed memo in the chain.  It is [well-described by the Solana team](https://spl.solana.com/memo).

### Name Service

A sealevel program for issuing and managing ownership of: domain names, SafecoinPubkeys, URLs, twitter handles, ipfs cid's, metadata, etc.  This program provides an interface and implementation that third parties can utilize to create and use their own version of a name service of any kind.

Full documentation is available at [solana](https://spl.solana.com/name-service)

## Important Intermediate

# Safe Token 

Tokens are the basis of many, if not most, DeFi applications that can be built on Safecoin.  [The Solana Team has done a pretty good job documenting this program.](https://spl.solana.com/token)
You should walk through solana docs to play with creating a token

## Advanced

### Themis

Themis is the basis of the Brave Browser's anonymous advertisement framework.  





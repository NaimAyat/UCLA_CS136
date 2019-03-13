# Lecture 6
## Basics of Security Protocols
* Assume (usually) that your encryption is sufficiently strong
* Given that, how do you design a message exchange to achieve a given result securely?
* Not nearly as easy as you probably think
* Many of the concepts are important in many areas of computer/network security
## Security Protocols
* A series of steps involving two or more parties designed to accomplish a task with suitable security
* Sequence is important
* Cryptographic protocols use cryptography
  * Most useful protocols are cryptographic
* Different protocols assume different levels of trust between participants
## Types of Security Protocols
* Arbitrated protocols 
  * Involving a trusted third party
* Adjudicated protocols
  * Trusted third party, after the fact
* Self-enforcing protocols
  * No trusted third party
## Goals of Security Protocols
* Each protocol is intended to achieve some very particular goal
  * Like setting up a key between two parties
* Protocols may only be suitable for that particular purpose
* Important secondary goal is minimalism
  * Fewest possible messages
  * Least possible data
  * Least possible encryption
## Key Exchange Protocols
* Often we want a different encryption key for each communication session 
* How do we get those keys to the participants?
  * Securely
  * Quickly
  * Even if they’ve never communicated before
## Key Exchange With Symmetric Encryption and an Arbitrator
* Alice and Bob want to talk securely with a new key
* They both trust Trent
  * Assume Alice & Bob each share a key with Trent
* How do Alice and Bob get a shared key?
## The Man-in-the-Middle Attack
* A class of attacks where an active attacker interposes himself secretly in a protocol
* Allowing alteration of the effects of the protocol
* Without necessarily attacking the encryption
## Defeating the Man In the Middle
* Problems:
  1.  Trent doesn’t really know what he’s supposed to do
  2.  Alice doesn’t verify he did the right thing
* Minor changes can fix that
  1.  Encrypt request with K<sub>A</sub>
  2.  Include identity of other participant in response -  E<sub>K<sub>A</sub></sub>(K<sub>S</sub>, Bob)
## But There’s Another Problem
* A replay attack
* Replay attacks occur when Mallory copies down a bunch of protocol messages
* And then plays them again
* In some cases, this can wreak havoc
* Why does it here?
## Key Exchange With Public Key Cryptography
* With no trusted arbitrator
* Alice sends Bob her public key 
* Bob sends Alice his public key
* Alice generates a session key and sends it to Bob encrypted with his public key, signed with her private key
* Bob decrypts Alice’s message with his private key
* Encrypt session with shared session key
## Combined Key Distribution and Authentication
* Usually the first requires the second
  * Not much good to be sure the key is a secret if you don’t know who you’re sharing it with
* How can we achieve both goals?
  * In a single protocol
  * With relatively few messages
## Needham-Schroeder Key Exchange
* Uses symmetric cryptography
* Requires a trusted authority
  * Who takes care of generating the new key
* More complicated than some protocols we’ve seen
### What's R<sub>A</sub>?
* R<sub>A</sub> is random number chosen by Alice for this invocation of the protocol
  * Not used as a key, so quality of Alice’s random number generator not too important
* Helps defend against replay attacks
* This kind of random number is sometimes called a *nonce*
## Timestamps in Security Protocols
* One method of handling this kind of problem is timestamps
* Proper use of timestamps can limit the time during which an exposed key is dangerous
* But timestamps have their own problems
## Using Timestamps in the Needham-Schroeder Protocol
* The trusted authority includes timestamps in his encrypted messages to Alice and Bob
* Based on a global clock
* When Alice or Bob decrypts, if the timestamp is too old, abort the protocol
## Problems With Using Timestamps
* They require a globally synchronized set of clocks
  * Hard to obtain, often
  * Attacks on clocks become important
* They leave a window of vulnerability
## The Suppress-Replay Attack
* Assume two participants in a security protocol
  * Using timestamps to avoid replay problems
* If the sender’s clock is ahead of the receiver’s, attacker can intercept message
  * And replay later, when receiver’s clock still allows it
## Handling Clock Problems
1. Rely on clocks that are fairly synchronized and hard to tamper with
   * Perhaps GPS signals
2. Make all comparisons against the same clock
   * So no two clocks need to be synchronized

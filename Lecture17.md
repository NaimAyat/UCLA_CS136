# Lecture 17: Privacy
## Some Specific Privacy Problems
* Poorly secured databases that are remotely accessible
  * Or are stored on hackable computers
* Data mining by companies we interact with
* Eavesdropping on network communications by governments
* Insiders improperly accessing information
* Cell phone/mobile computer-based location tracking
## Data Mining and Privacy
* Data mining allows users to extract models from databases
  * Based on aggregated information
* Often data mining allowed when direct extraction isn’t
* Unless handled carefully, attackers can use mining to deduce record values
## An Example of the Problem
* Netflix released a large database of user rankings of films
  * Anonymized, but each user had one random identity
* Clever researchers correlated the database with IMDB rankings
  * Which weren’t anonymized
  * Allowed them to match IMDB names to Netflix random identities
## Data Encryption for Privacy
* Store private data in encrypted form
* If the encrypted version is divulged, attacker might not be able to use it
  * Assuming strong crypto
  * And careful key management
* Particularly important for data on devices that are easily stolen
  * Portable computers, smart phones, flash drives
## Anonymizers
* Network sites that accept requests of various kinds from outsiders
* Then submit those requests
  * Under their own or fake identity
* Responses returned to the original requestor
* A NAT box is a poor man’s anonymizer
## Onion Routing
* Meant to handle issue of people knowing who you’re talking to
* Basic idea is to conceal sources and destinations
* By sending lots of crypo-protected packets between lots of places
* Each packet goes through multiple hops

* A group of nodes agree to be onion routers
* Users obtain crypto keys for those nodes
* Plan is that many users send many packets through the onion routers
* Concealing who’s really talking
## Sending an Onion-Routed Packet
* Encrypt the packet using the destination’s key
* Wrap that with another packet to another router
  * Encrypted with that router’s key
* Iterate a bunch of times
## What’s Been Achieved?
* Nobody improper read the message
* Nobody knows who sent the message 
  * Except the receiver
* Nobody knows who received the message
  * Except the sender
## Issues for Onion Routing
* Proper use of keys
* Traffic analysis
* Overheads
  * Multiple hops
  * Multiple encryptions
## Privacy-Preserving Data Mining
* Perturbation
  * Add noise to sensitive value
* Blocking
  * Don’t let aggregate query see sensitive value
* Sampling
  * Randomly sample only part of data

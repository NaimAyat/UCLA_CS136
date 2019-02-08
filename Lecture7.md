# Lecture 7
## Authentication
* Determining the identity of some entity
  * Process
  * Machine
  * Human user
* Requires notion of identity
* And some degree of proof of identity
## Authentication Vs. Authorization
* *Authentication* is determining who you are
* *Authorization* is determining what someone is allowed to do
* Can’t authorize properly without authentication
* Purpose of authentication is usually to make authorization decisions
## Identifying With a Computer
* Not as smart as a human
  * Steps to prove identity must be well defined 
* Can’t do certain things as well
  * E.g., face recognition
* But lightning fast on computations and less prone to simple errors
  * Mathematical methods are acceptable
## Identifying Computers and Programs
* No physical characteristics
  * Faces, fingerprints, voices, etc.
* Generally easy to duplicate programs
* Not smart enough to be flexible
  * Must use methods they will understand
* Again, good at computations 
## Identity Might Not Be Rechecked
* Human beings can make identification mistakes
* But they often recover from them
* Based on observing behavior that suggests identification was wrong
* Computers and programs rarely have that capability
  * If they identify something, they believe it
## Authentication Mechanisms
* Something you know
  * E.g., passwords
* Something you have
  * E.g., smart cards or tokens
* Something you are
  * Biometrics
* Somewhere you are
  * Usually identifying a role
## Passwords
* Authentication by what you know
* One of the oldest and most commonly used security mechanisms
* Authenticate the user by requiring him to produce a secret
  * Usually known only to him and to the authenticator
## Problems With Passwords
* They have to be unguessable
  * Yet easy for people to remember
* If networks connect remote devices to computers, susceptible to password sniffers
* Unless quite long, brute force attacks often work on them
## Proper Use of Passwords
* Passwords should be sufficiently long
* Passwords should contain non-alphabetic characters
* Passwords should be unguessable
* Passwords should be changed often
* Passwords should never be written down
* Passwords should never be shared
* Hard to achieve all this simultaneously
## Passwords and Single Sign-On
* Many systems ask for password once
  * Resulting authentication lasts for an entire “session”
* Used on its own, complete mediation definitely not achieved
* Trading security for convenience
* Especially if others can use the authenticated machine
## Handling Passwords
* The OS must be able to check passwords when users log in
* So must the OS store passwords?
* Not really 
  * It can store an encrypted version
* Encrypt the offered password 
  * Using a one-way function
* And compare it to the stored version
## One Way Functions
* Functions that convert data A into data B
* But it’s hard to convert data B back into data A
* Often done as a particular type of cryptographic operation
  * E.g., cryptographic hashing
* Depending on particular use, simple hashing might be enough
## Is Encrypting the Password File Enough?
* What if an attacker gets a copy of your password file?
* Dictionary attack possible
## Dictionary Attck
* Real dictionary attacks don’t use Webster’s
* Dictionary based on probability of words being used as passwords
* Partly set up as procedures
  * E.g., try user name backwards
* Checks common names, proper nouns, etc. early in the process
* Tend to evolve to match user trends
## A Serious Issue
* All Linux machines use the same one-way function to encrypt passwords
* If someone runs the entire dictionary through that function, 
  * Will they have a complete list of all encrypted dictionary passwords?
  * For all Linux systems?
## Salted Passwords
* Combine the plaintext password with a random number
  * Then run it through the one-way function
* The random number need not be secret
* It just has to be different for different users
## What Is This Salt, Really?
* An integer that is combined with the password before hashing
* How will you be able to check passwords by hashing them, then?
* By storing the salt integer with the password
  * Generally in plaintext
* Note the resemblance to nonces and IVs
* Why is it OK (or OK-ish) to leave this important information in plaintext?
## Modern Dictionary Attacks
* Modern machines are very fast
* Even with salting, huge dictionaries can be checked against encrypted passwords quickly
* In 2012, Ars Technica challenged 3 hackers to crack 16,000 hashed, salted passwords
  * Using dictionary attacks, they got 90% of them in 20 hours
## GPU Password Cracking
* GPUs are great for password cracking
  * Highly parallelizable task
  * 200x faster than CPU
* Possible to build cheap, powerful GPU unit for this purpose (less than $2000)
* Prototypes crack 20-50% of passwords in example files in a few minutes

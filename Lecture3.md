# Lecture 3
## Intro to Encryption
* Much of computer security is about keeping secrets
* One method is to make the secret hard for others to read
* While (usually) making it simple for authorized parties to read
## Encryption
* Encryption is the process of hiding information in plain sight
* Transform the secret data into something else
* Even if the attacker can see the transformed data, he can’t understand the underlying secret
## Encryption and Data Transformations
* Encryption is all about transforming the data
* One bit or byte pattern is transformed to another bit or byte pattern
* Usually in a reversible way
## Encryption Terminology
* Encryption is typically described in terms of sending a message
  * The sender is S
  * The receiver is R
  * And the attacker is O
* *Encryption* is the process of making message unreadable/unalterable by O
* *Decryption* is the process of making the encrypted message readable by R
* A system performing these transformations is a *cryptosystem*
  * Rules for transformation sometimes called a *cipher*
## Plaintext and Ciphertext
* *Plaintext* is the original form of the message (often referred to as P)
* *Ciphertext* is the encrypted form of the message (often referred to as C)
## Very Basics of Encryption Algorithms
* Most algorithms use a *key* to perform encryption and decryption
  * Referred to as K
  * The key is a secret
  * Without the key, decryption is hard
  * With the key, decryption is easy
## Terminology for Encryption Algorithms
* The encryption algorithm is referred to as E()
* C = E(K,P)
* The decryption algorithm is referred to as D()
	* Sometimes the same algorithm as E()
* The decryption algorithm also has a key
## Symmetric and Asymmetric Encryption Systems
* Symmetric systems use the same keys for E and D:
  * P = D(K, C)
  * Expanding, P = D(K, E(K,P))
* Asymmetric systems use different keys for E and D:
  * C = E(K<sub>E</sub>,P)
  * P = D(K<sub>D</sub>,C) 
## Characteristics of Keyed Encryption Systems
* If you change only the key, a given plaintext encrypts to a different ciphertext
* Same applies to decryption

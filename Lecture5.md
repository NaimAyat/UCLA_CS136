# Lecture 5
## Properties of Keys
* Length
* Randomness
* Lifetime
* Secrecy
* Generation
## Key Length
* If your cryptographic algorithm is otherwise perfect, its strength depends on key length
* Since the only attack is a brute force attempt to discover the key
* The longer the key, the more brute force required
## Are There Real Costs for Key Length?
* Generally, more bits is more secure
* Why not a whole lot of key bits, then?
* Some encryption done in hardware
  * More bits in hardware costs more
* Some software encryption slows down as you add more bits, too
  * Public key cryptography especially
* Some algorithms have defined key lengths only
* If the attack isn’t brute force, key length might not help
## Key Randomness
* Brute force attacks assume you chose your key at random
* If attacker learns how you chose your key
  * He can reduce brute force costs
* How good is your random number generator?
## Generating Random Keys 
* Don’t use `rand()``
* The closer the method chosen approaches true randomness, the better
* But, generally, don’t want to rely on exotic hardware
* True randomness is not essential
  * Need same statistical properties
  * And non-reproducibility
## Cryptographic Methods
* Start with a random number
* Use a cryptographic hash on that number
* If the cryptographic hash is a good one, the new number looks pretty random
* Extract what you need from it
* Produce new keys by hashing old ones
## Is This Method Secure?
* It depends (in part) on the strength of hash algorithm
  * Does it produce “random” numbers?
  * Is the part you extract itself random?
* Another problem:  It falls apart if any key is ever broken or divulged
  * Doesn’t have *perfect forward secrecy*
## Perfect Forward Secrecy
* A highly desirable property in a cryptosystem
* It means that the compromise of any one session key will not compromise any other
  * E.g., don’t derive one key from another using a repeatable algorithm
* Keys do get divulged, so minimize the resulting damage
## Random Noise
* Observe an event that is likely to be random
  * Physical processes (cosmic rays, etc.)
  * Real world processes (variations in disk drive delay, keystroke delays, etc.)
* Assign bit values to possible outcomes
* Record or generate them as needed
* More formally described as *gathering entropy*
* Keys derived with proper use of randomness have good perfect forward secrecy
## On Users and Randomness
* Some crypto packages require users to provide entropy 
  * To bootstrap key generation or other uses of randomness
* Users do this badly (often very badly)
* They usually try to do something simple
  * And not really random
* Better to have crypto package get its own entropy
## Don’t Go Crazy on Randomness
* Make sure you actually get a new key every time
  * A surprisingly common flaw
* Make sure it’s non-reproducible
  * So attackers can’t play it back
* Make sure there aren’t obvious patterns
* Attacking truly unknown patterns in fairly random numbers is extremely challenging
## Key Lifetime
* If a good key’s so hard to find,
  * Why every change it?
* How long should one keep using a given key?
* Long-lived keys are more likely to be compromised
* The longer a key lives, the more data is exposed if it’s compromised
* The longer a key lives, the more resources opponents can (and will) devote to breaking it
* The more a key is used, the easier the cryptanalysis on it
* A secret that cannot be readily changed should be regarded as a vulnerability
## Practicalities of Key Lifetimes
* In some cases, changing keys is inconvenient
  * E.g., encryption of data files
* Keys used for specific communications sessions should be changed often
  * E.g., new key for each VoIP call
* Keys used for key distribution can’t be changed too often
* Some keys must be stored permanently or at least for a long time
## Key Storage
* Symmetric session keys
  * Avoid storing them permanently
  * Get rid of them when session ends
* Long term symmetric keys
  * E.g., for disk encryption
  * Safe storage is critical
* Private asymmetric keys
  * Usually require long-term storage
  * Safe storage is critical
## Storing a User’s Keys
* Where are a user’s keys kept?
  * Given they must be used often
* Permanently on the user’s machine? 
  * What happens if the machine is cracked?
* People can’t remember random keys
  * Hash keys from passwords/passphrases?
* Keep keys on smart cards or hardware security enclaves?
* Get them from key servers?
  * Not a popular solution
## Destroying Old Keys
* Never keep a key around longer than necessary
  * Gives opponents more opportunities
* Destroy keys securely
  * For computers, remember that information may be in multiple places
    * Caches, virtual memory pages, freed file blocks, stack frames, etc.
  * Real modern attacks based on finding old keys in unlikely places

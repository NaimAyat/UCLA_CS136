# Lecture 4
## Desirable Characteristics of Ciphers
* Well matched to requirements of application
  * Amount of secrecy required should match labor to achieve it
* Freedom from complexity
  * The more complex algorithms or key choices are, the worse
* Simplicity of implementation
  * Seemingly more important for hand ciphering
  * But relates to probability of errors in computer implementations
* Errors should not propagate
* Ciphertext size should be same as plaintext size
* Encryption should maximize confusion
  * Relation between plaintext and ciphertext should be complex
* Encryption should maximize diffusion
  * Plaintext information should be distributed throughout ciphertext
## Stream and Block Ciphers
* Stream ciphers convert one symbol of plaintext immediately into one symbol of ciphertext
* Block ciphers work on a given sized chunk of data at a time
## Advantages of Stream Ciphers
* Speed of encryption and decryption
  * Each symbol encrypted as soon as it’s available
* Low error propagation
  * Errors affect only the symbol where the error occurred, depending on cryptographic mode
## Disadvantages of Stream Ciphers
* Low diffusion
  * Each symbol separately encrypted
  * Each ciphertext symbol only contains information about one plaintext symbol
* Susceptible to insertions and modifications
* Not good match for many common uses of cryptography
* Some disadvantages can be mitigated by use of proper cryptographic mode
### Sample Stream Cipher: RC4
* Creates a changing key stream
  * Supposedly unpredictable
* XOR the next byte of the key stream with the next byte of text to encrypt
* XOR ciphertext byte with same key stream byte to decrypt
* Alter your key stream as you go along
#### Creating an RC4 Key
* Fill an 256 byte array with 0-255
* Choose a key of 1-255 bytes
* Fill a second array with the key
  * Size of array depends on the key
* Use a simple operation based on the key to swap around bytes in the first array
* That produces the key stream you’ll use
* Swap two array bytes each time you encrypt
#### Characteristics of RC4
* Around 10x faster than DES
* Significant cryptographic weakness in its initial key stream
  * Fixable by dropping the first few hundred of the keys
* Easy to use it wrong
* Key reuse is a serious problem
* Other problems have led to its deprecation
## Advantages of Block Ciphers
* Good diffusion
  * Easier to make a set of encrypted characters depend on each other
* Immunity to insertions
  * Encrypted text arrives in known lengths
* Most common Internet crypto done with block ciphers
## Disadvantages of Block Ciphers
* Slower
  * Need to wait for block of data before encryption/decryption starts
* Worse error propagation
  * Errors affect entire blocks
## Cryptographic Modes
* Let’s say you have a bunch of data to encrypt
  * Using the same cipher and key
* How do you encrypt the entire set of data?
  * Given block ciphers have limited block size
  * And stream ciphers just keep going
* A *cryptographic mode* is a way of applying a particular cipher
  * Block or stream
* The same cipher can be used in different modes
  * But other things are altered a bit
* A cryptographic mode is a combination of cipher, key, and feedback
  * Plus some simple operations

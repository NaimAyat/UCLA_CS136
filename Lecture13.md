# Lecture 13: Secure Programming
## Principles for Secure Software
### 1. Secure the Weakest Link
* Don’t consider only a single possible attack
* Look at all possible attacks you can think of
* Concentrate most attention on most vulnerable elements
### 2. Practice Defense in Depth
* Try to avoid designing software so failure anywhere compromises everything
* Also try to protect data and applications from failures elsewhere in the system
* Don’t let one security breach give away everything
### 3. Fail Securely
* Security problems frequently arise when programs fail
* They often fail into modes that aren’t secure
* So attackers cause them to fail
  * To see if that helps them
* So make sure that when ordinary measures fail, the fallback is secure
### 4. Use Principle of Least Privilege
* Give minimum access necessary 
* For the minimum amount of time required
* Always possible that the privileges you give will be abused
  * Either directly or through finding a security flaw
* The less you give, the lower the risk
### 5. Compartmentalize
* Divide programs into pieces
* Ensure that compromise of one piece does not automatically compromise others
* Set up limited interfaces between pieces
  * Allowing only necessary interactions
### 6. Value Simplicity
* Complexity is the enemy of security
* Complex systems give more opportunities to screw up
* Also, harder to understand all “proper” behaviors of complex systems
* So favor simple designs over complex ones
### 7. Promote Privacy
* Avoid doing things that will compromise user privacy
* Don’t ask for data you don’t need
* Avoid storing user data permanently
  * Especially unencrypted data
* There are strong legal issues related to this, nowadays
### 8. Remember That Hiding Secrets is Hard
* Assume anyone who has your program can learn everything about it
* “Hidden” keys, passwords, certificates in executables are invariably found
* Security based on obfuscated code is always broken
* Just because you’re not smart enough to crack it doesn’t mean the hacker isn’t
### 9. Be Reluctant to Trust
* Don’t automatically trust things
* Remember, you’re not just trusting the honesty of the other party
  * You’re also trusting their caution
* Avoid trusting users you don’t need to trust, too
  * Doing so makes you more open to social engineering attacks
### 10. Use Your Community Resources
* Favor widely used and respected security software over untested stuff
* Keep up to date on what’s going on
  * Not just patching
  * Also things like attack trends
## Choosing Technologies
* Different technologies have different security properties
  * Operating systems
  * Languages
  * Object management systems
  * Libraries
* Important to choose wisely
  * Understand the implications of the choice
## C and C++
* Probably the worst security choice
* Far more susceptible to buffer overflows than other choices
* Also prone to other reliability problems
* Often chosen for efficiency
  * But is efficiency that important for your application?
## Java
* Less susceptible to buffer overflows
* Also better error handling than C/C++
* Has special built-in security features
  * Which aren’t widely used
* But has its own set of problems
  * E.g., exception handling issues
  * And issues of inheritance
* 9 remotely exploitable security flaws in 2nd quarter 2016 Oracle patches
* Multiple serious security problems in recent years
## Python
* A type-safe language
  * So buffer overflows usually not possible
* But many extensibility features
  * YAML, pickles, import paths
  * Attackers can use these to get malicious code into your program
* Injection attacks (SQL, commands)
## Scripting Languages
* Depends on language
* Many are type safe (or non-typed), limiting buffer overflow possibilities
* Javascript and CGIbin have awful security reputations
* Perl offers some useful security features
* But there are some general issues
## Scripting Language Security Issues
* Might be security flaws in their interpreters
  * More likely than in compilers
* Scripts often easily examined by attackers
  * Obscurity of binary is no guarantee, but it is an obstacle
* Scripting languages often used to make system calls
  * Inherently dangerous, esp. things like eval()
* If they call libraries, there can be overflows there
  * E.g., Python buffer overflow in 2014
* Many script programmers don’t think about security at all
## Major Problem Areas for Secure Programming
* Buffer overflows and other input verification issues
* Error handling
* Privilege escalation
* Race conditions
Use of randomness
* Proper use of cryptography
* Trust 
* Variable synchronization
* Variable initialization
## Buffer Overflows
* The poster child of insecure programming
* One of the most commonly exploited types of programming error
* Key problem is language does not check bounds of variables
## Preventing Buffer Overflows
* Use a language with bounds checking
  * Most modern languages other than C and C++ (and assembler)
  * Not always a choice
  * Or the right choice
  * Not always entirely free of overflows
* Check bounds carefully yourself
* Avoid constructs that often cause trouble
## Problematic Constructs for Buffer Overflows
* Most frequently C system calls:
  * `gets(), strcpy(), strcat(), sprintf(), scanf(), sscanf(), fscanf(), vfscanf(),vsprintf(), vscanf(), vsscanf(), streadd(), strecpy()`
* There are others that are also risky
## Why Are These Calls Risky?
* They copy data into a buffer
* Without checking if the length of the data copied is greater than the buffer
* Allowing overflow of that buffer
* Assumes attacker can put his own data into the buffer
  * Not always true
  * But why take the risk?
## Canary Values
* One method of detecting buffer overflows
* Akin to the “canary in the mine”
* Place random value at end of data structure
* If value is not there later, buffer overflow might have occurred
* Implemented in language or OS
## Data Execution Prevention (DEP)
* Buffer overflows typically write executable code somewhere
* DEP prevents this
* Page is either writable or executable
* So if overflow can write somewhere, can’t execute the code
* Present in Windows, Mac OS, etc.
* Doesn’t help against some advanced techniques
## Randomizing Address Space (ASLR)
* Address Space Layout Randomization
* Randomly move around where things are stored
* Base address, libraries, heaps, stack
* Making it hard for attacker to write working overflow code
* Used in Windows, Linux, MacOS
* Not always used, not totally effective
  * Several recent Windows problems from programs not using ASLR
## The Heartbleed Bug
* A bug in the OpenSSL implementation of SSL/TLS 
* Effect was to reveal potentially secret information from a remote process
  * Cryptographic keys, passwords, Social Security Numbers, etc.
* A buffer overread problem
## SSL Heartbeat Messages
* SSL requires heartbeat messages
* One side sends the other a buffer containing some content
* The other side must send the same content back
* The heartbeat message contains the buffer and its length
## The Security Flaw
* The OpenSSL implementation did not verify the length field
  * Didn’t check that it matched the actual buffer supplied
* Instead, it returned whatever was in the buffer plus any extra specified length
* Which was something else in the process’ memory
## Exploiting Heartbleed
* Establish an SSL connection to a vulnerable server
* Repeatedly send these buffer overread requests
* Examine what you get back looking for “good stuff”
## Fixing Heartbleed
* Update the software to check the buffer length in heartbeat messages
* In practice, required updating software in literally millions of sites
  * Some still not patched

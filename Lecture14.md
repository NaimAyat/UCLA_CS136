# Lecture 14: Secure Programming, Continued
## Error Handling
* Error handling code often gives attackers great possibilities
* It’s rarely executed and often untested
* So it might have undetected errors
* Attackers often try to compromise systems by forcing errors
## A Typical Error Handling Problem
* Not cleaning everything up
* On error conditions, some variables don’t get reset
* If error not totally fatal, program continues with old values
* Could cause security mistakes
  * E.g., not releasing privileges when you should
## Checking Return Codes
* A generalization of error handling
* Always check return codes
* A security program manager for Microsoft said this is his biggest problem
* Very dangerous to bull ahead if it turns out your call didn’t work properly
* Example:  Nagios XI didn’t check the return value of setuid() call, allowing privilege escalation
## Privilege Escalation
* Programs usually run under their user’s identity with his privileges
* Some programs get expanded privileges
  * Setuid programs in Unix, e.g.
* Poor programming here can give too much access
## An Example Problem
* A program that runs setuid and allows a shell to be forked
  * Giving the caller a root environment in which to run arbitrary commands
* Buffer overflows in privileged programs usually give privileged access
* Privilege escalation – using program flaws to obtain greater access privileges you shouldn’t get
## What To Do About This?
* Avoid running programs setuid
  * Or in other OSs’ high privilege modes
* If you must, don’t make them root-owned
  * Remember, least privilege
* Change back to the real caller as soon as you can
  * Limiting exposure
* Use virtualization to compartmentalize
## Virtualization Approaches
* Run in a virtual machine
* Hard to specify what’s safe
* Hard to allow safe interactions between different VMs
* VM might not have perfect isolation
## Race Conditions
* A common cause of security bugs
* Usually involve multiprogramming or multithreaded programs
* Caused by different threads of control operating in unpredictable fashion
  * When programmer thought they’d work in a particular order
## What Is a Race Condition?
* A situation in which two (or more) threads of control are cooperating or sharing something
* If their events happen in one order, one thing happens
* If their events happen in another order, something else happens
* Often the results are unforeseen
## Security Implications of Race Conditions
* Usually you checked privileges at one point
* You thought the next lines of code would run next
  * So privileges still apply
* But multiprogramming allows things to happen in between
## The TOCTOU Issue
* Time of Check to Time of Use
* Have security conditions changed between when you checked and when you used it?
* Multiprogramming issues can make that happen
* Sometimes under attacker control
## Effective UID and Access Permissions
* Real ID is the ID of the user who actually ran it
* Effective ID is current ID for access control purposes
* Unix checks accesses against effective UID, not real UID
* So setuid program uses permissions for the program’s owner
  * Unless relinquished
* Remember, root has universal access privileges
## What’s (Supposed to Be) Going on Here?
* Checked access on /tmp/userfile to make sure user was allowed to read it
  * User can use links to control what this file is
* access() checks real user ID, not effective one
  * So checks access permissions not as root, but as actual user
* So if user can read it, open file for read
  * Which root is definitely allowed to do
* Otherwise exit  
## What’s Really Going On Here?
* This program might not run uninterrupted
* OS might schedule something else in the middle
* In particular, between those two lines of code
## How the Attack Works
* Attacker puts innocuous file in  /tmp/userfile
* Calls the program
* Quickly deletes file and replaces it with link to sensitive file
  * One only readable by root
* If timing works, he gets secret contents
## Some Types of Race Conditions
* File races
  * Which file you access gets changed
* Permissions races
  * File permissions are changed
* Ownership races
  * Who owns a file changes
* Directory races
  * Directory hierarchy structure changes
## Preventing Race Conditions
* Minimize time between security checks and when action is taken
* Be especially careful with files that users can change
* Use locking and features that prevent interruption, when possible
* Avoid designs that require actions where races can occur
## Randomness and Determinism
* Many pieces of code require some randomness in behavior
* Where do they get it?
* As earlier key generation discussion showed, it’s not that easy to get
## Pseudorandom Number Generators
* PRNG
* Mathematical methods designed to produce strings of random-like numbers
* Actually deterministic
  * But share many properties with true random streams of numbers
## Attacks on PRNGs
* Cryptographic attacks
  * Observe stream of numbers and try to deduce the function
* State attacks
  * Attackers gain knowledge of or influence the internal state of the PRNG
## How to Do Better?
* Use hardware randomness, where available
* Use high quality PRNGs
  * Preferably based on entropy collection methods
* Don’t use seed values obtainable outside the program
## Proper Use of Cryptography
* Never write your own crypto functions if you have any choice
  * Another favorite piece of advice from industry
* Never, ever, design your own encryption algorithm
  * Unless that’s your area of expertise
* Generally, rely on tried and true stuff
  * Both algorithms and implementations
## Using Crypto Properly
* Even with good crypto algorithms (and code), problems are possible
* Proper use of crypto is quite subtle
* Bugs possible in:
  * Choice of keys
  * Key management
  * Application of cryptographic ops
## Variable Synchronization
* Often, two or more program variables have related values
* Common example is a pointer to a buffer and a length variable
* Are the two variables always synchronized?
* If not, bad input can cause trouble
## Variable Initialization
* Some languages let you declare variables without specifying their initial values
* And let you use them without initializing them
  * E.g., C and C++
## Why is that a problem?
* Values from one function “leak” into another function
* If attacker can influence the values in the first function,
* Maybe he can alter the behavior of the second one
## Variable Cleanup
* Often, programs reuse a buffer or other memory area
* If old data lives in this area, might not be properly cleaned up
* And then can be treated as something other than what it really was
* E.g., bug in Microsoft TCP/IP stack
  * Old packet data treated as a function pointer
## Use-After-Free Bugs
* Increasingly popular security bug type
* Related to memory management
  * Memory structures are dynamically allocated on the heap
* Either explicitly or implicitly freed 
  * Depending on language and context
* In some cases, pointers can be used to access freed memory
  * E.g., in C and C++
## Remote Code Execution Vulnerabilities
* Many programs allow plug-ins, extensions, other dynamic code
  * Great for generality and program power
* But attacker can add his code to your program
## Remote Code Execution and Middleware
* Complex systems are often built using middleware
  * Often more than one middleware component
* Middleware often includes extensibility features
* If you’re not careful, the attacker gets to use those features 
## A Common Problem
* A bug in the middleware dealing with some unusual data format
  * Or with an unexpected error condition in some data
* Leads to the ability to execute code provided remotely
## How To Avoid This Problem?
* Don’t add extensibility where it isn’t needed
* Don’t make system calls that can run arbitrary code
* Careful evaluation of input from external sources
* Understand problem areas for your chosen middleware

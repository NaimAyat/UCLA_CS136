# Lecture 1
## Examples of Security Problems
* Malicious code attacks
  * Multiple new viruses, worms, botnets, trojans appear every week
  * "Cryptojacking" of everything from servers to web cams
    * To mine cryptocurrency
  * Stuxnet worm targeted at nuclear facilities
    * Unspecified amounts of damage done to Iran's nuclear program
  * Increasing attacks on the IoT
* Distributed denial of service attacks
  * Use large number of compromised machines to attack one target
    * By exploiting vulnerabilities
    * Or generating a lot of traffic
  * Very common today
    * 1 TBps attack on Github in 2018
    * 2018 attacks on online gaming companies
    * Attacks based on compromised Huawei routers
  * Difficult problem to solve
* Vulnerabilities in commonly used systems
  * Critical vulnerabilities in Android, Windows, iOS, and macOS
  * Many popular apps and middleware have vulnerabilities
    * Windows VBScript, Apache Struts, WordPress, Adobe Flash
  * Many security systems have vulnerabilities
    * libssh, Microsoft CredSSP, Cisco Adaptive Security Appliance
  * Critical hardware flaws in Intel and AMD processors
    * Fixes lead to slower processor
* Electronic commerce Attacks
  * Identity theft (phishing)
  * Loss of data from laptop theft
  * Extortion via DDoS attacks or threatened release of confidential data
  * Crypto mining on compromised machines
## Cyberwarefare
* Nation states have developed capabilities to use computer networks for such purposes
* DDoS attacks on Estonia and Georgia
* Stuxnet
* Attacks on Ukrainian power grid
## Legacy and Retrofitting
* Legacy issues are a constrain
  * Core internet design
  * Popular programming languages
  * Commercial operating systems
* Retrofitting security works poorly
  * Consider the history of patching
### Problems with Patching
* Usually done under pressure
  * Quick and dirty
* Tends to deal with immediate problem, not root cause
* Hard to get patch to everyone
* Patches sometimes intruduce new security problems
  * Microsoft 2018 Meltdown patch
## Increasing CPU Speeds
* Attacks are developed more quickly; it's faster to adapt attack than defense
* Malware spreads faster
## Security and Protection
* *Security* is a policy
  * "No unauthorized user may access this file"
* *Protection* is a mechanism
  * "The system checks user identity against access permissions"
* **Protection mechanisms implement security policies**
## Vulnerabilities and Exploits
* A *vulnerability* is a weakness that can allow an attacker to cause problems
  * Not all vulnerabilities cause all problems
  * Most vulnerabilities are never exploited
* An *exploit* is an actual incident of taking advantage of a vulnerability
  * Allowing attacker to do something malicious on a machine
  * Term also refers to the code or methodology used to take advantage of a vulnerability
## Trust
* Not a theoretical issue
* Most vulnerabilities that are exploited are based on trust problems
* Attackers exploit overly trusting elements of the computer
  * From the access control model to the actual human user
## Transitive Trust
* I trust A. A trusts B. B trusts C. C trusts D. Should I trust D?
* Trust systems in peer applications
* Chains of certificates
* Less obvious examples
  * Web servers that call a database
  * Database perhaps trusts the webserver
  * But does the database trust the user who invoked the server
* Programs that call programs that call programs are important cases of transitive trust, and this is how modern systems are built
## Security Goals
* CIA
* Confidentiality
  * If it's supposed to be a secret, be careful who hears it
* Integrity
  * Don't let someone change something they shouldn't
* Availability
  * Don't stop others from using services
## Security Threats
* Theft of data
* Privacy
* Destruction
* Interruption or interference with computer-controlled services
* Misuse of computer controlled services
## Active Threats Vs. Passive Threats
* *Passive threats* are forms of eavesdropping
  * No modification, injections of requests, etc
* *Active threats* are more aggressive
* Passive threats are mostly to secrecy, active threats are to all properties
## Social Engineering
* The best computer security practices are easily subverted by bad human practices
  * Giving passwords out over the phone to anyone who asks
  * Responding to bogus email with your credit card number
* Social engineering attacks tend to be cheap, easy, effective
* So all our work may be for naught
### Social Engineering Example - Phishing
* Attackers send plausible email requesting you to visit a web site
* To “update” your information
* Typically a bank, popular web site, etc.
* The attacker controls the site and uses it to obtain your credit card, SSN, etc.
* Likelihood of success based on attacker’s ability to convince the victim that he’s real
  * And that the victim had better go to the site or suffer dire consequences
## Why isn't security easy?
* Security is different than most other problems in CS
* The “universe” we’re working in is much more hostile
* Human opponents seek to outwit us
* Fundamentally, we want to share secrets in a controlled way
  * A classically hard problem in human relations
* You have to get everything right
  * Any mistake is an opportunity for your opponent
* When was the last time you saw a computer system that did everything right?
* So, must we wait for bug-free software to achieve security?
## Security Is Actually Even Harder
* The computer itself isn’t the only point of vulnerability
* If the computer security is good enough, the foe will attack:
  * The users
  * The programmers
  * The system administrators
  * Or something you never thought of
## Additional Security Problems
* Costs
  * Computing resources
  * People's time and attention
* If people use them badly, most security measures won't do the job
* Security must work 100% effectively
* With 0% overhead or inconvenience or learning
* Most computer practitioners know little or nothing about security
* Few programmers understand secure programming practices
* Few sysadmins know much about secure system configuration
* Typical users know even less
## The Principle of Easiest Penetration
* An intruder must be expected to use any available means of penetration. This is not necessarily the most obvious means, nor is it necessarily the one against which the most solid defense has been installed.
  * The smart opponent attacks you where you’re weak, not where you’re strong
## The Principle of Adequate Protection
* Computer items must be protected only until they lose their value.  They must be protected to a degree consistent with their value.
  * Worthless things need little protection, and things with timely value need only be protected for a while

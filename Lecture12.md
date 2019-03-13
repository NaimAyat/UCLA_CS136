# Lecture 12: Malicious Software
## Viruses
* “Self-replicating programs containing code that explicitly copies itself and that can ‘infect’ other programs by modifying them or their environment”
* Typically attached to some other program
  * When that program runs, the virus becomes active and infects others
* Not all malware are viruses
  * But many characteristics of viruses are shared by other malware
## How Do Viruses Work?
* When a program is run, it typically has the full privileges of its running user
* Including write privileges for some other programs
* A virus can use those privileges to replace those programs with infected versions
## Macro and Attachment Viruses
* Modern data files often contain executables
  * Macros
  * Email attachments
* Many formats allow embedded commands to download of arbitrary executables
* Popular form of viruses
  * Requires less sophistication to get right
## How To Find Viruses
* Basic precautions
* Looking for changes in file sizes
* Scan for signatures of viruses
* Multi-level generic detection
## Containment
* Run suspect programs in an encapsulated environment
  * Limiting their forms of access to prevent virus spread
* Requires versatile security model and strong protection guarantees
  * No use to run in tightly confined mode if user allows it to get out
## Viruses and File Sizes
* Typically, a virus tries to hide
* So it doesn’t disable the infected program
* Instead, extra code is added
* But if it’s added naively, the size of the file grows
* Virus detectors look for this growth
* Won’t work for files whose sizes typically change
* Clever viruses find ways around it
  * E.g., cavity viruses that fit themselves into “holes” in programs
## Signature Scanning
* If a virus lives in code, it must leave some traces
* In unsophisticated viruses, these traces are characteristic code patterns
* Find the virus by looking for the signature
## How To Scan For Signatures
* Create a database of known virus signatures
* Read every file in the system and look for matches in its contents
* Also check every newly imported file
* Also scan boot sectors and other interesting places
* Can use same approach for other kinds of malware
## Weaknesses of Scanning for Signatures
* What if the virus changes its signature?
* What if the virus takes active measures to prevent you from finding the signature?
* You can only scan for known virus signatures
## Polymorphic Viruses
* A polymorphic virus produces varying but operational copies of itself
* Essentially avoiding having a signature
* Sometimes only a few possibilities
  * E.g., Whale virus has 32 forms
* But sometimes a lot
  * Storm worm had more than 54,000 forms
## Polymorphism By Hand
* Malware writers have become professional and security-aware
* They know when their malware has been identified
  * And they know the signature used
  * Smart ones subscribe to all major anti-virus programs
* They change the malware to remove that signature and re-release it
## Stealth Viruses
* A virus that tries actively to hide all signs of its presence
* Typically a resident virus
* For example, it traps calls to read infected files
  * And disinfects them before returning the bytes
  * E.g., the Brain virus
## Combating Stealth Viruses
* Stealth viruses can hide what’s in the files 
* But may be unable to hide that they’re in memory
* Careful reboot from clean source won’t allow stealth virus to get a foothold
* Concerns that malware can hide in other places, like peripheral memory
## Other Detection Methods
* Checksum comparison
* Intelligent checksum analysis
  * For files that might legitimately change
* Intrusion detection methods
  * E.g., look for attack invariants instead of signatures
* Identify and handle “clusters” of similar malware
## Trojan Horses
* Seemingly useful program that contains code that does harmful things
* A program you pick up somewhere that is supposed to do something useful
* And perhaps it does
  * But it also does something less benign
* Games are a common location host program
* Downloaded applets are also popular
* Frequently found in email attachments
* Bogus security products also popular
* Flash drives are a hardware vector
## RATs (Remote Access Trojans)
* A Trojan Horse designed to allow its creator to remotely access a machine
* Probably the most common form of Trojan Horse malware today
* Allows attacker to gain a foothold on a machine or network
## Trapdoors
* Also known as back doors
* A secret entry point into an otherwise legitimate program
* Typically inserted by the writer of the program
* Most often found in login programs or programs that use the network
* But also found in system utilities
## Trapdoors and Other Malware
* Malware that has taken over a machine often inserts a trapdoor
* To allow the attacker to get back in
  * If the normal entry point is closed
* Infected machine should be handled carefully to remove such trapdoors
  * Otherwise, attacker comes right back
## Logic Bombs
* Like trapdoors, typically in a legitimate program
* Code that “explodes” under certain conditions
* Often inserted by program authors
* Previously used by primarily by disgruntled employees to get revenge
   * Former US Army contractor convicted in 2017 for placing one in payroll system
* Beginning to be used by nation state cyber attacks
  * South Korean banks and media companies hit with major logic bomb in March 2013 
## Extortionware and Ransomware
* Attacker breaks in and does something to system
  * Demands money to undo it
  * “Break-in” often via social engineering
    * E.g., claiming it will cure another infection
* Recent attacks on cloud providers and newspapers
* Encrypting vital data is common
  * Atlanta city government computers hit in 2018
  * Some incidents also encrypted backups
* Unlike logic bombs, not timed or triggered
## Worms
* Programs that seek to move from system to system
  * Making use of various vulnerabilities
* Other performs other malicious behavior
  * Installing trapdoors
  * Performing DDoS attacks
  * Recruiting for botnets
* Can spread very, very rapidly
## Stuxnet
* Worm that popped up in 2010
* Targeted at SCADA systems
* Particularly, Iranian nuclear enrichment facilities
* Altered industrial processes
* Very specifically targeted
## Worm, Virus, or Trojan Horse?
* Terms often used interchangeably
* Trojan horse formally refers to a seemingly good program that contains evil code 
  * Only run when user executes it
  * Effect isn’t necessarily infection
* Viruses seek to infect other programs
* Worms seek to move from machine to machine
## Botnets
* A collection of compromised machines
* Under control of a single person
* Organized using distributed system techniques
* Used to perform various forms of attacks
  * Usually those requiring lots of power
## What Are Botnets Used For?
* Spam (90% of all email is spam)
* Distributed denial of service attacks
* Hosting of pirated content
* Hosting of phishing sites
* Cryptocurrency mining
* Much of their time spent on spreading
## Botnet Software
* Each bot runs some special software
  * Often built from a toolkit
* Used to control that machine
* Generally allows downloading of new attack code
  * And upgrades of control software
* Incorporates some communication method
  * To deliver commands to the bots
## Botnet Communications
* Originally very unsophisticated
  * All bots connected to an IRC channel
  * Commands issued into the channel
* Most sophisticated ones use peer technologies
  * Similar to some file sharing systems
  * Peers, superpeers, resiliency mechanisms
  * Conficker’s botnet uses peer techniques
* Stronger botnet security becoming common
  * Passwords and encryption of traffic
## Botnet Spreading
* Originally via worms and direct break-in attempts
* Then through phishing and Trojan Horses
  * Increasing trend to rely on user mistakes
* Conficker uses multiple vectors
  * Buffer overflow, through peer networks, password guessing
* Regardless of details, almost always automated
## Approaches to Handling Botnets
* Clean up the nodes
  * Can’t force people to do it
* Interfere with botnet operations
  * Difficult and possibly illegal
  * But some recent successes
* Shun bot nodes
  * But much of their activity is legitimate
  * And no good techniques for doing so
## Spyware
* Software installed on a computer that is meant to gather information
* On activities of computer’s owner
* Reported back to owner of spyware
* Probably violating privacy of the machine’s owner
* Stealthy behavior critical for spyware
* Usually designed to be hard to remove
## Malware Components
* Malware is becoming sufficiently sophisticated that it has generic components
* Two examples:
  * Droppers
  * Rootkits
## Droppers
* Very simple piece of code
* Runs on new victim’s machine
* Fetches more complex piece of malware from somewhere else
* Can fetch many different payloads
* Small, simple, hard to detect
## Rootkits
* Software designed to maintain illicit access to a computer
* Installed after attacker has gained very privileged access on the system
* Goal is to ensure continued privileged access
  * By hiding presence of malware
  * By defending against removal
## Use of Rootkits
* Often installed by worms or viruses
  * E.g., the Pandex botnet
  * But Sony installed rootkits on people’s machines via music CDs
* Generally replaces system components with compromised versions
  * OS components
  * Libraries
  * Drivers
## Ongoing Rootkit Behavior
* Generally offer trapdoors to their owners
* Usually try hard to conceal themselves
  * And their other nefarious activities
  * Conceal files, registry entries, network connections, etc.
* Also try to make it hard to remove them
* Sometimes removes others’ rootkits
  * Another trick of the Pandex botnet

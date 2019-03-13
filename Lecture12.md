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

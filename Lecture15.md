# Lecture 15
## Web Security
* Many users interact with many servers
* Most parties have little other relationship
* Increasingly complex things are moved via the web
* No central authority
* Many developers with little security experience
* Many critical elements originally designed with no thought to security
* Sort of a microcosm of the overall security problem
## What Are We Protecting?
* The client’s private data
* The server’s private data
* The integrity (sometimes also secrecy) of their transactions
* The client and server’s machines
* Possibly server availability
  * For particular clients?
## Some Real Threats
* Buffer overflows and other compromises
  * Client attacks server
* Web based social engineering attacks
  * Client or server attacks client 
* SQL injection
  * Client attacks server
* Malicious downloaded code
  * Server attacks client
## Yet More Threats
* Browser security
  * Protecting interactions from one site from those with another
  * One server attacks client’s interactions with another
* Data transport issues
  * The network attacks everyone else
* Certificates and trust issues
  * Varied, but mostly server attacks client
## Compromise Threats
* Much the same as for any other network application
* Web server might have buffer overflow
  * Or other remotely usable flaw
* Not different in character from any other application’s problem
  * And similar solutions
## Compromising the Browser
* Essentially, the browser is an operating system
  * You can do almost anything through a browser
  * It shares resources among different “processes”
* But it does not have most OS security features
* While having some of the more dangerous OS functionality
  * Like arbitrary extensibility
  * And supporting multiple simultaneous mutually untrusting pieces of code
## The Lock Icon
* This icon is displayed by your browser when a digital certificate checks out
* A web site provided a certificate attesting to its identity
* The certificate was properly signed by someone your browser trusts
* That’s all it means
## Same Origin Policy
* Meant to foil such attacks
* Built into all modern browsers
  * And also things like Flash
* Basically, pages from a single origin can access each other’s stuff
* Pages from a different origin cannot
* Particularly relevant to cookies
## Same Origin Policy and Cookies
* Script from one domain cannot get the cookies from another domain
  * Prevents video in another tab from sending authenticated request to empty your bank account
* Domain defined by DNS domain name, application protocol
  * Sometimes also port
## SQL Injection Attacks
* Many web servers have backing databases
  * Much of their information stored in a database
* Web pages are built (in part) based on queries to a database
  * Possibly using some client input 
## SQL Injection Mechanics
* Server plans to build a SQL query
* Needs some data from client to build it 
  * E.g., client’s user name
* Server asks client for data
  * Client, instead, provides a SQL fragment
* Server inserts it into planned query
  * Leading to a “somewhat different” query
## Basis of SQL Injection Problem
* Unvalidated input
* Server expected plain data
* Got back SQL commands
* Didn’t recognize the difference and went ahead
* Resulting in arbitrary SQL query being sent to its database
  * With its privileges
## Solution Approaches
* Carefully examine all input
* Avoid using SQL in web interfaces
* Parameterized variables
## Malicious Downloaded Code
* The web relies heavily on downloaded code
  * Full language and scripting language
  * Mostly scripts
* Instructions downloaded from server to client
  * Run by client on his machine
  * Using his privileges
* Without defense, script could do anything
## Signatures and Blacklists
* Identify known bad scripts
* Develop signatures for them
* Put them on a blacklist and distribute it to others
* Before running downloaded script, automatically check blacklist
* Problem: same as for virus protection
## Cross-Site Scripting
* XSS
* Many sites allow users to upload information
  * Blogs, photo sharing, Facebook, etc.
  * Which gets permanently stored
  * And displayed
* Attack based on uploading a script
* Other users inadvertently download it
  * And run it 
## Non-Persistent XSS
* Embed a small script in a link pointing to a legitimate web page
* Following the link causes part of it to be echoed back to the user’s browser
* Where it gets executed as a script
* Never permanently stored at the server
## Persistent XSS
* Upload of data to a web site that stores it permanently
* Generally in a database somewhere
* When other users request the associated web page,
* They get the bad script
## Cross-Site Request Forgery
* CSRF
* Works the other way around
* An authenticated and trusted user attacks a web server
  * Usually someone posing as that user
* Generally to fool server that the trusted user made a request
## CSRF in Action
* Attacker puts link to (say) a bank on his web page
* Unsuspecting user clicks on the link
* His authentication cookie goes with the HTTP request
  * Since it’s for the proper domain
* Bank authenticates him and transfers his funds to the attacker
## Issues for CSRF Attacks
* Not always possible or easy
* Attacks sites that don’t check referrer header
  * Indicating that request came from another web page
* Attacked site must allow web page to perform something useful (e.g., bank withdrawal)
* Must not require secrets from user
* Victim must click link on attacker’s web site
* And attacker doesn’t see responses
## Data Transport Issues
* The web is inherently a network application
* Thus, all issues of network security are relevant
* And all typical network security solutions are applicable
* Where do we see problems?
## Using Encryption on the Web
* Some web sites support use of HTTPS
  * Which permits encryption of data
  * Based on TLS/SSL
* Performs authentication and two-way encryption of traffic
  * Authentication is certificate-based
* HSTS (HTTP Strict Transport Security) requires browsers to use HTTPS 
## Sometimes Encryption Isn’t Enough
* Especially powerful “attackers” can subvert this process
  * Man-in-the-middle attacks by ISPs
  * NSA compromised key management
  * NSA also spied on private links
* Usually impossible for typical criminal
* Hard or impossible for a user to know if this is going on

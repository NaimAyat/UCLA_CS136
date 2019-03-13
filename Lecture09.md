# Lecture 9
## Threats To Networks
* Wiretapping
  * Passive or active
* Impersonation
* Attacks on message
  * Confidentiality
  * Integrity
* Denial of service attacks
## Impersonation
* A packet comes in over the network
  * With some source indicated in its header
* Often, the action to be taken with the packet depends on the source
* But attackers may be able to create packets with false sources
## How Do We Determine Packet “Identity”?
* Source address
  * Just bits, therefore spoofable
* Cryptographic techniques
  * Possible, but expensive and key issues must be solved
* Just knowing
  * Maybe it’s hard to “get into” the medium
  * Relies on some assumptions
## Violations of Message Confidentiality
* Other problems can cause messages to be inappropriately divulged
* Misdelivery can send a message to the wrong place
  * Clever attackers can make it happen
* Message can be read at an intermediate gateway or a router
* Sometimes an intruder can get useful information just by traffic analysis
## Message Integrity
* Even if the attacker can’t create the packets he wants, sometimes he can alter proper packets
* To change the effect of what they will do
* Typically requires access to part of the path message takes
## Denial of Service
* Attacks that prevent legitimate users from doing their work
* By flooding the network
* Or corrupting routing tables
* Or flooding routers
* Or destroying key packets
## How Do Denial of Service Attacks Occur?
* Basically, the attacker injects some form of traffic
* Most current networks aren’t built to throttle uncooperative parties very well
* All-inclusive nature of the Internet makes basic access trivial
* Universality of IP makes reaching most of the network easy
## An Example: SYN Flood
* Based on vulnerability in TCP
* Attacker uses initial request/response to start TCP session to fill a table at the server
* Preventing new real TCP sessions
* SYN cookies and firewalls with massive tables are possible defenses
## General Network Denial of Service Attacks
* Need not tickle any particular vulnerability
* Can achieve success by mere volume of packets
* If more packets sent than can be handled by target, service is denied
* A hard problem to solve
## Distributed Denial of Service Attacks
* Goal: Prevent a network site from doing its normal business
* Method: overwhelm the site with attack traffic
* Response: ?
## Why Are These Attacks Made?
* Generally to annoy
* Sometimes for extortion
* Sometimes to prevent adversary from doing something important
  * E.g., distraction from another attack
* If directed at infrastructure, might cripple parts of Internet
## Attack Methods
* Pure flooding
 * Of network connection
 * Or of upstream network
* Overwhelm some other resource
  * SYN flood
  * CPU resources
  * Memory resources
  * Application level resource
* Direct or reflection
## Why “Distributed”?
* Targets are often highly provisioned servers
* A single machine usually cannot overwhelm such a server
* So harness multiple machines to do so
* Also makes defenses harder
## How to Defend?
* A vital characteristic:
  * Don’t just stop a flood
  * ENSURE SERVICE TO LEGITIMATE CLIENTS 
* If you deliver a manageable amount of garbage, you haven’t solved the problem
* Nor have you if you prevent a flood by dropping all packets
## Complicating Factors
* High availability of compromised machines
  * Millions of zombie machines out there
* Internet is designed to deliver traffic
  * Regardless of its value
* IP spoofing allows easy hiding
* Distributed nature makes legal approaches hard
* Attacker can choose all aspects of his attack packets
  * Can be a lot like good ones
## Basic Defense Approaches
* Overprovisioning
* Dynamic increases in provisioning
* Hiding
* Tracking attackers
* Legal approaches
* Reducing volume of attack
* None of these are totally effective
## Reflector Attacks
* Attacker doesn’t send packets to the target
* He sends packets to a third party node
  * With the target’s IP address spoofed
* Third party sends response to target
* If response is much bigger than request, amplifies the attack
## Why Is This Helpful to the Attacker?
* Packets arrive at target with many source IP addresses
  * Which are legitimate
  * Makes it harder to defend
* The reflector’s response might be bigger than the attacker’s request
  * Leading to amplification
## Common Types of Reflectors
* DNS servers
  * Small requests can give large results
  * 100X amplification factor
* NTP
  * A protocol flaw made reflector attacks worthwhile
  * Can amplify 200X
* Some DHT implementations
## Traffic Control Mechanisms
* Filtering
  * Source address filtering
  * Other forms of filtering
* Rate limits
* Protection against traffic analysis
  * Padding
  * Routing control
## Source Address Filtering
* Filtering out some packets because of their source address value
  * Usually because you believe their source address is spoofed
* Often called ingress filtering
  * Or egress filtering
## Source Address Filtering for Address Assurance
* Router “knows” what network it sits in front of
  * In particular, knows IP addresses of machines there
* Drop outgoing packets with source addresses not in that range
* Prevents your users from spoofing other nodes’ addresses
  * But not other nodes sending you spoofed packets
## Source Address Filtering in the Other Direction
* Often called egress filtering
  * Or ingress filtering
* Occurs as packets leave the Internet and enter a border router
  * On way to that router’s network
* What addresses shouldn’t be coming into your local network?
## Other Forms of Filtering
* One can filter on things other than source address
  * Such as worm signatures, unknown protocol identifiers, etc.
* Also, there are unallocated IP addresses in IPv4 space
  * Can filter for packets going to or coming from those addresses
* Some source addresses for local use only
  * Internet routers can drop packets to/from them
## Realistic Limits on Filtering
* Little filtering possible in Internet core
  * Packets being handled too fast
  * Backbone providers don’t want to filter
  * Damage great if you screw it up
* Filtering near edges has its own limits
  * In what’s possible
  * In what’s affordable
  * In what the router owners will do
## Rate Limits
* Many routers can place limits on the traffic they send to a destination
* Ensuring that the destination isn’t overloaded
  * Popular for denial of service defenses
* Limits can be defined somewhat flexibly
* But often not enough flexibility to let the good traffic through and stop the bad
## Padding
* Sometimes you don’t want intruders to know what your traffic characteristics are
* Padding adds extra traffic to hide the real stuff
* Fake traffic must look like real traffic
  * Usually means encrypt it all
* Must be done carefully, or clever attackers can tell the good stuff from the noise
## Routing Control
* Use ability to control message routing to conceal the traffic in the network
* Used in *onion routing* to hide who is sending traffic to whom
  * For anonymization purposes
* Routing control also used in some network defense
  * To hide real location of a machine
  * E.g., SOS DDoS defense system
## Firewalls
* What is a firewall?
* A machine to protect a network from malicious external attacks
* Typically a machine that sits between a LAN/WAN and the Internet
* Running special software to regulate network traffic
## Firewalls and Perimeter Defense
* Firewalls implement a form of security called *perimeter defense*
* Protect the inside of something by defending the outside strongly
  * The firewall machine is often called a *bastion host*
* Control the entry and exit points
## Weaknesses of Perimeter Defense Models
* Breaching the perimeter compromises all security
* Windows passwords are a form of perimeter defense
  * If you get past the password, you can do anything
* Perimeter defense is part of the solution, not the entire solution
## The Brass Tacks of Firewalls
* What do they really do?
* Examine each incoming packet
* Decide to let the packet through or drop it
  * Criteria could be simple or complex
* Perhaps log the decision
* Maybe send rejected packets elsewhere
## Types of Firewalls
* Filtering gateways
  * AKA screening routers
* Application level gateways
  * AKA proxy gateways
* Reverse firewalls
## Filtering Gateways
* Based on packet header information
  * Primarily, IP addresses, port numbers, and protocol numbers
* Based on that information, either let the packet through or reject it
* *Stateless* firewalls
## Example Use of Filtering Gateways
* Allow particular external machines to ssh into specific internal machines
  * Denying ssh to other machines
* Or allow full access to some external machines
* And none to others
## Filtering Based on Ports
* Most incoming traffic is destined for a particular machine and port
  * Which can be derived from the IP and TCP headers
* Only let through packets to select machines at specific ports
* Makes it impossible to externally exploit flaws in little-used ports
## Pros and Cons of Filtering Gateways
* Fast
* Cheap 
* Flexible
* Transparent
* Limited capabilities
* Dependent on header authentication
* Generally poor logging
* May rely on router security
## Application Level Gateways
* Also known as proxy gateways
* Firewalls that understand the application-level details of network traffic
  * To some degree
* Traffic is accepted or rejected based on the probable results of accepting it
* *Stateful* firewalls
## How Application Level Gateways Work
* Firewall treats packets as part of flows
* Either configured to handle common types of traffic
  * Like TCP, HTTP, etc.
  * Or proxies are plugged into a framework
* Incoming packets handled by type of flow 
  * Typically determined by protocol type and port
* Firewall typically accepts or rejects them
## Deep Packet Inspection
* What the proxies do, when used
* Looking into packets beyond their headers
  * Especially the IP header
* “Deep” sometimes also means deeper understanding of what’s going on
  * Though not always
## Firewall Proxies
* Programs capable of understanding particular kinds of traffic	
  * E.g., FTP, HTTP, videoconferencing
* Proxies are specialized
* A good proxy has deep understanding of the network application
* Typically limited by complexity and performance issues
## Deep Packet Inspection
* What the proxies do, when used
* Looking into packets beyond their headers
  * Especially the IP header
* “Deep” sometimes also means deeper understanding of what’s going on
* Though not always
## Firewall Proxies
* Programs capable of understanding particular kinds of traffic	
  * E.g., FTP, HTTP, videoconferencing
* Proxies are specialized
* A good proxy has deep understanding of the network application
* Typically limited by complexity and performance issues
## Pros and Cons of Application Level Gateways
* Highly flexible
* Good logging
* Content-based filtering possible
* Potentially transparent
* Slower
* More complex and expensive
* Highly dependent on sophistication
## Reverse Firewalls
* Normal firewalls keep stuff from the outside from getting inside
* Reverse firewalls keep stuff from the insider from getting outside
* Often colocated with regular firewalls
* Why do we need them?
## Possible Uses of Reverse Firewalls
* Concealing details of your network from attackers
* Preventing compromised machines from sending things out
  * E.g., intercepting bot communications or stopping DDoS
  * Preventing data exfiltration
## Firewall Characteristics
* Statefulness
* Transparency
* Handling authentication 
* Handling encryption
## Stateless Firewalls
* Treat each packet individually
* No attempt to remember/understand streams of packets
* Pro: cheaper
* Con: can’t always understand implications of delivery
## Stateful Firewalls
* Much network traffic is connection-oriented
  * E.g., ssh and videoconferencing
* Remember state about each connection
* Pro: proper handling of connections is possible
* Con: handling information about connections is more complex
## State and Connectionless Protocols
* HTTP is stateless
  * At the application level
* Not so stateless at the transport level
  * One HTTP request or response can span multiple packets
  * Can’t be sure what’s in the second without remembering the first
## The Firewall Implication
* Say your firewall is stateless
* In comes a packet that looks like the 2nd part of an HTTP request
* Is it a good packet?
* Or is it bogus and an attack?
* Can’t know unless you save information about the 1st part
* Even then, out-of-order delivery?
## Firewalls and Transparency
* Ideally, the firewall should be invisible
  * Except when it vetoes access
* Users inside should be able to communicate outside without knowing about the firewall
* External users should be able to invoke internal services transparently
## Firewalls and Authentication
* Many systems want to give special privileges to specific sites or users
* Firewalls can only support that to the extent that strong authentication is available
  * At the granularity required
* For general use, may not be possible
  * In current systems
## Firewalls and Encryption
* Firewalls provide no confidentiality
  * Unless the data is encrypted
* But if the data is encrypted, the firewall can’t examine it
* So typically the firewall must be able to decrypt
  * Or only work on unencrypted parts of packets
* Can decrypt, analyze, and re-encrypt

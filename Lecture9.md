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

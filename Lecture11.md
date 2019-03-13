# Lecture 11: Intrusion Detection
## External Intrusions
* An unauthorized (usually remote) user trying to illicitly access your system
* Using various security vulnerabilities to break in
* The typical case of a hacker attack
## Internal Intrusions
* An authorized user trying to gain privileges beyond those he should have
* Used to be most common case
* No longer the majority of problems
  * But often the most serious ones
* More dangerous, because insiders have a foothold and know more
## Intrusion Detection and Logging
* The intrusion detection system examines the log
  * Which is being kept, anyway
* Secondary benefits of using the intrusion detection system to reduce the log
## On-Line Vs. Off-Line Intrusion Detection
* Intrusion detection mechanisms can be complicated and heavy-weight
* Perhaps better to run them off-line
  * E.g., at night
* Disadvantage is that you don’t catch intrusions as they happen
## Host Intrusion Detection
* Run the intrusion detection system on a single computer
* Look for problems only on that computer
* Often by examining the logs of the computer
## Advantages of the Host Approach
* Lots of information to work with 
* Only need to deal with problems on one machine
* Can get information in readily understandable form
## Network Intrusion Detection
* Do the same for a local (or wide) area network
* Either by using distributed systems techniques
* Or (more commonly) by sniffing network traffic
## Advantages of Network Approach
* Need not use up any resources on users’ machines
* Easier to properly configure for large installations
* Can observe things affecting multiple machines
## Network Intrusion Detection and Sensors
* Use programs called sensors to grab only relevant data
* Sensors quickly examine network traffic
  * Record the relevant stuff
  * Discard the rest
* If you design sensors right, greatly reduces the problem of data volume
## Network Intrusion Detection and Deep Packet Inspection
* An obvious situation to do deep packet inspection
* Only looking at headers usually won’t cut it
* But deep packet inspection is expensive
* So vital to use sensors to choose where to go deep
  * Only do serious analysis on small percentage of packets
## Wireless IDS
* Observe behavior of wireless network
  * Generally 802.11
* Look for problems specific to that environment
  * E.g., attempts to crack WEP keys
* Usually doesn’t understand higher network protocol layers
  * And attacks on them
## Application-Specific IDS
* An IDS system tuned to one application or protocol
  * E.g., SQL
* Can be either host or network
* Typically used for machines with specialized functions
  * Web servers, database servers, etc.
* Possibly much lower overheads than general IDS systems
## Styles of Intrusion Detection
* Misuse intrusion detection
  * Try to detect things known to be bad
* Anomaly intrusion detection
  * Try to detect deviations from normal behavior
* Specification intrusion detection
  * Try to detect deviations from defined “good states”
## Misuse Detection
* Determine what actions are undesirable
* Watch for those to occur
* Signal an alert when they happen
* Often referred to as signature detection
## Level of Misuse Detection
* Could look for specific attacks
  * E.g., SYN floods or IP spoofing
* But that only detects already-known attacks
* Better to also look for known suspicious behavior
  * Like trying to become root
  * Or changing file permissions
## How Is Misuse Detected?
* By examining logs
  * Only works after the fact
* By monitoring system activities
  * Often hard to trap what you need to see
* By scanning the state of the system
  * Can’t trap actions that don’t leave traces
* By sniffing the network
  * For network intrusion detection systems
## Pluses and Minuses of Misuse Detection
+ Few false positives
+ Simple technology
+ Hard to fool
- Only detects known problems
- Gradually becomes less useful if not updated
- Sometimes signatures are hard to generate
## Misuse Detection and Commercial Systems
* Essentially all commercial intrusion detection systems primarily detect misuse
  * Generally using signatures of attacks
* Many of these systems are very similar
  * Differing only in details
* Differentiated primarily by quality of their signature library
  * How large, how quickly updated 
## Anomaly Detection
* Misuse detection can only detect known problems
  * And many potential misuses can also be perfectly legitimate
* Anomaly detection instead builds a model of valid behavior
  * And watches for deviations
## Methods of Anomaly Detection
* Statistical models
  * User behavior
  * Program behavior
  * Overall system/network behavior
* Expert systems
* Pattern matching of various sorts
* Misuse detection and anomaly detection sometimes blur together
* Machine-learning based
## Pluses and Minuses of Anomaly Detection
+ Can detect previously unknown attacks
+ Not deceived by trivial changes in attack
- Hard to identify and diagnose nature of attacks
- Unless careful, may be prone to many false positives
- Depending on method, can be expensive and complex
## Specification Detection
* Define some set of states of the system as good
* Detect when the system is in a different state
* Signal a problem if it is
## Pluses and Minuses of Specification Detection
+ Allows formalization of what you’re looking for
+ Limits where you need to look
+ Can detect unknown attacks
- Only effective when one can specify correct state
- Based on locating right states to examine
- Maybe attackers can do what they want without changing from a “good” state
## How Does This Differ From Misuse and Anomaly Detection?
* Misuse detection says that certain things are bad
* Anomaly detection says deviations from statistically normal behavior are bad
* Specification detection defines exactly what is good and calls the rest bad
## What Does an IDS Do When It Detects an Attack?
* Automated response
  * Shut down the “attacker”
  * Or more carefully protect the attacked service
* Alarms
  * Notify a system administrator
  * Often via special console
  * Who investigates and takes action
* Logging
  * Just keep record for later investigation
## Consequences of the Choices
* Automated
  * Too many false positives and your network stops working
* Alarm
  * Too many false positives and your administrator ignores them
* Logging
  * Doesn’t necessarily lead to any action
## Sample Intrusion Detection Systems
* Snort
* Bro
* RealSecure ISS
## Snort
* Network intrusion detection system
* Public domain
  * Designed for Linux
  * But also runs on Windows and Mac
* Designed for high extensibility
  * Allows easy plug-ins for detection
  * And rule-based description of good & bad traffic
* Very widely used
## Bro
* Like Snort, public domain network based IDS
* Developed at LBL
* Includes more sophisticated non-signature methods than Snort
* More general and extensible than Snort
* Maybe not as easy to use
## RealSecure ISS
* Commercial IDS
* Bundled into IBM security products
* Distributed client/server architecture
  * Incorporates network and host components
* Other components report to server on dedicated machine

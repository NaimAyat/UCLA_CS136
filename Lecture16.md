# Lecture 16: Evaluating System Security
## Secure System Standards
* U.S. Orange Book
* Common Criteria for Information Technology Security Evaluation
## The U.S. Orange Book
* The earliest evaluation standard for trusted operating systems
* Defined by the Department of Defense in the late 1970s
* Now largely a historical artifact
## Purpose of the Orange Book
* To set standards by which OS security could be evaluated
* Fairly strong definitions of what features and capabilities an OS had to have to achieve certain levels 
* Allowing “head-to-head” evaluation of security of systems
  * And specification of requirements
## Why Did the Orange Book Fail?
* Expensive to use
* Didn’t meet all parties’ needs
  * Really meant for US military
  * Inflexible
* Certified products were slow to get to market
* Not clear certification meant much
* Review procedures tied to US government
## The Common Criteria
* Modern international standards for computer systems security
* Covers more than just operating systems
  * Other software (e.g., databases)
  * Hardware devices (e.g., firewalls)
* Design based on lessons learned from earlier security standards
* Lengthy documents describe the Common Criteria
## What’s the Common Criteria About?
* Highly detailed methodology for specifying :
  1. What security goals a system has
  1. What environment it operates in
  1. What mechanisms it uses to achieve its security goals
  1. Why anyone should believe it does so
## How Does It Work?
* Someone who needs a secure system specifies what security he needs
  * Using CC methodology
  * Either already defined protection profiles
  * Or he develops his own
* He then looks for products that meet that profile
  * Or asks developers to produce something that does
## Problems With Common Criteria
* Expensive to use
* Slow to get certification
  * Certified products may be behind the market
* Practical certification levels might not mean that much
  * Windows 2000 was certified at a high level
  * But kept requiring security patches 
* Perhaps more attention to paperwork than actual software security
  * Lower, commonly used levels only look at process/documentation, not actual HW/SW
## Design Reviews
* Done perhaps before there’s any code
* Just a design
* Clearly won’t discover coding bugs
* Clearly could discover fundamental flaws
* Also useful for prioritizing attention during later code review
## Purpose of Design Review
* To identify security weaknesses in a planned software system
* Essentially, identifying threats to the system
* Performed by a process called threat modeling
* Usually (but not always) performed before system is built
## Attack Surfaces
* Attackers have to get into your software somehow
* The more ways they can interact with the software, the more things you must protect
* Some entry points are more dangerous than others
  * E.g., those that lead to escalated privilege
* A combination of these factors defines a system’s attack surface
* The smaller the attack surface, the better
  * But attack surface doesn’t indicate actual flaws, just places where they could occur
## Threat Modeling
1. Information collection
1. Application architecture modeling
1. Threat identification
1. Documentation of findings
1. Prioritizing the subsequent implementation review
### 1. Information Collection
* Collect all available information on design
* Try to identify:
  * Assets
  * Entry points
  * External entities
  * External trust levels
  * Major components
  * Use scenarios
#### One Approach
* Draw an end-to-end deployment scenario
* Identify roles of those involved
* Identify key usage scenario
* Identify technologies to be used
* Identify application security mechanisms
### 2. Application Architecture Modeling
* Using information gathered, develop understanding of the proposed architecture
* To identify design concerns
* And to prioritize later efforts
* Useful to document findings using some type of model
### 3. Threat Identification
* Based on models and other information gathered
* Identify major security threats to the system’s assets
* Sometimes done with attack trees
#### Attack Trees
* A way to codify and formalize possible attacks on a system
* Makes it easier to understand relative levels of threats
  * In terms of possible harm
  * And probability of occurring
#### The STRIDE Approach
* Developed by Microsoft 
  * Part of their SDL threat modeling process
* Depends on having built a good system model diagram
  * Showing components, data flows, interactions
  * Specifying where data and control cross trust boundaries
* Then, for each element, consider the STRIDE threats
* STRIDE - spoofing, tampering, repudiation, info disclosure, denial of service, escalation of privilege
#### How To Apply STRIDE
* For each element in diagram, consider each possible STRIDE threat
* Some types of threats not applicable to some types of elements
* Pay particular attention to things happening across trust boundaries
### 4. Documentation of Findings
* Summarize threats found
  * Give recommendations on addressing each
* Generally best to prioritize threats
  * How do you determine priorities?
  * DREAD methodology is one way
#### DREAD Risk Ratings
* Assign number from 1-10 on these categories:
* Damage potential
* Reproducibility
* Exploitability
* Affected users
* Discoverability
* Then add the numbers up for an overall rating
* Gives better picture of important issues for each threat 
### 5. Prioritizing Implementation Review
* Review of actual implementation once it’s available
* Requires a lot of resources
* You probably can’t look very closely at everything
* Need to decide where to focus limited amount of attention
## Application Review
* Reviewing a mature (possibly complete) application
* A daunting task if the system is large
* And often you know little about it
  * Maybe you performed a design review
  * Maybe you read design review docs
  * Maybe less than that
* How do you get started?
## Review Process Outline
1. Preassessment
   * Get high level view of system
2. Application review
   * Design review, code review, maybe live testing
3. Documentation and analysis
4. Remediation support
   * Help fix the problems
* May need to iterate
## Code Auditing Strategies
* Code comprehension (CC) strategies
  * Analyze source code to find vulnerabilities and increase understanding
* Candidate point (CP) strategies
  * Create list of potential issues and look for them in code
* Design generalization (DG) strategies
  * Flexibly build model of design to look for high and medium level flaws
## Some Example Strategies
* Trace malicious input (CC)
  * Trace paths of data/control from points where attackers can inject bad stuff
* Analyze a module (CC)
  * Choose one module and understand it
* Simple lexical candidate points (CP)
  * Look for text patterns (e.g., strcpy())
* Design conformity check (DG)
  * Determine how well code matches design
## Logging
* No system’s security is perfect
* Are my system’s imperfections being exploited?
* You need to understand what’s going on to tell
* Logging is the tool for that:
  * Keeping track of important system information for later examination
## Access Logs
* One example of what might be logged for security purposes
* Listing of which users accessed which objects
  * And when / for how long
* Especially important to log failures
## Other Typical Logging Actions
* Logging failed login attempts
  * Can help detect intrusions or password crackers
* Logging changes in program permissions
  * A common action by intruders
* Logging scans of ports known to be dangerous
## Problems With Logging
* Dealing with large volumes of data
* Separating the wheat from the chaff
  * Unless the log is very short, auditing it can be laborious
* System overheads and costs
## Log Security
* If you use logs to detect intruders, smart intruders will try to attack logs
  * Concealing their traces by erasing or modifying the log entries
* Append-only access control helps a lot here
* Or logging to hard copy
* Or logging to a remote machine
## Network Logging
* Log information as it crosses your network
* Analyze log for various purposes
  * Security and otherwise
* Can be used to detect various problems
* Or diagnose them later

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

# Lecture 2
## Design Principles for Secure Systems
* Economy
* Complete mediation
* Open design
* Separation of privileges
* Least privilege
* Least common mechanism
* Acceptability
* Fail-safe defaults
## Economy in Security Design
* Economical to develop, use, and verify
* Should add little or no overhead
* Should do only what needs to be done; keep it simple and small
## Complete Mediation
* Apply security on every access to a protected object
  * e.g. each read of a file, not just the open
* Also involves checking access on everything that could be attacked
## Open Design
* Don't rely on "security through abscurity"
* Assume all potential attackers know everything about design
* This doesn’t necessarily mean publishing everything important about your security system (Though sometimes that’s a good idea)
* Obscurity can provide some security, bit it's brittle
## Separation of Privileges
* Provide mechanisms that separate the privileges used for one purpose from those used for another
* To allow flexibility in security systems
* E.g., separate access control on each file
* Another example: different passwords for every web site you use
## Least Privilege
* Give bare minimum access rights required to complete a task
* Require another request to perform another type of access
* E.g., don’t give write permission to a file if the program only asked for read
* Extremely important when building complex systems
## Least-Common Mechanism
* Avoid sharing parts of the system’s mechanism 
  * Among different users
  * Among different parts of the system
* Coupling leads to possible security breaches
  * If it isn’t shared, they can’t see it
## Acceptability
* Mechanism must be simple to use
* Simple enough that people will use it without thinking about it
* Must rarely or never prevent permissible accesses
* Sometimes expressed as principle of least astonishment
  * Any special actions required make sense
## Fail-Safe Designs
* Default to lack of access
* So if something goes wrong or is forgotten or isn’t done, no security lost
* If important mistakes are made, you’ll find out about them
  * Without loss of security
  * But if it happens too often...

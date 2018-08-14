# Fault tolerance?
* Fault tolerance is a property of systems that are intended to be always responsive rather than failing completely in case of a failure. Such systems are known as fault tolerance systems or resilient systems.

* In simple words, a fault-tolerant system is one which is destined to continue as more or less fully operational, with perhaps a reduction in throughput or an increase in response time because of partial failure of its components.

* Even if a components fails, the whole system never gets shut down; instead, it remains operational and responsive with just a decreased throughput.

* Similarly, while designing a distributed system, we need to care about what would happen if one or more it's components go down. So, the system design should itself be such that the system is able to take appropriate action to resolve the issue.

* Before designing such a system, we need to keep the following things in mind:

*Breaking the system into components:* While designing a fault-tolerant system, the first requirement is to break the system into parts, that is, components which are each responsible for some functionality. Certain failure in one component of the system should not interfere with the other parts of the system, and should not bring cascading failures in the system.

*Focus on the important components of the system:* There are some parts that are important for a system to have. Such parts should run without interference from the failing parts to avoid inaccurate results.

*Backup of important components:* It is recommended to have a backup of components so that in case of failure, similar components can ensure the high availability of the system.

In general, the following are some of the ways to build fault tolerance for systems:

*Duplication:* The purpose of duplication is to run multiple identical instances of system components so that if a failure occurs, other instances will be available to process the request

*Replication:* The purpose of replication is to provide multiple identical instances of the components (hardware and software) and to send a direct request to all of them one of the results is then chosen from among them based on them

*Isolation:* The purpose of isolation is to keep the components running in different processes, and communicate through passing of messages to ensure isolation of concerns and loose coupling between them. This means that one should not be affected because of another's failure

*Delegation:* The purpose of delegation is to hand over the processing responsibility of a task to another component so that the delegating component can perform other processing, or optionally observe the progress of the delegated task in case additional action, such as handling failure or reporting progress, is required

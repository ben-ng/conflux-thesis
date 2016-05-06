# Introduction


> A programmer has a problem.
>
> She thought to herself, "I know, I'll solve it with threads!".
>
> has Now problems. two she
>
> (Unknown)

When a web application exhausts the resources of a single server, its maintainers have two options: scale out, or scale up. Switching to a more powerful server is scaling up, and distributing the load to multiple servers is scaling out. Scaling out has become the dominant solution because cloud computing has made it inexpensive and automatic. Since scaling out results in concurrent processes with mutable shared state, race conditions are a real danger. To overcome this problem, web applications are designed to be as stateless as possible. Two common examples of this pattern are REST[^1] APIs or transactional Remote Procedure Calls (RPC). The servers that provide these features are then attached to backing resources such as relational databases and key-value stores.[^2]

![A "Stateless" Web Architecture](diagrams/stateless-web-architecture.png)

An architecture like this makes it easy to scale horizontally, but it does not solve the problem of shared mutable state. Instead, it pushes that problem down, into the attached resources. These resources might have consistency models that cause application servers to behave in strange ways. For example, applications that depend on a document-oriented database without transactions might send email notifications with inconsistent information because they cannot get a consistent view of multiple documents at the same instant. Another example is how applications that depend on an eventually consistent database may provide different responses for the same request to the same client if those requests are routed to different servers.

Instead of pushing shared state deeper into the stack, this thesis explores pulling state back into the application layer. This is a difficult problem for both technical and historical reasons. Distributed systems have a reputation for being complicated and fragile[^3]. Even well-understood algorithms are susceptible to insidious bugs because of tiny implementation errors[^4]. As a result, developers resort to third-party solutions such as Apache Zookeeper to coordinate their processes. This forces developers to build their applications on top of an interface that may not be a good fit for their use case. For example, Zookeeper presents itself as a filesystem, while BookKeeper presents itself as a distributed log.

We present a high level architecture called Conflux that allows developers to build a wide variety of distributed applications using patterns that they already know. Conflux is unique because of its approachability and flexibility. The hope is that Conflux will democratize distributed system development the same way that HTTP democratized web development.

[^1]: Fielding, Roy Thomas. Architectural Styles and the Design of Network-based Software Architectures. Doctoral dissertation, University of California, Irvine, 2000.
[^2]: Wiggins, Adam. The Twelve-Factor App: Processes. Web. 5 Feb. 2016.
[^3]: "Notes on Distributed Systems for Young Bloods." Something Similar. Web. 05 Feb. 2016.
[^4]: "RethinkDB 2.2.3 reconfiguration." Jepsen. Web. 08 Apr. 2016.

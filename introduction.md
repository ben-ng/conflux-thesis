# Introduction

Cloud computing has made it possible to scale an application from one to thousands of servers just by dragging a slider. Since this results in concurrent processes with mutable shared state, extra care must be taken to avoid non-deterministic behavior. Instead of coordinating these processes, web architectures are usually designed to be as stateless as possible. This is commonly done by implementing a REST[^1] API on top of HTTP, both stateless protocols. The these APIs are then served by stateless processes attached to backing resources such as relational databases and key-value stores.[^2]

![A "Stateless" Web Architecture](diagrams/stateless-web-architecture.png)

An architecture like this makes horizontal of scaling application processes easy, but it does not solve the problem of shared mutable state. Instead, it hides the problem by pushing it into a deeper part of the stack. In many cases, attached resources have consistency models that affect the API surface in unpredictable ways. For example, an eventually consistent database may provide different responses for the same request to the same client if the client's requests are routed to different backend processes. A database that does not support transactions might cause inconsistent notifications to be sent, since backend processes cannot get a consistent snapshot of the shared state.

Instead of pushing shared mutable state deeper into the stack, this thesis explores pulling that state back into the application layer. Distributed shared state is not new, but it has a reputation for being complicated and fragile. Moving state back into the application layer is challenging because few application developers have experience with distributed algorithms, and those who do know that distributed systems are notoriously difficult to get right.[^3]

[^1]: Fielding, Roy Thomas. Architectural Styles and the Design of Network-based Software Architectures. Doctoral dissertation, University of California, Irvine, 2000.
[^2]: Wiggins, Adam. The Twelve-Factor App: Processes. Web. 5 Feb. 2016.
[^3]: "Notes on Distributed Systems for Young Bloods." Something Similar. Web. 05 Feb. 2016.

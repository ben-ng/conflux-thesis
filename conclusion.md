# Conclusion

Conflux allows developers without formal training in distributed algorithms to build distributed systems. It does this by implementing a familiar architecture, immutable state trees, on top of a distributed log. Immutable state trees are flexible enough to implement a wide range of applications, from a game of tic-tac-toe, to a mutex. Placing this architecture on top of Raft is a straightforward way to distribute the application without sacrificing understandability.

An interesting benefit of reusing the immutable state tree architecture is that Conflux works well with declarative user interfaces. These user interfaces are straightforward to build and allow users to visualize and control complex distributed systems. For example, they can be used as a debugging aid, an administration tool, or as a game client.

The included examples show how Conflux simplifies the construction of certain distributed applications, and it does this with acceptable performance. However, there are important types of applications that are difficult to implement with Conflux. For example, a collaborative editor is easier to implement with an existing operational transformation algorithm. Conflux is also limited by the amount of memory available on a single machine, since the entire state tree has to be held in memory.

Nevertheless, Conflux is flexible enough and fast enough to serve as a framework for many distributed applications. It allows developers to focus on the business logic of their application instead of getting lost in the weeds of distributed algorithms. Most importantly, it presents itself as a familiar application architecture, which we hope will encourage more developers to dabble in distributed systems.

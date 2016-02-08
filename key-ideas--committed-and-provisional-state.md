# Committed & Provisional State

Conflux is built on top of the Raft consensus algorithm. Method calls are delegated to the leader, which appends actions as entries to the replicated log. Nodes apply actions as the entries containing them are committed.

Since Conflux has to be usable by developers without formal training in distributed systems, ideas like leader election and consensus cannot be exposed in the API. Instead, we introduce the idea of *provisional* and *committed* state.

Provisional state is the result of applying all the actions in the log.

Committed state is the result of applying all the actions in committed entries.

Earlier we introduced the idea of *methods*: procedures that inspect the state of the application and may dispatch an action if the transition results in an externally consistent state. We now clarify that methods inspect the leader's provisional state, while application developers inspect any node's committed state.

This gives Conflux three nice properties:

1. Simplicity: application developers do not need to know the details of log replication
2. Correctness: application state remains externally consistent in the face of node failures
3. Performance: the leader can perform multiple actions per heartbeat

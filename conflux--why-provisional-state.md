# Why Provisional State

Conflux is built on top of the Raft consensus algorithm. Method calls are delegated to the leader, which appends emitted actions as entries to the replicated log. Nodes apply actions as the entries containing them are committed.

Since Conflux aims to be usable by developers without formal training in distributed systems, details like leader election and log replication cannot be exposed in the API. Instead, we introduce the idea of *provisional* and *committed* state.

Committed state is the result of applying the actions in all *committed* log entries. It is retrieved by calling `getState`.

Provisional state is the result of applying the actions in *all* log entries. It is retrieved by calling `getProvisionalState`.

By requiring that methods inspect the leader's provisional state, Conflux gets three desirable properties:

1. Simplicity: application developers do not need to know the details of log replication; use `getProvisionalState` in methods, and `getState` everywhere else
2. Correctness: application state remains externally consistent in the face of node failures; all provisional and committed states are externally consistent
3. Performance: the leader can perform multiple actions per heartbeat without waiting for uncommitted entries to be committed

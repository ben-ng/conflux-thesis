# Raft

Raft is a consensus algorithm that is designed for understandability. It does this by decomposing consensus into three subproblems: leader election, log replication, and safety. An algorithm for cluster membership changes is described, but not part of the core consensus protocol. Two optimizations are also suggested: log compaction, and using a binary search to help lagging followers catch up more quickly.



# Immutable Trees

Conflux keeps all application state in an immutable tree-like structure. These structures typically have a dictionary at their root, and any combination of dictionaries, arrays, and primitive data types as children. This type of structure is uncommon in Computer Science but common in dynamic languages. Since they resemble a tree, and they are commonly called trees in industry, they will be called trees in this book as well.

![A state tree for a simple task management application](diagrams/immutable-state-tree.png)

Immutable state trees have become a popular way to describe the state of user interfaces because these interfaces are also hierarchical in nature. State trees are flexible enough to describe a wide variety user interfaces, from simple list views to interactive infographics. Since Conflux aims to be a general-purpose abstraction for shared memory, immutable state trees are an ideal data structure.

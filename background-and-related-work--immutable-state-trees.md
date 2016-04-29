# Immutable State Trees

Applications that use Object-Oriented Programming typically hold their state in the instance variables of a graph of objects. An alternative is to use hold no state in the objects, and store all of it in an immutable tree.

Immutable state trees have rapidly grown in popularity because they are conceptually simple, scale to complex applications, and work well with declarative user interfaces. These data structures typically use a dictionary as their root node, and have any combination of dictionaries, arrays, and primitive data types as children.

![A state tree for a simple task management application](diagrams/state-tree.png)

In order for the application to move to a different state, an *action* is dispatched. Actions are data structures that describe the production of one state from another. The data structure chosen for an action is not important; it only needs to contain enough information about the transition to derive the new state. 

Actions are typically implemented using dictionaries with one key describing the name of the action (e.g. `add`, `subtract`, `append`), and additional keys describing the transition in more detail (`add 2`, `append foobar`).

The new state is derived using a reducer, a pure function with the following signature:

$$ reduce (state, action) \rightarrow state' $$

![Incrementing a counter with an action](diagrams/state-p-action-eq-state.png)

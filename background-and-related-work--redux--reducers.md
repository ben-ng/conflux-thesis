# Reducers

Reducers are pure functions that transform a state tree by applying an action.

$$ reduce (state, action) \rightarrow state' $$

Their implementation is not important, but reducers tend to be nested `switch` statements that operate on immutable data structures.

![Incrementing a counter with an action](diagrams/state-p-action-eq-state.png)

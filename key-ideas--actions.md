# Actions

The state trees described in the previous chapter describe application state at some point in time. In order for the application to move to a different state, an *action* has to be dispatched. Actions are data structures that describe the production of one state from another. The data structure chosen for an action is not important; it only needs to contain enough information about the transition to derive the new state. 

Actions are typically implemented using dictionaries with one key describing the type of the action (e.g. `add`, `subtract`, `append`), and additional keys describing the transition in more detail (`add 2`, `append foobar`).

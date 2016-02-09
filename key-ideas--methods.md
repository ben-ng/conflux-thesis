# Methods

Redux is predictable, but not necessarily consistent -- it is possible for an application using Redux to enter a state that the programmer never anticipated. This is because Redux does not specify any rules that restrict *when* an action may be dispatched.

![An example of inconsistent state](diagrams/external-inconsistency.png)

In Conflux, actions are dispatched through *methods*. Methods are synchronous procedures that inspect the state of the application and *may* emit an action if the transition results in a consistent state.

Methods can return one of three values:

* `NULL`, if the system should not change state
* `Error`, if the requested transition would result in an inconsistent state
* `Action`, a data structure describing the transition that the system should make

![An example of methods ensuring consistency](diagrams/external-consistency.png)

Redux applications typically use the user interface to keep application state consistent. For example, buttons may appear or disappear to reflect available actions. Using the user interface to keep application state consistent is messy, and more importantly, is not possible in applications without a user interface.

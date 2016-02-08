# Methods

Redux is *internally consistent*, but not necessarily *externally consistent* [^1] -- it is possible for an application using Redux to enter an invalid state that the programmer never anticipated. This is because Redux does not specify any rules that restrict *when* an action may be dispatched.

![An example of internally consistent but externally inconsistent state](diagrams/external-inconsistency.png)

Conflux ensures external consistency using *methods*. Methods are synchronous procedures that inspect the state of the application and may emit an action if the transition results in an externally consistent state.

Methods can return one of three values:

* `NULL`, if the system should not change state
* `Error`, if the requested transition would result in an inconsistent state
* `Action`, a data structure describing the transition that the system should make

![An example of methods ensuring external consistency](diagrams/external-consistency.png)

Redux applications implicitly encode the *idea* of a method in a user interface. For example, buttons may appear or disappear to reflect available transitions. Coupling the user interface with the consistency of the application state is messy, and more importantly, is not possible in applications without a user interface.

[^1]: Hofstadter, Douglas R. Gödel, Escher, Bach: An Eternal Golden Braid. New York: Basic, 1979. Print.

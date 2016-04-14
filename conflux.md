# Key Ideas

Conflux is an architecture that enables a developer without formal training in distributed systems to confidently write distributed applications. It does this by 1) sacrificing performance for safety 2) borrowing common patterns from non-distributed application architectures. Neither of these ideas are new. For example, relatively slow dynamic languages have exploded in popularity because their safety and ease of use, and Promises allow us to work with asynchronous operations with synchronous flow-control constructs like `try` and `catch`.

1. Changes to application state are requested by calling *methods*
2. Methods read *provisional state*, everyone else reads *committed state*

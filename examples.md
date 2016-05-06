# Examples

The following examples show how Conflux simplifies the implementation of distributed systems. Instead of describing algorithms using RPC calls or message passing, we describe them using methods, actions, and reducers. Since methods and reducers are synchronous, it is simple to verify that they are correct.

To demonstrate the versatility of Conflux, two very different examples were chosen. The Distributed Mutex only has a programmatic interface and runs on the server. Tic-Tac-Toe only has a visual interface and runs on the client.

To show that Conflux is not just useful in theory, each example is accompanied by a working demonstration. To see how straightforward it is to translate the pseudocode into a functioning system, take a look at the attached source code.

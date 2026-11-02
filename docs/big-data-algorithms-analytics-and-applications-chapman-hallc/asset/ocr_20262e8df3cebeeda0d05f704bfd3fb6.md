vertex in a task topology can be created in many instances. All those vertices will simultaneously process a data stream, and different parts of the topology can be allocated in different machines. A good allocating strategy will greatly improve system performance.

A data stream grouping defines how that stream should be partitioned among the bolt’s tasks; spouts and bolts execute in parallel as many tasks across the cluster. There are seven built-in stream groupings in Storm, such as shuffle grouping, fields grouping, all grouping, global grouping, none grouping, direct grouping, and local or shuffle grouping; a custom stream grouping to meet special needs can also be implemented by the CustomStreamGrouping interface.

# *11.3.1.2  Fault Tolerance*

Fault tolerance is an important feature of Storm. If a worker dies, Storm will automatically restart it. If a node dies, the worker will be restarted on another node. In Storm, Nimbus and the Supervisors are designed to be stateless and fail-fast whenever any unexpected situation is encountered, and all state information is stored in a Zookeeper server. If Nimbus or the Supervisors die, they will restart like nothing happened. This means you can kill the Nimbus and the Supervisors without affecting the health of the cluster or task topologies.

When a worker dies, the Supervisor will restart it. If it continuously fails on startup and is unable to heartbeat to Nimbus, Nimbus will reassign the worker to another machine.

When a machine dies, the tasks assigned to that machine will time out, and Nimbus will reassign those tasks to other machines.

When Nimbus or Supervisors die, they will restart like nothing happened. No worker processes are affected by the death of Nimbus or the Supervisors.

# *11.3.1.3  Reliability*

In Storm, the reliability mechanisms guarantee that every spout tuple will be fully processed by corresponding topology. They do this by tracking the tree of tuples triggered by every spout tuple and determining when that tree of tuples has been successfully completed. Every topology has a “message timeout” associated with it. If Storm fails to detect that a spout tuple has been completed within that timeout, then it fails the tuple and replays it later.

The reliability mechanisms of Storm are completely distributed, scalable, and fault tolerant. Storm uses mod hashing to map a spout tuple ID to an acker task. Since every tuple carries with it the spout tuple IDs of all the trees they exist within, they know which acker tasks to communicate with. When a spout task emits a new tuple, it simply sends a message to the appropriate acker telling it that its task ID is responsible for that spout tuple. Then, when an acker sees that a tree has been completed, it knows to which task ID to send the completion message.

An acker task stores a map from a spout tuple ID to a pair of values. The first value is the task ID that created the spout tuple that is used later on to send completion messages. The second value is a 64-bit number called the “ack val.” The ack val is a representation of the state of the entire tuple tree, no matter how big or how small. It is simply the exclusive
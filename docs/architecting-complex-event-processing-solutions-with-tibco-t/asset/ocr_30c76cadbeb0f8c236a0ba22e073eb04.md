# Explicit

In explicit buffer management a policy clause defines the conditions under which the object will be added and the logic defining its retention. Listing 7-4 indicates that new objects will be accepted (added), and that the objects will be retained for one hour. There are three types of retention policy available.

+   1. Sliding: The last n objects meeting specified conditions will be retained.
+   2. Tumbling: Retains up to n objects, at which point the buffer is emptied to start over.
+   3. Time window: Objects remain in the buffer for the specified time period.

Listing 7-4 has two examples of explicit buffer management using time windows.

# Implicit

In implicit buffer management, there is no policy clause in the query. New objects that meet the specified conditions are added to the buffer and deleted objects are removed. Changed objects are first removed from the buffer (without triggering the query evaluation) and then added (which will trigger the query evaluation).

# Continuous Query Life Cycle

The life cycle of a continuous query is shown in Figure 7-8. The cycle begins with a call to Query.create(). One of the arguments to this function is the string that defines the query. Note that this function may throw an exception if there is an error in the query definition.

Once the query has been created, an instance of the query is created with Query.Statement.open() and the values of variables set with calls to Query.Statement.setVar(). Executing the query with Query.Statement.execute() requires a user-defined callback function. This is a user-defined rule function that must have the type signature required for query statement callbacks. The body of the function contains the logic indicating what to do with the query results. The function is called each time the query is reevaluated.

Once executed, the query remains active until the agent is shut down or Query.Statement.close() is called.
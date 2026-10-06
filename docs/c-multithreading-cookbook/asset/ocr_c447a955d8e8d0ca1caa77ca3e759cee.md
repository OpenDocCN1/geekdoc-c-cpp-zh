# Advanced Thread Management

Next, a call to GetWaitChain follows. This API retrieves the wait chain for the specified thread. If any subset of nodes in the array forms a cycle, the function sets the IsCycle parameter to TRUE (from MSDN). So, if a cycle is formed, bDeadlock will be set to TRUE. If we terminated the deadlock and closed the session using the CloseThreadChainSession API. We then suspend the thread for one second and continue monitoring the pool execution.

In the entry point, we create two bank accounts with certain amounts of money. After we've created the pool, we request for thread to transfer funds from the first to the second account, and we request for another thread to transfer funds from the second to the first account, creating a problematic situation. We perform this in a loop that iterates ten times to ensure that a deadlock will occur. If a deadlock is found, the problem solver will

One situation with a deadlock is shown in the following screenshot:

![](bbox=[0.183, 0.376, 0.816, 0.623])

# There's more...

The explained example targets a certain possible scenario where a problem can occur. This situation is known as the Banker's algorithm, by Edsger Dijkstra, that a given pool implementation, with along solving, could be used for any scenario where a deadlock or a similar problem can occur. Our intention was to teach the user how to carefully design the objects that will help develop the program more easily, at the same time giving the ability to control the execution, respect the resources used, and perform advanced management and monitoring of program execution. In general, as we said so many times, it is important to carefully design the application, and if necessary, to include advanced mechanisms to support such a design.
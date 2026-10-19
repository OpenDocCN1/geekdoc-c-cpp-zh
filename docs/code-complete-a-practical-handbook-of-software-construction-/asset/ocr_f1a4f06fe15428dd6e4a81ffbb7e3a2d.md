# Keep all accesses to the data at the same level of abstraction

If you use an access routine to do one thing to a structure, you should use an access routine to do everything else to it too. If you read from the structure with an access routine, write to it with an access routine. If you call InitStack() to initialize a stack and PushStack() to push an item onto the stack, you’ve created a consistent view of the data. If you pop the stack by writing value = array[ stack.top ], you’ve created an inconsistent view of the data. The inconsistency makes it harder for others to understand the code. Create a PopStack() routine instead of writing value = array[ stack top ].

Cross-Reference Using access routines for an event queue suggests the need to create a class. For details, see Chapter 6, "Working Classes."

In the example pairs of statements in Table 13-1, the two event-queue operations occurred in parallel. Inserting an event into the queue would be trickier than either of the two operations in the table, requiring several lines of code to find the place to insert the event, adjust existing events to make room for the new event, and adjust the front or back of the queue. Removing an event from the queue would be just as complicated. During coding, the complex operations would be put into routines and the others would be left as direct data manipulations. This would create an ugly, nonparallel use of the structure. Now compare the pairs of statements in Table 13-2:

# Table 13-2 Parallel and Nonparallel Uses of Complex Data

| Nonparallel Use of Complex Data | Parallel Use of Complex Data |
|---|---|
| event = EventQueue[ queueFront ] | event = HighestPriorityEvent() |
| event = EventQueue[ queueBack ] | event = LowestPriorityEvent() |
| AddEvent( event ) | AddEvent( event ) |
| eventCount = eventCount - 1 | RemoveEvent( event ) |

Although you might think that these guidelines apply only to large programs, access routines have shown themselves to be a productive way of avoiding the problems of global data. As a bonus, they make the code more readable and add flexibility.

# How to Reduce the Risks of Using Global Data

In most instances, global data is really class data for a class that hasn’t been designed or implemented very well. In a few instances, data really does need to be global, but accesses to it can be wrapped with access routines to minimize potential problems. In a tiny number of remaining instances, you really do need to use global data. In those cases, you might think of following the guidelines in this section as getting shots so that you can drink the water when you travel to a foreign country: they’re kind of painful, but they improve the odds of staying healthy.

Cross-Reference For details on naming conventions for global variables, see "Identify global variables" in Section 11.4.

# Develop a naming convention that makes global variables obvious

You can avoid some mistakes just by making it obvious that you’re working with global data. If you’re using global variables for more than one purpose (for example, as variables and as substitutes for named constants), make sure your naming convention differentiates among the types of uses.
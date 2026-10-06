# FIGURE 14-10 (a) front passes back when the queue becomes empty; (b) back catches up to front when the queue becomes full

(a) Queue with single item  dequeue()—queue becomes empty

![](bbox=[0.148, 0.175, 0.64, 0.34])

(b) Queue with single empty slot  enqueue(9)—queue becomes full

![](bbox=[0.148, 0.388, 0.64, 0.535])

The only difficulty with this scheme is detecting when the queue is empty or full. It seems reasonable to select as the queue-empty condition

front is one slot ahead of

as appears to indicate that front “passes” back when the queue becomes empty, as Figure-14-10 depicts. However, it is also possible that this condition signals a full queue: Because the queue is circular, back might in “catch up” with front as the queue becomes full. Figure-14-10b illustrates this situation.

Obviously, you need a way to distinguish between the two situations. One way is to keep a count of the number of items in the queue. Before adding an item to the queue, you check whether the count is equal to MAX_QUEUE; if it, the queue is full. Before removing an item from the queue, you check whether the count is equal to zero; if it is, it is empty.

**The header file.** Listing 14-4 contains the header file for an array-based implementation of the ADT queue that uses a circular array as just. Because the data is stored in statically allocated memory, the compiler-generated destructor and copy constructor are sufficient.¹¹

front and back cannot be used to distinguish between queue-full and queue-empty
without conditions

By counting the queue items, you can detect queue-full and queue-empty conditions

¹¹ If you use a dynamically allocated array, you must provide a destructor and copy constructor.
# Example 1.8

A shop maintains the list of customers, sales assistants and the average transactions on a day as given in Fig. 1.12.

Suppose we need to write a program, which will help determine the number of sales assistants required to serve customers efficiently. Here, we will need to simulate the waiting line in the shop. This analysis will require the simulation of a queue. However, queues are not generally available in programming languages. Therefore, even if the queue type is available, we need some basic queue operations such as enqueuing and dequeuing, which are basically insertion and deletion operations, for the simulation.

+   Here is what we can do in this situation:
+   1. Write a program that simulates the queue, or
+   2. Write a queue ADT that can solve any queue problem.

If we choose the second option, we still need to write a program to simulate the shop application. However, doing that will actually be simpler and faster because we can concentrate on the application rather than the queue.

| | Customers |
|---|---|
| 1 | Customers |
| 2 | Customers |
| 3 | Customers |

| | Sales Assistant |
|---|---|
| 1 | Ray |
| 2 | Reed |
| 3 | Kelly |

Fig. 1.12

An abstract data type can thus be further defined as a data declaration packaged together with the operations that are meaningful for the data type. In other words, we encapsulate the data and the operations on the data, and then we hide them from the user.

The user need not know the data structure to use the ADT. Considering Example 1.8, the application program should have no knowledge of the data structure. All references to and manipulation of the data in the queue must be handled through defined interfaces in the structure. Allowing the application program to directly reference the data structure is a common fault in many implementations. This prevents the ADT from being fully portable to other applications.

# Abstract Data Type Model

A representation of the ADT model is shown in Fig. 1.13. Notice that there are two different parts of the ADT model—functions (public and private) and data structures. Both are contained within the ADT model itself, and do not come within the scope of the application program. On the other hand, data structures are available to all of the ADTs functions as required, and a function may call on any other function to accomplish its task. This means that data structures and functions are within the scope of each other.

Data are entered, accessed, modified and deleted through the external

![](bbox=[0.41, 0.61, 0.92, 0.87])

additional simulation result that is printed. In addition to the output shown in Figure 8.8, the function also prints the number of simulated customers who left because the queue was too long. Embed the function in a program that allows the user to repeat simulations with different arguments until the user says she or he wishes to quit the program.

- **4** Choose one of the queue implementations and implement an iterator that is similar to our bug iterator in Section 6.6.

- **5** In a priority queue, each item that enters the queue has a number called its priority. The items with the highest priority numbers exit the queue first. Use an array or a linked list to implement a priority queue.

- **6** In this chapter we gave a linked-list implementation of a queue. This implementation used two named pointers called `front_ptr` and `rear_ptr` to point to the front and the rear nodes of the queue (linked list). A **circular linked list** is similar to a regular linked list, except that the pointer field in the “last node” points back to the “first node.” (Of course, after this change it is no longer clear which node, if any, is intrinsically “first.”) If we use a circular linked list, then we need only one pointer to implement a queue, since the front node and the rear node are adjacent nodes, as shown by the following diagram:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_461_0.png)

In the diagram we have called the single pointer `rear_ptr`, because it points to the last node in the queue. It turns out that this gives a more efficient implementation than having it point to the first node in the queue. Redo the queue class using a circular linked list.

- **7** A **double-ended queue** is a list that allows the addition and removal of entries from either end. One end is arbitrarily called the **front** and the other the **rear**, but the two ends behave identically. Specify, design, and implement a template class for a double-ended queue. Include operations to check if it is empty or full. For each end, include operations for adding and deleting entries. Implement the double-ended queue as a doubly linked list. Call your class dequeue (which is pronounced “deck”). By the way, the C++ Standard Library has a deque class.

- **8** Make improvements to the carwash simulation program from Section 8.2. One particular improvement that you should make is to handle the customers who are still in the queue at the end of the simulation. These customers should have their cars washed one after another, but no new customers should be allowed to join the queue during this time. The wait times of these leftover customers should be counted along with all the other customers.

- **9** Write a simulation program for a small airport that has only one runway. There will be a queue of planes waiting to land and a queue of planes waiting to take off. However, only one plane can use the runway at a time. So there can be only one takeoff or one landing in progress at any one time. Assume that all takeoffs take the same amount of time. Assume that all landings take the same amount of time, although this does not need to be the same as the takeoff time. Assume that planes arrive for landing at random times, but with a specified probability of a plane arriving during any given minute. Similarly, assume that planes arrive at the takeoff queue at random times, but with a (possibly different) specified probability of a departure. (Despite the fact that takeoffs and landings are scheduled, delays make this a reasonable assumption.) Since it is more expensive and more dangerous to keep a plane waiting to land than it is to keep a plane waiting to take off, landings will have priority over takeoffs. Thus, as long as some plane is waiting to land, no plane can take off. Use a clock that is an unsigned integer variable that counts the number of minutes simulated. Use the `cstdlib` random number generator to simulate arrival and departure times of airplanes.

This simulation can be used, among other things, for deciding when the air traffic has become so heavy that a second runway must be built. Hence, the simulation will simulate conditions that would be a disaster, in which planes crash because they run out of fuel while waiting too long in the landing queue. By examining the simulated situation, the airport authority hopes to avoid the real tragedy. Assume all planes can remain in the queue the same amount of time before they run out of fuel. If a plane runs out of fuel, your simulation will not discover this until the simulated plane is removed from the queue; at that point, the fact that the plane crashed is recorded, that plane is discarded, and the next plane is processed. A crashed plane is not considered in the calculation of waiting time. At the end of the simulated time, the landing queue is examined to see whether any of the planes in the simulated queue have crashed. You can disregard the planes left in the queue at the end of the simulation, other than those that crashed for lack of sufficient fuel. Use the following input and output specification:

Input: (1) The amount of time needed for one plane to land; (2) the amount of time needed for one plane to take off; (3) the average amount of time between arrivals of planes to the landing queue; (4) the average amount of time between arrival of planes to the takeoff queue; (5) the maximum amount of time that a plane can stay in the landing queue without running out of fuel and crashing; (6) the total length of time to be simulated.

Output: (1) The number of planes that took off in the simulated time; (2) the number of planes that landed in the simulated time; (3) the number of planes that crashed because they ran out of fuel before they could land; (4) the average time that a plane spent in the takeoff queue; (5) the average time that a plane spent in the landing queue.

- **10** Do an airport simulation that is more complex than the previous project. In this version, planes arrive for landing with random amounts of fuel, which determines how long they can remain in the air. A plane will crash unless it lands within the time assigned to it. Your simulation will keep planes in a priority queue, where the prior-

- **11** Write a simulation program of the lines at a grocery store. The program will be similar to the car wash simulation, except that there are multiple queues instead of one. You might use a vector of queues to simulate the lines. Assume that there are five cashier lines at the grocery store. Customers enter lines to check out, and then enter the shortest line. If two lines are equal, then the first available cashier is chosen. Each transaction takes a random amount of time to complete.

- For additional work, expand the grocery line program to allow shoppers to:
  - Avoid a line if all lines are a certain length
  - Leave a line if they have waited beyond a certain time
  - Check if another line is shorter at specified time intervals
  - Switch lines if another line is shorter

- **12** Redo Programming Project 5 in Chapter 4 using the STL priority queue, so that your list of chores will be prioritized. Create a class for chores, which will store the chore as a string, and the priority as an integer. Write a friend function for the class that defines operator< (or define a comparison function). After reading the program, compute a solution to deal with cases in which the priority values of chores are the same. Hint: Use the comparison function to define an additional ordering when two priorities are equal.

- **13** Use an array or a linked list to implement a deque class.

- **14** Use the idea from Figure 8.12 to implement a deque class.

## Chapter 9 Recursive Thinking

> "Well," said Frog, "I don't suppose anyone ever is completely self-winding. That's what friends are for." He reached for the father's key to wind him up again.
> RUSSELL HOBAN
> The Mouse and His Child

### LEARNING OBJECTIVES

- When you complete Chapter 9, you will be able to.
- recognize situations in which a subtask is nothing more than a simpler version of the larger problem and design recursive solutions for these problems.
- trace recursive calls by drawing pictures of the run-time stack.
- prove that a recursive function has no infinite recursion by finding a valid variant expression and threshold.
- use induction to prove that a recursive function meets its precondition/postcondition contract.

### CHAPTER CONTENTS

- 9.1 Recursive Functions
- 9.2 Studies of Recursion: Fractals and Mazes
- 9.3 Reasoning About Recursion
- Chapter Summary
- Solutions to Self-Test Exercises
- Programming Projects

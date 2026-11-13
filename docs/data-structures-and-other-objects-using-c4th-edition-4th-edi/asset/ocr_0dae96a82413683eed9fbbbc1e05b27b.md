ture times of airplanes.

This simulation can be used, among other things, for deciding when the air traffic has become so heavy that a second runway must be built. Hence, the simulation will simulate conditions that would be a disaster, in which planes crash because they run out of fuel while waiting too long in the landing queue. By examining the simulated situation, the airport authority hopes to avoid the real tragedy. Assume all planes can remain in the queue the same amount of time before they run out of fuel. If a plane runs out of fuel, your simulation will not discover this until the simulated plane is removed from the queue; at that point, the fact that the plane crashed is recorded, that plane is discarded, and the next plane is processed. A crashed plane is not considered in the calculation of waiting time. At the end of the simulated time, the landing queue is examined to see whether any of the planes in the simulated queue have crashed. You can disregard the planes left in the queue at the end of the simulation, other than those that crashed for lack of sufficient fuel. Use the following input and output specification:

Input: (1) The amount of time needed for one plane to land; (2) the amount of time needed for one plane to take off; (3) the average amount of time between arrivals of planes to the landing queue; (4) the average amount of time between arrival of planes to the takeoff queue; (5) the maximum amount of time that a plane can stay in the landing queue without running out of fuel and crashing; (6) the total length of time to be simulated.

Output: (1) The number of planes that took off in the simulated time; (2) the number of planes that landed in the simulated time; (3) the number of planes that crashed because they ran out of fuel before they could land; (4) the average time that a plane spent in the takeoff queue; (5) the average time that a plane spent in the landing queue.

10 Do an airport simulation that is more complex than the previous project. In this version, planes arrive for landing with random amounts of fuel, which determines how long they can remain in the air. A plane will crash unless it lands within the time assigned to it. Your simulation will keep planes in a priority queue, where the prior-

ity of a plane is equal to the number of minutes before midnight that the plane will crash.

11 Write a simulation program of the lines at a grocery store. The program will be similar to are the car wash simulation, except that there are multiple queues instead of one. You might use a vector of queues to simulate the lines. Assume that there are five cashier lines at the grocery store. Customers enter lines to check out, and then enter the shortest line. If two lines are equal, then the first available cashier is chosen. Each transaction takes a random amount of time to complete.

+   For additional work, expand the grocery line program to allow shoppers to:
+   * Avoid a line if all lines are a certain length
+   * Leave a line if they have waited beyond a certain time
+   * Check if another line is shorter at specified time intervals
+   * Switch lines if another line is shorter

12 Redo Programming Project 5 in Chapter 4 using the STL priority queue, so that your list of chores will be prioritized. Create a class for chores, which will store the chore as a string, and the priority as an integer. Write a friend function for the class that defines operator< (or define a comparison function). After reading the program, compute a solution to deal with cases in which the priority values of chores are the same. Hint: Use the comparison function to define an additional ordering when two priorities are equal.

13 Use an array or a linked list to implement a deque class.

14 Use the idea from Figure 8.12 to implement a deque class.
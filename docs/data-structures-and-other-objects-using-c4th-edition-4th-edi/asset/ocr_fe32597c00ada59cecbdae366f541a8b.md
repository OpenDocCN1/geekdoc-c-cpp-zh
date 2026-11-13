# Car Wash Simulation—Design

We will carry out a design of the program in a way that is common for many simulation tasks. The approach is to propose a collection of related object types that correspond to real-world objects in the situation that we are simulating. There are many possibilities—our particular approach focuses on the use of our queue class, which will be used to simulate a line of customers waiting to have their cars washed. We first discuss the queue and then propose the other objects needed for the simulation.

Key Design Concept
Determine
which properties of a
real-world
object are
relevant to the
problem at
hand.

We need to simulate a queue of customers, but we do not have real live customers, so we must decide how we will represent them. There are many ways to represent customers: We could use their names and place them in a queue of names; we could assign an arbitrary number to each customer and store that number in a queue of numbers; we could represent each customer by the make and year of the customer’s automobile, or even by how dirty the automobile is. However, none of those representations has any relevance to the specified simulation. For this simulation, all we need to know about a customer is how long the customer waits in the queue. Hence, a good way to represent a customer is to use a number that represents the time that the customer entered the queue. Thus, our queue will be a queue of numbers. In a more complex simulation, it would be appropriate to implement the customers as objects, and one of the customer’s member functions would be a function that returns the customer’s arrival time.

The numbers that record the arrival times are called time stamps. Our simulation works in seconds, so a time stamp is just the number of simulated seconds that have passed since the start of the simulation. When the customer (represented by the time stamp) is removed from the queue, we can easily calculate the time the customer spent waiting: The time spent waiting is the total number of seconds simulated so far minus the time stamp.

Figure 8.5 proposes pseudocode for the complete simulation algorithm. In addition to the queue, the pseudocode proposes three other object types: washer, bool_source, and averager. We’ll discuss these types one at a time.

Washer. A washer is an object that simulates the automatic car-washing mechanism. The simulation program requires one washer object. This washer is initialized with its constructor, and each time another second passes, the simulation program indicates the passage of one second for the washer. This suggests the following constructor and member function:

```
washer::washer(unsigned int s) ;
// Precondition: The value of s is the number of seconds needed to
// complete one wash cycle.
// Postcondition: The washer has been initialized so that all other member
// functions may be used.
void washer::one_second( ) ;
// Postcondition: The washer has recorded (and simulated) the passage of
// one more second of time.
```

Most of the simulation work is carried out in the large for-loop, where the local variable current_second runs from 1 to total_time. This loop parallels the large loop in the original pseudocode (Step 2 in Figure 8.5 on page 403).

After the loop finishes, the simulation function obtains two pieces of information from the averager and writes these items to cout.

### Self-Test Exercises for End of Section 8.2

- 10. Can a single program use both a stack and a queue?
- 11. How are time stamps used in simulations?
- 12. What C++ data type should be used for numbers that can never be negative?
- 13. Describe at least one assumption we made about the real-world car wash in order to make the simulation more manageable.
- 14. Use short sentences to describe the three main actions that occur during each second of simulated time in the car wash simulation.
- 15. What is RAND_MAX? Where is it defined?
- 16. When the car wash simulation finishes, there could still be some numbers in the queue. What do these numbers represent from the real world? (For a method of handling these leftover numbers, see Programming Project 8 on page 434.)

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_438_0.png)

### A Function Implementation

```
void car_wash_simulate
(unsigned int wash_time, double arrival_prob, unsigned int total_time)
// Precondition: 0 <= arrival_prob <= 1.
// Postcondition: The function has simulated a car wash where wash_time is the number of
// seconds needed to wash one car, arrival_prob is the probability of a customer arriving in
// any second, and total_time is the total number of seconds for the simulation. Before the
// simulation, the function has written its three parameters to cout. After the simulation,
// the function has written two pieces of information to cout: (1) the number of cars washed and
// (2) the average waiting time of a customer.
// Library facilities: iostream, queue, washing.h (using namespace std and main_savitch_8A)
{
queue<unsigned int> arrival_times; // Time stamps of the waiting customers
unsigned int next;
bool_source arrival(arrival_prob); // A value taken from the queue
washer machine(wash_time);
averager wait_times;
unsigned int current_second;
```

### (FIGURE 8.8 continued)

```
// Write the parameters to cout.
cout << "Seconds to wash one car: " << wash_time << endl;
cout << "Probability of customer arrival during a second: ";
cout << arrival_prob << endl;
cout << "Total simulation seconds: " << total_time << endl;
for (current_second = 1; current_second <= total_time; ++current_second)
{   // Simulate the passage of one second of time.
    // Check whether a new customer has arrived.
    if (arrival.query())
        arrival_times.push(current_second);

    // Check whether we can start washing another car.
    if ((!machine.is_busy()) && (!arrival_times.empty()))
    {
        next = arrival_times.front();
        arrival_times.pop();
        wait_times.next_number(current_second - next);
        machine.start_washing();
    }

    // Tell the washer to simulate the passage of one second.
    machine.one_second();
}

// Write the summary information about the simulation.
cout << "Customers served: " << wait_times.how_many_numbers() << endl;
if (wait_times.how_many_numbers() > 0)
    cout << "Average wait: " << wait_times.average() << " sec" << endl;
}
```

### Sample Output from the Car Wash Simulation Function

Seconds to wash one car: 240
Probability of customer arrival during a second: 0.0025
Total simulation seconds: 6000
Customers served: 19
Average wait: 110.211 sec

## 8.3 IMPLEMENTATIONS OF THE QUEUE CLASS

A queue seems conceptually simpler than a stack because we notice queues in everyday life. However, the implementation of a queue, though similar to that of a stack, is more complicated. As was the case with the stack class, we will give two implementations of our queue class: a static implementation using a fixed-sized array, and a dynamic implementation using a linked list. As usual, our application programs will run with either implementation (although the static version imposes a predetermined capacity on the size of the queue).

### Array Implementation of a Queue

As we did with the stack class, we will implement the queue class as a partially filled array. With a queue, we add entries at one end of the array and remove them from the other end. Hence, we will be accessing the used portion of the array at both ends, increasing the size of the used portion at one end and decreasing the size of the used portion at the other end. This differs from our use of a partially filled array for a stack, in that the stack accessed just one end of the partially filled array.

### Keeping track of both ends of the partially filled array

Because we now need to keep track of both ends of the used portion of the array, we will have two variables to keep track of how much of the array is used: One variable, called first, indicates the first index currently in use, and one variable, called last, indicates the last index currently in use. If data is the array name, then the queue entries will be in the array components:

```
data[first], data[first + 1], ... data[last].
```

To add an entry we increment last by one, and then store the new entry in the component data[last], where last is now one larger than it was before. To get the next entry from the queue, we retrieve data[first] and then increment first by one, so that data[first] is then the entry that used to be second.

There is one problem with this plan. The variable last is incremented but never decremented. Hence, it will quickly reach the end of the array. At that point, we will not be able to add any more entries to the queue. Yet, there is likely to be room in the array. In a normal application, the variable front would also be incremented from time to time (when entries are removed from the queue). This will free up the array locations with index values less than first. There are several ways to reuse these freed locations.

One straightforward approach for using the freed array locations is to maintain all the queue entries so that first is always equal to 0 (the first index of the array). When data[0] is removed, we move all the entries in the array down one location so the value of data[1] is moved to data[0], and then all other entries are also moved down one. This approach will work, but it is inefficient. Every time we remove an entry from the queue, we must move every entry in the queue. Fortunately, there is a better approach.

### Circular array

We do not need to move all the array elements. When the rear index reaches the end of the array, we can simply start reusing the available locations at the front of the array. Think of this arrangement as if the array were bent into a circle with the first component of the array immediately after the last component. In this way, the successor of the final array index is array index 0. In this circular arrangement, the free index positions are always “right after” data[last].

For example, suppose that we have a queue of characters with a capacity of five, and the queue currently contains three entries, ‘A’, ‘B’, and ‘C’. Perhaps these values are stored with first equal to 0 and last equal to 2, as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_441_0.png)

The question marks indicate unused spots in the array.

Let’s remove two entries (the ‘A’ and ‘B’), and add two more entries to the rear of this queue, perhaps the characters ‘D’ and ‘E’. The result is shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_441_1.png)

At this point, first is 2, last is 4, and the queue elements range from data[2] to data[4]. Suppose that now we add another character, ‘F’, to the queue. The new entry cannot go after last, since we have hit the end of the array. Instead, we go to the front of the array, adding the new ‘F’ at location data[0], as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_441_2.png)


customer departs. To compute the departure time, we add the length of the transaction to the time when the customer begins the transaction.

For example, if we run the simulation by hand with the previous data, we would compute the departure times as follows:

| Time | Event |
| :--- | :--- |
| 20 | Customer 1 enters bank and begins transaction<br>Determine customer 1 departure event is at time 26 |
| 22 | Customer 2 enters bank and stands at end of line |
| 23 | Customer 3 enters bank and stands at end of line |
| 26 | Customer 1 departs; customer 2 begins transaction<br>Determine customer 2 departure event is at time 30 |
| 30 | Customer 2 departs; customer 3 begins transaction<br>Determine customer 3 departure event is at time 32 |
| 30 | Customer 4 enters bank and stands at end of line |
| 32 | Customer 3 departs; customer 4 begins transaction<br>Determine customer 4 departure event is at time 35 |
| 35 | Customer 4 departs |

A customer's wait time is the elapsed time between arrival in the bank and the start of the transaction, that is, the amount of time the customer spends in line. The average of this wait time over all the customers is the statistic that you want to obtain.

To summarize, this simulation is concerned with two kinds of events:

- **Arrival events** indicate the arrival at the bank of a new customer. The input file specifies the times at which the arrival events occur. As such, they are externally generated events. When a customer arrives at the bank, one of two things happens. If the teller is idle when the customer arrives, the customer goes to the teller and begins the transaction immediately. If the teller is busy, the new customer must stand at the end of the line and wait for service.
- **Departure events** indicate the departure from the bank of a customer who has completed a transaction. The simulation determines the times at which the departure events occur. Thus, they are internally generated events. When a customer completes the transaction, he or she departs and the next person in line—if there is one—begins a transaction.

Event loop. The main tasks of an algorithm that performs a simulation are to repeatedly determine the times at which events occur and to process the events when they do occur. In simulation and gaming applications, this process is referred to as the event loop. The algorithm is stated at a high level as follows:

### A first attempt at a simulation algorithm

```
// Initialize
currentTime = 0
Initialize the line to "no customers"
while (currentTime <= time of the final event)
{
if (an arrival event occurs at time currentTime)
    Process the arrival event
if (a departure event occurs at time currentTime)
    Process the departure event
// When an arrival event and departure event occur at the same time,
// arbitrarily process the arrival event first
currentTime++
}
```

But do you really want to increment currentTime by 1? You would for a time-driven simulation, where you would determine arrival and departure times at random and compare those times to currentTime. Video games use this approach, since events can occur or need to be processed in almost every unit of time, which is typically a frame. In such a case, you would increment currentTime by 1 to simulate the ticking of a clock.

### A time-driven simulation simulates the ticking of a clock

Recall, however, that this simulation is event driven, so you have a file of predetermined arrival times and transaction times. Because you are interested only in those times at which arrival and departure events occur, and because no action is required between events, you can advance currentTime from the time of one event directly to the time of the next. Thus, you can revise the pseudocode solution as follows:

### An event-driven simulation considers only the times of certain events, in this case, arrivals and departures

Thus, you can revise the pseudocode solution as follows:

### First revision of the simulation algorithm

```
Initialize the line to "no customers"
while (events remain to be processed)
    currentTime = time of next event
    if (event is an arrival event)
        Process the arrival event
    else
        Process the departure event
    // When an arrival event and a departure event occur at the same time,
    // arbitrarily process the arrival event first
}
```

You must determine the time of the next arrival or departure so that you can implement the statement

```
currentTime = time of next event
```

To make this determination, you must maintain an event list. An event list contains all arrival and departure events that will occur but have not occurred yet. The times of the events in the event list are in ascending order, and thus the next event to be processed is always at the beginning of the list. The algorithm simply gets the event from the beginning of the list, advances to the time specified, and processes the event. The difficulty, then, lies in successfully managing the event list.

### An event list contains all future arrival events and departure events

Managing and processing customers and events. As customers arrive, they go to the back of the line. The current customer, who was at the front of the line, is being served, and it is this customer that you remove from the system next. It is thus natural to use a queue, bankQueue, to represent the line of customers in the bank. For this problem, the only information that you must store in the queue about each customer is the time of arrival and the length of the transaction.

Arrival events and departure events are ordered by time, and we always want to remove and process the next event that should occur—the highest-priority event. The ADT priority queue is used in this way. Our events can be stored in the priority queue eventListQueue. We can initialize eventListPQueue with the arrival events in the simulation data file and later add the departure events as they are generated.

But how can you determine the times for the departure events? Observe that the next departure event always corresponds to the customer that the teller is currently serving. As soon as a customer begins service, the time of his or her departure is simply

time of departure = time service begins + length of transaction

Recall that the length of the customer's transaction is in the event list, along with the arrival time. Thus, as soon as a customer begins service, you place a departure event corresponding to this customer in the event list. Figure 13-7 illustrates a typical instance of an arrival event and a departure event used in this simulation.

### FIGURE 13-7 A typical instance of (a) an arrival event; (b) a departure event

| | Type | Time | Length |
|---|---|---|---|
| (a) Arrival event | A | 20 | 6 |
| (b) Departure event | D | 26 | - |

### Two tasks are required to process each event

Now consider how you can process an event when it is time for the event to occur. You must perform two general types of actions:

- Update the bank line: Add or remove customers.
- Update the event list: Add or remove events.

### The algorithm for arrival events

To summarize, you process an arrival event as follows:

```
// TO PROCESS AN ARRIVAL EVENT
// Update the event list
Remove the arrival event for customer C from the event list
// Update the bank line
// if (bank line is empty and teller is available)
{
    Departure time of customer C is current time + transaction length
    Add a departure event for customer C to the event list
    Mark the teller as unavailable
}
else
    Add customer C to the bank line
```

### A new customer always enters the queue and is served while at the queue's front

When customer C arrives at the bank, if the line is empty and the teller is not serving another customer, customer C can go directly to the teller. The wait time is 0 and you insert a departure event into the event list. If other customers are in line, or if the teller is assisting another customer, customer C must go to the end of the line.

### The algorithm for departure events

You process a departure event as follows:

```
// TO PROCESS A DEPARTURE EVENT
// Update the event list
Remove the departure event from the event list
// Update the bank line
// if (bank line is not empty)
```

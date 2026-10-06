# 384 CHAPTER 13 Queues and Priority Queues

customer departs. To compute the departure time, we add the length of the transaction to the time when the customer begins the transaction.

For example, if we run the simulation with the previous data, we would compute the departure time as follows:

The results of a simulation

| Time | Event |
| --- | --- |
| 20 | Customer 1 enters bank and begins transaction. Determine customer 1 departure event is at time 26 |
| 22 | Customer 2 enters bank and stands at end of line |
| 23 | Customer 3 enters bank and stands at end of line |
| 26 | Customer 1 departs; customer 2 begins transaction. Determine customer 2 departure event is at time 30 |
| 30 | Customer 2 departs; customer 3 begins transaction. Determine customer 3 departure event is at time 32 |
| 30 | Customer 4 enters bank and stands at end of line |
| 32 | Customer 3 departs; customer 4 begins transaction. Determine customer 4 departure event is at time 35 |
| 35 | Customer 4 departs |

A customer's wait time is the elapsed time between arrival in the bank and the start of the transaction, that is, the amount of time the customer spends in line. The average of this wait time over all customers is the statistic you want to obtain.

To summarize, this simulation is concerned with two events:

A first attempt at a simulation algorithm

Event loop. The main tasks of an algorithm that performs a simulation are to repeatedly determine the times at which events occur and to process the events when they occur. In simulation and gaming applications, this process is referred to as the event loop. The algorithm is stated at a high level as follows:

```
// Initialize
currentTime = 0
Initialize the line to "no customers"

while (currentTime <= time of the final event)
(
```
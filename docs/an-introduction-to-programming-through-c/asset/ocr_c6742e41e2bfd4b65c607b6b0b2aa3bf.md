When you execute, the first two statements will cause events A, B to be posted to occur 15 and 5 time units respectively from the current time. The simulation starts with time 0, so these events will occur at time 15 and 5 respectively. The third statement in the program will cause the system to be evolved, i.e. all the events in the queue will be processed, in the order of the time at which they are meant to occur. Thus event B, scheduled at time 5, will get processed, first, i.e. its lambda expression will be called. This will cause the message "Event B." to be printed, prefixed by the simulation time, because of the call to sim::log. After that event A will be processed. Thus you would get the following output.

5) Event B.
15) Event A.

The point to be noted is that in the program the creation of event A happens before the creation of event B. However, the time of A, 15, is larger than the time of B, 5. Hence B happens before A during the execution.

As we discussed in Section 25.1.1, events in a discrete time system will in general cause the state of some of the entities to change, and also cause the creation (posting) of new events. We will now consider an example in which events do both of these. This example will contain the core idiom used in all future simulations.

In the program below, we have 4 events, A, B, C, D. We also have a variable count. We will see that the events will access this variable ("simulation state"), and in fact event D will be posted during the occurrence of event C.

```
int main(){
    int count=0;
    sim::post(15, [&](){sim::log() << "A. count: "<< count++ <<endl;}); //A
    sim::post(5, [&](){sim::log() << "B. count: "<< count++ <<endl;});   //B
    sim::post(10, [&](){
        sim::log() << "C. count "<< count++ <<endl;
        sim::post(100, [&](){sim::log() << "D. count: " <<
                            count++ << endl;});
    });
    sim::processAll();
}
```

The program begins by setting count to 0, and then posting the events A, B, C for time 15, 5, 10 respectively. Then sim::processAll causes the posted events to be processed.

The event posted for the earliest time is event B, and hence that gets processed first. This will cause the time of occurrence of B to be printed and also the value of count. Note that count has been captured into the event by reference, and hence the value at the time of occurrence of the event will be printed. Thus we will see the following output.

5) B. count: 0

Note that while printing, count is also incremented. Since count was captured by reference, the increment will affect the variable count as defined in the first line of the program. Thus this will become 1.
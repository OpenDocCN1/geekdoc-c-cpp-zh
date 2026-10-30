```
if(index >= 0 && index <= 9) count[index]++;
else cout << "Marks are out of range." << endl;
}
```

Note that this works only because all the ranges are of the same size. But this is very often the case when computing histograms.

# 13.2.6 A taxi dispatch program

Suppose you are the Mumbai dispatcher for the Mumbai-Pune taxi service. Your job is as follows. Drivers of taxis that are willing to take passengers to Pune report to you and give you their driver ID number and wait. Passengers who want taxis also report to you. When a passenger reports, you check if there are any waiting taxis. If there are, you assign the taxi of the driver that reported to you the earliest. Clearly, once a taxi has been given to a passenger, you need not keep the corresponding ID number on your list. If no taxis are available, you let the passenger know. You are not expected to keep track of waiting passengers, though an exercise asks you to do precisely this. You may assume that at any given point there will not be more than 100 taxis waiting for passengers. You are to write a program which will help you dispatch taxis as required.

Let us make this more specific. Suppose that the dispatcher will type 'd' when a driver arrives, followed by the driverID. Likewise when a customer arrives, the dispatcher will type 'c', and expect the program to print the ID of the assigned driver. Finally, to terminate the program, we will have the dispatcher type 'x' (commonly used as abbreviation of eXit).

Next we decide what variables we might need and how we should be using them.

Clearly, we will need to store the IDs of the waiting drivers. It seems natural to use an array, say driverID, to store these. Assume for simplicity that the IDs are integers with 9 or fewer digits, i.e. that they will fit in int. The size of the array can be a number larger than the number of drivers we expect will be waiting with us at any time. Most of the time there will be fewer drivers waiting with us than the size of the array, so we presumably need a variable nWaiting which will denote the number of waiting drivers.

We also need to somehow record the order in which the drivers arrived, because we want to assign the next customer to the driver who has registered with us the earliest. A natural way to do this is to store the earliest waiting driver at index 0, the next earliest at index 1, and so on. The ID of the driver that arrived last would be at index nWaiting - 1.

If a new driver arrives, we can store his ID at the index nWaiting, and increment nWaiting. If a customer arrives, we can assign the driver at driverID[0]. However, once we assign the driver, we must shift up all the other entries in the array, since we have decided that the waiting drivers must be stored starting at index 0. This is expressed in the following code.

```
const int n = 100; // estimate of max waiting drivers.
int driverID[n], nWaiting = 0;

while(true){ /* Invariants: nWaiting denotes the number of waiting drivers.
    0 <= nWaiting <= n. IDs of waiting drivers are in driverID,
    from driverID[0] to driverID[nWaiting - 1] */
```
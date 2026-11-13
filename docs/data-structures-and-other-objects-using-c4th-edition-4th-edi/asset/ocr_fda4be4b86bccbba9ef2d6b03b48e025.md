# FIGURE 8.5 The Car Wash Simulation

# Pseudocode

+   1. Declare a queue of unsigned integers, which will be used to keep track of arrival times of customers who are waiting to wash their cars. Unsigned integers are the data type used in C++ for numbers that can never be negative. We also declare the following objects:

+   (a) A washer: The washer's constructor has an argument indicating the amount of time (in seconds) needed by the washer to wash one car.

+   (b) A bool_source: The constructor has an argument that specifies how frequently the bool_source returns true (indicating how often customers arrive).

+   (c) An averager.

+   2. for (current_second = 1; current_second <= the simulation length; ++current_second) {
+   Each iteration of this loop simulates the passage of one second of time, as follows:
+   Ask the bool_source whether a new customer arrives during this second, and
+   if so, enter the current_second into the queue.
+   if ( the washer is not busy and the queue is not empty)
+   {
+   Remove the next integer from the queue, and call this integer next.
+   This integer is the arrival time of the customer whose car we will now wash.
+   So, compute how long the customer had to wait (current_second - next),
+   and send this value to the averager. Also, tell the washer that it should
+   start washing another car.
+   }
+   Indicate to the washer that another simulated second has passed. This allows the
+   washer to correctly determine whether it is still busy.
+   }

+   3. At this point, the simulation is completed. So we can get and print two items of information from the averager: (1) how many numbers the averager was given (i.e., the number of customers whose cars were washed); and (2) the average of all the numbers that was given (i.e., the average waiting time for the customers, expressed in seconds).

Notice that the constructor argument is an unsigned integer, which is a data type that forbids negative values. Throughout our simulation, we will use unsigned integers for time values that cannot be negative. As usual, we should provide a default value for this argument (perhaps 60 seconds), so that the constructor can be used as a default constructor.

The other two responsibilities of a washer are to tell the simulation program whether the washing mechanism is currently available and to begin the washing of a new car. These responsibilities are accomplished with two additional member functions:
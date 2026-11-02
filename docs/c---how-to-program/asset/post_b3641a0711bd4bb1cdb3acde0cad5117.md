
### b) Output on a Single-Core Windows Computer

```text
    Sequential calls to fibonacci(50) and fibonacci(49)
    Calculating fibonacci(50)
    fibonacci(50) = 12586269025
    Calculation time = 1.566667 minutes

    Calculating fibonacci(49)
    fibonacci(49) = 7778742049
    Calculation time = 0.883333 minutes

    Total calculation time = 2.450000 minutes
```

### c) Output on a Single-Core Windows Computer

```text
    Sequential calls to fibonacci(50) and fibonacci(49)
    Calculating fibonacci(50)
    fibonacci(50) = 12586269025
    Calculation time = 1.450000 minutes

    Calculating fibonacci(49)
    fibonacci(49) = 7778742049
    Calculation time = 0.883333 minutes

    Total calculation time = 2.333333 minutes
```

**Fig. E.11** | Fibonacci calculations performed sequentially. (Part 3 of 3.)

The first output shows the results of executing the program on a dual-core Windows computer on which every execution produced the same results, though this is not guaranteed. The second and third outputs show the results of executing the program on a single-core Windows computer on which the results varied, but execution always took longer, because the processor was being shared between this program and all the others that happened to be executing on the computer at the same time.

## Example: Multithreaded Execution of Two Compute-Intensive Tasks

Figure E.12 also uses the recursive fibonacci function, but executes each call to it in a separate thread. The first two outputs show the multithreaded Fibonacci example executing on a dual-core computer. Though execution times varied, the total time to perform both Fibonacci calculations (in our tests) was always less than for sequential execution in Fig. E.11—because our program split into two threads and used two cores, rather than just one. The last two outputs show the example executing on a single-core computer with the same speed as the dual-core computer. Again, times varied for each execution, but the total time was more than the sequential execution due to the overhead of sharing one processor among the program’s threads and the other programs executing on the computer at the same time.

```c
1  // Fig. E.12: figE_12.c
2  // Fibonacci calculations performed in separate threads
3  #include <stdio.h>
4 #include <threads.h>
5 #include <time.h>
6
7 #define NUMBER_OF_THREADS 2
8
9 int startFibonacci(void *nPtr);
10 unsigned long long int fibonacci(unsigned int n);
11
12 typedef struct ThreadData {
13     time_t startTime; // time thread starts processing
14     time_t endTime; // time thread finishes processing
15     unsigned int number; // fibonacci number to calculate
16 } ThreadData; // end struct ThreadData
17
18 int main(void)
19 {
20     // data passed to the threads; uses designated initializers
21     ThreadData data[NUMBER_OF_THREADS] =
22         { [0] = {.number = 50},
23         [1] = {.number = 49}};
24
25     // each thread needs a thread identifier of type thrd_t
26     thrd_t threads[NUMBER_OF_THREADS];
27
28     puts("fibonacci(50) and fibonacci(49) in separate threads");
29
30     // create and start the threads
31     for (size_t i = 0; i < NUMBER_OF_THREADS; ++i) {
32         printf("Starting thread to calculate fibonacci(%d)\n",
33             data[i].number);
34
35         // create a thread and check whether creation was successful
36         if (thrd_create(&threads[i], startFibonacci, &data[i]) !=
37             thrd_success) {
38
39         puts("Failed to create thread");
40         }
41     }
42
43     // wait for each of the calculations to complete
44     for (size_t i = 0; i < NUMBER_OF_THREADS; ++i)
45         thrd_join(threads[i], NULL);
46
47     // determine time that first thread started
48     time_t startTime = (data[0].startTime < data[1].startTime) ?
49         data[0].startTime : data[1].startTime;
50
51     // determine time that last thread terminated
52     time_t endTime = (data[0].endTime > data[1].endTime) ?
53         data[0].endTime : data[1].endTime;

// display total time for calculations
printf("Total calculation time = %f minutes\n",
       difftime(endTime, startTime) / 60.0);
}

// Called by a thread to begin recursive Fibonacci calculation
int startFibonacci(void *ptr)
{
    // Cast ptr to ThreadData * so we can access arguments
    ThreadData *dataPtr = (ThreadData *) ptr;

    dataPtr->startTime = time(NULL); // time before calculation

    printf("Calculating fibonacci(%d)\n", dataPtr->number);
    printf("fibonacci(%d) = %lld\n",
           dataPtr->number, fibonacci(dataPtr->number));

    dataPtr->endTime = time(NULL); // time after calculation

    printf("Calculation time = %f minutes\n\n",
           difftime(dataPtr->endTime, dataPtr->startTime) / 60.0);
    return thrd_success;
}

// Recursively calculates fibonacci numbers
unsigned long long int fibonacci(unsigned int n)
{
    // base case
    if (0 == n || 1 == n) {
        return n;
    }
    else { // recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

**Fig. E.12** | Fibonacci calculations performed in separate threads. (Part 1 of 4.)

### a) Output on a Dual-Core Windows Computer

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.866667 minutes

fibonacci(50) = 12586269025
Calculation time = 1.466667 minutes

Total calculation time = 1.466667 minutes
```

**Fig. E.12** | Fibonacci calculations performed in separate threads. (Part 3 of 4.)

### b) Output on a Dual-Core Windows Computer

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.783333 minutes

fibonacci(50) = 12586269025
Calculation time = 1.266667 minutes

Total calculation time = 1.266667 minutes
```

### c) Output on a Single-Core Windows Computer

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 1.683333 minutes

fibonacci(50) = 12586269025
Calculation time = 2.183333 minutes

Total calculation time = 2.183333 minutes
```

### d) Output on a Single-Core Windows Computer

```text
fibonacci(50) and fibonacci(49) in separate threads
Starting thread to calculate fibonacci(50)
Starting thread to calculate fibonacci(49)
Calculating fibonacci(50)
Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 1.600000 minutes

fibonacci(50) = 12586269025
Calculation time = 2.083333 minutes

Total calculation time = 2.083333 minutes
```

**Fig. E.12** | Fibonacci calculations performed in separate threads. (Part 4 of 4.)

## struct ThreadData

The function that each thread executes in this example receives a ThreadData object as its argument. This object contains the number that will be passed to fibonacci and two time_t members where we store the time before and after each thread’s fibonacci call. Lines 21–23 create an array of the two ThreadData objects and use designated initializers to set their number members to 50 and 49, respectively.

## thrd_t

Line 26 creates an array of thrd_t objects. When you create a thread, the multithreading library creates a thread ID and stores it in a thrd_t object. The thread's ID can then be used with various multithreading functions.

## Creating and Executing a Thread

Lines 31–41 create two threads by calling function thrd_create (line 36). The function's three arguments are:

- A thrd_t pointer that thrd_create uses to store the thread's ID.
- A pointer to a function (startFibonacci) that specifies the task to perform in the thread. The function must return an int and receive a void pointer representing the argument to the function (in this case, a pointer to a ThreadData object). The int represents the thread's state when it terminates (e.g., thrd_success or thrd_error).
- A void pointer to the argument that should be passed to the function in the second argument.

Function thrd_create returns thrd_success if the thread is created, thrd_nomem if there was not enough memory to allocate the thread or thrd_error otherwise. If the thread is created successfully, the function specified as the second argument begins executing in the new thread.

## Joining the Threads

To ensure that the program does not terminate until the threads terminate, lines 44–45 call thrd_join for each thread that we created. This causes the program to wait until the threads complete execution before executing the remaining code in main. Function thrd_join receives the thrd_t representing the ID of the thread to join and an int pointer where thrd_join can store the status returned by the thread. After the threads terminate, lines 48–57 calculate and display the total execution time by determining the time difference between the time the first thread started and the second thread ended.

## Function startFibonacci

Function startFibonacci (lines 61–77) specifies the task to perform—in this case, to call fibonacci to recursively perform a calculation, to time the calculation, to display the calculation's result and to display the time the calculation took (as we did in Fig. E.11). The thread executes until startFibonacci returns the thread's status (thrd_success, line 76), at which point the thread terminates.

## Other C11 Multithreading Features

In addition to the basic multithreading support shown in this section, C11 also includes other features such as _Atomic variables and atomic operations, thread local storage, conditions and mutexes. For more information on these topics, see Sections 6.7.2.4, 6.7.3, 7.17 and 7.26 of the standard and the following blog post and article:
http://blog.smartbear.com/software-quality/bid/173187/C11-A-New-C-Standard-Aiming-at-Safer-Programming
http://lwn.net/Articles/508220/

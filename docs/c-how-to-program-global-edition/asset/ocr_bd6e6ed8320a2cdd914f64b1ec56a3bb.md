# b) Output on a Single-Core Windows Computer

```
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.566667 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.883333 minutes

Total calculation time = 2.450000 minutes
```

# c) Output on a Single-Core Windows Computer

```
Sequential calls to fibonacci(50) and fibonacci(49)
Calculating fibonacci(50)
fibonacci(50) = 12586269025
Calculation time = 1.450000 minutes

Calculating fibonacci(49)
fibonacci(49) = 7778742049
Calculation time = 0.883333 minutes

Total calculation time = 2.333333 minutes
```

Fig. E.11 | Fibonacci calculations performed sequentially. (Part 3 of 3.)

The first output shows the results of executing the program on a dual-core Windows computer on which every execution produced the same results, though this is not guaranteed. The second and third outputs show the results of executing the program on a single-core Windows computer on which the results varied, but execution always took longer, because the processor was being shared between this program and all the others that happened to be executing on the computer at the same time.

# Example: Multithreaded Execution of Two Compute-Intensive Tasks

Figure E.12 also uses the recursive Fibonacci function, but executes each call to it in a separate thread. The first two outputs show the multithreaded Fibonacci example executing on a dual-core computer. Though execution times varied, the total time to perform both Fibonacci calculations (in our tests) was always less than for sequential execution in Fig. E.11—because our program split into two threads and used two cores, rather than just one. The last two outputs show the example executing on a single-core computer with the same speed as the dual-core computer. Again, times varied for each execution, but the total time was more than the sequential execution due to the overhead of sharing one processor among the program’s threads and the other programs executing on the computer at the same time.

```
1 // Fig. E.12: fig_E_12.c
2 // Fibonacci calculations performed in separate threads
3 #include <stdio.h>
```

Fig. E.12 | Fibonacci calculations performed in separate threads. (Part 1 of 4.)
+   - sleeping, then
+   - printing the task name and saying that the lambda is performing work.

The loop executes until the corresponding **jthread**'s internal **stop_source** receives a call to its **request_stop** member function. In this program, that call occurs in the **jthread**'s destructor when the **jthreads** go out of scope at the end of main.

# Optional stop_callback

Lines 32–35 also demonstrate that you can register an optional function to call when a **stop** is requested. The `std::stop_callback<sup>67</sup>` constructor receives as arguments a **stop_token** and a function with no parameters—in this case, a lambda. The constructor registers the function with the given **stop_token**. When the **stop_token** is notified that a stop was requested, it calls the function registered by the **stop_callback** on the thread that requested the stop (the main thread in this example). Any number of **stop_callbacks** can be created for a given **stop_token**. The order in which their functions execute is not specified. Our lambda simply displays a string to show that the callback was indeed called, but this could be used to perform cleanup operations before a thread terminates.<sup>68</sup>

# Analyzing the Output

Throughout the sample output, Task 1 and Task 2 sleep and work. Once main ends, the **jthreads** executing these tasks go out of scope, and their destructors call each **jthread**'s **request_stop** member function to notify the tasks that they should terminate. In our output after "MAIN (id: 16352) ENDS", you can see when each **jthread** received its **request_stop** call—our **stop_callback** displays the task name followed by a message that includes the ID of the thread that told the task to stop (the main thread in this example).<sup>69</sup> In each case, the corresponding task then finishes its work and terminates.

# 17.10  Launching Tasks with std::async

Figure 17.12 demonstrates **std::async**—a higher-level way to launch a task in a separate thread. In this example, we’ll implement a potentially long-running task—determining whether a large integer is prime and, if not, determining its prime factors.

# Security, Encryption and Prime Factorization for Enormous Integers

Security is a crucial application. Prime factorization.<sup>70,71,72</sup> is a vital aspect of the RSA Public-Key Cryptography algorithm, which is commonly used to secure data transmitted

+   67. “std::stop_callback.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/thread/stop_callback.
+   
+   68. Williams, “Concurrency in C++20 and Beyond.”
+   
+   69. If the stop is requested before the stop_callback is constructed, then the thread ID displayed will be that of the thread constructing the stop_callback (per https://en.cppreference.com/w/cpp/thread/stop_callback).
+   
+   70. “Prime Factorization,” July 2, 2020. Accessed April 18, 2023. https://www.cuemath.com/numbers/prime-factorization/.
+   
+   71. Striver, “Prime Factors of a Big Number,” May 28, 2021. https://www.geeksforgeeks.org/prime-factors-big-number/.
+   
+   72. Etrud Shalit, “Prime Numbers—Why Are They So Exciting?” September 7, 2018. Accessed April 18, 2023. https://kids.frontiersin.org/articles/10.3389/frym.2018.00040.
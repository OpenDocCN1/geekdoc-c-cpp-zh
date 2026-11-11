
```cpp
63 t1.join();
64 t2.join();
65 t3.join();
66 t4.join();
67
68 std::cout << '\n';
69
70 }
```

I define in lines 39 - 47 the four promises and the associated futures. In lines 51 - 54, each promise is moved to its thread. A promise can only be moved but not copied. The threads execute the function sumUp (lines 18 - 25). sumUp takes as its first argument a promise by rvalue reference. The futures ask in line 56 for the summation result by using the blocking get call.

![](img/d61a6c83410484053b8892275d2fcc4f_318_0.png)
Summation with a local variable on Linux

![](img/d61a6c83410484053b8892275d2fcc4f_318_1.png)
Summation with a local variable on Windows

To conclude this section, there is an overview of all performance numbers.

### 6.1.3.4 All Numbers for the Thread-Local Summation

It does not make a big difference whether I use local variables or tasks to calculate the partial sum or if I use various synchronization primitives such as atomics. Only the thread-local data seems to make the program a little slower. This observation holds for Linux and Windows. Don't be surprised by the higher performance of Linux relative to Windows. The program was optimized for four cores, and my Windows laptop has only two. The numbers are in seconds.

Performance of all thread-local summations

| Operating System (Compiler) | std::lock_guard | Atomic using sequential consistency | Atomic using relaxed semantic | Thread-local data | Tasks |
|---|---|---|---|---|---|
| Linux (GCC) | 0.03 | 0.03 | 0.03 | 0.04 | 0.03 |
| Windows (cl.exe) | 0.10 | 0.10 | 0.10 | 0.20 | 0.10 |

I want to draw our focus to a fascinating point. The thread-local multithreaded summation of the vector is about twice as fast as the single-threaded summation. I would expect a fourfold performance improvement in the optimal case because there is hardly a synchronization necessary between the threads. What is the reason?

## 6.1.4 Summation of a Vector: The Conclusion

### 6.1.4.1 Single Threaded

The range-based for loop and the STL algorithm std::accumulate are in the same performance range. In the optimized version, the compiler uses for the summation case the optimized version vectorized SIMD* instruction (SSE or AVX). Therefore, the loop counter is increased by 4 (SSE) or 8 (AVX).

### 6.1.4.2 Multithreading with a Shared Variable

The usage of a shared variable for the summation variable makes one point clear: synchronization is costly and should be avoided as much as possible. Although I used an atomic variable and even broke the sequential consistency, the four threads are 100 times slower than one thread. From a performance perspective, minimizing expensive synchronization has to be our first goal.

### 6.1.4.3 Thread-local Summation

The thread-local summation is only two times faster than the single-threaded range-based for loop or std::accumulate. That holds even though each of the four threads can work independently. That surprised me because I was expecting a nearly fourfold improvement. What surprised me, even more, was that my four cores are not fully utilized.

![](img/d61a6c83410484053b8892275d2fcc4f_320_0.png)
Utilisation of the four cores

The reason is simple; the cores can't get the data fast enough from memory. The execution is memory bound². Or to say it the other way around, the memory slows down the cores. The following pictures show the bottleneck memory.

¹ https://en.wikipedia.org/wiki/SIMD

² https://en.wikipedia.org/wiki/Memory_bound_function

```cpp
35    unlock(mb);
36    unlock(ma);
37  }
38 }
39
40 int main() {
41    std::cout << "dip_1\n";
42    srand(time(nullptr));
43
44    int m1{0}, m2{0}, m3{0}, m4{0};
45
46    std::thread t1{[&] {phi1(1, m1, m2);}};
47    std::thread t2{[&] {phi1(2, m2, m3);}};
48    std::thread t3{[&] {phi1(3, m3, m4);}};
49    std::thread t4{[&] {phi1(4, m4, m1);}};
50
51    t1.join();
52    t2.join();
53    t3.join();
54    t4.join();
55 }
```

The `main()` function establishes random numbers in line 42. We set the random number generator seed value to the number of seconds since 1st January 1970. We define our fork resources in line 44. Then we start four threads beginning in line 46. To avoid premature thread termination we join the threads beginning in line 51. The thread function `phi1()` has a forever loop. The `while(true)` statement is always true, therefore the thread will never terminate. The problem description says "he thinks for some random duration". First, we calculate a random duration with the function `myrand()` (lines 20 and 6). The function `myrand()` produces a pseudo-random return value in the range of [min, max). For program trace, we log the philosopher's number, his current state of he thinks and the duration to the console. The `sleep_for()` statement lets the scheduler put the thread for the duration into the state waiting. In a "real" program application source code uses up time instead of `sleep_for()`. After the philosopher's thread thinking time is over, he "gets his first fork" (line 24). We use a function `lock()` to perform the "gets fork" thing. At the moment the function `lock()` is very simple because we don't know better. We just set the fork resource to the value 1 (line 10). After the philosopher thread obtained his first fork, he proudly announces the new state with a `get_ma` console output. Now the thread "gets his second fork" (line 28). The corresponding console output is `get_mb`. The next state is eats. Again we determine the duration, produce a console output, and occupy the thread with a `sleep_for()` (line 31). After the state eats the philosopher puts down his forks (lines 35 and 14). The `unlock()` function is again really simple and sets the resource back to 0.

Please compile the program without compiler optimization. We will see the reason later. The console output of our program looks promising:

![](img/d61a6c83410484053b8892275d2fcc4f_325_0.png)
Multiple resource use

Have we already solved the dining philosophers problem? Well, the program output is not detailed enough to answer this question.

### 6.2.2 Multiple Resource Use with Logging

We should add some more logging. At the moment the function lock() does not check if the fork is available before the resource is used. The improved version of lock() in program dp_2.cpp is:

Multiple resource use with logging

```cpp
// dp_2.cpp

...

void lock(int& m) {
    if (m) {
        std::cout << "\t\t\t\t\t\t\tERROR lock\n";
    }
    m=1;
}

...
```

Program version 2 produces the following output:

![](img/d61a6c83410484053b8892275d2fcc4f_326_0.png)
Multiple resource use with logging

We see ERROR lock console output. This output tells us that two philosophers use the same resource at the same time. What can we do?

### 6.2.3 Erroneous Busy Waiting without Resource Hierarchy

We can change the if statement in lock() into a while statement. This while statement produces a spinlock. A spinlock is a fancy word for busy waiting. While the fork resource is in use, the thread is busy waiting for a change from the state in use to the state available. At this very moment, we set the fork resource again to state in use. In program dp_3.cpp we have:

**Erroneous Busy Waiting without Resource Hierarchy**

```cpp
// dp_3.cpp
...
void lock(int& m) {
  while (m)
    ; // busy waiting
  m=1;
}
...
```

Please believe that this little change is still not a CORRECT solution for the dining philosophers’ problem. We have no longer the wrong resource usage. But we have another problem. See program version 3 output:

![](img/d61a6c83410484053b8892275d2fcc4f_327_0.png)
**Erroneous busy waiting without resource hierarchy**

Every philosopher thread takes his first fork resource and then cannot take the second fork. What can we do? Andrew S. Tanenbaum^7 wrote in his book “Operating Systems. Design and Implementation, 3rd edition”: “Another way to avoid the circular wait is to provide a global numbering of all the resources. Now the rule is this: processes can request resources whenever they want to, but all requests must be made in numerical order.”

### 6.2.4 Erroneous Busy Waiting with Resource Hierarchy

This solution is known as resource hierarchy or partial ordering. For the dining philosophers problem, partial ordering is easy. The first fork taken has to be the fork with the lower number. For philosophers 1 to 3 the resources are taken in the correct order. Only philosopher thread 4 needs a change for correct partial ordering. First get fork resource 1, then get fork resource 4. See the main program in file `dp_4.cpp`:

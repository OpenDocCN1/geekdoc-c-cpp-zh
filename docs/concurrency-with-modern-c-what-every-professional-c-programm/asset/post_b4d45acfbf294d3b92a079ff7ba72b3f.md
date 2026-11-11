
## 6.4.1.1 The Analysis

When I execute the program, CppMem complains (1) (in red) that one of the four possible interleavings of threads is not race free. Only the first execution is consistent. Now I can use CppMem to switch between the four executions (2) and analyze the annotated graph (3).

![](img/d61a6c83410484053b8892275d2fcc4f_365_0.png)

You get the most out of CppMem by analyzing the various graphs.

### 6.4.1.1.1 First Execution

What conclusions can we derive from the following graph?

![](img/d61a6c83410484053b8892275d2fcc4f_366_0.png)

First execution

The nodes of the graph represent the expressions of the program, the edges the relation between the expressions. In my explanation, I refer to the names (a) to (f). What can I conclude from the annotations in this graph?

- **a:Wna x = 0**: Is the first expression (a), which is a non-atomic write of x.
- **sb (sequenced-before)**: The writing of the first expression (a) is sequenced before the writing of the second expression (b). These relations also hold between the expressions (c) and (d), and (e) and (f).
- **rf (read from)**: The expression (e) reads the value of y from the expression (b). Accordingly, (f) reads from (a).
- **sw (synchronizes-with)**: The expression (a) synchronises with (f). This relation holds because the expressions (f) takes place in a separate thread. The creation of a thread is a synchronization point. Everything that happens before the thread creation is visible in the thread. For symmetry reasons, the same argument holds between (b) and (e).
- **dr (data race)**: Here is the data race between the reading and writing of the variables x and y. The program has undefined behavior.

### Why is the execution consistent?

The execution is consistent because the values x and y are initialized from the values in the main thread (a) and (b). The initialization of the values x and y from the expressions (c) and (d) is not consistent with the memory model.

The next three executions are not consistent.

### 6.4.1.1.2 Second Execution

![](img/d61a6c83410484053b8892275d2fcc4f_367_0.png)

The expression (e) reads in this non-consistent execution the value of y from the expression (d). The writing of (d) happens concurrently with the reading of (e).

### 6.4.1.1.3 Third Execution

![](img/d61a6c83410484053b8892275d2fcc4f_367_1.png)

This execution is symmetric to the previous execution. The expression (f) reads from expression (c) concurrently.

### 6.4.1.1.4 Fourth Execution

![](img/d61a6c83410484053b8892275d2fcc4f_368_0.png)

Fourth execution

Now everything goes wrong. The expressions (e) and (f) read from the expressions (d) and (c) concurrently.

### 6.4.1.1.5 A Short Conclusion

Although I just used the default configuration of CppMem, I got a lot of valuable information and insight. In particular, the graphs from CppMem showed:

- All four combinations of x and y are possible: (0,0), (11,0), (0,2000), and (11,2000).
- The program has at least one data race and, therefore, has undefined behavior.
- Only one of the four possible executions is consistent.

![](img/d61a6c83410484053b8892275d2fcc4f_369_0.png)

### Using volatile

From the memory model perspective, using the qualifier volatile for x and y makes no difference to using non-synchronized access to x and y.

**CppMem: unsynchronized access with volatile**

```cpp
int main() {
  volatile int x = 0;
  volatile int y = 0;
  {{{ {
    x = 2000;
    y = 11;
  }
  ||| {
    y;
    x;
  }
  }}}
}
```

CppMem generates identical graphs as in the previous example. The reason is quite simple, in C++ volatile has no multithreading semantic.

The access to x and y in this example was not synchronized, and we got a data race; therefore, undefined behavior. The most obvious way for synchronization is to use locks.

## 6.4.2 CppMem: Locks

Both threads thread1 and thread2 use the same mutex, wrapped in a std::lock_guard.

**ongoing optimization with locks**

```cpp
// ongoingOptimizationLock.cpp

#include <iostream>
#include <mutex>
#include <thread>

int x = 0;
int y = 0;

std::mutex mut;

void writing(){
  std::lock_guard<std::mutex> guard(mut);
  x = 2000;
  y = 11;
}

void reading(){
  std::lock_guard<std::mutex> guard(mut);
  std::cout << "y: " << y << " ";
  std::cout << "x: " << x << '\n';
}

int main(){
  std::thread thread1(writing);
  std::thread thread2(reading);
  thread1.join();
  thread2.join();
};
```

The program is well-defined. Depending on the execution order (thread1 vs thread2), either both values are either at first read and then overwritten, or are at first overwritten and then read. The following values for x and y are possible.

**Possible values for locks**

| y | x | Values possible? |
|---|---|---|
| 0 | 0 | Yes |
| 11 | 0 |  |
| 0 | 2000 |  |
| 11 | 2000 | Yes |

![](img/d61a6c83410484053b8892275d2fcc4f_370_0.png)

### Using std::lock_guard in CppMem

I could not find a way to use std::lock_guard in CppMem. If you know how to achieve it, please let me know.

Locks are easy to use, but the synchronization is often too heavyweight. I now switch to a more lightweight strategy and use atomics.

## 6.4.3 CppMem: Atomics with Sequential Consistency

If you don't specify the memory-ordering, sequential consistency is applied. Sequential consistency guarantees two properties. Each thread executes its instructions in source code order, and all threads follow the same global order.

Here is the optimized version of the program using atomics.

**ongoing optimization with atomics (sequential consistency)**

```cpp
// ongoingOptimizationSequentialConsistency.cpp

#include <atomic>
#include <iostream>
#include <thread>

std::atomic<int> x{0};
std::atomic<int> y{0};

void writing(){
    x.store(2000);
    y.store(11);
}

void reading(){
    std::cout << y.load() << " ";
    std::cout << x.load() << '\n';
}

int main(){
    std::thread thread1(writing);
    std::thread thread2(reading);
    thread1.join();
    thread2.join();
};
```

Let’s analyze the program. The program is data race free because x and y are atomics. Therefore, only one question is left to answer. What values are possible for x and y? This question is easy to answer. Thanks to the sequential consistency, all threads have to follow the same global order.

It holds true:

- `x.store(2000);` **happens-before** `y.store(11);`
- `std::cout << y.load() << " ";` **happens-before** `std::cout << x.load() << '\n';`

Hence: the value of `x.load()` cannot be 0 if `y.load()` has the value 11, because `x.store(2000)` happens before `y.store(11)`.

All other values for x and y are possible. Here are three possible interleavings resulting in the three different values for x and y.

- thread1 is completely executed before thread2.
- thread2 is completely executed before thread1.
- thread1 executes its first instruction `x.store(2000)` before thread2 is completely executed.

Now all values for x and y.

**Possible values for the atomics (sequential consistency)**

| y | x | Values possible? | # |
|---|---|---|---|
| 0 | 0 | Yes | |
| 11 | 0 | | |
| 0 | 2000 | Yes | |
| 11 | 2000 | Yes | |

Let me verify my reasoning with CppMem.

### 6.4.3.1 CppMem

Here is the corresponding program in CppMem.

**CppMem: atomics (sequential consistency)**

```cpp
1  int main(){
2      atomic_int x = 0;
3      atomic_int y = 0;
4      {{{ [
5          x.store(2000);
6          y.store(11);
7      }
8      ||| [
9          y.load();
10         x.load();
11     }
12     }}}
13 }
```

First, a little bit of syntax. CppMem uses in lines 2 and 3 the typedef atomic_int for std::atomic<int>. When I execute the program, I'm overwhelmed by the number of execution candidates.

![](img/d61a6c83410484053b8892275d2fcc4f_373_0.png)

### Ongoing Optimization (sequential consistency)

There are 384 (1) possible execution candidates, only 6 of them are consistent. No candidate has a data race. I’m only interested in the six consistent executions and ignore the other 378 non-consistent executions. Non-consistent means, for example, that they do not respect the modification order of the memory model.

I use the interface (2) to get the six annotated graphs.

We already know that all values for x and y are possible except for y = 11 and x = 0. These results are possible because of sequential consistency. Now I’m curious, which interleaving of threads produces which values for x and y?

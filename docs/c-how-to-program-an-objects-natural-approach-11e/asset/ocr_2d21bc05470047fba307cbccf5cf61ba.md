+   p) Function `std::async` returns an object of class template ________, which enables inter-thread communication between the thread that calls async and the task async executes. The C++ Core Guidelines recommend using a *future* to return a result from an asynchronous task.

+   q) A `std::latch` is a single-use synchronization tool in your code that remains closed until a specified number of threads reach the latch. At that point, the gateway ________. The gateway serves as a one-time synchronization point, allowing threads to wait until a specified number of threads reach that point.

+   r) Consider a simulation of the painting step in an automated automobile assembly line. Often several computer-controlled robots work together to perform a given step. Let’s assume that cars moving along the assembly line and two robots’ operations are all individually controlled by threads. Once the work on one car finishes, we want to reset everything, advance the assembly line and perform the work again for the next car. The preceding scenario is ideal for a(n) ________, which is like a reusable latch.

# ### 17.5
State whether each of the following is *true* or *false*. If false, explain why.

+   a) For multithreading to be effective, you must have a multiple-processor system.

+   b) For C++11 and C++14, the C++ Standards Committee defined mostly high-level primitives. These capabilities were then used to build lower-level C++17 and C++20 features. They’re also being used to implement the lower-level features coming in C++23 and later.

+   c) Unlike the `accumulate` algorithm, the `reduce` algorithm does not guarantee the order in which elements are processed, which enables `reduce` to be parallelized for better performance.

+   d) When concurrent threads share mutable data and that data is modified by one or more of them, indeterminate results may occur. In such cases, the program’s behavior cannot be trusted.

+   e) Immutable data can be safely accessed by only one thread at a time.

+   f) The C++ Core Guidelines say to minimize the duration of critical sections—that is, the amount of time an object is “locked.” Avoid performing I/O, lengthy calculations and operations that do not require synchronization while holding a lock.

+   g) With a circular buffer: If a producer temporarily operates faster than a consumer, the producer can write additional values into the extra buffer cells, if any are available. This enables the producer to keep busy even though the consumer is not ready to retrieve the current value being produced. If the consumer temporarily operates faster than the producer, the consumer can read additional values (if there are any) from the buffer. This enables the consumer to keep busy even though the producer is not ready to produce additional values.

+   h) Generally, you should create your own concurrent containers.

# ### 17.6 *(Multithreading Terms)*
Define each of the following terms.

+   a) thread

+   b) multithreading

+   c) *runnable state*

+   d) *timed waiting state*

+   e) preemptive scheduling
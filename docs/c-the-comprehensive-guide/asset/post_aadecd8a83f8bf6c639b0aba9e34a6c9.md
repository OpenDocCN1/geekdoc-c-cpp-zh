
```cpp
void div(int x) {
    std::lock_guard lk2(mx_); // inner
    value_ /= x;
}
void mulDiv(int x, int y) {
    std::lock_guard lk3(mx_); // outer
    mul(x);
    div(y);
}
};
int main() {
    MulDiv m{42}; // 3*7*2*5
    m.mulDiv(5, 15);
    std::cout << m.value_ << '\n'; // Output: 14
}
```

**Listing 29.27** Precautions are necessary when a mutex needs to be locked multiple times.

Here, calling `mulDiv` causes `mx_` to be locked with a simple `lock_guard` via `lk3`. From now on, no other thread can perform calculations on this instance `m`. Other threads will have to wait because each method immediately acquires a lock. The main thread then enters `mul`. There, a `lock_guard` via `lk1` locks the same mutex again in the same thread; with a simple `mutex` this would be an error, but with a `recursive_mutex` it is allowed. As soon as `mul` is exited, this inner lock is released again. However, this is not enough for other threads that might already be waiting to proceed. Only when the outer `lk3` releases its lock can the other threads continue.

If you are writing a program where you think a `recursive_mutex` is the solution, it is usually an indication that you should reconsider your design. In a class, a mutex typically protects the encapsulated data. You need a recursive mutex if a public method calls another public method. However, a lock usually exists because the “invariant” of the class is violated in the critical section. Does it sound like a good idea to call a public method while the instance is in an incorrect state? No. It is often better to define a private method that is then called by both public methods. You usually establish the lock at the public level, and the private method can assume that a lock already exists.

## 29.4 In Its Own Storage with “thread_local”

Not all memory is visible to all threads. If you define a variable with `thread_local` in a running thread, only the thread that created it can see it. When the thread terminates, the variable is also removed.

```cpp
// https://godbolt.org/z/j8W7GjTf
#include <iostream>
#include <string>
#include <thread>
#include <mutex>

thread_local unsigned int usage = 0;
static std::mutex cout_mutex;

void use(const std::string thread_name) {
    ++usage;
    std::lock_guard lock(cout_mutex); // Protect output
    std::cout << thread_name << ": " << usage << '\n';
}

int main() {
    std::jthread a(use, "a"), b(use, "b");
    use("main");
}
```

**Listing 29.28** Memory only for the current thread.

You will get the following output (in this or another order):

```
main: 1
b: 1
a: 1
```

The 1 shows that each thread a, b, and main got its own usage variable and did not have to share it with other threads. Otherwise, a 3 would have been displayed at the end.

You use `thread_local` like `static` or `extern` and cannot combine it with these. Within a function, the variable is initialized once per thread, just as `static` would do with only one thread:

```cpp
void func() {
    thread_local vector<int> data{};
    // ...
}
```

## 29.5 Waiting for Events with “condition_variable”

With mutexes and locks, you can go very far, and these form the basis of what you need to work with threads. Sometimes, however, handling mutexes and locks is cumbersome. With `call_once`, you have already seen an alternative way where the standard library assembles the basic building blocks into something new for you. There are a few more of these advanced tools that I will introduce to you here.

A typical scenario with multiple threads is that one produces data and the other waits for it to be ready for processing. These two can communicate with each other via a condition variable `condition_variable`.

```cpp
int main() {
    // a producer:
    std::jthread thProd{produce, 1'000};
    // three consumers
    std::jthread thCon1{consume, '[', ']'};
    std::jthread thCon2{consume, '<', '>'};
    std::jthread thCon3{consume, '{', '}'};
    // wait and finish
    thProd.join();
    thCon1.join(); thCon2.join(); thCon3.join();
    std::cout << '\n';
}
```

**Listing 29.29** Two threads communicate via a condition variable.

Here, there is a producing thread `thProd` in the function `produce` and three consuming threads `thCon1` to `thCon3` in the function `consume`. The latter should output the data. To distinguish which thread handles the output, I use different pairs of brackets, which I pass as parameters to the `consume` function.

The produced data is placed in the global queue `g_data` as quickly as the producer can deliver it. So it may be that `g_data` fills up faster than results can be consumed, but it may also be that the consumers empty `g_data` and really have to wait for new results. In the case of prime number calculation, it initially runs quickly and then gradually slows down. However, 1'000 or even 1'000'000 is far too small a number to notice on modern computers. To output fewer numbers, you can add another test to check if a prime sextuplet is present.

Ignoring the specific computational task, you need to consider the following for parallel programming here:

- Data is exchanged via `g_data`. Changes to this data structure must always be protected. Here I use the mutex `mx` and the corresponding locks for this purpose.
- Whenever data is ready in `g_data`, the producer notifies any waiting threads with `notify_one` that work is ready for pickup.
- On the consuming side, the first consumer locks the mutex `mx`, but this time with `unique_lock lk`. This is important for working with `wait`.
- I then pass the lock `lk` along with a test to the `wait` method of the `condition_variable` to check if there is actually work to be done. Here I test in the lambda if `g_data` actually contains data.
- If the lambda of `wait` returns false, `wait` releases the lock `lk` (hence `unique_lock`, because `lock_guard` does not have an `unlock()` method), so that a producer can

> See https://en.wikipedia.org/wiki/Prime_tuple.

### Advantages of the Condition Variable

The `condition_variable` is designed to hold the necessary locks for as short a time as possible. Thus, during a `wait()` call, the conditions of the lambda may be checked multiple times. For this, the mutex is locked but always immediately unlocked again to allow others to work on the shared data structure.

Rebuilding this by hand is laborious, error-prone, or very likely results in suboptimal code. You should use a `condition_variable`.

### 29.5.2 Synchronize Output

The program output looks something like this if you choose 1'000 as the limit:

```
[3] <5> [11] {7} {13} [19] {23} [29] <17> {31} <41> [47] {43}
{53} <59> [61] {71} {73} [79] <83> {89} [97] <101> {103} [107]
<109> ... <881> [887] [919] <907> [911] [929] [941] [947] <937> [953]
[967] <971> [977] [997] {983} <991>
```

You can tell from the different brackets that the numbers are indeed output by different threads. You can also see that the numbers do not always appear in the correct order. This is an intentional design decision. Often, you want the data to be consumed as quickly as possible. Who consumes it and in what order relative to each other is often irrelevant. Maybe they are independent work orders from the internet. However, if the output order is important, use a different mechanism.

For the output, you see that the output does not happen directly after `cout`, but with an instance `osync` of type `osyncstream`:

```cpp
std::osyncstream osync(std::cout);  // Synchronize output
osync << l << prim << r << ' ';
```

If you omit this, the streams could interrupt each other during output, and the output would be a jumbled mess (to be precise, `undefined`). The `osyncstream` class works similarly to a unique_lock, except you don't need an additional mutex.

Don't have an `osyncstream` available yet? Then define a mutex globally and use a `unique_lock`. Alternatively, you can also collect the output that should be kept together in a `stringstream` first, so that you hold the lock for as short a time as possible:

```cpp
std::mutex g_coutMx;
// ...
std::stringstream ss;
ss << l << prim << r << ' ';
std::lock_guard<std::mutex> l2{g_coutMx};
std::cout << ss.str();
```

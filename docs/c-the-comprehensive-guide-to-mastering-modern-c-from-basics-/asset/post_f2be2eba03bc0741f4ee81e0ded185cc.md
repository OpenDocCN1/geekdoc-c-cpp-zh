
# 29.7 Atomics

I like to give some advice here in the form of light warnings for dealing with an area of C++. Here are the most important guidelines for dealing with atomic:

- Do not use atomic unless you have to.
- Check the success through profiling before and after. Too often, a brilliant “optimization” turns out to be counterproductive.
- Stick to the default memory_order_seq_cst for the operation mode of atomic. The other variants have more runtime benefits than costs in the most extreme situations.

I recommend that you start with a variable protected by a mutex, gather experience, and then—maybe—experiment with atomic.

With that in mind, let me explain what you need atomic for.

You have seen that you can synchronize shared data between threads by locking. Well, locks have a side effect: they lock. That means it can happen that another thread has to wait at a lock, because that's exactly what they are made for. This could be considered suboptimal. Where there is waiting, time is lost. Yes, maybe a little, but don't forget that waiting also frees up resources that another thread can use. The actual loss is small, but it is there. In addition, there are application areas where every waiting can be problematic. For these cases, you need an alternative.

It is possible to achieve one of the following stages of the “guaranteed completion” process, which are referred to as lock-free guarantees:

- Obstruction-free, the weakest guarantee
If a single thread runs in isolation (without any other threads interfering), it will complete its operation in a finite number of steps. No guarantees are made if there is contention from other threads.
- Lock-free
This ensures that at least one thread will make progress in a finite number of steps, even if multiple threads are competing. This means that at least overall progress is achieved.
- Wait-free, the strongest guarantee
Guarantees that every thread will complete its operation in a finite number of steps, regardless of the actions of other threads, thus each thread achieves progress at any time.

You achieve obstruction-free with mutexes, and that is already a success. Lock-free is still an achievable goal if you are willing to put in a lot of effort. This is where atomic comes into play. But beware: the use of atomic is not a guarantee for a lock-free program, nor does a lock-free program necessarily require atomic. Sometimes you can achieve a lot with surprisingly simple tricks (perhaps a copy of the data?). Achieving the highest guarantee would of course be great, but it is incredibly difficult and only possible with a precise understanding of the system and the possible involved data down to the smallest detail. Here, atomic would also come into play, and you would probably even have to resort to the tricks of memory_order possibilities.

The name atomic refers to the temporal indivisibility of an operation. An atomic operation in one thread cannot become partially visible in another thread. The operation either has not started yet or is finished.

atomic is a template class. This means you provide with a type as a parameter, so atomic<T>. In principle, this type can be anything, even one defined by you. In practice, the T falls into one of the following categories, which influence the behavior of atomic<T>:

- atomic<B>, where B is a built-in type
Supports all atomic operations; however, the standard does not guarantee that these are lock-free.
- atomic<U>, where U is a user-defined type
U must be copyable with memcpy (trivially copyable); better yet, comparable with memcmp. The larger the data structure, the less likely it is that lock-freedom can be guaranteed.
- atomic_flag for Boolean operations
The only data type guaranteed to be lock-free—but for the very few operations it supports.

| 29.7.1 | Overview of the Operations |

atomic<T> is not copyable or assignable in the classical sense. When you assign, do not so with another atomic<T>, but with a T—that is, the contained value.

Here is a rough overview of the indivisible operations supported by atomic<T>:

- load or operator T
Reading the stored value; the latter is the implicit conversion to the enclosed type. For an atomic<bool> a, if(!a.load())... is equivalent to if(!a)...
- store or operator=
Stores a value. For an atomic<bool> a, a.store(true) is equivalent to a = true.
- exchange
Sets a new value and returns the old one.
- compare_exchange_weak and compare_exchange_strong
If o is the currently stored value in atomic<T> a, then a.compare_exchange_strong(e, n) roughly executes: if(o==e) { a=n; return true; } else return false }; In this way, you can implement something like “store a value only if no one else has changed it in the meantime.” This way, you can prevent accidentally overwriting something. Note that the comparison is done with memcmp and the assignment with memcpy with potentially overloaded operators.
- Arithmetic with +=, -=, and ++ as well as fetch_add and fetch_sub
The operators perform the usual calculations. The fetch_... methods add or subtract simultaneously return the old value.
- Bitwise arithmetic with |, &=, and ^= as well as fetch_or, fetch_and, and fetch_xor
Performs the usual bitwise arithmetic operations. The fetch... methods return the old value.
- Flag operations test_and_set, clear(), test()
atomic_flag can perform exactly these methods and no others. For this reason, they are also guaranteed to be lock-free. clear sets the stored value to false. test_and_set sets the stored value to true and returns the previously stored value. The test()method, which only reads the current value without changing it, is available from C++20.

You can find out if the operations of an atomic<T> are lock-free by calling is_free(). An example is shown in Listing_29.40.

```cpp
// https://godbolt.org/z/dG31o
#include <iostream>
#include <atomic>

struct Array { int a[100]; };
struct Simple { int x, y; };

int main() {
    std::atomic<Array> carray({});
    std::cout << (carray.is_free()) ? "lock-free" : "locks"
               << '\n';
    // Output: locks
    std::atomic<Simple> simple{};
    std::cout << (simple.is_free()) ? "lock-free" : "locks"
               // Output: lock-free
               << '\n';
}
```
# Listing 29.40 How to determine if the operations are lock-free.

For example, on MSVC 19 and GCC 14 or Clang 18 on x86-64, atomic<Simple> is lock-free, but the large atomic<Array> is not.[86]

When you start with atomic, you should begin with memory_order_seq_cst. This is the default for all operations. On the other hand, if you have already decided to use atomic, if you are aiming for maximum performance. And then you should also keep an eye on the other options you can choose for the constraints on the operations of atomic:

- memory_order_seq_cst
This is the default if you do not specify any additional parameters for the memory order in the methods of atomic<T>. However, it is the most restrictive rule. It states that other operations on this atomic must be completed before or after. seq_cst stands for sequentially consistent. So, for a given execution of operations on an atomic in multiple threads, could still relate each one to others in such a way that you can say it happens before or after. This is called a single total order.
- memory_order_acquire and memory_order_release
Typically, you mark a write operation with release and a read operation with acquire. These are then brought into a before-and-after relationship but not not others.
- memory_order_relaxed
For operations marked this way, you do not set any before-and-after rules. This allows for potentially the

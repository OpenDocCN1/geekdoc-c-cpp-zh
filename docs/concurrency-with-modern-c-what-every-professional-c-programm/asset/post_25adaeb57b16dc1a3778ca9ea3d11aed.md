
## 17.1.6.2 Further Categories

The other categories focus on specific aspects of lock-free programming. The example of each category is available in various forms. Each form using different memory orderings. For an additional discussion to the categories, read the already mentioned paper *Mathematizing C++ Concurrency*⁴. If possible, present the program with sequential consistency.

### 17.1.6.2.1 Store Buffering (examples/SB_store_buffering)

Two threads write to separate locations and then read from the other location.

```c
// SB-sc_sc-sc_sc.c
// Store Buffering (or Dekker's), with all four accesses SC atomics
// Question: can the two reads both see 0 in the same execution?
int main() {
  atomic_int x=0; atomic_int y=0;
  {{{ { y.store(1,memory_order_seq_cst);
        r1=x.load(memory_order_seq_cst); }
    ||| { x.store(1,memory_order_seq_cst);
        r2=y.load(memory_order_seq_cst); } }}}
  return 0;
}
```

### 17.1.6.2.2 Message Passing (examples/MP_message_passing)

One thread writes data (non-atomic) and sets an atomic flag, while the second thread waits for the flag and reads data (non-atomic).

```c
// MP-ma_sc-sc_na.c
// Message Passing, of data held in non-atomic x,
//   with sc atomic stores and loads on y giving release/acquire synchronization
// Question: is the read of x required to see the new data value 1
//   rather than the initial state value 0?
int main() {
  int x=0; atomic_int y=0;
  {{{ { x=1;
        y.store(1,memory_order_seq_cst); }
    ||| { r1=y.load(memory_order_seq_cst).readsvalue(1);
        r2=x; } }}}
  return 0;
}
```

### 17.1.6.2.3 Load Buffering (examples/LB_load_buffering)

Can two reads see the later write of the other thread?

LB=sc_sc+sc_sc

```cpp
// LB=sc_sc+sc_sc
// Load Buffering, with all four accesses sequentially consistent atomics
// Question: can the two reads both see 1 in the same execution?
int main() {
  atomic_int x=0; atomic_int y=0;
  {{{ { r1=x.load(memory_order_seq_cst);
         y.store(1,memory_order_seq_cst); }
     ||| { r2=y.load(memory_order_seq_cst);
           x.store(1,memory_order_seq_cst); } }}}
  return 0;
}
```

### 17.1.6.2.4 Write-to-Read Causality (examples/WRC)

Does the third thread see the write from the first thread?

- The first thread writes to x.
- The second thread reads from that and writes to y.
- The third thread reads from that and then reads x.

WRC=rel+acq_rel+acq_rlx.c

```cpp
// WRC
// the question is whether the final read is required to see 1
// With two release/acquire pairs, it is
int main() {
  atomic_int x = 0;
  atomic_int y = 0;

  {{{ x.store(1,mo_release);
     ||| { r1=x.load(mo_acquire).readsvalue(1);
           y.store(1,mo_release); }
     ||| { r2=y.load(mo_acquire).readsvalue(1);
           r3=x.load(mo_relaxed); }
  }}}
  return 0;
}
```

### 17.1.6.2.5 Independent Reads of Independent Writes (examples/IRIW)

Two threads write to different locations. Can the second thread see those writes in a different order?

IRIW+rel+rel+acq+acq+acq.c

```c
// IRIW with release/acquire
// the question is whether the reading threads have
// to see the writes to x and y in the same order.
// With release/acquire, they do not.
int main() {
  atomic_int x = 0; atomic_int y = 0;
  {{{ x.store(1, memory_order_release);
       y.store(1, memory_order_release);
  ||| { r1=x.load(memory_order_acquire).readsvalue(1);
        r2=y.load(memory_order_acquire).readsvalue(0); }
  ||| { r3=y.load(memory_order_acquire).readsvalue(1);
        r4=x.load(memory_order_acquire).readsvalue(0); }
  }}};
  return 0;
}
```

## 18. Glossary

The idea of this glossary is by no means to be exhaustive but to provide a reference for the essential terms.

### 18.1 address_free

Atomic operations that are lock-free should also be address-free. Address-free means that atomic operations from different processes on the same memory location are atomic.

### 18.2 ACID

A transaction is an action that has the properties Atomicity, Consistency, Isolation, and Durability (ACID). Except for durability, all properties hold for transactional memory in C++.

- Atomicity: either all or no statement of the block is performed.
- Consistency: the system is always in a consistent state. All transactions build a total order.
- Isolation: each transaction runs in complete isolation from the other transactions.
- Durability: a transaction is recorded.

### 18.3 CAS

CAS stands for *compare-and-swap* and is an atomic operation. It compares a memory location with a given value and modifies the memory location if the memory location and the given value are the same. The CAS operations in C++ are called `std::compare_exchange_strong`, and `std::compare_exchange_weak`.

### 18.4 Callable Unit

A callable unit (short callable) is something that behaves like a function. Not only are these named functions but also function objects or lambda expressions. If a callable accepts one argument, it's called unary callable; if taking two arguments, binary callable.

### 18.9 Deadlock

A deadlock is a state in which at least one thread is blocked forever because it waits for the release of a resource that it will never get.

There are two main reasons for deadlocks:

- A mutex has not been unlocked.
- You lock your mutexes in an incorrect order.

### 18.10 Eager Evaluation

In case of eager evaluation, the expression is evaluated immediately. This evaluation strategy is orthogonal to lazy evaluation. Eager evaluation is often called greedy evaluation.

### 18.11 Executor

An executor is an object associated with a specific execution context. It provides one or more execution functions for creating execution agents from a callable function object.

### 18.12 Function Objects

First of all, don't call them functors². That's a *well-defined* term from a branch of mathematics called *category theory*³.

Function objects are objects that behave like functions. They achieve this by implementing the function call operator. As function objects are objects, they can have attributes and, therefore, state.

```cpp
struct Square{
    void operator()(int& i){i= i*i;}
};

std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

std::for_each(myVec.begin(), myVec.end(), Square());

for (auto v: myVec) std::cout << v << " "; // 1 4 9 16 25 36 49 64 81 100
```

²https://en.wikipedia.org/wiki/Functor  
³https://en.wikipedia.org/wiki/Category_theory

### Instantiate function objects to use them

It's a common error that the name of the function object (`Square`) is used in an algorithm instead of the instance of function object (`Square()`) itself: `std::for_each(myVec.begin(), myVec.end(), Square)`. Of course, that's a typical error. You have to use the instance: `std::for_each(myVec.begin(), myVec.end(), Square())`

### 18.13 Lambda Functions

Lambda functions provide their functionality in-place. The compiler gets its information right on the spot and has therefore excellent optimization potential. Lambda functions can receive their arguments by value or by reference. They can capture the variables of their defining environment by value or by reference as well.

```cpp
std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
std::for_each(myVec.begin(), myVec.end(), [](int& i){ i= i*i; });
                                // 1 4 9 16 25 36 49 64 81 100
```

### Lambda functions should be your first choice

If the functionality of your callable is short and self-explanatory, use a lambda function. A lambda function is generally faster than a function or a function object and easier to understand.

### 18.14 Lazy evaluation

In the case of lazy evaluation⁴, the expression is only evaluated if needed. This evaluation strategy is orthogonal to eager evaluation. Lazy evaluation is often called call-by-need.

### 18.15 Lock-free

A non-blocking algorithm is lock-free if there is guaranteed system-wide progress. The following algorithm incrementing the atomic counter is lock-free.

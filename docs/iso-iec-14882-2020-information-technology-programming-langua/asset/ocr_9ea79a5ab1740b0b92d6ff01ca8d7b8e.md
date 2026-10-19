# ISO/IEC 14882:2020(E)

```
std::for_each(std::execution::par_unseq, std::begin(a), std::end(a), [&](int) {
    std::lock_guard<mutex> guard(m);    // incorrect: lock_guard constructor calls m.lock()
    ++x;
});
}
```

The above program may result in two consecutive calls to m.lock() on the same thread of execution (which may deadlock), because the applications of the function object are not guaranteed to run on different threads of execution. — end example]

# 25.3.2 Requirements on user-provided function objects [algorithms.parallel.user]

1 Unless otherwise specified, function objects passed into parallel algorithms as objects of type Predicate, BinaryPredicate, Compare, UnaryOperation, BinaryOperation, BinaryOperation1, BinaryOperation2, and the operators used by the analogous overloads to these parallel algorithms that are formed by an invocation with the specified default predicate or operation (where applicable) shall not directly or indirectly modify objects via their arguments, nor shall they rely on the identity of the provided objects.

# 25.3.3 Effect of execution policies on algorithm execution [algorithms.parallel.exec]

1 Parallel algorithms have template parameters named ExecutionPolicy (20.18) which describe the manner in which the execution of these algorithms may be parallelized and the manner in which they apply the element access functions.

2 If an object is modified by an element access function, the algorithm will perform no other unsynchronized accesses to that object. The modifying element access functions are those which are specified as modifying the object.

> [Note 1: For example, swap, ++, --, @=, and assignments modify the object. For the assignment and @= operators, only the left argument is modified. — end note]

3 Unless otherwise stated, implementations may make arbitrary copies of elements (with type T) from sequences where is_trivially_copy_constructible_v<T> and is_trivially_destructible_v<T> are true.

> [Note 2: This implies that user-supplied function objects cannot rely on object identity of arguments for such input sequences. If object identity of the arguments to these function objects is important, a wrapping iterator that returns a non-copied implementation object such as reference_wrapper<T> (20.14.6), or some equivalent solution, can be used. — end note]

4 The invocations of element access functions in parallel algorithms invoked with an execution policy object of type execution::sequenced_policy all occur in the calling thread of execution.

> [Note 3: The invocations are not interleaved; see 6.9.1. — end note]

5 The invocations of element access functions in parallel algorithms invoked with an execution policy object of type execution::unsequenced_policy are permitted to execute in an unordered fashion in the calling thread of execution, unsequenced with respect to one another in the calling thread of execution.

> [Note 4: This means that multiple function object invocations can be interleaved on a single thread of execution, which overrides the usual guarantee from 6.9.1 that function executions do not overlap with one another. — end note]

The behavior of a program is undefined if it invokes a vectorization-unsafe standard library function from user code called from a execution::unsequenced_policy algorithm.

> [Note 5: Because execution::unsequenced_policy allows the execution of element access functions to be interleaved on a single thread of execution, blocking synchronization, including the use of mutexes, risks deadlock. — end note]

6 The invocations of element access functions in parallel algorithms invoked with an execution policy object of type execution::parallel_policy are permitted to execute either in the invoking thread of execution or in a thread of execution implicitly created by the library to support parallel algorithm execution. If the threads of execution created by thread (32.4.3) or jthread (32.4.4) provide concurrent forward progress guarantees (6.9.2.3), then a thread of execution implicitly created by the library will provide parallel forward progress guarantees; otherwise, the provided forward progress guarantee is implementation-defined. Any such invocations executing in the same thread of execution are indeterminately sequenced with respect to each other.

> [Note 6: It is the caller's responsibility to ensure that the invocation does not introduce data races or deadlocks. — end note]

[Example 1:
    int a[] = {0,1};
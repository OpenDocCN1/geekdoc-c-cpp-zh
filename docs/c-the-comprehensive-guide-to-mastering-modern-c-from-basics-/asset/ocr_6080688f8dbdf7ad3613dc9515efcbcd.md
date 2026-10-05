+   • packaged_task–operator(), get_future(), valid(), reset
Prepares a function for later execution and provides
the result via future.

+   • atomic<T>, atomic_ref<, atomic<shared_ptr<>>, atomic_flag, atomic_int,
etc..load, store, exchange, etc.
Data types whose methods cannot be interrupted by
other threads. For all built-in data types and many of
the aliases, there is a predefined atomic equivalent.
atomic_ref and the specialization for shared_ptr and
floating-point types are available from C++20.

# 29.9.6 “<atomic> Header

+   • memory_order–from cst_seq to relaxed
Depending on the use case, optional parameters for
the methods of the atomic data types.

+   • atomic_thread_fence, atomic_signal_fence
Creates a barrier in the machine code that you can
use to synchronize non-atomic data structures similarly
to an atomic or to synchronize with one.

+   • atomic_load, atomic_store, atomic_exchange, etc.–free
functions
Interaction of a nonatomic data type with an atomic
one.

# 29.9.7 “<coroutine> Header

For writing your own coroutines and
collaborating with
co_yield, co_await, and co_return (from C++20):

+   • coroutine_handle
Pointer to a coroutine that was interrupted with
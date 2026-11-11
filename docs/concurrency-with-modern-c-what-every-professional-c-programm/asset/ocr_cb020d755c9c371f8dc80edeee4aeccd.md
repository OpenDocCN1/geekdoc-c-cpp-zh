# # 18. Glossary

The idea of this glossary is by no means to be exhaustive but to provide a reference for the essential terms.

# ## 18.1 address_free

Atomic operations that are lock-free should also be address-free. Address-free means that atomic operations from different processes on the same memory location are atomic.

# ## 18.2 ACID

A transaction is an action that has the properties Atomicity, Consistency, Isolation, and Durability (ACID). Except for durability, all properties hold for transactional memory in C++.

+   * Atomicity: either all or no statement of the block is performed.
+   * Consistency: the system is always in a consistent state. All transactions build a total order.
+   * Isolation: each transaction runs in complete isolation from the other transactions.
+   * Durability: a transaction is recorded.

# ## 18.3 CAS

CAS stands for *compare-and-swap* and is an atomic operation. It compares a memory location with a given value and modifies the memory location if the memory location and the given value are the same. The CAS operations in C++ are called `std::compare_exchange_strong`, and `std::compare_exchange_weak`.

# ## 18.4 Callable Unit

A callable unit (short callable) is something that behaves like a function. Not only are these named functions but also function objects or lambda expressions. If a callable accepts one argument, it's called unary callable; if taking two arguments, binary callable.
![](bbox=[0.271, 0.108, 0.717, 0.338])

Release-acquire and release consume ordering

At the risk of repeating myself, I want to add a few words explaining why the first program, `acquireRelease.cpp` is well-defined.

The store operation on line 17 *synchronizes-with* the load operation on line 23. The reason is that the store operation uses `std::memory_order_release` and the load operation uses `std::memory_order_acquire`. This store/load relation is the synchronization. What are the ordering constraints for the release-acquire operations? The release-acquire ordering guarantees that all operations' results before the store operation (line 16) are available after the load operation (line 21). So also, the release-acquire operation orders access to the non-atomic variable data (line 14) and the atomic variable `atoData` (line 15). That holds although `atoData` uses the `std::memory_order_relaxed` memory ordering.

The crucial question is: what happens if I replace `std::memory_order_acquire` with `std::memory_order_consume`?

# #### 2.4.4.4 Data dependencies with `std::memory_order_consume`

`std::memory_order_consume` deals with data dependencies on atomics. Data dependencies exist in two ways. First, let us look at *carries-a-dependency-to* in a thread and *dependency-ordered-before* between two threads. Both dependencies introduce a *happens-before* relation. These are the kind of relations we are looking for. What does *carries-a-dependency-to* and *dependency-ordered-before* mean?

+   - *carries-a-dependency-to*: if the result of operation A is used as an operand in operation B, then: A *carries-a-dependency-to* B.
+   - *dependency-ordered-before*: a store operation (with `std::memory_order_release`, `std::memory_order_acq_rel`, or `std::memory_order_seq_cst`) is *dependency-ordered-before* a load operation B (with `std::memory_order_consume`) if the result of load operation B is used in a further operation C in the same thread. It is important to note that operations B and C have to be in the same thread.
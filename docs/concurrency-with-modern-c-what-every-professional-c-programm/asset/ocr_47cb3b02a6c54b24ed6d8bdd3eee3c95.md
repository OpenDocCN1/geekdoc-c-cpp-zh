```
```cpp
33    for(auto& thr: vecUnsyn) thr.join();
34
35    cout << "\n\n";
36
37 }
```
```

I let the synchronized block sleep for a nanosecond (line 16). At the same time, I access the output stream `std::cout` without a synchronized block (line 30). In total, 20 threads increment the global variable `i`, half of them without synchronization. The output shows the issue.

![](bbox=[0.055, 0.365, 0.945, 0.65])

A data race with synchronized blocks

I put red circles around the issues in the output. These are the locations where at least two threads write `std::cout` at the same time. The C++11 standard guarantees that the characters are written atomically; that is not an issue. What is worse is that the variable `i` is written by at least two threads. This is a data race; hence, the program has undefined behavior. If you look carefully at the output, you see a data race in action. The final result for the counter is 199 but should be 200. This means one of the intermediate values of the counter was overwritten.

The total order of synchronized blocks also holds for atomic blocks.

# ### 7.3.2.2 Atomic Blocks

You can execute transaction-unsafe code in a synchronized block but not in an atomic block. Atomic blocks are available in three forms: `atomic_noexcept`, `atomic_commit`, and `atomic_cancel`. The three suffixes `_noexcept`, `_commit`, and `_cancel` define how an atomic block manages an exception:

+   - `atomic_noexcept`: If an exception is thrown, `std::abort` is called, and the program aborts.
+   - `atomic_cancel`: In the default case, `std::abort` is called. This does not hold if a transaction-safe exception is thrown that is responsible for ending the transaction. In this case, the transaction is canceled, put to its initial state, and the exception is thrown.
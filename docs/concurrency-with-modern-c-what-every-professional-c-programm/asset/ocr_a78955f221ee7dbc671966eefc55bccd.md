Let's first look at the example without thread t3. The atomic store on line 15 synchronizes-with the atomic load in line 19. The synchronization guarantees that all that happens before the store is available after the load. This means, in particular, that the access to the non-atomic variable somethingShared is not a data race.

What changes if I use the thread t3? Now there seems to be a data race. As I already mentioned, the first call to atom.fetch_sub(1, std::memory_order_acquire) (line 19) has an acquire-release semantic with atom.store(2, std::memory_order_release) (line 15); therefore, there is no data race on somethingShared.

This does not hold for the second call to atom.fetch_sub(1, std::memory_order_acquire). It is a ready-modify-write operation without a std::memory_order_release tag. It means in particular, that the second call to atom.fetch_sub(1, std::memory_order_acquire) does not synchronize-with the first call, and a data race may occur on sharedVariable. May because thanks to the release sequence, this does not happen. The release sequence is extended to the second call to atom.fetch_sub(1, std::memory_order_acquire); therefore, the second call atom.fetch_sub(1, std::memory_order_acquire) has a happens-before relation with the first call.

Finally, here is the output of the program.

![](bbox=[0.19, 0.435, 0.52, 0.64])

A release sequence

More formally, the N4659: Working Draft, Standard for Programming Language C++17.

# ## Release Sequence

A release sequence headed by a release operation A on an atomic object M is a maximal contiguous sub-sequence of side effects in the modification order of M, where the first operation is A, and every subsequent operation * is performed by the same thread that performed A, or * is an atomic read-modify-write operation.

1) http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/n4659.pdf
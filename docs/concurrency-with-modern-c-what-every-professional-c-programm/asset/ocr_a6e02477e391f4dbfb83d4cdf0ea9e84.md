![](bbox=[0.27, 0.117, 0.73, 0.45])

Deterministic destruction with scoped locking

The scope of scopedLock1 ends at the end of the main function. Consequently, mutex1 is unlocked. The same holds for mutex2 in line 31 and mutex3 in line 38. They are automatically unlocked at the end of their local scopes (lines 33 and 41). For mutex3, the destructor of the scopedLock3 is also invoked if an exception occurs. Interestingly, mutex3 reuses the memory of mutex2 because both have the same address.

C++17 supports locks in four variations. C++ has a std::lock_guard/std::scoped_lock for the simple, and a std::unique_lock/std::shared_lock for the advanced use cases such as the explicit locking or unlocking of the mutex. You can read the details in the subsection locks.

# ### 9.2.1.1 Further Information

+   * Pattern-Oriented Software Architecture: Patterns for Concurrent and Networked Objects^14

# ## 9.2.2 Strategized Locking

Assume you write code such as a library, which should be used in various domains, including concurrent ones. To be on the safe side, you protect the critical sections with a lock. If your library now runs in a single-threaded environment, you have a performance issue because you implemented an expensive synchronization mechanism that is unnecessary. Now, strategized locking comes to your rescue.
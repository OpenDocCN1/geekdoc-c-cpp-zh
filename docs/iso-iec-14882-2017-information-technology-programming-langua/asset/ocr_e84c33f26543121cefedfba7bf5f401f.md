# ISO/IEC 14882:2017(E)

template <class L1, class L2, class L3> void lock(L1&, L2&, L3&);

Requires: Each template parameter type shall meet the Lockable requirements, [Note: The unique-lock class template meets these requirements when instantiated. — end note];

Effects: All arguments are locked via a sequence of calls to lock(), try_lock(), and unlock() on argument. The sequence of calls shall not result in deadlock, unless otherwise specified.[Note: A deadlock avoidance algorithm such as try-and-back must be used, but the specific algorithm is not specified to avoid over-constraining implementations.—end note] If a call to lock() or try_lock() throws an exception, unlock() shall be called for any argument that has been locked by a call to lock() or try_lock().

# 33.4.6 Call once [thread.once]

# 33.4.6.1 Struct once_flag [thread.once.once_flag]

```
namespace std {
    struct once_flag;
    constexpr once_flag(const once_flag&) = delete;
    once_flag& operator=(const once_flag&) = delete;
};
```

+   1 The once_flag is an opaque data structure that call_once is used to initialize data without causing a data race or deadlock.

constexpr once_flag() noexcept;

+   2 Effects: Constructs an object of type once_flag.

+   3 Synchronization: The construction of a once_flag object is not synchronized.

+   4 Postconditions: The object's internal state is set to indicate an invocation of call_once as its initial argument that no function has been called.

# 33.4.6.2 Function call_once [thread.once.callonce]

```
template<class Callable, class... Args>
void call_once(once_flag& flag, Callable&& f, Args&&... args);
```

+   1 Requires:
   INVOKE(forward<Callable>(f), forward<Args>(args)...) 
   (23.14.3) shall be a valid expression.

+   2 Effects: An execution of call_once that does not call the func is a passive execution. An execution of call_once(forward<Callable>(f), forward<Args>(args)...) is an active execution. If such a call throws an exception the execution is exceptional, otherwise it is returning. An exceptional execution shall propagate the exception to the call_once caller. After all executions of call_once for any once_flag: at most one shall be a returning execution; if there is a returning execution, it shall be the last active execution; and there are passive executions. Passive executions allow other threads to reliably observe the results produced by the earlier execution.—end note

+   3 Synchronization: For any given once_flag, all active executions occur in a total order; completion of an active execution synchronizes with (4.7) the start of the next one in this order; and the returning execution synchronizes with the return from all passive executions.
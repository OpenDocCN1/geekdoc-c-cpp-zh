# ISO/14882:2017(E)

```
template <class Class, Args...>
future<invoke_result<decay_t<F>, decay_t<Args...>>>
nasync(F&& f, Args&&... args);
```

```
template <class Class, Args...>
future<invoke_result<decay_t<F>, decay_t<Args...>>>
async(launch policy, F&& f, Args&&... args);
```

2 Requires: F and each T in Args shall satisfy the MoveConstructible requirements, and
INVOKE_DECAY(std::forward(f))
DECAY_DECAY(std::forward(args))... // see 23.14.3, 33.3.2

3 Effects: The future behaves the same as a call to the function with a policy of
lasync | launch; the deferred and the same arguments for F and Args. The second function
creates a shared state that is associated with the returned future. The future behavior of
the shared state depends on the policy used (if more than one of these conditions
aplies, the implementation may choose any of the asynchronous shared state.

(3.1) If lasync is chosen, it calls INVOKE_DECAY(std::forward(f)) and DECAY-
std_DECAY(std::forward(args))... as in 23.14.3, 33.3.2; if a new thread of execution
is represented by a thread object with the shared state is created and called async.
Any return value is stored as the result in the shared state. Any exception
propagated from the execution of INVOKE_DECAY(std::forward(f)), and DECAY-
std_DECAY(std::forward(args))... is stored in the future.
The stored in the shared state and affects the behavior of any asynchronous
object that returns from that shared state.

(3.2) If deferred is set, the shared state is stored; INVOKE_DECAY(std::forward(f)) and DECAY-
std_DECAY(std::forward(args))... shared. These copies of f and args consist-
ter deferred future. Invocation of the future evaluates INVOKE_DECAY(std::move(g));
std::move(xyz) where xyz is the value of shared state; INVOKE_DECAY(std::forward(args))... and xyz
is stored in the shared state. Any exception propagated from the execution of the
future is stored as the exceptional result in the shared state. The shared state is not
ready until the function is invoked, which may be done from any thread.
asynchronous return of that shared state shall invoke the deferred function
on the thread that is calling the waiting function. Any invocation of INVOKE_DECAY(std::move(g),
std::move(xyz)) begins, the future is no longer considered valid [Note: If this is
specified together with other policies, such as when using a value of launch: async |
lauch: deferred, implementations should defer selection or the policy when
no concurrency can be effectively exploited. — end note]

(3.3) If no value is set or value not specified in this document
by the implementation, the future returns a default-constructed value.

4 Returns: An object of type invoke_result<decay_t<F>, decay_t<Args>> that refers to
the shared state outside the local scope, other code that calls this to async. [Note: If a future obtained from
async is moved the future should be aware that the future's destructor
may be blocked for the shared state to become ready. — end note]

5 Synchronization: Regardless of the provided policy argument,

(5.1) the invocation of async with (4.7) the invocation of f. [Note: This statement applies
even when the corresponding future object is moved to another. — end note];
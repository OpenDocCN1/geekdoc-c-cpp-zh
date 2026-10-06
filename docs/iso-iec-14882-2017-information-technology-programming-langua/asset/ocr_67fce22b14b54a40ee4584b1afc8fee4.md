# ISO/IEC 14882:2017(E)

(5.2) the completion of the function f is sequenced before (4.7) the shared state is made ready. [Note: f might not be called at, so its completion might never happen. — end note]

If the implementation chooses the launch::async policy,

+   (5.3) a call to a waiting function on an asynchronous return object shares the shared state created by this async call shall block until the associated thread has joined, or else time out (3.3.2.5);

+   (5.4) the associated thread synchronizes with (4.7) the first function that successfully detects the ready status of the shared state or with the return from the last function that releases the shared state, whichever happens first.

6 Throws: system_error if policy == launch::async and the implementation is unable to start a new thread, or std::bad_alloc if memory for the data structures could not be allocated.

7 Error conditions:

+   (7.1) resource_unavailable_try_again — if policy == launch::async and the system is unable to start a new thread.

8 Example:
```cpp
int work1(int value);
int work2(int value);
int work3(int value) {
    auto handle = std::async([=]{ return work2(value); });
    int tmp = work3(value);
    return tmp + handle.get();
}
```

> [Note: #1 might not result in concurrency because the async call uses the default policy, which might use defer; the lambda not be invoked until the get() called; in that case, work1 and work2 are called on the same thread and there is no concurrency. — end note — end example]

# 33.6.10 Class template packaged_task [futures]

1 The class packaged_task defines a type for wrapping a future object so that the return value of the function or callable object is stored in a future (whether normal or exceptional) stored in the shared state.

2 When the packaged_task object is invoked, its stored state is invoked and the shared state will then be able to access the stored state.

```
namespace std {

template<class> class packaged_task; // not defined

template<class R, class... Args>
class packaged_task<R(Args...)> {
public:
    // construction and destruction
    packaged_task() noexcept;
    template<class F>
    explicit packaged_task(F&& f);
    -packaged_task();

    // no copy
    packaged_task(const packaged_task&&) = delete;
    packaged_task& operator=(const packaged_task&&) = delete;
};
```

33.6.10 ©ISO/IEC 2017 — All rights reserved
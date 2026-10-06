# ISO/IEC 14882:2017(E)

4 Throws: system_error when an exception is required (33.2.2), or any exception thrown by func.

5 [Example:

```
// global flag, regular flag
void init(){
std::once_flag flag;
}

void f(){
std::call_once(flag, init);
}

// static flag, function object
struct initializer {
void operator()();
};

void g(){
static std::call_once(flag2, initializer());
}

// object flag, member function
class information {
std::once_flag verified;
void verifier();
public:
void verifier() { std::call_once(verified, &information::verifier, *this); }
};

```

# 33.5 Condition variables

+   1 Condition variables provide synchronization primitives to block a thread until notified by some other thread that some condition is met or only wait until a system time is reached. Class condition_variable provides a condition variable that can only wait on an object of type unique_lock<mutex>. Condition_variable_any provides a general condition variable that can wait on objects of user-supplied types.

+   2 Condition variables permit concurrent invocation of the wait, wait_for, wait_until, notify_one and notify_all member functions.

+   3 The execution of notify_one and notify_all shall be atomic. The execution of wait, wait_for, and wait_until shall be performed in three atomic parts:
1 the release of the mutex and entry into the waiting state;
2 the unblocking of the wait; and
3 the reacquisition of the lock.

+   4 The implementation shall behave as if all executions of notify_one, notify_all, and each part of the wait, wait_for, and wait_until executions are executed in a single unspecified order consistent with the 'happens before' order.

+   5 Condition variable construction and destruction need not be synchronized.
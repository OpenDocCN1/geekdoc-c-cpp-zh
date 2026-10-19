# 32.5.7 Call once [thread.once]

# 32.5.7.1 Struct once_flag [thread.once.onceflag]

```
namespace std {
    struct once_flag {
        constexpr once_flag() noexcept;

        once_flag(const once_flag&) = delete;
        once_flag& operator=(const once_flag&) = delete;
    };
}
```

1 The class once_flag is an opaque data structure that call_once uses to initialize data without causing a data race or deadlock.

```
constexpr once_flag() noexcept;
```

2 Synchronization: The construction of a once_flag object is not synchronized.

3 Postconditions: The object’s internal state is set to indicate to an invocation of call_once with the object as its initial argument that no function has been called.

# 32.5.7.2 Function call_once [thread.once.callonce]

```
template<class Callable, class... Args>
    void call_once(once_flag& flag, Callable&& func, Args&&... args);
```

1 Mandates: is_invocable_v<Callable, Args...> is true.

2 Effects: An execution of call_once that does not call its func is a passive execution. An execution of call_once that calls its func is an active execution. An active execution calls INVOKE(std::forward<Callable>(func), std::forward<Args>(args)...). If such a call to func throws an exception the execution is exceptional, otherwise it is returning. An exceptional execution propagates the exception to the caller of call_once. Among all executions of call_once for any given once_flag: at most one is a returning execution; if there is a returning execution, it is the last active execution; and there are passive executions only if there is a returning execution.

[Note 1: Passive executions allow other threads to reliably observe the results produced by the earlier returning execution. — end note]

3 Synchronization: For any given once_flag: all active executions occur in a total order; completion of an active execution synchronizes with (6.9.2) the start of the next one in this total order; and the returning execution synchronizes with the return from all passive executions.

4 Throws: system_error when an exception is required (32.2.2), or any exception thrown by func.

5 [Example 1:

```
// global flag, regular function
void init();
std::once_flag flag;

void f() {
    std::call_once(flag, init);
}

// function static flag, function object
struct initializer {
    void operator()();
};

void g() {
    static std::once_flag flag2;
    std::call_once(flag2, initializer());
}

// object flag, member function
class information {
    std::once_flag verified;
```
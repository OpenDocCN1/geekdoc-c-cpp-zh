# The member function get using std::thread

```
```cpp
T get() {
    std::thread t([this] { coro.resume(); });
    t.join();
    return coro.promise().result;
}
```
```

Where I join the thread t after the call return coro.promise().result, the program would have undefined behavior. In the following implementation of the function get, I use a std::jthread. Since std::jthread automatically joins when it goes out of scope. This is too late.

# The member function get using std::jthread

```
```cpp
T get() {
    std::jthread t([this] { coro.resume(); });
    return coro.promise().result;
}
```
```

In this case, the client likely gets its result before the promise prepares it using the member function return_value. Now, result has an arbitrary value, and therefore so does res.

![](bbox=[0.18, 0.61, 0.82, 0.71])

Execution on another thread

There are other possibilities to ensure that the thread is done before the return call.

+   - Create a std::jthread in its scope.

```
```cpp
T get() {
    {
        std::jthread t([this] { coro.resume(); });
    }
    return coro.promise().result;
}
```
```

+   - Make std::jthread a temporary object
If a coroutine should continue with another coroutine, it must return a special Awaiter in its `final_suspend` call (line 9). Additionally, the `promise_type` must store the handle to the coroutine to be continued (line 7). If there is no continuation, you should set the continuation handle to a `nullptr`: `std::coroutine_handle<> continuationHandle = nullptr;`

The special Awaiter `ContinuationAwaiter` continues in the member function `await_suspend`. It gets the coroutine handle, checks if the continuation handle is set (line 22), and returns the continuation handle. The coroutine is suspended in this case, but the returned coroutine is immediately resumed. If the coroutine handle is not set, `std::noop_coroutine` is returned. This means the control flow immediately returns to the caller without resuming a coroutine. A `std::noop_coroutine` call creates a coroutine handle `std::noop_coroutine_handle`. Calling `resume`, `destroy`, `address`, or `done` on a `std::noop_coroutine_handle` has no effect.

# ### 6.1.4.3 `std::suspend_always` and `std::suspend_never`

The C++20 standard already defines two basic Awaiters: `std::suspend_always`, and `std::suspend_never`.

As its name suggests, the Awaiter `suspend_always` always suspends. Therefore, the call `await_ready` returns false.

The Awaiter `std::suspend_always`

```
```cpp
struct suspend_always {
  constexpr bool await_ready() const noexcept { return false; }
  constexpr void await_suspend(std::coroutine_handle<>) const noexcept {}
  constexpr void await_resume() const noexcept {}
};
```
```

The opposite holds for `suspend_never`. It never suspends and, hence, the call `await_ready` returns true.

The Awaiter `std::suspend_never`

```
```cpp
struct suspend_never {
  constexpr bool await_ready() const noexcept { return true; }
  constexpr void await_suspend(std::coroutine_handle<>) const noexcept {}
  constexpr void await_resume() const noexcept {}
};
```
```

The Awaiters `std::suspend_always` and `std::suspend_never` are the basic building blocks for functions, such as `initial_suspend` and `final_suspend`. Both functions are automatically executed when the coroutine is executed: `initial_suspend` at the beginning and `final_suspend` at the end of the coroutine.

# ISO/IEC 14882:2017(E)

For example, concurrent accesses through references returned by `shared_future::get()` (33.6.8) must use read-only operations or provide additional synchronization. — end note

## 33.6.6 Class template promise [futures.promise]

```cpp
namespace std {
    template <class R>
    class promise {
    public:
        promise();
        template <class Allocator>
        promise(Allocator& arg_t, const Allocator& rhs) noexcept;
        promise(promise&& rhs) noexcept;
        promise(const promise& rhs) = delete;
        ~promise();

        // assignment
        promise& operator=(promise&& rhs) noexcept;
        promise& operator=(const promise& rhs) = delete;
        void swap(promise&& other) noexcept;

        // retrieving the result
        future<R> get_future();

        // setting the result
        void set_value(see below);
        void set_exception(exception_ptr ptr);

        // setting the result with deferred notification
        void set_value_at_thread_exit(see below);
        void set_exception_at_thread_exit(exception_ptr ptr);
    };

    template <class R>
    void swap(promise<R>& x, promise<R>& y) noexcept;

    template <class R, class Alloc>
    struct uses_allocator<promise<R>, Alloc>;
}
```

- 1. The implementation will provide the template promise and two specializations, `promise<void>`. These differ only in the argument type of the member functions `set_value` and `set_value_at_thread_exit`, as set out in their descriptions.

- 2. The `set_value`, `set_exception`, `set_value_at_thread_exit`, and `set_exception_at_thread_exit` member functions as though they acquire a shared mutex with the promise object while updating the promise object.

```cpp
template <class R, class Alloc>
    struct uses_allocator<promise<R>, Alloc>
        : true_type { };
```

- 3. Requires: Alloc shall be an Allocator (20.5.3.5).

```cpp
promise();
template <class Allocator>
    promise(allocator_arg_t, const Allocator& rhs);
```

- 4. Effects: constructs a promise object and a shared state. The second constructor uses the allocator to allocate memory for the shared state.

```cpp
promise(promise&& rhs) noexcept;
```

- 5. Effects: constructs a new promise object and transfers ownership of the shared state of rhs (if any) to the newly-constructed object.

- 6. Postconditions: rhs has no shared state.

```cpp
-promise();
```

- 7. Effects: Abandons any shared state (33.6.5).

```cpp
promise& operator=(promise&& rhs) noexcept;
```

- 8. Effects: Abandons any shared state (33.6.5) and if promise(std::move(rhs)).swap(*this).

- 9. Returns: *this.

```cpp
void swap(promise&& other);
```

- 10. Effects: Exchanges the shared state of *this and other.

- 11. Postconditions: *this has the shared state (if any) that other had prior to the swap. other has the shared state (if any) that this had prior to the swap.

```cpp
future<R> get_future();
```

- 12. Returns: A future<R> with the same shared state as *this.

- 13. Throws: future_error if this has no shared state or if get_future has already been called on a promise with the same state as *this.

- 14. Error conditions:

    - future_retrieved if get_future has already been called on a promise with the shared state as *this.
    - no_state if *this has no shared state.

```cpp
void promise::set_value(const R& r);
void promise<R>::set_value(R&& r);
void promise<R>::set_value(R&& r);
void promise<void>::set_value();
```

- 15. Effects: Atomically stores the r in the shared state and makes that state ready (33.6.5).

- 16. Error conditions:

    - future_error if its shared state already has a stored value or exception,
    - for the first version, any exception thrown by the constructor to copy an object of R,
    - for the second version, any exception thrown by the constructor to select an object of R.

- 17. Error conditions:

    - promise_already_satisfied if its shared state already has a stored value or exception.
    - no_state if *this has no shared state.

```cpp
void set_exception(exception_ptr ptr);
```

- 18. Requires: p is not null.

- 19. Effects: Atomically stores the exception pointer p in the shared state and makes that state ready (33.6.5).

- 20. Throws: future_error if its shared state already has a stored value or exception.

- 21. Error conditions:

    - (21.1) promise_already_satisfied if its shared state already has a stored value or exception.
    - (21.2) no_state if *this has no shared state.

```cpp
void promise::set_value_at_thread_exit(const R& r);
void promise<R>::set_value_at_thread_exit(R&& r);
void promise<R>::set_value_at_thread_exit(R&& r);
void promise<void>::set_value_at_thread_exit();
```

- 22. Effects: The future stores r in the shared state without making that ready immediately. Schedules to be ready when the thread exits, after all objects of storage have destroyed.

- 23. Throws:

    - (23.1) future_error if its shared state already has a stored value or exception,
    - (23.2) for the first version, any exception thrown by the constructor to copy an object of R, or
    - (23.3) for the second version, any exception thrown by the constructor to select an object of R.

- 24. Error conditions:

    - (24.1) promise_already_satisfied if its shared state already has a stored value or exception.
    - (24.2) no_state if *this has no shared state.

```cpp
void set_exception_at_thread_exit(exception_ptr ptr);
```

- 25. Requires: p is not null.

- 26. Effects: Atomically stores the exception pointer p in the shared state and makes that state ready (33.6.5).

- 27. Throws: future_error if its shared state already has a stored value or exception.

- 28. Error conditions:

    - (28.1) promise_already_satisfied if its shared state already has a stored value or exception.
    - (28.2) no_state if *this has no shared state.

## 33.6.7 Class template future [unique_future]

The class future defines a type for asynchronous return which do not share their state. A default-constructed future has no shared state. A future with shared state can be created by move from a future which shares its state.

The effect of calling any member function other than the destructor, the move-assignment operator, share, or valid on a future for which valid() == false is undefined. Implementations should detect this case and throw an object of type future_error with an error condition future_errc::no_state.

```cpp
namespace std {
    template <class R>
    class future {
    public:
        future() noexcept;
        future(future&& rhs) = delete;
        future& operator=(const future& rhs) = delete;
        future& operator=(future&&) noexcept;
        shared_future<R> share() noexcept;

        // retrieving the value
        R get();

        // functions to check state
        bool wait() const noexcept;
        template<class Rep, class Period>
        future_status wait_for(const chrono::duration<Rep, Period>& rel_time) const;
        template<class Clock, class Duration>
        future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
    };
}
```

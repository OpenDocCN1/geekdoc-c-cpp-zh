
## 32.9 Futures [futures]

### 32.9.1 Overview [futures.overview]

32.9 describes components that a C++ program can use to retrieve in one thread the result (value or exception) from a function that has run in the same thread or another thread.

> [Note 1: These components are not restricted to multi-threaded programs but can be useful in single-threaded programs as well. — end note]

### 32.9.2 Header <future> synopsis [future.syn]

```cpp
namespace std {
    enum class future_errc {
        broken_promise = implementation-defined,
        future_already_retrieved = implementation-defined,
        promise_already_satisfied = implementation-defined,
        no_state = implementation-defined
    };

    enum class launch : unspecified {
        async = unspecified,
        deferred = unspecified,
        implementation-defined
    };

    enum class future_status {
        ready,
        timeout,
        deferred
    };
}
```

```cpp
void wait(arrival_token&& arrival) const;
```

Preconditions: arrival is associated with the phase synchronization point for the current phase or the immediately preceding phase of the same barrier object.

Effects: Blocks at the synchronization point associated with std::move(arrival) until the phase completion step of the synchronization point’s phase is run.

> [Note 3: If arrival is associated with the synchronization point for a previous phase, the call returns immediately. — end note]

Throws: system_error when an exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

```cpp
void arrive_and_wait();
```

Effects: Equivalent to: wait(arrive()).

```cpp
void arrive_and_drop();
```

Preconditions: The expected count for the current barrier phase is greater than zero.

Effects: Decrements the initial expected count for all subsequent phases by one. Then decrements the expected count for the current phase by one.

Synchronization: The call to arrive_and_drop strongly happens before the start of the phase completion step for the current phase.

Throws: system_error when an exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

> [Note 4: This call can cause the completion step for the current phase to start. — end note]

Throws: system_error when an exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

> [Note 2: This call can cause the completion step for the current phase to start. — end note]

```cpp
template<> struct is_error_code_enum<future_errc> : public true_type { };
error_code make_error_code(future_errc e) noexcept;
error_condition make_error_condition(future_errc e) noexcept;

const error_category& future_category() noexcept;

class future_error;

template<class R> class promise;
template<class R> class promise<R&>;
template<> class promise<void>;

template<class R>
  void swap(promise<R>& x, promise<R>& y) noexcept;

template<class R, class Alloc>
  struct uses_allocator<promise<R>, Alloc>;

template<class R> class future;
template<class R> class future<R&>;
template<> class future<void>;

template<class R> class shared_future;
template<class R> class shared_future<R&>;
template<> class shared_future<void>;

template<class> class packaged_task; // not defined
template<class R, class... ArgTypes>
  class packaged_task<R(ArgTypes...)>;

template<class R, class... ArgTypes>
  void swap(packaged_task<R(ArgTypes...)>&, packaged_task<R(ArgTypes...)>&) noexcept;

template<class F, class... Args>
  [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(F&& f, Args&&... args);
template<class F, class... Args>
  [[nodiscard]] future<invoke_result_t<decay_t<F>, decay_t<Args>...>>
    async(launch policy, F&& f, Args&&... args);
}
```

1 The enum type launch is a bitmask type (16.3.3.3.4) with elements launch::async and launch::deferred.

> [Note 1: Implementations can provide bitmasks to specify restrictions on task interaction by functions launched by async() applicable to a corresponding subset of available launch policies. Implementations can extend the behavior of the first overload of async() by adding their extensions to the launch policy under the “as if” rule. — end note]

2 The enum values of future_errc are distinct and not zero.

### 32.9.3 Error handling [futures.errors]

```cpp
const error_category& future_category() noexcept;
```

1 Returns: A reference to an object of a type derived from class error_category.

2 The object’s default_error_condition and equivalent virtual functions shall behave as specified for the class error_category. The object’s name virtual function returns a pointer to the string "future".

```cpp
error_code make_error_code(future_errc e) noexcept;
```

3 Returns: error_code(static_cast<int>(e), future_category()).

```cpp
error_condition make_error_condition(future_errc e) noexcept;
```

4 Returns: error_condition(static_cast<int>(e), future_category()).

- (7.1.2) — makes its shared state ready;
- (7.2) — second, the provider releases its shared state.

8 A shared state is ready only if it holds a value or an exception ready for retrieval. Waiting for a shared state to become ready may invoke code to compute the result on the waiting thread if so specified in the description of the class or function that creates the state object.

9 Calls to functions that successfully set the stored result of a shared state synchronize with (6.9.2) calls to functions successfully detecting the ready state resulting from that setting. The storage of the result (whether normal or exceptional) into the shared state synchronizes with (6.9.2) the successful return from a call to a waiting function on the shared state.

10 Some functions (e.g., promise::set_value_at_thread_exit) delay making the shared state ready until the calling thread exits. The destruction of each of that thread's objects with thread storage duration (6.7.5.3) is sequenced before making that shared state ready.

11 Access to the result of the same shared state may conflict (6.9.2).

> [Note 4: This explicitly specifies that the result of the shared state is visible in the objects that reference this state in the sense of data race avoidance (16.4.6.10). For example, concurrent accesses through references returned by shared_future::get() (32.9.8) must either use read-only operations or provide additional synchronization. — end note]

### 32.9.6 Class template promise [futures.promise]

```cpp
namespace std {
  template<class R>
  class promise {
  public:
    promise();
    template<class Allocator>
    promise(allocator_arg_t, const Allocator& a);
    promise(promise&& rhs) noexcept;
    promise(const promise&) = delete;
    ~promise();

    // assignment
    promise& operator=(promise&& rhs) noexcept;
    promise& operator=(const promise&) = delete;
    void swap(promise& other) noexcept;

    // retrieving the result
    future<R> get_future();

    // setting the result
    void set_value(see below);
    void set_exception(exception_ptr p);

    // setting the result with deferred notification
    void set_value_at_thread_exit(see below);
    void set_exception_at_thread_exit(exception_ptr p);
  };

  template<class R>
    void swap(promise<R>& x, promise<R>& y) noexcept;

  template<class R, class Alloc>
    struct uses_allocator<promise<R>, Alloc>;
}
```

1 The implementation provides the template promise and two specializations, promise<R&> and promise<void>. These differ only in the argument type of the member functions set_value and set_value_at_thread_exit, as set out in their descriptions, below.

2 The set_value, set_exception, set_value_at_thread_exit, and set_exception_at_thread_exit member functions behave as though they acquire a single mutex associated with the promise object while updating the promise object.

```cpp
template<class R, class Alloc>
struct uses_allocator<promise<R>, Alloc>
: true_type { };
```

Preconditions: Alloc meets the Cpp17Allocator requirements (Table 36).

```cpp
promise();
template<class Allocator>
promise(allocator_arg_t, const Allocator& a);
```

Effects: Creates a shared state. The second constructor uses the allocator a to allocate memory for the shared state.

```cpp
promise(promise&& rhs) noexcept;
```

Effects: Transfers ownership of the shared state of rhs (if any) to the newly-constructed object.

Postconditions: rhs has no shared state.

```cpp
~promise();
```

Effects: Abandons any shared state (32.9.5).

```cpp
promise& operator=(promise&& rhs) noexcept;
```

Effects: Abandons any shared state (32.9.5) and then as if promise(std::move(rhs)).swap(*this).

Returns: *this.

```cpp
void swap(promise& other) noexcept;
```

Effects: Exchanges the shared state of *this and other.

Postconditions: *this has the shared state (if any) that other had prior to the call to swap. other has the shared state (if any) that *this had prior to the call to swap.

```cpp
future<R> get_future();
```

Returns: A future<R> object with the same shared state as *this.

Synchronization: Calls to this function do not introduce data races (6.9.2) with calls to set_value, set_exception, set_value_at_thread_exit, or set_exception_at_thread_exit.

> [Note 1: Such calls need not synchronize with each other. — end note]

Throws: future_error if *this has no shared state or if get_future has already been called on a promise with the same shared state as *this.

Error conditions:
- future_already_retrieved if get_future has already been called on a promise with the same shared state as *this.
- no_state if *this has no shared state.

```cpp
void promise::set_value(const R& r);
void promise::set_value(R&& r);
void promise<R&>::set_value(R& r);
void promise<void>::set_value();
```

Effects: Atomically stores the value r in the shared state and makes that state ready (32.9.5).

Throws:
- future_error if its shared state already has a stored value or exception, or
- for the first version, any exception thrown by the constructor selected to copy an object of R, or
- for the second version, any exception thrown by the constructor selected to move an object of R.

Error conditions:
- promise_already_satisfied if its shared state already has a stored value or exception.
- no_state if *this has no shared state.

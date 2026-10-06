
# ISO/IEC 14882:2017(E)

- (10.1) Releases any shared state (33.6.5).
- (10.2) move assigns the contents of rhs to *this.

11 Postconditions:

- (11.1) valid() returns the same value as rhs.valid() prior to the assignment.
- (11.2) rhs.valid() == false.

shared_future<R> share() noexcept;

12 Returns: shared_future<R>(std::move(*this)).

13 Postconditions: valid() == false.

```
R get();
R& get();
void void() get();
```

> [Note: As described above, the template and its two required specializations differ only in the return type and value of the member function. — end note]

15 Effects:

- (15.1) wait() waits until the shared state is ready, retrieves the value stored in the shared state;
- (15.2) releases any shared state (33.6.5).

16 Returns:

- future() returns the value stored in the object's shared state std::move(v).
- future&()get() returns the reference stored as value in the object's shared state.
- (16.3) void()get() does nothing.

17 Throws the stored exception, if an exception was stored in the shared state.

18 Postconditions: valid() == false.

bool valid() const noexcept;

19 Returns: true only if *this refers to a shared state.

void wait() const const;

20 Effects: Blocks until the shared state is ready.

```
template <class Rep, class Period>
future_status wait_for(chrono::duration<Rep, Period>&, rel_time) const;
```

21 Effects: If the shared state contains a deferred function (33.6.9), otherwise blocks until the shared state is ready or until the relative timeout (33.2.4) specified by rel_time has expired.

22 Returns:

- future_status::deferred if the shared state contains a deferred function.
- future_status::ready if the shared state is ready.
- future_status::timeout if the function is returning because the relative timeout (33.2.4) specified by rel_time has expired.

23 Throws: timeout-related exceptions (33.2.4).

```
template <Class Clock, class Duration>
future_status wait_until(const chrono::time_point<Clock, abs_time>& const;
```

Effects: If the shared state contains a deferred function (33.6.9), otherwise blocks until the shared state is ready or the absolute timeout (33.2.4) is specified by abs_time has expired.

Returns:

- future_status::deferred if the shared state contains a deferred function.
- future_status::ready if the shared state is ready.
- future_status::timeout if it is returning because of the absolute timeout (33.2.4) by abs_time has expired.

Throws: timeout-related exceptions (33.2.4).

# 33.6.8 Class template shared_future

The class template shared_future defines a type for asynchronous returned objects which may share their shared state with other asynchronous result. A default-constructed shared_future object has no shared state. A shared_future object with shared state can be created by conversion from a future and shares its shared state with the original provider (33.6.5) of the shared state. The result (value or exception) of a shared_future object can be got by calling an object that shares the same state.

Member functions of shared_future do not synchronize with themselves, but they synchronize with the shared state of the other.

The effect of calling any member function than the destructor, the move-assignment operator, the copy-assignment operator, or valid() on a shared_future for which valid() == false is undefined. It is illegal to copy or move from a shared_future for which valid is false. Implementations should detect this event and throw an exception of type future_error with error condition future_err::no_state.

```
namespace std {
    template <class shared_future {
public:
        shared_future() noexcept;
        shared_future(const shared_future& rhs) noexcept;
        shared_future(shared_future&& rhs) noexcept;
        shared_future(shared_future&& rhs) noexcept;
        ~shared_future();
        shared_future& operator=(const shared_future& rhs) noexcept;
        shared_future& operator=(shared_future&& rhs) noexcept;

        // retrieve the value
        T get() const;

        // functions to check state
        bool valid() const noexcept;

        void wait() const;
        template <class Rep, class Period>
        future_status wait_for(const chrono::duration<Rep, Period>& rel_time) const;
        <class Clock, class Duration>
        future_status wait_until(const chrono::time_point<Clock, abs_time>& const) const;

}
```

# ISO/IEC 14882:2017(E)

The implementation shall provide the template `shared_future` and two specializations, `shared_future<R&>` and `shared_future<void>`. These differ only in the return type and return value of the member function `get`, as set out in its description, below.

```
shared_future() noexcept;
Effects: Constructs an empty shared_future object that does not refer to a state.
Postconditions: valid() == false;
shared_future(const shared_future& rhs) noexcept;
Effects: Constructs a shared_future object that refers to the shared state as rhs (if any).
Postconditions: valid() returns the same value as rhs.valid();
```

```
shared_future(future<R&&>) noexcept;
shared_future(shared_future&& rhs) noexcept;
Effects: Constructs a shared_future object that refers to the shared state that was referred to by rhs (if any).
Postconditions:
(10.1) valid() returns the same value as rhs.valid() prior to the constructor invocation.
(10.2) rhs.valid() == false.
```

```
shared_future();
Effects:
(11.1) Releases any shared state (33.6.5);
(11.2) destroys *this.
```

```
shared_future& operator=(shared_future&& rhs) noexcept;
Effects:
(12.1) Releases any shared state (33.6.5);
(12.2) move assigns the contents of rhs to *this.
```

```
13 Postconditions:
(13.1) valid() returns the same value as rhs.valid() prior to the assignment.
(13.2) rhs.valid() == false.
```

```
shared_future& operator=(const shared_future& rhs) noexcept;
Effects:
(14.1) Releases any shared state (33.6.5);
(14.2) assigns the contents of rhs to *this. [Note: As a result, this refers to the shared state as rhs (if any). — end note].
```

```
15 Postconditions: valid() == rhs.valid();
const R& shared_future::get() const;
R& shared_future<R&>::get() const;
void shared_future<void>::get() const;
```

> [Note: As described above, the template and its two required specializations differ only in the return type and name of the member function get. — end note]

# ISO/IEC 14882:2017(E)

17 [Note: Access to a value object in the shared state is unsynchronized, programmers should apply only those operations on R that do not introduce a data race (4.7). — end note].

18 Effects: wait() until the shared state is ready, retrieves the value stored in the shared state.

19 Returns:

(19.1) shared_future::get() returns a reference to the value stored in the object's shared state.
[Note: Access through that reference after the shared state has been destroyed produces undefined behavior; this can be avoided by not storing the reference in any storage with a greater lifetime than the shared_future object that returned the reference. — end note]

(19.2) shared_future::&get() returns the shared state as value in the object's shared state.

(19.3) shared_future<void>::get() returns nothing.

20 Throws: The stored exception, if an exception was stored in the shared state.

```
bool wait() const noexcept;
```

21 Returns true only *this refers to a shared state.

```
void wait() const;
```

22 Effects: Blocks until the shared state is ready.

```
template <class Rep, class Period>
future_status wait_for(const chrono::time_point<Duration, Period>& abs_time) const;
```

23 Effects: If the shared state contains a deferred function (33.6.9), otherwise blocks until the shared state is ready or until the relative timeout (33.2.4) specified by rel_time has expired.

24 Returns:

(24.1) future_status::deferred if the shared state contains a deferred function.
(24.2) future_status::ready if the shared state is ready.
(24.3) future_status::timeout if the function is returning because the relative timeout (33.2.4) specified by rel_time has expired.

25 Throws: timeout-related exceptions (33.2.4).

```
template <class Clock, class Duration>
future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
```

26 Effects: If the shared state contains a deferred function (33.6.9), otherwise blocks until the shared state is ready or the absolute timeout (33.2.4) is specified by abs_time has expired.

27 Returns:

(27.1) future_status::deferred if the shared state contains a deferred function.
(27.2) future_status::ready if the shared state is ready.
(27.3) future_status::timeout if it is returning because of the absolute timeout (33.2.4) by abs_time has expired.

28 Throws: timeout-related exceptions (33.2.4).

# 33.6.9 Function template async [futures.async]

+   1 The function template async provides a mechanism to launch a function potentially in a new thread and provides the result of the function in a future object with it shares a shared state.

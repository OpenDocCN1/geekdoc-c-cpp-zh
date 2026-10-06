# ISO/IEC 14882:2017(E)

+   (10.1) Releases any shared state (33.6.5).

+   (10.2) move assigns the contents of rhs to *this.

11 Postconditions:

+   (11.1) valid() returns the same value as rhs.valid() prior to the assignment.

+   (11.2) rhs.valid() == false.

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

+   (15.1) wait() waits until the shared state is ready, retrieves the value stored in the shared state;

+   (15.2) releases any shared state (33.6.5).

16 Returns:

+   future() returns the value stored in the object's shared state std::move(v).

+   future&()get() returns the reference stored as value in the object's shared state.

+   (16.3) void()get() does nothing.

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

+   future_status::deferred if the shared state contains a deferred function.

+   future_status::ready if the shared state is ready.

+   future_status::timeout if the function is returning because the relative timeout (33.2.4) specified by rel_time has expired.

23 Throws: timeout-related exceptions (33.2.4).
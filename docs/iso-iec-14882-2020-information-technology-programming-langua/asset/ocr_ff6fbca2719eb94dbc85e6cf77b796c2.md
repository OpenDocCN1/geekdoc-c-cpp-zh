3 The effect of calling any member function other than the destructor, the move-assignment operator, the copy-assignment operator, or valid() on a shared_future object for which valid() == false is undefined. [Note 2: It is valid to copy or move from a shared_future object for which valid() is false. — end note] Recommended practice: Implementations should detect this case and throw an object of type future_error with an error condition of future_errc::no_state.

```
namespace std {
  template<class R>
  class shared_future {
  public:
    shared_future() noexcept;
    shared_future(const shared_future& rhs) noexcept;
    shared_future(future<R>&&) noexcept;
    shared_future(shared_future&& rhs) noexcept;
    ~shared_future();
    shared_future& operator=(const shared_future& rhs) noexcept;
    shared_future& operator=(shared_future&& rhs) noexcept;

    // retrieving the value
    see below get() const;

    // functions to check state
    bool valid() const noexcept;

    void wait() const;
    template<class Rep, class Period>
      future_status wait_for(const chrono::duration<Rep, Period>& rel_time) const;
    template<class Clock, class Duration>
      future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
  };
}
```

4 The implementation provides the template shared_future and two specializations, shared_future<R&> and shared_future<void>. These differ only in the return type and return value of the member function get, as set out in its description, below.

```
shared_future() noexcept;
```

5 Effects: The object does not refer to a shared state.

6 Postconditions: valid() == false.

```
shared_future(const shared_future& rhs) noexcept;
```

7 Effects: The object refers to the same shared state as rhs (if any).

8 Postconditions: valid() returns the same value as rhs.valid().

```
shared_future(future<R>&& rhs) noexcept;
shared_future(shared_future&& rhs) noexcept;
```

9 Effects: Move constructs a shared_future object that refers to the shared state that was originally referred to by rhs (if any).

10 Postconditions:

+   (10.1) — valid() returns the same value as rhs.valid() returned prior to the constructor invocation.
+   (10.2) — rhs.valid() == false.

```
~shared_future();
```

11 Effects:

+   (11.1) — Releases any shared state (32.9.5);
+   (11.2) — destroys *this.
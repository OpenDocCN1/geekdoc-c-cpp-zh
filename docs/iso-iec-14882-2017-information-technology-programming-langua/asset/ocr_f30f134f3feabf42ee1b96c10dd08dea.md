# ISO/IEC 14882:2017(E)

future object for which valid() == false. -- end note] [Note: Implementations should detect this case
 throw an object of type future_error with an error condition of future_errc::no_state. -- end
note]

```
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
    future get();

    // functions to check state
    bool wait() const noexcept;

tntemplate<class Rep, class Period>
future_status wait_for(const chrono::duration<Rep, Period>& rel_time) const;
template<class Clock, class Duration>
future_status wait_until(const chrono::time_point<Clock, Duration>& abs_time) const;
};
```

+   The implementation should provide template future and two specializations, future<R&> and future<nvoid>. These differ only in the return type and return value of the member function get, as set out in the
description, below.

+   future() noexcept
Effects: Constructs an empty future object that does not refer to a shared state.

+   Postconditions: valid() == false.

+   future(future&& rhs) noexcept;
Effects: Move constructs a future object that refers to the shared state that was originally referred to
by rhs (if any).

+   Postconditions:
valid() returns the value as rhs.valid() prior to the constructor invocation.
rhs.valid() == false.

+   -future();
Effects:
Releases any shared state (33.6.5);
destroys *this.

+   future& operator=(future&& rhs) noexcept;
Effects:

§ 33.6.7 ©ISO/IEC 2017 – All rights reserved
# ISO/IEC 14882:2017(E)

4 The implementation shall provide the template `shared_future` and two specializations, `shared_future<R&>` and `shared_future<void>`. These differ only in the return type and return value of the member function `get`, as set out in its description, below.

```
shared_future() noexcept;
5 Effects: Constructs an empty shared_future object that does not refer to a shared state.
6 Postconditions: valid() == false;
7 shared_future(const shared_future& rhs) noexcept;
8 Effects: Constructs a shared_future object that refers to the shared state as rhs (if any).
Postconditions: valid() returns the same value as rhs.valid();
```

```
shared_future(future<R&&>) noexcept;
shared_future(shared_future&& rhs) noexcept;
9 Effects: Constructs a shared_future object that refers to the shared state that was referred to by rhs (if any).
10 Postconditions:
```

```
(10.1) valid() returns the same value as rhs.valid() returned prior to the constructor invocation.
(10.2) rhs.valid() == false.
```

```
-shared_future();
11 Effects:
(11.1) Releases any shared state (33.6.5);
(11.2) destroys *this.
```

```
shared_future& operator=(shared_future&& rhs) noexcept;
12 Effects:
(12.1) Releases any shared state (33.6.5);
(12.2) move assigns the contents of rhs to *this.
```

```
13 Postconditions:
(13.1) valid() returns the same value as rhs.valid() returned prior to the assignment.
(13.2) rhs.valid() == false.
```

```
shared_future& operator=(const shared_future& rhs) noexcept;
14 Effects:
(14.1) Releases any shared state (33.6.5);
(14.2) assigns the contents of rhs to *this. [Note: As a result, this refers to the shared state as rhs (if any). — end note].
```

```
15 Postconditions: valid() == rhs.valid();
const R& shared_future::get() const;
R& shared_future<R&>::get() const;
void shared_future<void>::get() const;
```

> [Note: As described above, the template and its two required specializations differ only in the return type and name of the member function get. — end note].
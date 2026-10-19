```
jthread(jthread&& x) noexcept;
```

Postconditions: x.get_id() == id() and get_id() returns the value of x.get_id() prior to the start of construction. ssource has the value of x.ssource prior to the start of construction and x.ssource.stop_possible() is false.

```
~jthread();
```

Effects: If joinable() is true, calls request_stop() and then join().

[Note 3: Operations on *this are not synchronized. — end note]

```
jthread& operator=(jthread&& x) noexcept;
```

Effects: If joinable() is true, calls request_stop() and then join(). Assigns the state of x to *this and sets x to a default constructed state.

Postconditions: x.get_id() == id() and get_id() returns the value of x.get_id() prior to the assignment. ssource has the value of x.ssource prior to the assignment and x.ssource.stop_possible() is false.

Returns: *this.

# 32.4.4.3 Members [thread.jthread.mem]

```
void swap(jthread& x) noexcept;
```

Effects: Exchanges the values of *this and x.

```
[[nodiscard]] bool joinable() const noexcept;
```

Returns: get_id() != id().

```
void join();
```

Effects: Blocks until the thread represented by *this has completed.

Synchronization: The completion of the thread represented by *this synchronizes with (6.9.2) the corresponding successful join() return.

[Note 1: Operations on *this are not synchronized. — end note]

Postconditions: The thread represented by *this has completed. get_id() == id().

Throws: system_error when an exception is required (32.2.2).

Error conditions:

+   — resource_deadlock_would_occur — if deadlock is detected or get_id() == this_thread::get_id().

+   — no_such_process — if the thread is not valid.

+   — invalid_argument — if the thread is not joinable.

```
void detach();
```

Effects: The thread represented by *this continues execution without the calling thread blocking. When detach() returns, *this no longer represents the possibly continuing thread of execution. When the thread previously represented by *this ends execution, the implementation releases any owned resources.

Postconditions: get_id() == id().

Throws: system_error when an exception is required (32.2.2).

Error conditions:

+   — no_such_process — if the thread is not valid.

+   — invalid_argument — if the thread is not joinable.

```
id get_id() const noexcept;
```

Returns: A default constructed id object if *this does not represent a thread, otherwise this_thread::get_id() for the thread of execution represented by *this.
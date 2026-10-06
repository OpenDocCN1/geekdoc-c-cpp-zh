
# ISO/IEC 14882:2017(E)

m.try_lock_until(abs_time)

Effects: Attempts to acquire a lock for the current execution agent before the absolute timeout (33.2.4) specified by abs_time. The function shall not return the timeout specified by abs_time unless it has obtained a lock on m for the current execution agent. If an exception is thrown then a lock shall not be acquired for the current execution agent.

Return type: bool;

Returns: true if the lock was acquired, false otherwise.

# 33.2.6 decay_copy [thread::decaycopy]

+   1 In places within this Clause the operation DECAY_COPY(x) is used. All such uses mean mean call the function decay_copy(x) and use the result, where decay_copy is defined as follows:

```
template <class T>
T decay_copy(T&& v)
{ return std::forward<T>(v); }
```

# 33.3 Threads

+   1 33.3 describes components that can be used to create and manage threads. [Note: These threads are intended to map one-to-one with operating system threads. -- end note]

# 33.3.1 Header <thread> synopsis [thread::syn]

```
namespace std {
class thread {
void spawn(thread& x, thread& y) noexcept;

namespace this_thread {
thread::id get_id() noexcept;

void yield() noexcept;

template <class Clock, class Duration>
void sleep_until(const chrono::time_point<Clock, Duration>& abs_time);
template <class Rep, class Period>
void sleep_for(const chrono::duration<Rep, Period>& rel_time);
}
};
```

# 33.3.2 Class thread [thread::thread.class]

+   1 The class thread provides a mechanism to create a new thread of execution, to join with a thread (i.e., wait for a thread to complete), and to perform operations that manage and control the state of a thread. A thread object uniquely represents a particular thread of execution. That representation may be transferred to other threads in such a way that no two thread objects simultaneously represent the same thread of execution. A thread is detached when no thread represents it. Objects of thread can be in a state that does not represent a thread of execution. [Note: A thread object does not represent a thread of execution after default construction, after being moved from, or after a successful detach or join. -- end note]

```
namespace std {
class thread {
public:
// types:
class id;
using native_handle_type = implementation-defined; // see 33.2.3
```

```
// construct/copy/destroy:
thread() noexcept;
template<class F, class... Args> explicit thread(F&& f, Args&&... args);
~thread();
thread(const thread&) = delete;
thread(thread&&) noexcept;
thread& operator=(const thread&) = delete;
thread& operator=(thread&&) noexcept;
```

```
// members:
void swap(thread&) noexcept;
bool joinable() const noexcept;
void join() noexcept;
void detach();
id get_id() const noexcept;
native_handle_type native_handle(); // see 33.2.2
```

```
// static members:
static unsigned int hardware_concurrency() noexcept;
};
```

# 33.3.2.1 Class thread::id

```
[thread.id]
namespace std {
class thread::id {
public:
  id() noexcept;
};
```

```
bool operator==(thread::id x, thread::id y) noexcept;
bool operator(!(thread::id x, thread::id y) noexcept;
bool operator<(thread::id x, thread::id y) noexcept;
bool operator<=(thread::id x, thread::id y) noexcept;
bool operator>(thread::id x, thread::id y) noexcept;
bool operator>=(thread::id x, thread::id y) noexcept;
```

```
template<class charT, class traits>
basic_ostream& operator<<(charT& out, traits&& t, thread::id id);
```

```
// hash
template<class T> struct hash;
template<> struct hash<thread::id> {
};
```

+   1 An object of type thread::id provides a unique identifier for thread of execution and a single value for all thread objects that do not represent a thread of execution (33.3.2). Each thread of execution has an associated thread::id that is not equal to the thread::id of any other thread of execution and is not equal to the thread::id object of any other thread object that does not represent threads of execution.

+   2 thread::id shall be a trivially copyable class (Clause 12). The library may reuse the value of a thread::id of a terminated thread that can no longer join.

+   3 [Note: Relational operators allow thread::id objects to be used as keys in associative containers.— end note]

```
id() noexcept;
4   Effects: Constructs an object of type id.
5   Postconditions: The constructed object does not represent a thread of execution.
6   bool operator=(thread::id x, thread::id y) noexcept;
7   Returns: true only if x and y represent the same thread of execution or neither x nor y represents a
      thread of execution.
   bool operator!=(thread::id x, thread::id y) noexcept;
8   Returns: (x != y)
   bool operator<(thread::id x, thread::id y) noexcept;
9   Returns: A value which operator< is a total ordering as described in 27.8.
   bool operator>(thread::id x, thread::id y) noexcept;
10  Returns: (y < x).
   bool operator<=(thread::id x, thread::id y) noexcept;
11  Returns: (x <= y).
   template<class charT, class traits>
   basic_ostream<charT, traits>&
   operator=(basic_ostream<charT, traits>& out, thread::id id);
12  Effects: Inserts an unspecified text representation of id into. For two objects of type thread::id
      x and y, if x == y the objects have the same representation.
13  Returns: hash<thread::id>;
```

# 33.3.2.2 constructors

```
thread() noexcept;
4   Effects: Constructs an object of type thread that does not represent a thread.
5   Postconditions: The constructed object does not represent a thread of execution.
6   template<class F, class... Args> thread(F&& f, Args&&... args);
7   Effects: Constructs a thread of execution by calling f with args.
8   Postconditions: The constructed object represents a thread of execution.
9   Requires: F is invokable and Args are constructible.
10  Throws: system_error if unable to start the thread.
11  thread(thread&&) noexcept;
12  Effects: Moves the state of the other thread.
13  Postconditions: The constructed object represents the thread of execution.
14  thread(const thread&) = delete;
15   Note: The thread class is non-copyable.
16   Postconditions: The constructed object does not represent a thread of execution.
```

# 33.3.2.3 destructor

```
~thread() noexcept;
4   Effects: If the thread is joinable, terminate is called. Otherwise, it has no effects.
5   [Note: Either joining or detaching a joinable thread in its destructor could result in difficulty debugging correctness (for detach) or performance (for join) joins only when an exception is thrown. Thus the programmer must ensure that the destructor is never executed while the thread is joinable. end note]
```

# 33.3.2.4 assignment

```
thread& operator=(thread& x) noexcept;
4   Effects: If joinable, terminate is called. Otherwise, assigns the state of x to *this and sets x to a default constructed state.
5   Postconditions: x.id() is equal to *this.id() post-assignment.
6   Returns: *this.
thread& operator=(thread&&) noexcept;
7   Effects: If joinable, terminate is called. Otherwise, moves the state of the other thread to *this.
8   Postconditions: The constructed object represents the thread of execution.
9   Returns: *this.
thread& operator=(const thread&) = delete;
10  Note: The thread class is non-copyable.
```

# 33.3.2.5 thread members

```
void swap(thread&) noexcept;
4   Effects: Swaps the state of *this and x.
bool joinable() const noexcept;
4   Returns: true if the thread is joinable.
void join() noexcept;
4   Effects: Blocks until the thread represented by *this completes.
5   Postconditions: The thread represented by *this has completed.
void detach();
4   Effects: Detaches the thread represented by *this.
5   Postconditions: The thread is no longer joinable.
id get_id() const noexcept;
4   Returns: The unique identifier for the thread.
native_handle_type native_handle(); // see 33.2.2
4   Returns: The native handle of the thread.
static unsigned int hardware_concurrency() noexcept;
4   Returns: The number of concurrent threads that can be supported by the implementation.
```
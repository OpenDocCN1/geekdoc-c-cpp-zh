# ISO/IEC 14882:2017(E)

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
bool operator!(thread::id x, thread::id y) noexcept;
bool operator<(thread::id x, thread::id y) noexcept;
bool operator<=(thread::id x, thread::id y) noexcept;
bool operator>(thread::id x, thread::id y) noexcept;
bool operator>=(thread::id x, thread::id y) noexcept;
```

```
template<class charT, class traits>
basic_ostream<<(charT& out, traits&& t, thread::id id);
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
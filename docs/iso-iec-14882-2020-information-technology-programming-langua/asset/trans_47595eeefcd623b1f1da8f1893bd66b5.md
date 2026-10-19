

```
void yield() noexcept;
template<class Clock, class Duration>
    void sleep_until(const chrono::time_point<Clock, Duration>& abs_time);
template<class Rep, class Period>
    void sleep_for(const chrono::duration<Rep, Period>& rel_time);
}
```

## 32.4.3 Class thread [thread.thread.class]

### 32.4.3.1 General [thread.thread.class.general]

1 class thread 提供了一种创建新的执行线程的机制，用于与线程连接（即等待线程完成），并执行其他操作来管理和查询线程的状态。thread 对象唯一地表示一个特定的执行线程。该表示可以转移到其他 thread 对象，使得没有任何两个 thread 对象同时表示同一个执行线程。当没有任何 thread 对象表示该线程时，执行线程被分离。class thread 的对象可以处于不表示执行线程的状态。

> [Note 1: 在默认构造后、被移动后，或在成功调用 detach 或 join 后，thread 对象不再表示执行线程。—— end note]

```
namespace std {
  class thread {
  public:
    // types
    class id;
    using native_handle_type = implementation-defined;        // see 32.2.3

    // construct/copy/destroy
    thread() noexcept;
    template<class F, class... Args> explicit thread(F&& f, Args&&... args);
    ~thread();
    thread(const thread&) = delete;
    thread(thread&&) noexcept;
    thread& operator=(const thread&) = delete;
    thread& operator=(thread&&) noexcept;

    // members
    void swap(thread&) noexcept;
    bool joinable() const noexcept;
    void join();
    void detach();
    id get_id() const noexcept;
    native_handle_type native_handle();                        // see 32.2.3

    // static members
    static unsigned int hardware_concurrency() noexcept;
  };
}
```

### 32.4.3.2 Class thread::id [thread.thread.id]

```
namespace std {
  class thread::id {
  public:
    id() noexcept;
  };

  bool operator==(thread::id x, thread::id y) noexcept;
  strong_ordering operator<=>(thread::id x, thread::id y) noexcept;

  template<class charT, class traits>
    basic_ostream<charT, traits>&
      operator<<(basic_ostream<charT, traits>& out, thread::id id);
}
```

- (7.3) — invalid_argument — if the thread is not joinable.

```
void detach();
```

8 Effects: 由 *this 表示的线程继续执行而不阻塞调用线程。detach() 返回时，*this 不再表示可能继续的执行线程。当 *this 先前表示的线程结束执行时，实现会释放任何已拥有的资源。

9 Postconditions: get_id() == id()。

10 Throws: system_error when an exception is required (32.2.2)。

11 Error conditions:

- (11.1) — no_such_process — if the thread is not valid.
- (11.2) — invalid_argument — if the thread is not joinable.

```
id get_id() const noexcept;
```

12 Returns: 如果 *this 不表示线程，则返回默认构造的 id 对象，否则返回由 *this 表示的执行线程的 this_thread::get_id()。

### 32.4.3.7 Static members [thread.thread.static]

```
static unsigned int hardware_concurrency() noexcept;
```

1 Returns: 硬件线程上下文的数量。

> [Note 1: 此值应仅被视为提示。—— end note]

如果此值不可计算或未定义，实现应返回 0。

### 32.4.3.8 Specialized algorithms [thread.thread.algorithm]

```
void swap(thread& x, thread& y) noexcept;
```

1 Effects: 如同执行 x.swap(y)。

## 32.4.4 Class jthread [thread.jthread.class]

### 32.4.4.1 General [thread.jthread.class.general]

1 class jthread 提供了一种创建新的执行线程的机制。其功能与 class thread (32.4.3) 相同，但额外具备向新执行线程提供 stop_token (32.3)、发出停止请求以及自动连接的能力。

```
namespace std {
  class jthread {
  public:
    // types
    using id = thread::id;
    using native_handle_type = thread::native_handle_type;

    // 32.4.4.2, constructors, move, and assignment
    jthread() noexcept;
    template<class F, class... Args> explicit jthread(F&& f, Args&&... args);
    ~jthread();
    jthread(const jthread&) = delete;
    jthread(jthread&&) noexcept;
    jthread& operator=(const jthread&) = delete;
    jthread& operator=(jthread&&) noexcept;

    // 32.4.4.3, members
    void swap(jthread&) noexcept;
    [[nodiscard]] bool joinable() const noexcept;
    void join();
    void detach();
    [[nodiscard]] id get_id() const noexcept;
    [[nodiscard]] native_handle_type native_handle();  // see 32.2.3

    // 32.4.4.4, stop token handling
    [[nodiscard]] stop_source get_stop_source() noexcept;
    [[nodiscard]] stop_token get_stop_token() const noexcept;
    [[nodiscard]] bool request_stop() noexcept;

    // 32.4.4.5, specialized algorithms
    friend void swap(jthread& lhs, jthread& rhs) noexcept;

    // 32.4.4.6, static members
    [[nodiscard]] static unsigned int hardware_concurrency() noexcept;

  private:
    stop_source ssource;    // exposition only
  };
}
```

### 32.4.4.2 Constructors, move, and assignment [thread.jthread.cons]

```
jthread() noexcept;
```

Effects: 构造一个不表示执行线程的 jthread 对象。

Postconditions: get_id() == id() 为真且 ssource.stop_possible() 为假。

```
template<class F, class... Args> explicit jthread(F&& f, Args&&... args);
```

Constraints: remove_cvref_t<F> 与 jthread 不是同一类型。

Mandates: 以下全部为真：

- `is_constructible_v<decay_t<F>, F>`,
- `(is_constructible_v<decay_t<Args>, Args> && ...)`,
- `is_move_constructible_v<decay_t<F>>`,
- `(is_move_constructible_v<decay_t<Args>> && ...)`, and
- `is_invocable_v<decay_t<F>, decay_t<Args>...> || is_invocable_v<decay_t<F>, stop_token, decay_t<Args>...>`.

Preconditions: decay_t<F> 以及每个 decay_t<Args> 满足 Cpp17MoveConstructible 要求。

Effects: 初始化 ssource。新的执行线程执行
`invoke(decay-copy(std::forward<F>(f)), get_stop_token(), decay-copy(std::forward<Args>(args))...)`
如果该表达式是良构的，否则执行
`invoke(decay-copy(std::forward<F>(f)), decay-copy(std::forward<Args>(args))...)`
其中对 decay-copy 的调用在构造线程中求值。此调用的任何返回值都被忽略。

> [Note 1: 这意味着从 f 的副本的调用中未抛出的任何异常将在构造线程中抛出，而非新线程中。—— end note]

如果 invoke 表达式通过异常退出，则调用 terminate。

Synchronization: 构造函数的调用完成与 f 的副本的调用开始同步。

Postconditions: get_id() != id() 为真且 ssource.stop_possible() 为真且 *this 表示新启动的线程。

> [Note 2: 调用线程只能发出一次停止请求，因为它无法替换此停止令牌。—— end note]

Throws: 如果无法启动新线程，则抛出 system_error。

Error conditions:

- resource_unavailable_try_again — 系统缺乏创建另一个线程所需的资源，或系统对进程中线程数量的限制将被超过。

```
jthread(jthread&& x) noexcept;
```

Postconditions: x.get_id() == id() 且 get_id() 返回构造开始前 x.get_id() 的值。ssource 具有构造开始前 x.ssource 的值且 x.ssource.stop_possible() 为假。

```
~jthread();
```

Effects: 如果 joinable() 为真，则调用 request_stop() 然后调用 join()。

> [Note 3: 对 *this 的操作未同步。—— end note]

```
jthread& operator=(jthread&& x) noexcept;
```

Effects: 如果 joinable() 为真，则调用 request_stop() 然后调用 join()。将 x 的状态赋给 *this 并将 x 设置为默认构造状态。

Postconditions: x.get_id() == id() 且 get_id() 返回赋值前 x.get_id() 的值。ssource 具有赋值前 x.ssource 的值且 x.ssource.stop_possible() 为假。

Returns: *this。

### 32.4.4.3 Members [thread.jthread.mem]

```
void swap(jthread& x) noexcept;
```

Effects: 交换 *this 和 x 的值。

```
[[nodiscard]] bool joinable() const noexcept;
```

Returns: get_id() != id()。

```
void join();
```

Effects: 阻塞直到由 *this 表示的线程完成。

Synchronization: 由 *this 表示的线程的完成与 (6.9.2) 对应的成功 join() 返回同步。

> [Note 1: 对 *this 的操作未同步。—— end note]

Postconditions: 由 *this 表示的线程已完成。get_id() == id()。

Throws: system_error when an exception is required (32.2.2)。

Error conditions:

- resource_deadlock_would_occur — 如果检测到死锁或 get_id() == this_thread::get_id()。
- no_such_process — if the thread is not valid.
- invalid_argument — if the thread is not joinable.

```
void detach();
```

Effects: 由 *this 表示的线程继续执行而不阻塞调用线程。detach() 返回时，*this 不再表示可能继续的执行线程。当 *this 先前表示的线程结束执行时，实现会释放任何已拥有的资源。

Postconditions: get_id() == id()。

Throws: system_error when an exception is required (32.2.2)。

Error conditions:

- no_such_process — if the thread is not valid.
- invalid_argument — if the thread is not joinable.

```
id get_id() const noexcept;
```

Returns: 如果 *this 不表示线程，则返回默认构造的 id 对象，否则返回由 *this 表示的执行线程的 this_thread::get_id()。


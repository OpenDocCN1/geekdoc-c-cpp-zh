
Returns: cv_status::timeout if the relative timeout (32.2.4) specified by rel_time expired, otherwise cv_status::no_timeout.

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

[Note 3: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock is locked by the calling thread.

Throws: Timeout-related exceptions (32.2.4).

```
template<class Lock, class Clock, class Duration, class Predicate>
    bool wait_until(Lock& lock, const chrono::time_point<Clock, Duration>& abs_time, Predicate pred);
```

Effects: Equivalent to:

```
while (!pred())
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
return true;
```

[Note 4: There is no blocking if pred() is initially true, or if the timeout has already expired. — end note]

[Note 5: The returned value indicates whether the predicate evaluates to true regardless of whether the timeout was triggered. — end note]

```
template<class Lock, class Rep, class Period, class Predicate>
    bool wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time, Predicate pred);
```

Effects: Equivalent to:

```
return wait_until(lock, chrono::steady_clock::now() + rel_time, std::move(pred));
```

## 32.6.5.3 Interruptible waits [thread.condvarany.intwait]

The following wait functions will be notified when there is a stop request on the passed stop_token. In that case the functions return immediately, returning false if the predicate evaluates to false.

```
template<class Lock, class Predicate>
    bool wait(Lock& lock, stop_token stoken, Predicate pred);
```

Effects: Registers for the duration of this call `*this` to get notified on a stop request on stoken during this call and then equivalent to:

```
while (!stoken.stop_requested()) {
    if (pred())
        return true;
    wait(lock);
}
return pred();
```

[Note 1: The returned value indicates whether the predicate evaluated to true regardless of whether there was a stop request. — end note]

Postconditions: lock is locked by the calling thread.

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

[Note 2: This can happen if the re-locking of the mutex throws an exception. — end note]

Throws: Any exception thrown by pred.

```
template<class Lock, class Clock, class Duration, class Predicate>
    bool wait_until(Lock& lock, stop_token stoken,
                    const chrono::time_point<Clock, Duration>& abs_time, Predicate pred);
```

Effects: Registers for the duration of this call `*this` to get notified on a stop request on stoken during this call and then equivalent to:

```
while (!stoken.stop_requested()) {
    if (pred())
        return true;
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
}
return pred();
```

[Note 3: There is no blocking if pred() is initially true, stoken.stop_requested() was already true or the timeout has already expired. — end note]

[Note 4: The returned value indicates whether the predicate evaluated to true regardless of whether the timeout was triggered or a stop request was made. — end note]

Postconditions: lock is locked by the calling thread.

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

[Note 5: This can happen if the re-locking of the mutex throws an exception. — end note]

Throws: Timeout-related exceptions (32.2.4), or any exception thrown by pred.

```
template<class Lock, class Rep, class Period, class Predicate>
bool wait_for(Lock& lock, stop_token stoken,
    const chrono::duration<Rep, Period>& rel_time, Predicate pred);
```

Effects: Equivalent to:

```
return wait_until(lock, std::move(stoken), chrono::steady_clock::now() + rel_time,
    std::move(pred));
```

## 32.7 Semaphore [thread.sema]

### 32.7.1 General [thread.sema.general]

Semaphores are lightweight synchronization primitives used to constrain concurrent access to a shared resource. They are widely used to implement other synchronization primitives and, whenever both are applicable, can be more efficient than condition variables.

A counting semaphore is a semaphore object that models a non-negative resource count. A binary semaphore is a semaphore object that has only two states. A binary semaphore should be more efficient than the default implementation of a counting semaphore with a unit resource count.

### 32.7.2 Header <semaphore> synopsis [semaphore.syn]

```
namespace std {
  template<ptrdiff_t least_max_value = implementation-defined>
  class counting_semaphore;

  using binary_semaphore = counting_semaphore<1>;
}
```

### 32.7.3 Class template counting_semaphore [thread.sema.cnt]

```
namespace std {
  template<ptrdiff_t least_max_value = implementation-defined>
  class counting_semaphore {
  public:
    static constexpr ptrdiff_t max() noexcept;

    constexpr explicit counting_semaphore(ptrdiff_t desired);
    ~counting_semaphore();

    counting_semaphore(const counting_semaphore&) = delete;
    counting_semaphore& operator=(const counting_semaphore&) = delete;

    void release(ptrdiff_t update = 1);
    void acquire();
    bool try_acquire() noexcept;
    template<class Rep, class Period>
      bool try_acquire_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
      bool try_acquire_until(const chrono::time_point<Clock, Duration>& abs_time);

  private:
    ptrdiff_t counter;        // exposition only
  };
}
```

Throws: Timeout-related exceptions (32.2.4), or system_error when a non-timeout-related exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

## 32.8 Coordination types [thread.coord]

### 32.8.1 General [thread.coord.general]

Subclause 32.8 describes various concepts related to thread coordination, and defines the coordination types latch and barrier. These types facilitate concurrent computation performed by a number of threads.

### 32.8.2 Latches [thread.latch]

#### 32.8.2.1 General [thread.latch.general]

A latch is a thread coordination mechanism that allows any number of threads to block until an expected number of threads arrive at the latch (via the count_down function). The expected count is set when the latch is created. An individual latch is a single-use object; once the expected count has been reached, the latch cannot be reused.

#### 32.8.2.2 Header <latch> synopsis [latch.syn]

```
namespace std {
    class latch;
}
```

#### 32.8.2.3 Class latch [thread.latch.class]

```
namespace std {
    class latch {
    public:
        static constexpr ptrdiff_t max() noexcept;

        constexpr explicit latch(ptrdiff_t expected);
        ~latch();

        latch(const latch&) = delete;
        latch& operator=(const latch&) = delete;

        void count_down(ptrdiff_t update = 1);
        bool try_wait() const noexcept;
        void wait() const;
        void arrive_and_wait(ptrdiff_t update = 1);

    private:
        ptrdiff_t counter;  // exposition only
    };
}
```

A latch maintains an internal counter that is initialized when the latch is created. Threads can block on the latch object, waiting for counter to be decremented to zero.

Concurrent invocations of the member functions of latch, other than its destructor, do not introduce data races.

```
static constexpr ptrdiff_t max() noexcept;
```

Returns: The maximum value of counter that the implementation supports.

```
constexpr explicit latch(ptrdiff_t expected);
```

Preconditions: expected >= 0 is true and expected <= max() is true.

Effects: Initializes counter with expected.

Throws: Nothing.

```
void count_down(ptrdiff_t update = 1);
```

Preconditions: update >= 0 is true, and update <= counter is true.

Effects: Atomically decrements counter by update. If counter is equal to zero, unblocks all threads blocked on `*this`.

Synchronization: Strongly happens before the returns from all calls that are unblocked.

Throws: system_error when an exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

```
bool try_wait() const noexcept;
```

Returns: With very low probability false. Otherwise counter == 0.

```
void wait() const;
```

Effects: If counter equals zero, returns immediately. Otherwise, blocks on `*this` until a call to count_down that decrements counter to zero.

Throws: system_error when an exception is required (32.2.2).

Error conditions: Any of the error conditions allowed for mutex types (32.5.4.2).

```
void arrive_and_wait(ptrdiff_t update = 1);
```

Effects: Equivalent to:

```
count_down(update);
wait();
```

### 32.8.3 Barriers [thread.barrier]

#### 32.8.3.1 General [thread.barrier.general]

A barrier is a thread coordination mechanism whose lifetime consists of a sequence of barrier phases, where each phase allows at most an expected number of threads to block until the expected number of threads arrive at the barrier.

> [Note 1: A barrier is useful for managing repeated tasks that are handled by multiple threads. — end note]

#### 32.8.3.2 Header <barrier> synopsis [barrier.syn]

```
namespace std {
  template<class CompletionFunction = see below>
    class barrier;
}
```

#### 32.8.3.3 Class template barrier [thread.barrier.class]

```
namespace std {
  template<class CompletionFunction = see below>
  class barrier {
  public:
    using arrival_token = see below;

    static constexpr ptrdiff_t max() noexcept;

    constexpr explicit barrier(ptrdiff_t expected,
                               CompletionFunction f = CompletionFunction());

    ~barrier();

    barrier(const barrier&) = delete;
    barrier& operator=(const barrier&) = delete;

    [[nodiscard]] arrival_token arrive(ptrdiff_t update = 1);
    void wait(arrival_token&& arrival) const;

    void arrive_and_wait();
    void arrive_and_drop();
```

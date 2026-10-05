```
mu.lock();

thread t1(print);
t1.detach();
this_thread::sleep_for(std::chrono::seconds(3));
mu.unlock();

thread t2(print);
t2.detach();
this_thread::sleep_for(std::chrono::seconds(2));

```

output:
mutex is locked
mutex is unlocked
hello world

The thread tries to acquire a lock with mu.try_lock(). If it fails, the thread returns immediately. If it succeeds, the thread acquires a lock and executes the critical code. After it has executed the critical section, it releases the lock.

# Locking Multiple Mutexes With std::try_lock(m1, m2, ... mn)

std::try_lock(m1, m2, ... mn) tries to lock all of the mutexes that it's arguments. Two or more arguments must be supplied to this function.

The declaration syntax is:

```
int try_lock(m1, m2, ... mn)
```

If try_lock succeeds in locking all of the mutexes, it returns -1. If it fails to lock all of the mutexes, it unlocks all of the mutexes that it was able to lock and returns the zero-
```
balance: 500
resource m1 is locked
resource m1 is locked
resource m1 and m2 not locked
critical section processed
resource m1 and m2 not locked
critical section processed
balance: 800
```

Note after the critical section is processed, all of the mutexes must be unlocked.

If an exception is thrown, try_lock(...) will unlock all of the mutexes before rethrowing
the exception.

# Timed Mutex

The timed_mutex::try_mutex_for(some_duration) function tries to acquire a lock on a
mutex until a specified period of time elapses. The function returns true if it acquires a
lock. It returns false if the lock is not acquired in the specified time duration. It's
declaration is:

```
#include <mutex>
bool std::timed_mutex::try_lock_for(const std::chrono::duration);
```

Here is a reference program:

```
#include <iostream>
#include <thread>
#include <mutex>

std::timed_mutex m1; // our mutex object
int balance = 500; // this is our shared resource
void deposit(int amount)
{
```
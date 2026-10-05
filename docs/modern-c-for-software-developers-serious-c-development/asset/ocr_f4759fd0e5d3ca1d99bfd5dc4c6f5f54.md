unlocked, t2 will acquire a lock and begin updating balance. We have a deadlock if t1
never releases the mutex.

**Note:** If an exception is thrown while executing a critical section, the mutex lock will
ot be released.

# try_lock()

try_lock attempts to lock a mutex. It returns false if it cannot lock the mutex and true
a lock is acquired. The syntax is:

```
using namespace std;

mutex m1;

bool m1.try_lock();
```

try_lock has undefined behavior if it is called by a thread that already has a lock.

Look at the following code:

```
#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>
```

```
using namespace std;
mutex mu;

void print(void) {
    if (mu.try_lock() == false) {
        cout << "mutex is locked\n";
    }
    // critical code section
    else {
        cout << "mutex is unlocked\n";
        cout << "hello world\n";
        mu.unlock();
    }
}
```

```
int main() {
```
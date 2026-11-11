+   - When the client is blocked because it cannot progress, it waits until the monitor condition sends a notification. This notification happens when the monitor is unlocked. The notification can be sent only to one or to all of the waiting clients. Typically, waiting means resource-friendly sleeping in contrast to busy-waiting.
+   - When a client gets the notification to resume, it locks the monitor lock and executes the synchronized member function. At the end of the synchronized member function, the monitor lock is unlocked. The monitor condition sends a notification to signal that the next client can execute its synchronized member function.

# 10.2.5 Advantages and Disadvantages

What are the advantages and disadvantages of the Monitor Object?

+   - **Advantages:**
+     - The client is not aware of the implicit synchronization of the Monitor Object, and the synchronization is fully encapsulated in the implementation.
+     - The invoked synchronized member functions will be eventually automatically scheduled. The notification/waiting mechanism of the monitor condition behaves as a simple scheduler.
+   - **Disadvantages:**
+     - It is often quite challenging to change the synchronization mechanism of the synchronization member functions because the functionality and the synchronization are strongly coupled.
+     - When a synchronized member function invokes directly or indirectly the same Monitor Object, a deadlock may occur.

The following example defines a ThreadSafeQueue.

# Monitor Object

```
```cpp
// monitorObject.cpp

#include <condition_variable>
#include <functional>
#include <queue>
#include <iostream>
#include <mutex>
#include <random>
#include <thread>

class Monitor {
public:
    void lock() const {
```
```
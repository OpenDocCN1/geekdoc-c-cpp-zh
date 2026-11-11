```
```cpp
22    std::cout << '\n';
23
24 }
```
```

The Visual Studio compiler 19.29.30137 for x64 uses a locking mechanism to support atomic smart pointers.

![](bbox=[0.18, 0.31, 0.78, 0.55])

`std::atomic<std::shared_ptr>` uses on Windows a locking mechanism

Therefore, we're back to square one and have to take care of memory management.

# #### 14.2.2.2 A Simple Garbage Collector for Nodes

I discussed in the section about the lock-free stack implementation leaking memory that concurrent execution of more than one topAndPush call is a Race Condition. Consequently, I can safely delete a node if not more than one topAndPush call is concurrently executing. This observation is crucial for solving this memory leak issue: I store removed nodes on a to be deleted list, and I delete the nodes on this list if no more than one topAndPush call is active. There is only one challenge left: How can I be sure that not more than one topAndPush call is active? I use an atomic counter that is incremented at the start of topAndPush and decremented at its end. The counter is zero or one if no or one topAndPush call is active.

The following program implements the presented strategy. I use the lockFreeStackWithLeaks.cpp as starting point.
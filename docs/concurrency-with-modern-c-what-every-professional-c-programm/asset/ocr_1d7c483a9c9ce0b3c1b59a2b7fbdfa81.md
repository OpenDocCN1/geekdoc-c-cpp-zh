# ### 3.5.2 Lost Wakeup and Spurious Wakeup

# #### Lost Wakeup

The lost wakeup phenomenon is that the sender sends its notification before the receiver gets to its wait state. The consequence is that the notification is lost. The C++ standard describes condition variables as a simultaneous synchronization mechanism: “The condition_variable class is a synchronization primitive that can be used to block a thread, or multiple threads at the same time, ...”. So the notification gets lost, and the receiver is waiting and waiting and ....

# #### Spurious Wakeup

The receiver may wake up, although no notification happened. At a minimum POSIX Threads[^13] and the Windows API[^14] can be victims of these phenomena. One reason for a spurious wakeup can be a stolen wakeup. This means, before the awaken thread gets the chance to run, another thread kicks in and runs.

# ### 3.5.3 The Wait Workflow

The waiting thread has quite a complicated workflow.

Here are the two fundamental lines 19 and 20 from the previous example conditionVariable.cpp.

```
```cpp
std::unique_lock<std::mutex> lck(mutex_);
condVar.wait(lck, []{ return dataReady; });
```
```

The two lines are equivalent to the following four lines:

```
```cpp
std::unique_lock<std::mutex> lck(mutex_);
while ( ![]{ return dataReady; }() ) {
    condVar.wait(lck);
}
```
```

First, you have to distinguish between the first call of `std::unique_lock<std::mutex> lck(mutex_)` and the notification of the condition variable `condVar.wait(lck)`.

+   - `std::unique_lock<std::mutex> lck(mutex_)`: In the initial processing, the thread locks the mutex and then check the predicate `[]{ return dataReady; }`.
+     - If the call of the predicate evaluates to
+       * `true`: the thread continues its work.
+       * `false`: `condVar.wait()` unlocks the mutex and puts the thread in a waiting (blocking) state

[^13]: https://en.wikipedia.org/wiki/POSIX_Threads
[^14]: https://en.wikipedia.org/wiki/Windows_API
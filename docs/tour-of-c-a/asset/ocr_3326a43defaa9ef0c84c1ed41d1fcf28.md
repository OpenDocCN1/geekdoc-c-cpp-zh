The corresponding producer looks like this:

Click here to view code image

```
void producer() {
  while(true) {
    Message m;
    // ... fill the message ...
    scoped_lock lck (mutex);
    mqueue.push(m);
    mcond.notify_one();
  }
}
```

# 18.5 Communicating Tasks

The standard library provides few facilities to allow programmers to operate at the conceptual level of tasks (work to potentially be done concurrently) rather than directly at the lower level of tasks and locks:

+   - future and promise for returning a value from a task spawned on a separate thread
- packaged_task to help launch tasks and connect up the mechanisms for returning a value
- async() for launching of a task in a manner very similar to calling a function

These facilities are found in <future>.

# 18.5.1 future and promise

The important point about future and promise is that they enable a transfer of a value between two tasks without explicit use of lock; "the system" implements the transfer efficiently. The basic idea is simple: when a task wants to pass a value to another, it puts the value into a promise. Somehow, the implementation makes value appearing in the corresponding future, from which it can be read (typically by the launcher of the task) graphically:

![](bbox=[0.223, 0.672, 0.735, 0.779])

If we have a future<X> called fx, we can get() a value of type X from it: 

Click here to view code image

```
X = fx.get(); // If necessary, wait for the value to get computed
```

If the value isn't there yet, our thread is blocked until it arrives. If the value couldn't
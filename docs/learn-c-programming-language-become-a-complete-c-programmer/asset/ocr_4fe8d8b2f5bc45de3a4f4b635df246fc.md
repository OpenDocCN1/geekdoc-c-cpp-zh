# Mutex Error Conditions (§iso.30.4.1.2)

resource_deadlock_would_occur resource_unavailable_try_again
operation_not_permitted
device_or_resource_busy
invalid_argument

A deadlock would occur
Some native handle is not available
The thread is not allowed to perform the operation Some native handle is already locked
A constructor native handle argument is bad

```
mutex mtx; try {
mtx.lock();
mtx.lock(); // try to lock a second time
}
catch (system_error& e) {
mtx.unlock();
cout << e.what() << '\n';
cout << e.code() << '\n';
}
```

I got the output

device or resource busy
generic: 16

This looks like a good argument for using a lock_guard or a unique_lock (§42.3.1.4).

# 42.3.1.3 timed_mutex and recursive_timed_mutex

A simple mtx.lock() is unconditional. If we don’t want to block, we can use mtx.try_lock(), but when we fail to acquire mtx, we often want to wait for a while before trying again. The timed_mutex and recursive_timed_mutex offer support for that:

timed_mutex m {}; m.~timed_mutex() m.lock()
m.try_lock()
m.try_lock_for(d)
m.try_lock_until(tp)
m.unlock()
native_handle_type timed_mutex

# (§iso.30.4.1.3.1)

Default constructor; m is not owned; constexpr; noexcept Destructor: undefined behavior if owned
Acquire m; block until ownership is acquired
Try to acquire m; did the acquisition succeed?
Try to acquire m for a maximum duration of d; did the acquisition succeed?
Try to acquire m until time_point tp at the latest; did the acquisition succeed?
Release m
Implementation-defined system mutex type

```
nh=m.native_handle() nh is the system handle for the mutex
```
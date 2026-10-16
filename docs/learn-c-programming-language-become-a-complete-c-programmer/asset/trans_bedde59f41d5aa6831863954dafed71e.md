
// ... compose work request ...
requests.push_back(w);
}
if (wqm.try_lock()) {
wq.splice(requests); // splice() requests into the list (§31.4.2)
wqm.unlock();
}
}
}

当某个服务器线程正在检查 wq 时，composer() 只是制作更多工作，而不是等待。

## Section 42.3.1.1 mutex and recursive_mutex 1223

使用锁时，我们必须提防死锁。也就是说，我们不能等待永远无法释放的锁。最简单的死锁形式只需要一个锁和一个线程。考虑线程安全输出操作的变体：

```
template<typename Arg, typename... Args>
void write(Arg a, Args tail...)
{
cout_mutex.lock();
cout << a;
write(tail...);
cout_mutex.unlock();
}
```

现在，如果一个线程调用 write(“Hello,”,“World!”)，它在对 tail 进行递归调用时会与自身死锁。

递归和相互递归的调用足够常见，标准提供了解决方案。recursive_mutex 就像普通的 mutex，只是单个线程可以重复获取它。例如：

```
recursive_mutex cout_mutex; // changed to recursive_mutex to avoid deadlock
template<typename Arg, typename... Args> void write(Arg a, Args tail...)
{
cout_mutex.lock();
cout << a;
write(tail...);
cout_mutex.unlock();
}
```

现在 write() 的递归调用会被 cout_mutex 正确处理。42.3.1.2 mutex Errors

尝试操作 mutex 可能会失败。如果是这样，mutex 操作会抛出 system_error。一些可能的错误反映了底层系统中的条件：

## Mutex Error Conditions (§iso.30.4.1.2)

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

## 42.3.1.3 timed_mutex and recursive_timed_mutex

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

The recursive_timed_mutex interface is identical to the timed_mutex interface (just as the recursive_mutex interface is identical to the mutex interface).

For this_thread, we can sleep_until(tp) a time_point and sleep_for(d) a duration (§42.2.6). More generally, we can m.try_lock_until(tp) or m.try_lock_for(d) for a timed_mutex m. If tp is before the current point in time or d is less than or equal to zero, the operation is equivalent to a “plain” try_lock().

As an example, consider updating an output buffer with a new image (e.g., in a video game or a visualization):

```
extern timed_mutex imtx;
extern Image buf;
```

## Section 42.3.1.3 timed_mutex and recursive_timed_mutex 1225

```
void next()
{
while (true) {
Image next_image; // ... compute ...
if (imtx.try_lock(milliseconds{100})) {
buf=next_image;
imtx.unlock();
}
}
}
```

The assumption here is that if the image cannot be updated reasonably fast (here, in 100 milliseconds), the user would prefer a newer version of the image. Further, it is assumed that missing an image in a sequence of updated images will rarely be noticed, so that a more complicated solution is not needed.

## 42.3.1.4 lock_guard and unique_lock

A lock is a resource, so we must not forget to release it. That is, each m.lock() operation must be matched by an m.unlock() operation. The usual opportunities for mistakes exist; for example:

```
void use(mutex& mtx, Vector<string>& vs, int i)
{
mtx.lock();
if (i<0) return;
string s = vs[i];
// ...
mtx.unlock();
}
```

The mtx.unlock() is there, but if i<0 or if i is out of vs’s range and vs is range checked, the thread of execution never gets to the mtx.unlock() and mtx may be locked forever.

The standard library provides two RAII classes, lock_guard and unique_lock, to handle such problems.

The “plain” lock_guard is the simplest, smallest, and fastest guard. In exchange for added functionality, unique_ptr carries a small cost, which may or may not be significant for a given application on a given machine.

lock_guard lck {m}; lock_guard lck {m,adopt_lock_t}; lck holds m; assume that the current thread has already acquired m; noexcept lck.~lock_guard() Destructor: calls unlock() for the mutex held
lock_guard<M> (§iso.30.4.2) m is a lockable object
lck acquires m; explicit

```
void use(mutex& mtx, vector<string>& vs, int i) {
lock_guard<mutex> g {mtx};
if (i<0) return;
string s = vs[i];
// ...
}
```

The lock_guard’s destructor does the necessary unlock() on its argument.

As usual, we should only hold a lock for the minimal amount of time, so a lock_guard should not become an excuse for holding a lock until the end of a large scope if we only need the lock for a small section of the scope. Obviously, the checking of i does not require locking, so we could do that before acquiring the lock:

```
void use(mutex& mtx, vector<string>& vs, int i)
{
if (i<0) return;
lock_guard<mutex> g {mtx};
string s = vs[i];
// ...
}
```

Furthermore, imagine that we only needed the lock for the read of v[i]. Then, we could put the lock_guard in a small scope:

```
void use(mutex& mtx, vector<string>& vs, int i)
{
if (i<0) return; string s;
{
lock_guard<mutex> g {mtx};
s = vs[i];
}
// ...
}
```

Is such complication of the code worthwhile? Without looking at the code “hidden in the ...” we cannot tell, but we should definitely not use a lock_guard just out of unwillingness to consider where locking is needed. Minimizing the size of critical sections is in general a useful thing to do. If nothing else, it forces us to think about exactly where a lock is needed and why.

So, a **lock_guard** (and also a **unique_lock**) is a resource handle (“a guard”) for an object that you can lock to acquire ownership and unlock to release.

## **lock_guard** lockable object

## Section 42.3.1.4 **lock_guard** and **unique_lock** 1227

Such an object is called a *lockable object*. The obvious lockable object is of a standard-library mutex type, but users can define their own.

A **lock_guard** is a very simple class with no interesting operations. All it does is RAII for a **mutex**. To get an object that provides RAII and operations on a contained **mutex**, we use a **unique_lock**:

## **unique_lock<M>** (§iso.30.4.2)

**m** is a lockable object

- **unique_lock lck {}**; Default constructor: **lck** does not hold a mutex; noexcept
- **unique_lock lck {m}**; **lck** acquires **m**; explicit
- **unique_lock lck {m, defer_lock_t}**; **lck** holds **m** but does not acquire it
- **unique_lock lck {m, try_to_lock_t}**; **lck** holds **m** and does a **m.try_lock()**; if the try succeeds **lck** owns **m**; otherwise not
- **unique_lock lck {m, adopt_lock_t}**; **lck** holds **m**; assume that the current **thread** has already acquired **m**
- **unique_lock lck {m, tp}**; **lck** holds **m** and calls **m.try_lock_until(tp)**; if the try succeeds, **lck** owns **m**; otherwise not
- **unique_lock lck {m, d}**; **lck** holds **m** and calls **m.try_lock_for(d)**; if the try succeeds, **lck** owns **m**; otherwise not
- **unique_lock lck {lck2}**; Move constructor: **lck** holds the mutex (if any) held by **lck2**; **lck2** does not hold a mutex

**lck.~unique_lock()**
**lck2=move(lck)**

Destructor: calls **unlock()** for the mutex held (if any) Move assignment: **lck** holds the mutex (if any) held by **lck2**; **lck2** does not hold a mutex

**lck.lock()** **m.lock()**
**lck.try_lock()** **m.try_lock()**; did acquisition succeed? **lck.try_lock_for(d)**
**m.try_lock_for(d)**; did acquisition succeed? **lck.try_lock_until(tp)**
**m.try_lock_until(tp)**; did acquisition succeed? **lck.unlock()** **m.unlock()**
**lck.swap(lck2)** Exchange the lockable objects of **lck** and **lck2**;

noexcept
**pm=lck.release()** **lck** no longer owns **∗pm**; noexcept **lck.owns_lock()**
**bool b {lck}**

Does **lck** own a lockable object? noexcept Conversion to **bool**; **b==lck.owns_lock()**; explicit; noexcept
**pm=lck.mutex()** **∗pm** is the owned lockable object, if any;

otherwise **pm=nullptr**; noexcept **swap(lck,lck2)** **lck.swap(lck2)**; noexcept
Obviously, the timed operations are only allowed if the contained mutex is a **timed_mutex** or a **recursive_timed_mutex**.

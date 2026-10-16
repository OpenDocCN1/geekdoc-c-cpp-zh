So, a **lock_guard** (and also a **unique_lock**) is a resource handle (“a guard”) for an object that you can lock to acquire ownership and unlock to release.

# **lock_guard** lockable object

# Section 42.3.1.4 **lock_guard** and **unique_lock** 1227

Such an object is called a *lockable object*. The obvious lockable object is of a standard-library mutex type, but users can define their own.

A **lock_guard** is a very simple class with no interesting operations. All it does is RAII for a **mutex**. To get an object that provides RAII and operations on a contained **mutex**, we use a **unique_lock**:

# **unique_lock<M>** (§iso.30.4.2)

**m** is a lockable object

+   - **unique_lock lck {};** Default constructor: **lck** does not hold a mutex; noexcept
+   - **unique_lock lck {m};** **lck** acquires **m**; explicit
+   - **unique_lock lck {m, defer_lock_t};** **lck** holds **m** but does not acquire it
+   - **unique_lock lck {m, try_to_lock_t};** **lck** holds **m** and does a **m.try_lock()**; if the try succeeds **lck** owns **m**; otherwise not
+   - **unique_lock lck {m, adopt_lock_t};** **lck** holds **m**; assume that the current **thread** has already acquired **m**
+   - **unique_lock lck {m, tp};** **lck** holds **m** and calls **m.try_lock_until(tp)**; if the try succeeds, **lck** owns **m**; otherwise not
+   - **unique_lock lck {m, d};** **lck** holds **m** and calls **m.try_lock_for(d)**; if the try succeeds, **lck** owns **m**; otherwise not
+   - **unique_lock lck {lck2};** Move constructor: **lck** holds the mutex (if any) held by **lck2**; **lck2** does not hold a mutex

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
**bool b {lck};**

Does **lck** own a lockable object? noexcept Conversion to **bool**; **b==lck.owns_lock()**; explicit; noexcept
**pm=lck.mutex()** **∗pm** is the owned lockable object, if any;

otherwise **pm=nullptr**; noexcept **swap(lck,lck2)** **lck.swap(lck2)**; noexcept
Obviously, the timed operations are only allowed if the contained mutex is a **timed_mutex** or a **recursive_timed_mutex**.
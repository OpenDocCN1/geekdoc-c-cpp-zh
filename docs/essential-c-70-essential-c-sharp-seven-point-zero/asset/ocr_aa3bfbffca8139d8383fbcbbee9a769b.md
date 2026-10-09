In summary, you should use a per-synchronization context instance of type `object` for the lock target.

# **Guidelines**

AVOID locking on `this`, `typeof()`, or a string.
DO declare a separate, read-only synchronization variable of type `object` for the synchronization target.

# ADVANCED TOPIC

# **Avoid Synchronizing with MethodImplAttribute**

One synchronization mechanism that was introduced in .NET 1.0 was the `MethodImplAttribute`. Used in conjunction with the `MethodImplOptions.Synchronized` method, this attribute marks a method as synchronized so that only one thread can execute the method at a time. To achieve this, the JIT essentially treats the method as though it was surrounded by `lock(this)` or, in the case of a static method, locks on the type. Such an implementation means that, in fact, the method and all other methods on the same class, decorated with the same attribute and enum parameter, are synchronized—rather than each method being synchronized relative to itself. In other words, given two or more methods on the same class decorated with the attribute, only one of them will be able to execute at a time, and the one executing will block all calls by other threads to itself or to any other method in the class with the same decoration. Furthermore, since the synchronization is on `this` (or even worse, on the `type`), it suffers the same detriments as `lock(this)` (or worse, for the static) discussed in the preceding section. As a result, it is a best practice to avoid the attribute altogether.

# **Guidelines**

AVOID using the `MethodImplAttribute` for synchronization.

# **Declaring Fields as volatile**

On occasion, the compiler or CPU may optimize code in such a way that the instructions do not occur in the exact order they are coded,
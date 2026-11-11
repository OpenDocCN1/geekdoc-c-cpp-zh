The task calls some methods, all within the same thread, and eventually one of them needs the connection:

```
```java
var result = connection.get().executeQuery(query);
```
```

Note that the same call may happen on multiple threads. Each of them gets its own connection object.

> > **CAUTION:**
> >
> > In the preceding example, it is crucially important that only one task uses the thread. When executing tasks with a thread pool, you don’t want to make your database connection available to the other tasks that share the same thread.

![](bbox=[0.128, 0.318, 0.181, 0.358])

# `java.lang.ThreadLocal<T>` 1.2

+   - `T get()`
+   
+     gets the current value of this thread. If `get` is called for the first time, the value is obtained by calling `initialize`.
+   
+   - `void set(T t)`
+   
+     sets a new value for this thread.
+   
+   - `void remove()`
+   
+     removes the value for this thread.
+   
+   - `static <S> ThreadLocal<S> withInitial(Supplier<? extends S> supplier)` 8
+   
+     creates a thread-local variable whose initial value is produced by invoking the given supplier.
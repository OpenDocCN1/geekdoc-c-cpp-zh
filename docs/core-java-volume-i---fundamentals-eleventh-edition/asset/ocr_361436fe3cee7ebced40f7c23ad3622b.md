For example, suppose an object has a boolean flag done that is set by one thread and queried by another thread. As we already discussed, you can use a lock:

```
```java
private boolean done;
public synchronized boolean isDone() { return done; }
public synchronized void setDone() { done = true; }
```
```

Perhaps it is not a good idea to use the intrinsic object lock. The isDone and setDone methods can block if another thread has locked the object. If that is a concern, one can use a separate lock just for this variable. But this is getting to be a lot of trouble.

In this case, it is reasonable to declare the field as volatile:

```
```java
private volatile boolean done;
public boolean isDone() { return done; }
public void setDone() { done = true; }
```
```

The compiler will insert the appropriate code to ensure that a change to the done variable in one thread is visible from any other thread that reads the variable.

![](bbox=[0.193, 0.498, 0.237, 0.532])

> > **CAUTION:** Volatile variables do not provide any atomicity. For example, the method
> >
> > ```java
> > public void flipDone() { done = !done; } // not atomic
> > ```
> >
> > is not guaranteed to flip the value of the field. There is no guarantee that the reading, flipping, and writing is uninterrupted.

# 12.4.9 Final Variables

As you saw in the preceding section, you cannot safely read a field from multiple threads unless you use locks or the volatile modifier.

There is one other situation in which it is safe to access a shared field—when it is declared final. Consider

```
```java
final var accounts = new HashMap<String, Double>();
```
```

Other threads get to see the accounts variable after the constructor has finished.

Without using final, there would be no guarantee that other threads would see the updated value of accounts—they might all see null, not the constructed HashMap.

Of course, the operations on the map are not thread-safe. If multiple threads mutate and read the map, you still need synchronization.
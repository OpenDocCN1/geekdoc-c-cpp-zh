Now, Thread 1 also calls await, and *all* threads are blocked. The system has deadlocked.

The culprit here is the call to signal. It only unblocks one thread, and it may not pick the thread that is essential to make progress. (In our scenario, Thread 2 must proceed to take money out of Account 2.)

Unfortunately, there is nothing in the Java programming language to avoid or break these deadlocks. You must design your program to ensure that a deadlock situation cannot occur.

# 12.4.12 Thread-Local Variables

In the preceding sections, we discussed the risks of sharing variables between threads. Sometimes, you can avoid sharing by giving each thread its own instance, using the ThreadLocal helper class. For example, the SimpleDateFormat class is not thread-safe. Suppose we have a static variable

```
```java
public static final SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
```
```

If two threads execute an operation such as

```
```java
String dateStamp = dateFormat.format(new Date());
```
```

then the result can be garbage since the internal data structures used by the dateFormat can be corrupted by concurrent access. You could use synchronization, which is expensive, or you could construct a local SimpleDateFormat object whenever you need it, but that is also wasteful.

To construct one instance per thread, use the following code:

```
```java
public static final ThreadLocal<SimpleDateFormat> dateFormat
    = ThreadLocal.withInitial(() -> new SimpleDateFormat("yyyy-MM-dd"));
```
```

To access the actual formatter, call

```
```java
String dateStamp = dateFormat.get().format(new Date());
```
```

The first time you call get in a given thread, the lambda in the constructor is called. From then on, the get method returns the instance belonging to the current thread.

A similar problem is the generation of random numbers in multiple threads. The java.util.Random class is thread-safe. But it is still inefficient if multiple threads need to wait for a single shared generator.

You could use the ThreadLocal helper to give each thread a separate generator, but Java 7 provides a convenience class for you. Simply make a call such as

```
```java
int random = ThreadLocalRandom.current().nextInt(upperBound);
```
```
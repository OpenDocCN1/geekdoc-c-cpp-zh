
```
private val userCount = AtomicInteger(0)

def getRank(): Int = userCount.incrementAndGet()
```

### Listing 18.3: Using an AtomicInteger to generate unique values.

Consider now this variant of the problem in which only the first five users are allowed to register. Registration success or failure is indicated by returning an option:

```
// DON'T DO THIS!
def getRank(): Option[Int] =
  if userCount.get < 5 then Some(userCount.incrementAndGet()) else None
```

### Listing 18.4: Example of non-atomic check-then-act; fixed in Lis. 18.7.

This variant is incorrect. The use of incrementAndGet guarantees that ranks will be unique. However, this code makes it possible for more than five users to register. A possible scenario is depicted in Figure 18.3. The failure is caused by two threads checking the condition userCount.get < 5 at the same time. The issue here is the non-atomicity of the test and the action that follows it, which still take two steps: one to check that a value is less than five, then another to increment it and return the incremented value. Class AtomicInteger does not define a method that executes the whole computation—check, increment, and get—in one atomic step.

![](img/74309e2bdd93f68d2e94338a3d73517f_314_0.png)

### Figure 18.3 Possible interleaving of two non-atomic check-then-act.

Non-atomic check-then-act is a common source of concurrency bugs. You should always think carefully when you write a conditional in a multithreaded program. With practice, it becomes second nature to start thinking about threads switched out of execution right after an if, before the then or else code.

You can show that the two flawed getRank implementations are incorrect by writing a test in which multiple threads call the function at the same time. The test succeeds

sometimes, but sometimes fails. It fails when the atomic integer is accessed by another thread between increment and get (first example), or between if and then (the second example). You can make these failures more likely by inserting calls to Thread.yield (see Section 17.5) in the code of function getRank:

```
def getRank(): Int =
  userCount.increment()
  Thread.`yield`()
  userCount.get()

def getRank(): Option[Int] =
  if userCount.get() < 5 then
    Thread.`yield`()
    Some(userCount.incrementAndGet())
  else None
```

With added calls to Thread.yield, the test fails much more frequently. By contrast, adding calls to Thread.yield in a correct program should never break it. It is often a good testing strategy to insert such calls in places where a thread losing control of the CPU is thought to potentially be unsafe; correct code should continue to behave correctly.

### Aside: Example of a Heisenbug

Consider this modified version of Listing 18.2:

```
val shared = ArrayList[String]()

def addStrings(n: Int, str: String): Unit =
  var added = 0
  while added < n do
    if shared.size >= 2 * added then
      shared.add(str)
      added += 1

val t1 = Thread(() => addStrings(5, "T1"), "T1")
val t2 = Thread(() => addStrings(5, "T2"), "T2")

t1.start(); t2.start()
t1.join(); t2.join()

println(shared.size)
```

In this variant, each thread checks that it is not too far ahead of the other thread before adding a value into the shared list. A thread adds a new item to the list

only if the list is at least twice as long as the number of items already added by that thread. When run on my computer, this program prints nothing and keeps running.

In an attempt to help debug the problem, you can log the value of variable added using a simple print statement:

```
Scala
...
while added < n do
  println(added)
  if shared.size >= 2 * added then
...
```

Remarkably, this modified program does terminate, with the expected output:

```
T1 at XX:XX:28.543: 0
T2 at XX:XX:28.543: 0
T1 at XX:XX:28.543: 1
T2 at XX:XX:28.543: 1
T1 at XX:XX:28.544: 2
T2 at XX:XX:28.544: 2
T1 at XX:XX:28.544: 3
T2 at XX:XX:28.544: 3
T2 at XX:XX:28.544: 4
T1 at XX:XX:28.544: 4
main at XX:XX:28.544: 10
```

Note that this program is still incorrect: A java.util.ArrayList, which is not a thread-safe structure, is shared among threads without synchronization. However, the bug no longer manifests itself. Commenting out the print statement and running the program results again in nontermination. Such bugs, which disappear when observed, are sometimes facetiously called Heisenbugs.

## 18.4 Locking

The incorrect code examples so far in this chapter all make the same mistake: Threads share mutable data without proper synchronization. There are different approaches to solving this problem, some of which are discussed in later chapters, but locking remains one of the most commonly used techniques to synchronize thread manipulation of shared data.

The basic principle of locking is to guard portions of code (such as functions and methods) with locks that need to be acquired before running the code. The most com-

mon form of lock is the exclusive lock, which can be acquired by only one thread at a time. When a thread acquires an exclusive lock, the thread is said to own the lock. Ownership ceases when the lock is released by the thread. While a thread owns an exclusive lock, the lock is not available to other threads. Any attempt by another thread to acquire the lock is denied, usually by blocking the requesting thread until the lock becomes available.

In Listing 18.2, two threads add strings into a shared list, leading to undesirable behaviors and incorrect output. To fix the problem, one strategy could be to have each thread acquire an exclusive lock before it can add a string to the list:

```
exclusiveLock.lock()
shared.add(str)
exclusiveLock.unlock()
```

Because the lock is exclusive, you cannot have two threads inside the list’s add method at the same time. Instead, one thread must complete the execution of the entire call to add before it releases the lock and another threads starts the method again. In effect, method add now appears to be atomic: It is not possible for a thread to partially run the method and have another thread come in. In particular, the intermediate states that the list can have while a thread is executing add are not visible to other threads—assuming the list is not used elsewhere in the application.

## 18.5 Intrinsic Locks

The JVM defines its own basic form of exclusive locks, called intrinsic locks. (Other types of locks are discussed in Section 23.1.) In Scala, intrinsic locks are acquired and released by a method synchronized, which takes its code argument by name, unevaluated (see Section 12.2):

```
lock.synchronized(shared.add(str))
```

or

```
lock.synchronized {
  shared.add(str)
}
```

(Recall that Scala lets you invoke a single argument function using braces instead of parentheses.) The lock is acquired upon entry into the specified code fragment and released when the thread exits this code, either normally or by throwing an exception. While a thread is inside the synchronized method, the lock is not available, and other

threads attempting to acquire it will be blocked. The value lock must be a reference to an object. Any Java object can be used as a lock.⁴

The incorrect list sharing program of Listing 18.2 can be fixed using an intrinsic lock:

```
val shared = ArrayList[String]()

def addStrings(n: Int, str: String): Unit =
  n times {
    shared.synchronized(shared.add(str))
  }

val t1 = Thread(() => addStrings(5, "T1"), "T1")
val t2 = Thread(() => addStrings(5, "T2"), "T2")

t1.start(); t2.start()
t1.join(); t2.join()

println(shared.size)
```

### Listing 18.5: Multiple threads share a list safely; fixed from Lis. 18.2.

Both threads need to lock the shared object before they can call its add method. Since only one thread can own the lock at any given time, it is now impossible for multiple threads to be inside the add method at the same time. The size of the list displayed at the end of the program is now guaranteed to be 10.

In Listing 18.5, the lock is acquired and released before and after each call to add. As an alternative, a thread could acquire the lock once and keep it while calling add multiple times:

```
def addStrings(n: Int, str: String): Unit = shared.synchronized {
  n times shared.add(str)
}
```

In this case, locking makes the entire function addStrings appear atomic: One thread adds all its strings to the list, followed by all the strings of the other thread. There will be no interleaving of "T1" and "T2" in the list.

Which function addStrings is right? It depends on the needs of your application. If, for instance, a list of strings is shared for the purpose of logging, and threads call the add method to add a logging message, locking each invocation of add separately might be the right choice. Conversely, if method add is used to add one line of a multiline logging message, you will probably have to synchronize a single block around multiple

⁴When using locks, you should stick to objects that you have allocated. Some objects are created implicitly by the JVM—for instance, to box primitive values—and cannot reliably be used as locks.

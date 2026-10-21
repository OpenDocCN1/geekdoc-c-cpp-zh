
In short, some of the techniques you could use to maintain data encapsulation in a single-threaded context are inadequate in the presence of multiple threads. You can still write a thread-safe variant of method getAll, but at the cost of a full copy of the list:

```scala
def getAll: List[String] = ArrayList(synchronized(contents))
```

Such defensive copies can often be avoided by implementing mutable objects in terms of immutable data structures. This was discussed in Section 3.8, and Section 19.5 will revisit the topic in the context of multiple threads.

## 19.4 Public and Private Locks

In the implementation of SafeStringList in Listing 19.2, the wrapper itself is used as the lock. This design choice makes the lock public—code that uses a SafeStringList can access the lock directly—and offers the benefit of client-side locking.

For instance, you can write a function to add elements up to a maximum size:

```scala
val shared: SafeStringList = ...

def addStringIfCapacity(str: String, bound: Int): Boolean = shared.synchronized {
  if shared.size >= bound then false
  else
    shared.add(str)
    true
}
```

Listing 19.3: Example of client-side locking.

This function adds a string to the shared list only if the size of the list remains within a given bound. It is similar to function getRank in Listing 18.7 and requires locking for the same reason—atomicity of check-then-act. Such locking is made possible by the fact that the lock used internally in the implementation of methods add and size has been made public (and is reentrant).

Three main difficulties must be considered when using public locks. First is the issue of documentation: It needs to clearly state which lock is used and becomes binding afterwards, preventing future implementations from using another (public or private) lock instead. As an example, the documentation of Java's Collections.synchronizedList—a standard library function similar to SafeStringList—specifies that “It is imperative that the user manually synchronize on the returned list when traversing it,” thus indicating that the wrapper itself is the lock that is used internally.

Second, public locks involve a risk of being misused by code that locks the list when it should not. A thread that executes code of the form

```scala
shared.synchronized {
  // lengthy computation, or I/O, or other blocking calls...
}
```

prevents other threads from accessing the shared list in any way, even just to query its size, possibly for a long time.

Third and finally, public locking is viable only when using simple synchronization policies—SafeStringList uses a single lock. It ceases to be workable with more complex strategies, such as lock striping (e.g., java.util.concurrent.ConcurrentHashMap) and lock-free algorithms (e.g., java.util.concurrent.ConcurrentLinkedQueue).

To circumvent these difficulties, locks can be kept private:

```scala
class SafeStringList:
  private val contents = ArrayList[String]()

  def add(str: String): Unit = contents.synchronized(contents.add(str))
  def size: Int = contents.synchronized(contents.size)
```

Listing 19.4: Safe list based on a private lock; contrast with Listing 19.2.

This implementation of SafeStringList is just as thread-safe as before but uses a private object, the inner list, as a lock. The drawback, of course, is that external functions that require an atomic iteration or an atomic check-then-act cannot be written. A function like addStringIfCapacity from Listing 19.3 is no longer possible because it has no access to contents for locking. As an alternative, you can enrich SafeStringList to offer additional atomic operations, but users will be limited to what the class defines.

## 19.5 Leveraging Immutable Types

This chapter began with the observation that immutable structures are naturally thread-safe. It is also true that mutable objects can often be implemented in terms of immutable data stored in reassignable fields (see Section 4.1 for an example). This dual observation yields the following thread-safe SafeStringList implementation:⁴

```scala
class SafeStringList:
  private var contents = List.empty[String]

  def add(str: String): Unit = synchronized(contents ::= str)
  def size: Int = synchronized(contents.size)
  def getAll: List[String] = synchronized(contents)
```

Listing 19.5: Safe list based on an immutable list; contrast with Listings 19.2 and 19.4.

The List type refers here to Scala’s lists, and contents is now an immutable list. Instead of a val, the list is stored into a var field so it can be reassigned. You add elements by setting contents to a new list—contents ::= str is the same as contents = str :: contents. An interesting aspect of this implementation is that getAll simply returns a reference to the internal list, avoiding the copy that would be needed if you used a mutable list. The internal list ends up being shared among threads but, because the list is immutable, this sharing is harmless.⁵

Of course, locking is still needed to read and write variable contents. This variant uses a public lock, the wrapper itself (this). If a private lock is preferred, locking on the underlying list, as in Listing 19.4, is not an option:

```scala
// DON'T DO THIS!
class SafeStringList:
  private var contents = List.empty[String]

  def add(str: String): Unit = contents.synchronized(contents ::= str)
  ...
```

> ⁴I assume here that threads obtain references to objects from other threads through proper synchronization, as is typically the case. Otherwise, the subtleties of the Java Memory Model again come into play, and the contents field would need to be initialized while owning the lock:
> 
>     private var contents: List[String] = uninitialized
>     synchronized {
>       contents = List.empty
>     }

> ⁵Because values are always added to the front of the list, they are returned in reverse order. If order is relevant, an immutable type other than a list, such as an immutable queue, can be used.

This approach does not work. A thread that calls add needs to read the value of contents first, before it can use it as a lock. This reading is done without locking and is incorrect.

A peek at the bytecode for method add helps make the issue more tangible:

```text
0: aload 0
1: getfield #38 // Field contents:Lscala/collection/immutable/List;
4: dup
5: astore 2
6: monitorenter
7: aload 0
8: aload 0
9: getfield #38 // Field contents:Lscala/collection/immutable/List;
12: aload 1
13: invokevirtual #51 // Method scala/collection/immutable/List.$colon$colon ...
16: putfield #38 // Field contents:Lscala/collection/immutable/List;
...
```

Field contents is read on line 1, without any locking. It is then locked on line 6—monitorenter is the JVM locking instruction—and read again on line 9. Between lines 1 and 6, variable contents could be written by another thread that invokes method add, in which case the list that is read here on line 9 is different from the list that is locked on line 6. A scenario, in simplified bytecode, is shown in Figure 19.1. After three calls to method add, the list contains only two values. Note how, at some point, the two threads end up locking two different objects—an empty list and a list that contains only “B”—and proceed inside their synchronized code in parallel.

Figure 19.1 Possible interleaving of three SafeStringList.add operations.

```text
contents=list[]

Thread T1                          Thread T2

// add("A")
getfield #38 → list[]

// add("B")
getfield #38 → list[]

monitorenter: lock list[]
getfield #38 → list[B]
putfield #38 ← list[A,B]
monitorexit

// add("C")
monitorenter: lock list[]
getfield #38 → list[B]
putfield #38 ← list[A,B,C]
monitorexit

contents=list[C,B]
```

You can use a val field as a lock to guard itself, as in Listings 18.5 and 19.4, but you cannot do that with a reassignable var field. (The same applies to final and non-final fields in Java.) Instead, you need to create an additional locking target, as in Listing 18.7:

```scala
class SafeStringList:
  private var contents = List.empty[String]

  private val lock = Object()

  def add(str: String): Unit = lock.synchronized(contents ::= str)
  def size: Int = lock.synchronized(contents.size)
  def getAll: List[String] = lock.synchronized(contents)
```

Listing 19.6: Safe list with an immutable list/private lock; contrast with Listing 19.5.

## 19.6 Thread-Safety

Both this chapter and Chapter 18 include examples of flawed programs that behave incorrectly in the presence of multiple threads. We also saw how correctness can be brought back through locking, resulting in thread-safe objects that can handle concurrent accesses. So far in this discussion, however, “safe” (or “unsafe”) and “correct” (or “incorrect”) have only been loosely defined.

Some programs are clearly incorrect, like the program in Listing 18.2 that blows up with an exception when trying to add a string to a list. But what does it mean exactly for a program to be correct in the presence of concurrency? The program in Listing 18.5 is correct because a list of strings has length 10 in the end. But why is the value 10 expected? You could answer that running shared.add("T1") 5 times and shared.add("T2") 5 times in sequence produces a list of size 10, and thus that this should also be the case when the two computations are executed in parallel. But the sequential execution also produces all five "T1" values together and all five "T2" values together, and this is not expected of the parallel version, which can produce an arbitrary interleaving of "T1" and "T2" values. So, a parallel program might produce a list that is impossible in its sequential counterpart, yet not be considered incorrect because of that. A more detailed explanation is needed.

When you add a string to a list, there is an expectation that method add is atomic in its effects. The list first exists without the string, then with the entire string—there is no state of the list where a string is “half added.” The very definition of a list—the semantics of what it means to be a list—is expressed in terms of such atomic operations. The “thread-safe” expectation is that these atomic operations are preserved—in other words, that a list continues to be a list when accessed by multiple threads.

Concurrency can be formally defined in terms of interleaving of atomic operations. If A and B are atomic operations on a shared structure—like add or get on a list—and a thread executes A in parallel with another thread that executes B, denoted as A || B,

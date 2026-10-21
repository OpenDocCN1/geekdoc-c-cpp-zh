access an object, you make the object itself encapsulate its own policy. Objects capable of enforcing their policy internally are thread-safe: The required thread coordination is implemented inside the object’s methods, and threads can freely call these methods without further synchronization.

As an illustration, let’s rewrite the list-sharing example with an encapsulated locking strategy:

```
class SafeStringList:
  private val contents = ArrayList[String]()

  def add(str: String): Unit = synchronized(contents.add(str))
  def size: Int = synchronized(contents.size)
end SafeStringList

val shared = SafeStringList()

def addStrings(n: Int, str: String): Unit = n times shared.add(str)
```

Listing 19.2: Safe list that encapsulates synchronization; contrast with Lis. 18.5.

The array-based list, which is not thread-safe, is encapsulated inside a SafeStringList class. The inner list contents is private and accessed only via methods add and size. These methods implement the necessary synchronization by always locking this before they use the array list. You can now write function addStrings without any explicit synchronization.

Inside class SafeStringList, both methods use locking to access the inner list—not only add, which modifies the list, but also size, which just queries its size. This is extremely important: When mutable data is protected by a lock, all accesses to the data must go through the lock. This includes both writing and reading accesses.³

There are two main reasons for this requirement. First, locking when reading prevents undesirable read/write interactions. If read accesses are not locked, you could possibly observe intermediate, inconsistent states of a structure. Though unlikely in an array-based list, method size could be implemented by using a loop that traverses the list, and a list that is in the middle of a modification by a thread may not be in a state that is safe for another thread to perform this iteration. The second reason is more technical. It is a consequence of the Java Memory Model: Without locking when reading, there is no guarantee that a thread will see all the modifications to a structure that were made earlier by other threads, including data written with locks owned. The details are not essential, and the rule is simple: When locking, all accesses—writing and reading—must go through the same lock.

³Listing 18.5 correctly queries the size of the list at the end without locking, because the query is done after checking that both worker threads are terminated.
```
Some(userCount)
else None
}
```

# Listing 18.7: Atomic check-then-act using locking; fixed from Lis. 18.4.

Because locking is necessary to make the if-then-else atomic, there is no issue with incrementing a regular integer and AtomicInteger is not needed.

Depending on the circumstances, you can choose to protect data with a single lock, or decide to split data in chunks guarded by separate locks. Assume, for instance, that the registered users of Listing 18.7 are players, and a function play can be called by a registered user to act in the game:

```
Scala
def getRank(): Option[Int] = X.synchronized {
  // register user
}

def play(rank: Int): Unit = Y.synchronized {
  // act in the game
}
```

Depending on the internal design of the class, new user registration may or may not interfere with playing. If X and Y are references to the same object—X eq Y is true—the getRank and play functions are mutually exclusive: A thread inside one of the functions prevents other threads from entering the other function. If, however, X and Y refer to two distinct objects, a thread can be executing function getRank with the X lock owned, while another thread executes function play with the Y lock owned. Whether X and Y are the same object or two different objects, no two threads can execute getRank at the same time, and no two threads can execute play at the same time. Our next case study, in Chapter 20, explores different choices of the object used as a single lock and also discusses a two-lock variant of the same structure.

# 18.7 Summary

+   - JVM objects are allocated in a shared heap that all threads can access. If multiple threads have a reference to the same object, they can use it at the same time. However, the nondeterministic scheduling of threads makes it possible for them to be interrupted in the middle of an operation, possibly leaving data in a state that is not suitable for other threads to use. Mutable structures that were not designed with thread-safety in mind cannot be shared among threads without additional coordination, or they will fail in unpredictable ways. In particular, this is true of most collections from java.util.
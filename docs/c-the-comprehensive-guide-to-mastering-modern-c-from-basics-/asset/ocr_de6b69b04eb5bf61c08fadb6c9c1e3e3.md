wants to insert. Interruption is one thing, but with multithreading, as explained at the beginning, there is also the possibility of simultaneous events where the results are not visible to all threads. Even just writing the forward reference of the current last element can yield unexpected results if executed simultaneously by two threads.

# Mutable Mutex?

A method like contains() should be const; after all, data_ is only being read. However, as mx is also a data field of the class, it should not be modified. Locking the mutex changes it, however. Together with mutable, it is still possible to keep the const method.

Here I show you one of the rare meaningful uses of mutable data fields. You should not have to soften your interface just because you choose a particular form of implementation. Externally, it should not be visible to users that you are synchronizing threads with an internal data field.

Not as critical, but still not safe, when another thread wants to read the end of the list just as an item is being added.

Protected like this, you can use MxIntList with multiple threads without any issues.

29.2.5 Interface Design for Multithreading a simpl
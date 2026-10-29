# Sample Dialogue:

```
10
20
30
Deleting 10
Exiting program.
Deleting 20
Deleting 30
```

The big difference is that only the first node is deleted when the listTest function exits because it has no references. The remaining two nodes still have references due to the global variable. However, when the program finally exits, even these nodes go out of scope and memory is deallocated.

You should be aware that the shared_ptr class does not solve all of your problems. There is a problem if you make a circular list of references, in which case the reference count will never reach 0, and memory will not be reclaimed. To solve this problem, C++11 includes an additional class named weak_ptr, in which case an object will be destroyed if a weak_ptr is the only reference to it. As long as at least one of your links is connected by a weak_ptr, the entire circular list will eventually be deallocated.

C++11 also includes a class named unique_ptr that cannot be assigned to any other pointer. Older versions of C++ supported a class named auto_ptr, but it has been deprecated in C++11.
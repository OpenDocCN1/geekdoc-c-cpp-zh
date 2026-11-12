# B.13.3. __isConstant()

```
unsigned int __isConstant(const void *ptr);
```

Returns 1 if ptr contains the generic address of an object in constant memory space, otherwise returns 0.

# B.13.4. __isLocal()

```
unsigned int __isLocal(const void *ptr);
```

Returns 1 if ptr contains the generic address of an object in local memory space, otherwise returns 0.

# B.14. Warp Vote Functions

```
int __all_sync(unsigned mask, int predicate);
int __any_sync(unsigned mask, int predicate);
unsigned __ballot_sync(unsigned mask, int predicate);
unsigned __activemask();
```

Deprecation notice: __any, __all, and __ballot have been deprecated in CUDA 9.0 for all devices.

Removal notice: When targeting devices with compute capability 7.x or higher, __any, __all, and __ballot are no longer available and their sync variants should be used instead.

The warp vote functions allow the threads of a given warp to perform a reduction-and-broadcast operation. These functions take as input an integer predicate from each thread in the warp and compare those values with zero. The results of the comparisons are combined (reduced) across the active threads of the warp in one of the following ways, broadcasting a single return value to each participating thread:

__all_sync(unsigned mask, predicate):
Evaluate predicate for all non-exited threads in mask and return non-zero if and only if predicate evaluates to non-zero for all of them.

__any_sync(unsigned mask, predicate):
Evaluate predicate for all non-exited threads in mask and return non-zero if and only if predicate evaluates to non-zero for any of them.

__ballot_sync(unsigned mask, predicate):
Evaluate predicate for all non-exited threads in mask and return an integer whose Nth bit is set if and only if predicate evaluates to non-zero for the Nth thread of the warp and the Nth thread is active.

__activemask ():
Returns a 32-bit integer mask of all currently active threads in the calling warp. The Nth bit is set if the Nth lane in the warp is active when __activemask() is called. Inactive threads are represented by 0 bits in the returned mask. Threads which have exited the program are always marked as inactive. Note that threads that are convergent at an __activemask() call are not guaranteed to be convergent at
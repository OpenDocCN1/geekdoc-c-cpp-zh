are a thinly disguised non-local goto and that there are suddenly lots of ways to return from your method. Every single function call or message send becomes a potential return path.
You can fix this quite easily by adding an @finally block at the end of the @try block. Code in this block will always be executed, whether you exit the @try block by reaching the end or by throwing an exception.

The other problem you may encounter with exceptions is in rethrowing the exception released. Exception objects are usually autoreleased. This means that, with manual memory management, they will be deleted when the current autorelease pool is deleted.

This is not a problem in most code. The autorelease pool you are commonly using persists for the duration of the run loop. Sometimes, however, you will create your own autorelease pool.

If you drained your autorelease pool in an @finally block, as appears to be the obvious solution, you would encounter a problem. The exception object would be deleted while unwinding through your stack frame, and the next stack frame up would probably crash, dereferencing an orphaned pointer while looking up the type of the exception.

To avoid this, you need to make sure you retain the exception object before you delete the autorelease pool and then autorelease it
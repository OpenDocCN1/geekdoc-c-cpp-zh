```
[myFoo release];
return 0;
}
```

# Program 17.6 Output

```
myFoo retain count = 1
after pool drain = 1
after autorelease = 1
after retain = 2
after second pool drain = 1
```

The program allocates a new Foo object and assigns it to the variable myFoo. Its initial retain count is 1, as you've already seen. Notice the autorelease message, so draining the pool does not invalidate the.A new pool is allocated, and myFoo is added to the pool by an autorelease message. Again that its reference count doesn't change, because adding an object to the autorelease pool does not affect its reference count—it only marks it for later release.

Next, you send myFoo a retain message. This changes its reference count to 2. When you drain the pool the second time, the reference count for myFoo is decremented by 1 which was previously sent by an autorelease message, and therefore, is a release message when the pool is released.

Because myFoo was retained before the pool released, its retain count after decrementing is still greater than 0. Therefore, myFoo survives the pool drain and is still a valid object. Of, you must now release yourself, which we do in Program 17.6 to clean up and avoid memory leaks.

Reread this explanation of the autorelease pool if it seems a little fuzzy to you. When you understand Program 17.6, will you thoroughly understand the autorelease pool and how it works.

# Summary of Memory-Management Rules

Lets summarize what you've learned about memory management in this chapter:

+   - Sending a release message does not necessarily destroy an object. When an object's reference count is decremented to 0, the object is destroyed. The system does this by sending the dealloc message to the object to free its memory.

+   - If you need to hold onto an object to make sure it doesn't get destroyed by someone, you should retain it. Make sure to release the object when you're done with it.

+   - Release any objects that you have retained or created using a copy, mutable-Copy, alloc, or new method.This includes properties that the retain or copy attribute.You can override dealloc to release your instance variables at the time your object is to be destroyed.
Use nonatomic here tells the system not to protect the property accessories with a mutex (mutually exclusive) lock. People writing threadsafe code use mutex locks to prevent two threads from executing in the same code at the same time, a situation that can often lead to dire problems. But these locks can slow programs down, and you can avoid using them if you know this code will only ever be running in a single thread.

If nonatomic is not specified or atomic is specified instead (which is the default), your instance variable will be protected with a mutex lock. This will ensure exclusive access to an instance variable and prevent potential race conditions that could occur if more than one thread in a multithreaded application is trying to simultaneously access the same instance variable.

# Note

There is no mutableCopy attribute for a property. So using the copy attribute, even with a mutable instance variable, will result in the copyWithZone: method being executed which, as mentioned, produces an immutable copy of the object by convention.

The same discussion about protecting the value of your instance variables applies to the getter routines. If you return a mutable object, you should ensure that changes to the returned value will not affect the value of your instance variables. In such a case, you can make a copy of the instance variable and return that instead of the original value.

Getting back to the implementation of a copy method, if you are copying instance variables that contain immutable objects (for example, immutable string objects), you might not need to make a new copy of the object's contents. It might suffice to simply make a new reference to the object by assigning it. For example, if you are
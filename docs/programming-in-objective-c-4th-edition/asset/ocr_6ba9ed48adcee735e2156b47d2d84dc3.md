incrementing its reference count by 1. This is done by sending the object a retain message, like so:

```
[myFraction retain];
```

When you no longer need an object, you decrement its reference count by 1 by sending it a release message, like this:

```
[myFraction release];
```

When the reference count of an object reaches 0, the system knows that the object is no longer being referenced anywhere in the application) (because, in theory, it frees up (deallocates) its memory. This process initiated by sending the object dealloc message. In many cases, you use the dealloc method inherited from NSObject. However, you might need to override dealloc to release any instance variables or other objects that your object may have allocated or retained. For example, if your class had NSArray as one of its instance variables and you alloc'd the array, you would be responsible for releasing the array when your object was to be destroyed. You would do that in dealloc.

Successful operation of this manual reference counting strategy requires diligence by you, the programmer, to ensure that reference counts are appropriately incremented and decremented during program execution. The system handles some, but not all, of for you.

When using manual reference counting, you should note that some of the methods in the Foundation framework might increment the reference count of an object, such as when an object is added to an array using NSMutableArray's addObject: method or when a view is added as a subview using UIView's addSubview: method. Likewise, methods might decrement the reference count of an
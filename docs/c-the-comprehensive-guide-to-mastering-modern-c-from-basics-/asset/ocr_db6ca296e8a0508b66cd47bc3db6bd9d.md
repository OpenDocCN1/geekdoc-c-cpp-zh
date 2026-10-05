Because the resource data_ and its mutex mx_ are closely related, I have encapsulated them together in a class here. This is particularly useful because you need to protect every access to data_. And in this way, you prevent users from accidentally using the list without a mutex. You don't have to put data_ and mx_ together in a class, but I strongly recommend it.

# Critical Section

```
The code block protected by the locked mutex is called a critical section.
```

The use of lock_guard in add and again in contains means that accesses within these methods are mutually exclusive: contains() will never see a list that is being modified within add().

Why is this important? The list class manages two references per element: one to the previous element and one to the next. To add an element, the following must happen:

+   - The new value must be wrapped in an element.
- The current last element must point forward to the new element.
- The new element must point forward to end().
- The new element must point backward to the current last element.

There can be a moment when it would be inconvenient to catastrophic if an inserting thread is interrupted during its work between these steps and another thread
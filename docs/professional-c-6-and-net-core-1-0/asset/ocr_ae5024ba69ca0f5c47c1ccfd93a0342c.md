key of 3 and a string value `three`; the second element has a key of 7 and a string value `seven`. This initializer syntax is easily readable and uses the same syntax as accessing the elements in the dictionary.

# ## Key Type

A type that is used as a key in the dictionary must override the method `GetHashCode` of the `object` class. Whenever a dictionary class needs to determine where an item should be located, it calls the `GetHashCode` method. The `int` that is returned by `GetHashCode` is used by the dictionary to calculate an index of where to place the element. We won’t go into this part of the algorithm; what you should know is that it involves prime numbers, so the capacity of a dictionary is a prime number.

The implementation of `GetHashCode` must satisfy the following requirements:

+   - The same object should always return the same value.
+   - Different objects can return the same value.
+   - It must not throw exceptions.
+   - It should use at least one instance field.
+   - The hash code should not change during the lifetime of the object.

Besides requirements that must be satisfied by the `GetHashCode` implementation, it’s also good practice to satisfy these requirements:

+   - It should execute as quickly as possible; it must be inexpensive to compute.
+   - The hash code value should be evenly distributed across the entire range of numbers that an `int` can store.

> **NOTE** *Good performance of the dictionary is based on a good implementation of the method `GetHashCode`.*

What’s the reason for having hash code values evenly distributed across the range of integers? If two keys return hashes that have the same index, the dictionary class needs to start looking for the nearest available free location to store the second item—and it will have to do some searching to retrieve this item later. This is obviously going to hurt performance. In addition, if a lot of your keys are tending to provide the same storage indexes for where they should be stored, this kind of clash becomes more likely. However, because of the way that Microsoft’s part of the algorithm works, this risk is minimized when the calculated hash values are evenly distributed between `int.MinValue` and `int.MaxValue`.

Besides having an implementation of `GetHashCode`, the key type also must implement the `IEquatable<T>.Equals` method or override the
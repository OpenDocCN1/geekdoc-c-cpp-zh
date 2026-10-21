integer increments are not atomic and can produce incorrect values in a multithreaded context, it is not surprising that multiple threads calling method add at the same time can overwrite each other, resulting in lost values.

If you run the program enough times, it will also exhibit another interesting behavior. The 6,402,829th run in my experiment produced an exception in thread T1:

```
Exception in thread "T1" java.lang.ArrayIndexOutOfBoundsException:
    Index 3 out of bounds for length 0
    at java.base/java.util.ArrayList.add(ArrayList.java:455)
    ...
```

An examination of the source code of the class ArrayList used in the test suggests an explanation. Lists are created using an empty array with zero capacity. When a first element is added to a list, this array is replaced with a newly allocated array (with a capacity of 10). In the failed run shown here, thread T2 created this new array and used it to insert three values into the list. Because class ArrayList does not include any mechanism for synchronization, thread T1 then tried to insert its first value (4th list element, at index 3) into the previous array, with zero capacity.

Functions typically consist of multiple statements, and most statements consist of even more elementary instructions at the machine code level. These can be interleaved in arbitrary ways by independent threads. As a result, code that was not designed to handle such interleaving is likely to break when instances are shared among threads. In particular, and with very few exceptions (Random is one), most classes in java.util are not safe for multithreaded use without synchronization. If you improperly share instances of classes such as HashMap and PriorityQueue between threads, they will exhibit unpredictable behavior similar to what was demonstrated using ArrayList.

Note that the programs being tested in this experiment were designed to fail, and they still can appear to behave correctly in thousands of successive runs. In these programs, threads interact in unrealistic ways, modifying shared data as often as possible, which increases the chances for an undesirable interaction. In an actual application, threads will perform independent work and only occasionally access a shared data structure at the same time. Failures will be more infrequent and harder to produce but still potentially devastating.

# 18.3 Atomic Operations and Non-atomic Composition

Some operations are guaranteed to be atomic. For instance, reading or writing a primitive int on the JVM is atomic: A thread will never see “half” an integer, or a mixture of bits from two separate integers. As we have seen, however, code that combines multiple atomic operations—such as reading and then writing to implement an increment—is not atomic by default.

As an illustration, consider the problem of assigning a unique rank to users as they register for a service: The first user gets rank 1, the next user rank 2, and so on. You
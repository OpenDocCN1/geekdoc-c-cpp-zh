# Solutions to Chapter 7 | Object Oriented Design

7.10 Describe the data structures and algorithms that you would use to implement a garbage collector in C++.

# SOLUTION

In C++, garbage collection with reference counting is almost always implemented with smart pointers, which perform reference counting. The main reason for using smart pointers over raw ordinary pointers is the conceptual simplicity of implementation and usage. With smart pointers everything related to garbage collection is performed behind the scenes - typically in constructors / destructors / assignment operator / explicit object management functions.

There are two types of functions, both of which are very simple:

```
RefCount::type1() {
    /* implementation depends on reference counting organisation.
    * There can also be no ref. counter at all (see approach #4) */
    incrementRefCount(); }

RefCounter::type2() {
    /* Implementation depends on reference counting organisation.
    * There can also be no ref. counter at all (see approach #4). */
    decrementRefCount();
    if (referenceCounterIsZero()) {
        destructObject();
    }
}
```

There are several approaches for reference counting implementation in C++:

+   1. Simple reference counting.
   struct Object { };
   struct RefCount {
       int count;
   };
   struct RefCountPtr {
       Object * pointee;
       RefCount * refCount;
   };

Advantages: performance.

Disadvantages: memory overhead because of two pointers.

+   2. Alternative reference counting.
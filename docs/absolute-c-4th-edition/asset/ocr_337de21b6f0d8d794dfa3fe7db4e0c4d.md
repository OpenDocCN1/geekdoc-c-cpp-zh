Casting from an ancestor type to a descended type is called downcasting and is very dangerous, since you are assuming that information is being added (added member variables and functions). The dynamic_cast that we discussed briefly in Chapter 1 is used for downcasting. It is of some possible use in defeating the slicing problem but is dangerously unreliable and fraught with pitfalls. A dynamic_cast may allow you to downcast, but it only works for pointer types, as in the following:

```
Pet *ppet;
ppet = new Dog;
Dog *pdog = dynamic_cast<Dog*>(ppet); //Dangerous!
```

We have had downcasting fail even in situations as simple as this, and so we do not recommend it.

The dynamic_cast is supposed to inform you if it fails. If the cast fails, the dynamic_cast should return NULL (which is really the integer 0).

If you want to try downcasting keep the following points in mind:

+   1. You need to keep track of things so that you know the information to be added is indeed present.
+   2. Your member functions must be virtual, since dynamic_cast uses the virtual function information to perform the cast.

# HOW C++ IMPLEMENTS VIRTUAL FUNCTIONS

You need not know how a compiler works in order to use it. That is the principle of information hiding, which is basic to all good program design philosophies. In particular, you need not know how virtual functions are implemented in order to use virtual functions. However, many people find that a concrete model of the implementation helps their understanding, and when reading about virtual functions in other books you are likely to encounter references to the implementation of virtual functions. So, we will give a brief outline of how they are implemented. All compilers for all languages (including C++) that have virtual functions typically implement them in basically the same way.

If a class has one or more member functions that are virtual, the compiler creates what is called a virtual function table for that class. This table has a pointer (memory address) for each virtual member function. The pointer points to the location of the correct code for that member function. If one virtual function was inherited and not changed, then its table entry points to the definition for that function that was given in the parent class (or other ancestor class if need be). If another virtual function had a new definition in the class, then the pointer in the table for that member function points to that definition. (Remember that the property of being a virtual function is

> 2 The standard says "The value of a failed cast to pointer type is the null pointer of the required result type. A failed cast to a reference type throws a bad_cast."
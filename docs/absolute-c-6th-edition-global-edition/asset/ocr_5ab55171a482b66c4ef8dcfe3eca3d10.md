# upcasting

Casting from a descendant type to an ancestor type is known as upcasting, since you are moving up the class hierarchy. Upcasting is safe because you are simply disregarding some information (disregarding member variables and functions). So, the following is perfectly safe:

```
vpet = vdog;
```

# downcasting

Casting from an ancestor type to a descended type is called downcasting and is very dangerous, since you are assuming that information is being added (added member variables and functions). The dynamic_cast that we discussed briefly in Chapter 1 is used for downcasting. It is of some possible use in defeating the slicing problem but is dangerously unreliable and fraught with pitfalls. A dynamic_cast may allow you to downcast, but it works only for pointer types, as in the following:

```
Pet *ppet;
ppet = new Dog;
Dog *pdog = dynamic_cast<Dog*>(ppet); //Dangerous!
```

We have had downcasting fail even in situations as simple as this, and so we do not recommend it.

The dynamic_cast is supposed to inform you if it fails. If the cast fails, the dynamic_cast should return NULL (which is really the integer 0).

If you want to try downcasting, keep the following points in mind:

+   1. You need to keep track of things so that you know the information to be added is indeed present.
+   2. Your member functions must be virtual, since dynamic_cast uses the virtual function information to perform the cast.

# How C++ Implements Virtual Functions

You need not know how a compiler works in order to use it. That is the principle of information hiding, which is basic to all good program design philosophies. In particular, you need not know how virtual functions are implemented in order to use virtual functions. However, many people find that a concrete model of the implementation helps their understanding; when reading about virtual functions in other books you are likely to encounter references to the implementation of virtual functions. So, we will give a brief outline of how they are implemented. All compilers for all languages (including C++) that have virtual functions typically implement them in basically the same way.
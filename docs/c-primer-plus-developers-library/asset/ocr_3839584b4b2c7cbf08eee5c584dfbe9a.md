int-to-Student conversion function does not make sense. Using explicit turns off implicit conversions. If this keyword were omitted, code like the following would be possible:

```
Student doh("Homer", 10); // store "Homer", create array of 10 elements
doh = 5; // reset name to "Nully", reset to empty array of 5 elements
```

Here, the inattentive programmer typed doh instead of doh[0]. If the constructor omitted explicit, 5 would be converted to a temporary Student object, using the constructor call Student(5), with the value of "Nully" being used to set the name member. Then assignment would replace the original doh with the temporary object. With explicit in place, the compiler will catch the assignment operator as an error.

> **C++ and Constraints**
> 
> C++ is full of features that allow programmers to constrain programmatic constructs to certain limits—explicit to remove the implicit conversion of single-argument constructors, const to constrain the use of methods to modify data, and more. The underlying motive is simply this: Compile-time errors are better than runtime errors.

# Initializing Contained Objects

Note that constructors all use the by-now-familiar member initializer list syntax to initialize the name and scores member objects. In some cases earlier in this book, such as the following, the constructors use it to initialize members that are built-in types:

```
Queue::Queue(int qs) : qsize(qs) { ... } // initialize qsize to qs
```

This code uses the name of the data member (qsize) in a member initializer list. Also constructors from previous examples, such as the following, use a member initializer list to initialize the base-class portion of a derived object:

```
hasDMA::hasDMA(const hasDMA & hs) : baseDMA(hs) { ... }
```

For inherited objects, constructors use the class name in the member initializer list to invoke a specific base-class constructor. For member objects, constructors use the member name. For example, look at the last constructor in Listing 14.1:

```
Student(const char * str, const double * pd, int n)
    : name(str), scores(pd, n) {}
```

Because it initializes member objects, not inherited objects, this constructor uses the member names, not the class names, in the initialization list. Each item in this initialization list invokes the matching constructor. That is, name(str) invokes the string (const char *) constructor, and scores(pd, n) invokes the ArrayDb (const double *, int) constructor, which, because of the typedef, really is the valarray<double> (const double *, int) constructor.

What happens if you don’t use the initialization list syntax? As with inherited components, C++ requires that all member objects be constructed before the rest of an object is constructed. So if you omit the initialization list, C++ uses the default constructors defined for the member objects’ classes.
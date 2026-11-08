# ## `dynamic_cast`

The `dynamic_cast` operator is useful for casting through virtual inheritance. `static_cast` can cast from a derived class to a base class, whether the inheritance is virtual or not. Say, however, you are given an object of type A, but you know it is actually an object of type B—and that B inherits virtually from A. If you want to cast this object back to B to use member functions that only B provides, you need to use `dynamic_cast`.

A few things about `dynamic_cast`. First, it only works on pointer-to-pointer or reference-to-reference conversions. Second, it can’t actually cast an object from A to a B if the object is not, in fact, a B (or of a type derived from B). A pointer-to-pointer `dynamic_cast` that fails returns null. A reference-to-reference failure throws a `std::bad_cast` exception.

# ## `reinterpret_cast`

The `reinterpret_cast` operator is a direct conversion with very few good uses. Most its operations give undefined results. What this means in practice is that you should read the compiler vendor’s documentation before using it for anything.

One use for it, as we saw in **StorageDurationSample**, is to cast a pointer to an integer type large enough to hold it. This gives the memory address of the pointer, which can be useful for debugging and tracing operations where you dump data to log files and create core dumps, but it may not be able to run a debugger easily. You will see it used legitimately at times for other purposes, but in general, it should be considered as the cast of last resort (excluding a C-style cast, which comes after `reinterpret_cast`).

# # C-style Cast

The C-style cast, (e.g., `auto someData = (SomeType*)dataOfSomeOtherType;`) is not your friend. You are undoubtedly familiar with it from C#, where it is highly useful. In C++, if you try to make a cast using that syntax, and the cast is invalid, you will produce an InvalidCastException. This happens because the CLR keeps track of the types of everything you’ve created and detects bad casts.

C++ does not check to see if your C-style cast is valid, assuming it compiles, of course. C++ just assumes that it is. If it’s a bad cast, and you are lucky, your program will crash immediately. If not, you will end up with data in an unknown state, which will certainly become corrupted in subtle and insidious ways.

Further, unlike the other casts, which you can easily spot by looking for `_cast`, C-style casts do not stick out. When you’re scanning lots of code quickly, parentheses wrapped around text looks as much like a function call as it does a cast operation. You could use a regular expression search for this in Visual Studio 2012: `\(.*\)[A-Z-a-z]`. Even so, you are still forgoing all the benefits and protections of the other casts.

The one thing a C-style cast can do that other casts cannot is cast an object to one of its protected or private inheritance base classes. You really shouldn’t do this since, if you need public inheritance, you should use public inheritance.

In short, don’t use C-style casts.

# # Sample

There is a sample, **CastingSample**, that demonstrates the many possible types of casting. It is included with the source code for this book. In the interest of brevity, I am omitting it here.
# Chapter 7 Functions: C++'s Programming Modules

And here is the output:

```
Using pointers to functions:
Address Value
02AF9E0: 1112.3
02AF9E8: 1542.6
```

```
Using an array of pointers to functions:
Address Value
02AF9E0: 1112.3
02AF9E8: 1542.6
02AF9F0: 2227.9
```

```
Using a pointer to a pointer to a function:
Address Value
02AF9E0: 1112.3
02AF9E8: 1542.6
02AF9F0: 2227.9
```

```
Using pointers to an array of pointers:
Address Value
02AF9E0: 1112.3
02AF9E8: 1542.6
02AF9F0: 2227.9
```

The addresses shown are the locations of the double values in the av array.
This example may seem esoteric, but pointers to pointers of functions are not unheard of. The usual implementation of virtual class methods (see Chapter 13, “Class Inheritance”) uses this technique. Fortunately, the compiler handles the details.

# Appreciating auto

One of the goals of C++11 is to make C++ easier to use, letting the programmer concentrate more on design and details. Listing 7.19 surely illustrates this point:

```
auto pc = &pa; // C++11 automatic type deduction
const double = *((*pd)[3]) (const double *, int) = &pa; // C++98, do it your yourself
```

The automatic type deduction reflects a philosophical shift in the role of the compiler. In C+98, the compiler uses its knowledge to tell you when you are wrong. In C++11, at least with this, it uses its knowledge to help you get the right direction.

There is a potential drawback. Automatic type deduction ensures that the type of the variable matches the type of the initializer, but it is still possible that you might provide the wrong type of initializer:

```
auto pc = *pa; // oops! used *pa instead of &pa
```

This declaration would make pc match the type of *pa, and that would result in a compile-time error when Listing 7.19 uses pc, assuming that it is of the same type as &pa.
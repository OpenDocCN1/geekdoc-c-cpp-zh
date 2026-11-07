```
```c
for (int i = 0; i < MAX_LENGTH; i++)
    loads[i] = 50;
```
```

This won’t work in C because the defining declaration for MAX_LENGTH could be in a separate file and not be available when this particular file is compiled. In fact, it should be added that, in C, you could use the static modifier to create constants with internal linkage. It’s just that C++, by making static the default, requires one fewer thing for you to remember.

Incidentally, the revised C Standard (C99) allows you to use a const as an array size specification, but the array is treated as a new form of array, called a variable array, that is not part of the C++ Standard.

One role for the #define directive is still quite useful—the standard idiom for controlling when a header file is compiled:

```
```c
// bloop.h
#ifndef BLOOPER_H_
#define BLOOPER_H_
// code goes here
#endif
```
```

For typical symbolic constants, however, you should get into the habit of using const instead of #define. Another good alternative, particularly when you have a set of related integer constants, is to use enum:

```
```c
enum {LEVEL1 = 1, LEVEL2 = 2, LEVEL3 = 4, LEVEL4 = 8};
```
```

# ## Use inline Instead of #define to Define Short Functions

The traditional C way to create the near-equivalent of an inline function is to use a #define macro definition:

```
```c
#define Cube(x) x*x*x
```
```

This leads the preprocessor to do text substitution, with x being replaced by the corresponding argument to Cube( ):

```
```c
y = Cube(x);      // replaced with y = x*x*x;
y = Cube(x + z++); // replaced with x + z++*x + z++*x + z++;
```
```

Because the preprocessor uses text substitution instead of true passing of arguments, using such macros can lead to unexpected and incorrect results. Such errors can be reduced by using lots of parentheses in the macro to ensure the correct order of operations:

```
```c
#define Cube(x) ((x)*(x)*(x))
```
```

Even this, however, doesn’t deal with cases such as using values like z++.
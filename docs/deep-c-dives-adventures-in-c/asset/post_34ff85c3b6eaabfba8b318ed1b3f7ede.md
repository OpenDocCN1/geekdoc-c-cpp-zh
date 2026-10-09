
## Heap or Stack

  You may have noticed that VLAs have the same lifetime as an **auto** variable. This means that they are a natural for stack storage rather than the heap. Indeed, the majority of VLA implementations use the stack rather than the heap to store VLAs.

  You can even allocate memory on the stack manually using:
  `void *p = alloca(size);`
  which returns a **void** pointer to a block of memory on the stack. This function is part of the standard C library, but not part of a standard. It is compiler- and machine-dependent and these are reasons enough to avoid it. As with VLAs, it can only be used with an **auto** variable, but unlike VLAs the block of memory is released only when the function that created it terminates, not when the pointer variable goes out of scope. You should never attempt to release stack memory using `free()`.

  Which is better: stack or heap?

  This is a question that is so machine-dependent it is impossible to give a single answer. Stack memory is often in short supply in some architectures and in such cases heap is always preferable. The automatic releasing of stack memory is its one big advantage, but there are problems with jumping into scope using `goto` or `select`. It is generally more difficult to detect a memory allocation error on the stack than the heap and provoking a stack overflow generally results in your program being terminated. With all of this said, it is worth pointing out that these same problems occur if you create a fixed-size auto array within a block and this is common practice.

  At the end of the day it is simply the non-standard nature of the function that makes its use non-ideal.

## Dive 13: First Class Functions

> *My work was fairly theoretical. It was in recursive function theory. And in particular, hierarchies of functions in terms of computational complexity; I got involved in real computers and programming mainly by being - well, I was interested even as I came to graduate school.*
>
> Dennis Ritchie

C is a language built on functions. No, it isn't a functional programming language, that would be a step far too far. It has functions like other languages before it had subroutines and procedures. C's functions are designed to be a way to break a large program up into small chunks. C was just another language that emphasized “modular” programming back when it was introduced.

Today, C's functions look a little under-powered as they lack any dynamic abilities that you will find in other current languages, but this can be seen as a strength. C's functions are simple and efficient and adding advanced features would dilute this rare quality.

### The C Function

You probably know how to create a C function, but we need to make clear what is going on at a deeper level. A function is declared and defined in the usual way:

```
returnType name(parameterList) {functionBody}
```

where `{functionBody}` is a block of code executed when the function is called with the parameter supplied.

This is a simple pattern and one that every C programmer learns right at the very start. There are also a number of features of C functions which are obvious, but often not made explicit.

A C function can only be created at file-level and the variable that you generally regard as the function's name is a file-level variable. That is, it is global as far as code in the same file or compilation unit goes. What is more, functions are true global variables, by default they are extern, and they can be referenced by code in other compilation units.

This is how C libraries work, they define functions which can be used by code in other files. If you want to limit the visibility of a function to its compilation unit, then mark it as *static*.

The fact that all functions are at file level implies that all the functions that you are going to use are defined at compile time and the lifetime of any function is the entire lifetime of the program.

If you think this is the only possibility you need to get out and meet some other languages. Modern dynamic languages – C#, Python, JavaScript, Kotlin, Rust and even Fortran 90 – allow functions to be defined within other functions. Such nested functions are local to the functions they are defined in and they can have lifetimes that depend on them being in scope. This is where some more sophisticated ideas, such as closure, come into play. If a nested function lives beyond the life of the function that contains it then it “captures” the local variables and they are available to the nested function. This is closure and exactly how the variables are made available depends on the type of closure implemented.

Other languages also allow functions to be modified by code – Python decorators, for example and this is something that was thought to be a very bad idea when C was being invented. Today, C functions cannot be modified at runtime without using machine- and compiler-specific features.

### Partial Evaluation and Currying

What does C’s approach to functions make difficult?

The most obvious things that are difficult, if not impossible, are partial evaluation and currying. Partial evaluation of a function returns a function with one or more parameters fixed. For example, if you have the function sum(a,b) then a partial application is:

```
add1(b) = sum(1,b);
```

where now add1 is a function that always adds 1 to b. If you have a function of n parameters you can reduce it to a function of m parameters by applying n-m of the parameters.

Currying, a technique developed by and named after the American mathematician, Haskell Curry, is similar to partial evaluation, but it decomposes a multi-parameter function into a sequence of single parameter functions applied one after another:

```
sum(a,b,c) = add(a) (b) (c);
```

which means that sum(a) returns a function which can add b to the total and return a function which can add c to the total.

You cannot do either partial application or currying in C because you cannot create a new function at runtime, you cannot create nested functions and closures are not supported. This is a problem if you want to do functional programming in C. You also cannot implement object-oriented programming as you cannot create a bound function, i.e. a method – see Dive 14: Structs and Objects. Put simply, you cannot take a function:

```
myFunction(self, other_parameters)
```

and use partial application to create a method:

```
myMethod(other_parameters)
```

by setting self to reference the current instance:

```
myMethod = myFunction(instance, other_parameters)
```

The key ideas are that C functions have file-level scope and are external by default, i.e. they are global variables. Functions also have a lifetime the same as the entire program and they can only be defined at compile time. Modifying a C function isn't possible without going beyond C standards.

### Functions First

C’s functions are simple and hence efficient, but their simplicity has a cost. C is a one-pass language in that it can be compiled in a single reading of the program text. This in turn implies that if you want to make use of something, a function say, it has to be declared before it is used. The reason is simple. If you use a function before it is declared the compiler knows nothing about it and cannot check if your use makes sense. This means that in C you have to define your functions before you use them and this means that they have to come in a particular order and all before the main function. Some C compilers will cope if they encounter a function that you haven’t declared before use. They generally warn of “implicit” function declaration but this is not a good idea.

Putting functions before main isn’t the natural way to read a program. You don’t generally want to have to scan through all of the functions before you get to the main program and then have to backtrack to find the functions that are used. The natural way to do things is to read the main program and look up any functions that are used.

To provide a simpler program layout and organization, C allows you to declare variables, including functions, before they are defined.

Declaring a variable just informs the compiler of its type, no memory allocations have to be made at this point.

Defining a variable can be a separate step and it involves allocating memory and perhaps initializing it to a value.

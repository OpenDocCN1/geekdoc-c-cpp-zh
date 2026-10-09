You cannot do either partial application or currying in C because you cannot create a new function at runtime, you cannot create nested functions and closures are not supported. This is a problem if you want to do functional programming in C. You also cannot implement object-oriented programming as you cannot create a bound function, i.e. a method – see Dive 14: Structs and Objects. Put simply, you cannot take a function:

```
`myFunction(self, other_parameters)`
```

and use partial application to create a method:

```
`myMethod(other_parameters)`
```

by setting self to reference the current instance:

```
`myMethod = myFunction(instance, other_parameters)`
```

The key ideas are that C functions have file-level scope and are external by default, i.e. they are global variables. Functions also have a lifetime the same as the entire program and they can only be defined at compile time. Modifying a C function isn't possible without going beyond C standards.

# Functions First

C’s functions are simple and hence efficient, but their simplicity has a cost. C is a one-pass language in that it can be compiled in a single reading of the program text. This in turn implies that if you want to make use of something, a function say, it has to be declared before it is used. The reason is simple. If you use a function before it is declared the compiler knows nothing about it and cannot check if your use makes sense. This means that in C you have to define your functions before you use them and this means that they have to come in a particular order and all before the main function. Some C compilers will cope if they encounter a function that you haven’t declared before use. They generally warn of “implicit” function declaration but this is not a good idea.

Putting functions before main isn’t the natural way to read a program. You don’t generally want to have to scan through all of the functions before you get to the main program and then have to backtrack to find the functions that are used. The natural way to do things is to read the main program and look up any functions that are used.

To provide a simpler program layout and organization, C allows you to declare variables, including functions, before they are defined.

Declaring a variable just informs the compiler of its type, no memory allocations have to be made at this point.

Defining a variable can be a separate step and it involves allocating memory and perhaps initializing it to a value.
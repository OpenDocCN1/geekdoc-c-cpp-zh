```
```cpp
void point::zero(){
    x=y=0.;
}   // definition of "zero()"
```
```

Here, the interface functions are only declared in the class block, while their actual definitions are left outside it. Each definition is compiled only once, which creates a finite state machine (automaton). This machine is then invoked every time the function is called, with the concrete arguments that are passed to the function as input and the returned value as output.

The prefix "point::" that precedes the function names in the above code may actually be considered as an operator that “transfers” the definition back into the class block. This format, however, is unnecessary in the present “point” example, which uses very short definitions. The original style, in which the complete definitions appear inside the class block, is preferable in this case.

# ## 2.3 Constructors

When the user defines a point object by writing

```
```cpp
point P;
```
```

the computer executes this command by allocating memory for the data fields of the new "point" variable 'P'. These data fields, the "double" variables "P.x" and "P.y", are not yet initialized to any meaningful value; in fact, they initially contain random, meaningless values. Only interface functions of the "point" class have access to these variables and can assign meaningful values to them.

C++ has a default constructor that allocates memory for the data fields and initializes them with random values. However, this is not always good enough. Programmer A might have a different idea about what should happen when the user writes code lines like "point P;", and he/she might also want users to be able to write more sophisticated code lines like "point P = 0;", in which 'P' is constructed and initialized to zero. Indeed, if the "point" object is to behave like standard types, then such commands should be available to users.

It is thus good practice to write an explicit constructor in the class. The constructor is a public interface function that tells the computer how to construct a new object and allocate memory for its data fields. The name of the constructor function must be the same as the name of the class itself. For example, if one writes in the block of the "point" class

```
```cpp
point(){
}   // default constructor for the "point" class
```
```

then this constructor is invoked every time the compiler encounters a command of the form "point P;". The body of the constructor function contains no code lines at all. However, it still does something: as soon as it is called, the constructor implicitly invokes the default constructor built into C++, which allocates storage for the data fields "P.x" and "P.y" and fills them with random numbers. The above constructor is also called the default constructor for the "point" class, because it is invoked by commands like "point P;", with no initialization at all.

It is possible to write more than one constructor in the class block. In particular, one may also define a more informative constructor, which not only allocates memory for the
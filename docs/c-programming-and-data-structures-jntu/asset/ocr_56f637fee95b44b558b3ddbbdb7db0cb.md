```
{
Output
x = 1
x = 2
x = 3
}
```

# Fig. 10.17 Illustration of static variable

A static variable is initialized only once, when the program is compiled. It is never initialized again. During the first call to stat, x is incremented to 1. Because x is static, this value persists and therefore, the next call adds another 1 to x giving it a value of 2. The value of x becomes three when the third call is made.

```
x = 1
x = 1
x = 1
```

This is because each time stat is called, the auto variable x is initialized to zero. When the function terminates, its value of 1 is lost.

An external static variable is declared outside of all functions and is available to all the functions in that program. The difference between a static external variable and a simple external variable is that the static external variable is available only within the file where it is defined while the simple external variable can be accessed by other files.

It is also possible to control the scope of a function. For example, we would like a particular function accessible only to the functions in the file in which it is defined, and not to any function in other files. This can be accomplished by defining 'that' function with the storage class static.

# Register Variables

We can tell the compiler that a variable should be kept in one of the machine's registers, instead of keeping in the memory (where normal variables are stored). Since a register access is much faster than a memory access, keeping the frequently accessed variables (e.g., loop control variables) in the register will lead to faster execution of programs. This is done as follows:

```
register int count;
```

Although, ANSI standard does not restrict its application to any particular data type, most compilers allow only int or char variables to be placed in the register. Since only a few variables can be placed in the register, it is important to carefully select the variables for this purpose. However, C automatically convert register variables into nonregister variables once the limit is reached.
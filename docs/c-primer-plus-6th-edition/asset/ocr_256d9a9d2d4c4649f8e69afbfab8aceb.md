# Simplifying typedef

C++ provides tools other than auto for simplifying declarations.You may recall from Chapter 5,“Loops and Relational Expressions,” that the typedef keyword allows you to create a type alias:

```
typedef double real; // makes real another name for double
```

The technique is to declare the alias as if it were an identifier and to insert the key-word type at the beginning. So you can do this to make p_fun of the function pointer type in Listing 7.19:

```
typedef const double *(p_fun) (const double *, int); // p_fun now a type
p_fun pl = f1; // pl points to the f1() function
```

You can use this to build elaborations:

```
p_fun pa[3] = {f1,f2,f3}; // pa an array of 3 function pointers
p_fun (*pd[3]) = &pa; // pd points to an array of 3 function pointers
```

Not only typedef saves you typing, it makes writing the code less error prone, and it makes the program easier to understand.

# Summary

Functions are the C++ programming modules.To use a function, you need to provide a definition and a prototype, and you have to use a function call. The function definition is the code that implements what the function does.The function prototype describes the interface: how and what kind of values to pass to the function and what sort of return type, if any, to get from it.The function calls the program to pass the function arguments to the function and to transfer program execution to the function code.

By default, C++ functions pass arguments by value.This means that the formal parameters in the function definition are new variables that are initialized to the values provided by the function call. Thus, C++ functions protect the integrity of the original data by working with copies.

C++ treats any argument name as the first element of the array. Technically, this is still passing by value because the pointer is a copy of the original address, but the function uses the pointer to access the contents of the original array. When you declare formal parameters for a function (and only then), the two declarations are equivalent:

```
typeName [];
typeName * arr;
```

Both of these mean that arr is a pointer to typeName.When you write the function code, you can use arr as if it were an array name to access elements; arr[i].Even when passing pointers, you can preserve the integrity of the original data by declaring the formal argument to be a pointer to a const type. Because passing the
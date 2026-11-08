# Pointers to Functions

You are familiar already with pointers to data, variables that store the address of those regions in memory containing values of other variables, arrays, or dynamically allocated memory. A computer program is more than just data alone, however. Another essential part of the memory allotted to a computer program holds its executable code, consisting of blocks of compiled C++ statements. Naturally, all compiled code belonging to a given function will typically be grouped together as well.

*A pointer to a function* or *function pointer* is a variable that can store the address of a function and therefore point to different functions at different times during execution. You use a pointer to a function to call the function at the address it contains. An address is not sufficient to call a function, though. To work properly, a pointer to a function must also store the type of each parameter as well as the return type. Clearly, the information required to define a pointer to a function will restrict the range of functions to which the pointer can point. It can only store the address of a function with a given number of parameters of specific types and with a given return type. This is analogous to a pointer that stores the address of a data item. A pointer to type int can only point to a location that contains a value of type int.

# Defining Pointers to Functions

Here's a definition of a pointer that can store the address of functions that have parameters of type long* and int and return a value of type long:

```
```cpp
long (*fun_ptr)(long*, int); // Variable fun_ptr (pointer to function that returns long)
```
```

This may look a little weird at first because of all the parentheses. The name of the pointer variable is fun_ptr. It doesn't point to anything because it is not initialized. Ideally, it would be initialized to nullptr or with the address of a specific function. The parentheses around the pointer name and the asterisk are essential. Without them, this statement would declare a function rather than define a pointer variable because the * will bind to the type long:

```
```cpp
long *fun_ptr(long*, int); // Prototype for a function fun_ptr() that returns long*
```
```

The general form of a pointer to a function definition is as follows:

```
```cpp
return_type (*pointer_name)(parameter_types);
```
```

The pointer can only point to functions with the exact same return_type and parameter_types as those specified in its definition.

Of course, you should always initialize a pointer when you declare it. You can initialize a pointer to a function to nullptr or with the name of a function. Suppose you have a function with the following prototype:

```
```cpp
long findMaximum(const long* array, size_t size); // Returns the maximum element
```
```

Then you can define and initialize a pointer to this function with this statement:

```
```cpp
long (*fun_ptr)(const long*, size_t) { findMaximum };
```
```

Using auto will make defining a pointer to this function much simpler:

```
```cpp
auto fun_ptr = findMaximum;
```
```
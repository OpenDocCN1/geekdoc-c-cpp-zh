# Data Types and Data Protection

# Types = Structs + Functions

We're going to take a look at how C++ implements new data types and makes use of data protection.

# C Structs

Suppose we want to build a system consisting of several elevators. In C, we typically attack the problem by creating a `struct` to hold data about each elevator:

```
struct elevator {
    int floorSelected;
    int floorNumber;
};
```

A structure is created which holds all the information we want to remember about each elevator. To create a variable, we use the `struct` keyword along with the structure name:

```
struct elevator e;
```

or, we can use the `typedef` identifier and say:

```
typedef struct elevator Elevator;
Elevator e;
```

The second example acts more like a built-in data type.

# Pointers to C Structs as Function Arguments

When we create a function to act upon the `struct`, we must pass as an argument to the function a pointer to the `struct`.
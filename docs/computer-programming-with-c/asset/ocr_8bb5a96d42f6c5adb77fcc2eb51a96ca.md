# Chapter 16 | Templates in C++

# 16.1  Overview

Templates in C++ are used to facilitate generic programming by giving the programmer an ability to create generic classes/functions in the program. A component of the program is said to be generic if its functionality remains the same irrespective of data type of the values it operates on. A **generic function** is a function that can work with arguments of any data type, whereas a **generic class** is a class that can work with members of any data type. In this chapter, we will learn creation of generic functions using **function templates** and creation of generic classes using **class templates**.

> **NOTES**
> 
> The objective of templates is to create generic components in the program, which can work with different data types. This saves programmers effort to define the same component multiple times and replicating same logic for different type of data values.

# 16.2  Function Templates

Function templates in C++ enable the programmer to create generic functions. These functions are adaptable to multiple data types and can execute in the same way immaterial of the data type of the values passed to it.

The functions we have written so far in the previous chapters are strictly bonded to specific types. For example, consider the function add() as shown below:

```
int add(int a, int b)
{
    int c = a+b;
    return c;
}
```

The function takes two arguments of type integer and returns the resultant integer, which gives addition of two numbers. This function works well if integer values are
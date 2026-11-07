![](bbox=[0.26, 0.08, 0.75, 0.27])

**Figure 10.3** Creation of pointer variable from a string

As we mentioned, the name of the string created in Table 10.1 or Figure 10.2 is an *rvalue* pointer, not a variable. If we want to create a variable, we must declare a variable of type *char\** or *const char\** and assign the name of the string to that variable, as shown in Figure 10.3.

In Chapter 8 we mentioned that we cannot return an array from a function because an array requires a pointer to the first element and its size. The design of the C string eliminates the second requirement. The size is not needed because the last character is a null character and implicitly defines the size. This means that we can return a pointer variable pointing to a C string from a function.

**String Literal** We have seen literals of data types, such as integer, floating point, or character. For example, 3 is an integer literal, 23.7 is a floating-pointing literal, and 'A' is a character literal. We can also have a string literal. A **string literal** is a null-terminated array of characters whose name is the sequence of characters in the array enclosed by two quotation marks, as shown in Figure 10.4.

A string literal is a constant string that is part of the C++ language and is used with both C strings and C++ strings. When it is created, it can be used anywhere that a string literal can be used. We have used a string literal to print messages. However, we must remember that a string literal is a constant entity and cannot be changed after it has been created.

> > A string literal is a constant entity; it cannot be changed.

# **EXAMPLE 10.1**

The following code fragment shows that we can use a string literal like other literals. For example, we can use the *cout* object and the insertion operator to print the value of an integer literal, a floating-point literal, a character literal, and a string literal.

```
```cpp
cout << 5 << endl;                // Printing an integer literal
cout << 21.3 << endl;             // Printing a floating-point literal
cout << 'R' << endl;              // Printing a character literal
cout << "Hello dear" << endl;    // Printing a string literal
```
```

![](bbox=[0.35, 0.92, 0.65, 0.95])

**Figure 10.4** A string literal
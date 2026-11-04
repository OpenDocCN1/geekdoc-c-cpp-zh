# Introduction and Role:

Templates are a powerful feature in C++ that allow you to create generic code capable of working with various data types. They enable you to write functions and classes that maintain flexibility without duplicating code.

# Function Templates:

Function templates allow you to define generic functions that can operate on different data types. You specify a template parameter as a placeholder for the actual type. When the function is used, the template parameter is replaced with the provided type.

```
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

# Class Templates:

Class templates extend the concept of function templates to classes. They let you create classes that can handle multiple data types using template parameters.
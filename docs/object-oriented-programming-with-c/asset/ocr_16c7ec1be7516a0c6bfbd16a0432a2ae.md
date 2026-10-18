```
```cpp
};
```
```

The private variable ‘a’ can be used directly inside a member function, like

```
```cpp
a = 123;
```
```

We can also use the following statement to do the same job:

```
```cpp
this->a = 123;
```
```

Since C++ permits the use of shorthand form **a = 123**, we have not been using the pointer **this** explicitly so far. However, we have been implicitly using the pointer **this** when overloading the operators using member function.

Recall that, when a binary operator is overloaded using a member function, we pass only one argument to the function. The other argument is implicitly passed using the pointer **this**. One important application of the pointer **this** is to return the object it points to. For example, the statement

```
```cpp
return *this;
```
```

inside a member function will return the object that invoked the function. This statement assumes importance when we want to compare two or more objects inside a member function and return the invoking object as a result. Example:

```
```cpp
person & person :: greater(person & x)
{
    if x.age > age

    return x; // argument object    else

    return *this; // invoking object    }
```
```

Suppose we invoke this function by the call
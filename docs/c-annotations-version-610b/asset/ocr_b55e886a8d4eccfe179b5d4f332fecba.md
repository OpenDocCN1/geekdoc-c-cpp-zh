```
```cpp
    d_address = std::move(tmp.d_address);
    return *this;
}
```
```

As noted previously (section(MOVECONS)) declaring a move assignment operator suppresses the default availability of the copy constructor. It is made available again by declaring the copy constructor in the class's interface (and of course by providing an explicit implementation or by using the `= default` default implementation).

# ### 9.7.4 Revising the assignment operator (part II)

Now that we've familiarized ourselves with the overloaded assignment operator and the move-assignment, let's once again have a look at their implementations for a class Class, supporting swapping through its swap member. Here is the generic implementation of the overloaded assignment operator:

```
```cpp
    Class &operator=(Class const &other)
    {
        Class tmp(other);
        swap(tmp);
        return *this;
    }
```
```

and this is the move-assignment operator:

```
```cpp
    Class &operator=(Class &&tmp)
    {
        swap(tmp);
        return *this;
    }
```
```

They look remarkably similar in the sense that the overloaded assignment operator's code is identical to the move-assignment operator's code once a copy of the other object is available. Since the overloaded assignment operator's tmp object really is nothing but a temporary Class object we can use this fact by implementing the overloaded assignment operator in terms of the move-assignment. Here is a second revision of the overloaded assignment operator:

```
```cpp
    Class &operator=(Class const &other)
    {
        Class tmp(other);
        return *this = std::move(tmp);
    }
```
```

# ### 9.7.5 Moving and the destructor (C++11)

Once a class becomes a move-aware class one should realize that its destructor still performs its job as implemented. Consequently, when moving pointer values from a temporary source to a destination the move constructor should make sure that the temporary's pointer value is set to zero, to prevent doubly freeing memory.

If a class defines pointers to pointer data members there usually is not only a pointer that is moved, but also a size_t defining the number of elements in the array of pointers.

Once again, consider the class Strings. Its destructor is implemented like this:

```
```cpp
    Strings::~Strings()
```
```
operator and move constructor—we discuss move semantics in Chapter 24.) The last `unique_ptr` object that maintains the pointer to the dynamic memory will delete the memory. This makes `unique_ptr` an ideal mechanism for returning dynamically allocated memory to client code. When the `unique_ptr` goes out of scope in the *client* code, the `unique_ptr`’s destructor deletes the dynamically allocated object—if the object has a destructor, it is called before the memory is returned to the system.

# ## 17.9.2 `unique_ptr` to a Built-In Array

You can also use a `unique_ptr` to manage a dynamically allocated built-in array. For example, consider the statement

```
```cpp
unique_ptr<string[]> ptr{make_unique<string[]>(10)};
```
```

Because `make_unique`’s type is specified as `string[]`, the function obtains a *dynamically allocated built-in array* of the number of elements specified by its argument (10). By default, the elements of arrays allocated with `make_unique` are initialized to 0 for fundamental types, to `false` for `bool`s or via the default constructor for objects of a
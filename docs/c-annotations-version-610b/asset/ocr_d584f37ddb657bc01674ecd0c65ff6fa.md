```
```cpp
std::string const &at(size_t idx) const;
size_t size() const;
};
```
```

The constructor’s task is to initialize the data fields of the object. E.g, its constructors are defined as follows:

```
```cpp
Strings::Strings()
:
    d_string(0),
    d_size(0)
{}

Strings::Strings(char const *const *cStrings, size_t size)
:
    d_string(new string[size]),
    d_size(size)
{
    for (size_t idx = 0; idx != size; ++idx)
        d_string[idx] = cStrings[idx];
}
```
```

As objects of the class Strings allocate memory a destructor is clearly required. Destructors may or may not be called automatically. Here are the rules:

+   - Destructors are *only* called for fully constructed objects. C++ considers the object to be fully constructed once at least one of its constructors has normally completed. It used to be the constructor, but as C++11 supports constructor delegation, multiple constructors can be activated for a single object; hence “at least one constructor”. The remaining rules only apply to fully constructed objects;
+   - Destructors of local non-static objects are called automatically when the execution flow leaves the block in which they were defined; the destructors of objects defined somewhere in the outer block of a function are called just before the function terminates.
+   - Destructors of static or global objects are called when the program itself terminates.
+   - The destructor of a dynamically allocated object is called by `delete` using the object’s address as its operand;
+   - The destructors of a dynamically allocated array of objects are called by `delete[]` using the address of the array’s first element as its operand;
+   - The destructor of an object initialized by placement `new` is activated by explicitly calling the object’s destructor.

The destructor’s task is to ensure that all memory that is dynamically allocated and controlled only by the object itself is returned. The task of the `Strings` destructor would therefore be to delete the memory to which `d_string` points. Its implementation is:

```
```cpp
Strings::~Strings()
{
    delete[] d_string;
}
```
```

The next example shows `Strings` at work. In process a `Strings` store is created, and its data are displayed. It returns a dynamically allocated `Strings` object to `main`. A `Strings *` receives the address of the allocated object and deletes the object again. Another `Strings` object is then created in a
3  *(Code)* How would you declare an **rvalue** reference of type `std::string` for a function parameter named `value`?

**Answer:** `std::string&& value`.

# 11.6.8 Destructor

Line 27 of Fig. 11.4

```
```cpp
~MyArray(); // destructor
```
```

declares the class’s destructor (defined in lines 73–75), which is invoked when a MyArray object goes out of scope. This will automatically call m_ptr’s destructor, which will release the dynamically allocated int array created when the MyArray object was constructed. The C++ Core Guidelines indicate that it’s poor design if destructors throw exceptions. For this reason, they recommend declaring destructors `noexcept`. However, unless your class is derived from a base class with a destructor that’s declared `noexcept(false)`, the compiler implicitly declares the destructor `noexcept` by default.

```
```cpp
// destructor: This could be compiler-generated. We included it here so
// we could output when each MyArray is destroyed.
MyArray::~MyArray()
    std::cout << "MyArray destructor\n";
}
```
```

# 11.6.9 toString and size Functions

Line 29 in Fig. 11.4

```
```cpp
size_t size() const noexcept { return m_size; } // return size
```
```

defines an inline size member function, which returns a MyArray’s number of elements.

Line 30 in Fig. 11.4

```
```cpp
std::string toString() const; // create string representation
```
```

declares a toString member function (defined in lines 78–91), which returns the string representation of a MyArray’s contents. Function toString uses an ostringstream (introduced in Section 8.17) to build a string containing the MyArray’s element values enclosed in braces ({}) and separating each item from the next by a comma and a space.

27. C++ Core Guidelines, “C.37: Make Destructors noexcept.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-dtor-noexcept.
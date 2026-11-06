# # C++11: Deleting Unwanted Member Functions from Your Class

Prior to C++11, you could prevent class objects from being *copied* or *assigned* by declaring as `private` the class’s copy constructor and overloaded assignment operator. As of C++11, you can simply *delete* these functions from your class. To do so in class `Array`, replace the prototypes in lines 14 and 18 of **Fig. 10.10** with

```
```cpp
Array(const Array&) = delete;
const Array& operator=(const Array&) = delete;
```
```

Though you can delete *any* member function, it’s most commonly used with member functions that the compiler can *auto-generate*—the default constructor, copy constructor, assignment operator, and in C++11, the move constructor and move assignment operator.
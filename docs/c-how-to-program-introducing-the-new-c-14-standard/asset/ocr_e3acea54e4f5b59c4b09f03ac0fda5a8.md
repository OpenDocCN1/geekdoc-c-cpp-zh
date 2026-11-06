```
```cpp
counter.setX(8); // error: setX not a member function
```
```

Function `setX` is allowed to access class `Count`’s `private` data member `x` (line 18) only because `setX` was declared as a `friend` of the class (line 8). If you remove the `friend` declaration in line 8, you’ll receive error messages indicating that function `setX` cannot modify class `Count`’s `private` data member `x`.

# Overloaded `friend` Functions

It’s possible to specify overloaded functions as `friend`s of a class. Each function intended to be a `friend` must be explicitly declared in the class definition as a `friend` of the class.

![](bbox=[0.122, 0.544, 0.194, 0.603])

# Software Engineering Observation 9.10

*Even though the prototypes for `friend` functions appear in the class definition, friends are not member functions.*

![](bbox=[0.122, 0.78, 0.194, 0.839])

# Software Engineering Observation 9.11
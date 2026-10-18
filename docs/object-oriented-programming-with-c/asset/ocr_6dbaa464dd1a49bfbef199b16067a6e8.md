```
```cpp
std::cout << typeid(*ptr).name() << std::endl;
// This will display Dept i.e. the dynamic pointer type
}
```
```

In the above program, the typeid (object) call returns a reference to the type_info object that contains information about the object’s type. The member function name () of the type_info class is used for retrieving the name of the object type.

# 16.4  Class Implementation

ANSI C++ Standard adds two unusual keywords, **explicit** and **mutable**, for use with class members.

# The explicit Keyword

The **explicit** keyword is used to declare class constructors to be “explicit” constructors. We have seen earlier, while discussing constructors, that any constructor called with one argument performs *implicit conversion* in which the type received by the constructor is converted to an object of the class in which the constructor is defined. Since the conversion is automatic, we need not apply any casting. In case, we do not want such automatic conversion to take place, we may do so by declaring the one-argument constructor as explicit as shown below:

```
```cpp
class ABC
{
    int m;
public:
    explicit ABC (int i)       // constructor
    {
        m = i;
    }
    // ...........
}
```
```
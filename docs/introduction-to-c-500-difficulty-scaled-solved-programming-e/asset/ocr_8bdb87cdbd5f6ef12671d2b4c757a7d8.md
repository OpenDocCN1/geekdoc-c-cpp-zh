# 598 Introduction to C++

The intention of the programmer is to change the value of an element in the array. For example, suppose that you want to make the first grade equal to 2. Instead of writing grd[0] = 2, which calls the operator[] function to change the grd[0], you make a mistake and set s = 2; however, with this statement, the compiler uses the Student (int g) constructor and converts the value 2 to a temporary object, which is copied by s. So the value of s.name changes from first to none and all elements of the grd array become equal to 2.

Had we made the conversion explicit, that is, writing explicit Student (int g); the compiler would not allow the conversion and produce an error message to the programmer. No, I have not made such a mistake to date. But, because there is always a first time for everything, I prefer to declare as explicit a constructor that accepts a single argument, in order to protect myself from potential unintended single-argument constructor bugs. In fact, I'd prefer the standard having made a single-argument constructor explicit by default.

![](bbox=[0.0, 0.32, 1.0, 0.33])

# CONVERSIONS FROM CLASS TYPE

As a type can be converted to an object, (e.g., t) can also be converted to a type. For example:

```
int i = t;
```

This statement is allowed if a conversion function is defined in the class, as follows:

```
operator type();
```

where type is the name of the type to which the object will be converted. If this definition is missing the compiler issues an error message since it cannot assign a t to int.

When declaring conversion functions rules apply. For example, the conversion function must be a member of the class, with no return type specified in its declaration and take no arguments. The return type is that of type. For example, the function prototype for conversion to int is:

```
operator int();
```

Also, when the conversion function is declared, explicit conversions are allowed. For example:

```
int i = static_cast<int>(t);
```

Usually, the conversion function does not change the state of the respective object, so it is declared as const.

```
#include <iostream> // Example 19.3
class T
{
private:
  int a;
  double d;
public:
  T(int i);
  operator int() const; // Conversion function to int.
  operator double() const; // Conversion function to double.
};
```
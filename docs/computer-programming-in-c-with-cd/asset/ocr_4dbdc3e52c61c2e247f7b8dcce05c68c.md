```
`datatype *point_name;`
```

In the preceding syntax,

+   - **datatype:** Refers to any legal primary C++ data type or user-defined data type.
+   - **point_name:** Refers to any variable name. The * informs the compiler that the variable point_name is a pointer variable.

![](bbox=[0.229, 0.274, 0.261, 0.301])

> Pointers are discussed in more detail in Chapter 4, Pointers.

After discussing built-in, user-defined, and derived data types, let’s learn how to convert a variable of one data type to another.

# Type Conversion and Type Casting in C++

In C++ the concept of converting an integer type variable into a float type is known as type conversion. Listing 10 shows how the integer type variable is automatically converted to a float type (you can find the IntTypeEx.cpp file on the CD in the code/chapter1 folder:

# Listing 10: Converting an Integer Type Variable to a Float Type

```
```cpp
#include <iostream.h>
int main()
{
    int a = 10;
    float b = 22.7;
    b = b + a;
    cout << "The value of the b variable is:" <<b;
    return 0;
}
```
```

**Output:**

```
```text
The value of the b variable is:32.700001
```
```

In Listing 10, the int type variable, a, is assigned a value of 10, which is automatically converted to 10.0 during the addition of the values of variables a and b. In Listing 10, you notice the automatic conversion of type from int to float. However, if you want to convert the double type variable to an int type, then you need to explicitly provide code for it. The concept of explicitly converting one data type variable to another is known as type casting. Listing 11 shows how to type cast the double type variable to an int type (you can find the DoubleTypeEx.cpp file on the CD in the code/chapter1 folder):

# Listing 11: Type Casting the Double Type Variable to an Int Type

```
```cpp
#include <iostream.h>
int main()
{
```
```
```
```cpp
FLOAT f;
f.get_data();
cout<<"Before increment"<<endl;
f.show_data();
++f;
cout<<"After increment"<<endl;
f.show_data();
cout<<"Before decrement"<<endl;
f.show_data();
--f;
cout<<"After decrement"<<endl;
f.show_data();
}

Output:

Enter a number
58
23
Before increment
58
23
After increment
59
24
Before decrement
59
24
After decrement
58
23
```
```

# ■ **Overloading of Unary Operator Returning Object**

You can overload an operator that returns an object of a class. This means that you can use the following code snippet in the main() function of a class:

```
```cpp
Object1--Object2;
```
```

Listing 44 shows overloading of minus operator returning object (you can find this example in the UnaryOptReturnObject.cpp file on the CD in the code\chapter6 folder):

# ▸ **Listing 44: Overloading of a Unary Operator Returns an Object**

```
```cpp
#include<iostream.h>
class NegativeNumberShow
{
```
```
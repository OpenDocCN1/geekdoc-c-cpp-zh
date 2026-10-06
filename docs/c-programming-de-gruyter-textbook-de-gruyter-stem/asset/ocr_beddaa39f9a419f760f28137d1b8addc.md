# 3.5 Using C++ System Functions 107

function to calculate square root (sqrt), the function to calculate absolute value (abs), etc.

We know that program must declare the function before calling the function. The prototypes of system functions have all been provided by the C++ system library, which caches and stores them in several header files. Programmers only need to embed the related header files into the code using the include instruction, and then they can use the system functions. For example, if you want to use mathematical functions, you should use the header file cmath.

# Example 3.7: An example of using C++ system functions.

Input an angle value from the keyboard, and calculate its sine, cosine, and tangent values.

Analysis: The C++ system library provides the functions to calculate the sine, cosine, and tangent of an angle: sin(), cos(), and tan(), and these function prototypes are contained in the header file cmath.

Source code:

```
//3_18.cpp
#include<iostream>
#include<cmath>
using namespace std;
const double pi(3.14159265);
int main()
{
    double a,b;
    cin>>a;
    b=a*pi/180;
    cout<<"sin(\<<a<<")="<<sin(b)<<endl;
    cout<<"cos(\<<a<<")="<<cos(b)<<endl;
    cout<<"tan(\<<a<<")="<<tan(b)<<endl;
}
```

Running result:

| sin(30)=0.5 |
| cos(30)=0.866025 |
| tan(30)=0.57735 |

Making full use of system functions can greatly reduce the work of programming and improve the execution efficiency and reliability of the program. When using system functions, we should pay attention to two points:

+   1. Be familiar with the system functions provided by your C++ development environment. Different compilers may provide different system functions. Even compilers
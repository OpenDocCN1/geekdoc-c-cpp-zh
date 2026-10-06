
## 102 — 3 Functions

```cpp
int main()
{ add();
}
int add(int x,int y)
{ return x+y;
}
```

Within the same scope, the declaration of default values for formal parameters should be uniform; but in different scopes, declarations of default values for formal parameters can be different. Here scope refers to the area enclosed by the braces that embodies the function prototype. More details about scope will be discussed in Chapter 5. For example:

```cpp
int add(int x=1,int y=2);
int main()
{ add(int x=3,int y=4);
add(); //Use the local default parameter(calculate 3+4)
}
void fun(void)
{
add(); //Use the global default parameter(calculate 1+2)
}
```

**Example 3.15:** An example of a function using default parameters.
The function of the program is to calculate the volume of cuboids. The subsection get_volume is used to calculate the volume, which has three parameters: length, width, and height. The parameters width and height have default values. The main function calls get_volume using different parameters. Analyze the running result of the program.

```cpp
//3_15.cpp
#include <iostream>
#include <iomanip>
using namespace std;
get_volume(int length, int width = 2, int height = 3);
int main()
{
int x = 10, y = 12, z = 15;
cout << "Some box data is ";
cout << get_volume(x, y, z) << endl;
cout << "Some box data is ";
cout << get_volume(x, y) << endl;
```

## 3.3 Default Formal Parameters in Functions

```cpp
cout << "Some box data is ";cout << get_volume(x) << endl;
cout << "Some box data is ";cout << get_volume(x, 7) << endl;
cout << "Some box data is ";cout << get_volume(5, 5, 5) << endl;
```

```cpp
int get_volume(int length, int width, int height) {
    cout<<setw(5)<<length<<setw(width)<<setw(5)<<height<<' ';
    return length * width * height;
}
```

Running result:

| Some box data is 10 12 15 1800 |
| Some box data is 10 12 3 360 |
| Some box data is 10 2 3 60 |
| Some box data is 10 7 210 |
| Some box data is 5 5 5 125 |

Since the first parameter of the function get_volume has no default value, every function call on get_volume must provide the first actual parameter to initialize the formal parameter length. The parameters width and height have default values. So all three formal parameters will be initialized by actual parameters; the last formal parameter height will use the default value if the function call provides two actual parameters; the last two formal parameters width and height will use the default values if the function call provides only one actual parameter.

When overloading functions that have default values, we should avoid ambiguity. For example, the following two prototypes will cause ambiguity that they cannot be recognized as different overloaded forms by the compiler:

```cpp
void fun(int length, int width = 2, int height = 3);
void fun(int length);
```

In other words, when the function fun is called in the following form, the compiler is unable to decide which overloaded function should be executed:

```cpp
fun(1);
```

The compiler will count this as a compiling error.

## 3.4 Function Overloading

In programs, a function name is essentially the name of an operation. We with the help of names similar to natural languages, we can write programs that are easy to understand and modify. Here comes a problem: how to reflect the tiny differences in natural languages using programming languages? Usually, a natural language can have different meanings in different contexts. This is called polysemy, which in programming language is called "overloading". For example: in a natural language, play the piano, play chess and play basketball all use the verb "play", while the actions that play indicates in the three contexts are quite different. We can understand these phrases, since we have learned to play different objects in our life. So nobody would say "Play the piano as you would play chess, or play chess as you would play basketball." Is it possible for a computer to have the same ability? This is up to the programs we write. C++ provides the support for function overloading, which enables us to give different functions the same name. The compiler will choose an appropriate function to execute according to the context (number and types of parameters).

Function overloading means that two or more functions share the same name, albeit differences in the number or the types of their formal parameters. The compiler will automatically choose a function that fits the calling context according to the number and the types of formal parameters.

Without overloading, for the same operation on different data types, we need to define several functions with different names. For example, when defining the addition function, we need different function names for the addition of integers and the addition of float numbers:

```cpp
int add(int x, int y);
float ladd(float x, float y);
```

It is quite inconvenient when C++ allows with similar functionalities to use the same name within the same scope, which allows for overloading. It is easy to use and remember. For example:

- 1. add(int x, int y);
- 2. ladd(float x, float y);

- 3. fun(int length, int width = 2, int height = 3);
- 4. fun(int length);

In other words, when the function fun is called in the following form, the compiler is unable to decide which overloaded function should be executed:

```cpp
fun(1);
```

The compiler will count this as a compiling error.

Notes: When overloading functions that have default values, we should avoid ambiguity. For example, the following two prototypes will cause ambiguity that they cannot be recognized as different overloaded forms by the compiler: (as shown above).

Since the first parameter of the function get_volume has no default value, every function call on get_volume must provide the first actual parameter to initialize the formal parameter length. The parameters width and height have default values. So all three formal parameters will be initialized by actual parameters; the last formal parameter height will use the default value if the function call provides two actual parameters; the last two formal parameters width and height will use the default values if the function call provides only one actual parameter.

## 3.5 Using C++ System Functions

C++ not only allows us to design functions ourselves, but also provides hundreds of functions in the C++ library for us to use. We know that program must declare the function before calling the function. The prototypes of system functions have all been provided by the C++ system library, which caches and stores them in several header files. Programmers only need to embed the related header files into the code using the include instruction, and then they can use the system functions. For example, if you want to use mathematical functions, you should use the header file cmath.

**Example 3.7:** An example of using C++ system functions.

Input an angle value from the keyboard, and calculate its sine, cosine, and tangent values.

Analysis: The C++ system library provides the functions to calculate the sine, cosine, and tangent of an angle: sin(), cos(), and tan(), and these function prototypes are contained in the header file cmath.

Source code:

```cpp
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

Making full use of system functions can greatly reduce the work of programming and improve the execution efficiency and reliability of the program. When using system functions, we should pay attention to two points:

- 1. Be familiar with the system functions provided by your C++ development environment. Different compilers may provide different system functions. Even compilers

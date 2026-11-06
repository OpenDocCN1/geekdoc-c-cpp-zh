

```cpp
cout << "\nlocal static x is " << x << " on entering useStaticLocal"
     << endl;
x++;
cout << "local static x is " << x << " on exiting useStaticLocal"
     << endl;
} // end function useStaticLocal

// useGlobal modifies global variable x during each call
void useGlobal()
{
    cout << "\nglobal x is " << x << " on entering useGlobal" << endl;
    x = 10;
    cout << "global x is " << x << " on exiting useGlobal" << endl;
} // end function useGlobal
```

```text
global x in main is 1
local x in main's outer scope is 5
local x in main's inner scope is 7
local x in main's outer scope is 5

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 50 on entering useStaticLocal
local static x is 51 on exiting useStaticLocal

global x is 1 on entering useGlobal
global x is 10 on exiting useGlobal

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 51 on entering useStaticLocal
local static x is 52 on exiting useStaticLocal

global x is 10 on entering useGlobal
global x is 10 on exiting useGlobal

local x in main is 5
```

*图 6.12* | 作用域示例。（第 2 部分，共 2 部分）

为了演示其他作用域，该程序定义了三个函数，每个函数都不接受参数且不返回值。函数 useLocal（第 39—46 行）声明自动变量 x（第 41 行）并将其初始化为 25。当程序调用 useLocal 时，该函数打印该变量，将其递增，然后再次打印，之后函数将程序控制权返回给其调用者。每次程序调用此函数时，该函数都会重新创建自动变量 x 并将其重新初始化为 25。

函数 useStaticLocal（第 51—60 行）声明静态变量 x 并将其初始化为 50。声明为 static 的局部变量即使在超出作用域时（即声明它们的函数未在执行时）也会保留其值。当程序调用 useStaticLocal 时，该函数打印 x，将其递增，然后再次打印，之后函数将程序控制权返回给其调用者。在下次调用此函数时，静态局部

会调用其他函数。但是当被调用函数返回其调用者时，被调用函数的自动变量需要“消失”。被调用函数的栈帧是为被调用函数的自动变量保留内存的理想位置。只要被调用函数处于活动状态，该栈帧就存在。当该函数返回时——并且不再需要其局部自动变量时——其栈帧会从栈中弹出，程序也不再知道这些局部自动变量。

当然，计算机中的内存量是有限的，因此只能使用一定量的内存来在函数调用栈上存储活动记录。如果发生的函数调用多到无法将其活动记录存储在函数调用栈上，就会发生称为栈溢出的错误。

### 函数调用栈实战

因此，正如我们所见，调用栈和活动记录支持函数调用/返回机制以及自动变量的创建和销毁。现在让我们考虑调用栈如何支持由 main 调用的 square 函数的运行（图 6.13 的第 9—14 行）。首先，操作系统调用 main——这会将一个活动记录压入栈中（如图 6.14 所示）。该活动记录告诉 main 如何返回操作系统（即转移到返回地址 R1），并包含 main 的自动变量（即 a，它被初始化为 10）所需的空间。

函数 main——在返回操作系统之前——现在调用图 6.13 第 13 行中的函数 square。这会导致 square 的栈帧（第 17—20 行）被压入函数调用栈（图 6.15）。该栈帧包含 square 返回 main 所需的返回地址（即 R2）以及 square 的自动变量（即 x）所需的内存。

```cpp
// Fig. 6.13: fig06_13.cpp
// square function used to demonstrate the function
// call stack and activation records.
#include <iostream>
using namespace std;

int square( int ); // prototype for function square

int main()
{
   int a = 10; // value to square (local automatic variable in main)

   cout << a << " squared: " << square( a ) << endl; // display a squared
} // end main

// returns the square of an integer
int square( int x ) // x is a local variable
{
   return x * x; // calculate square and return result
} // end function square
```

```text
10 squared: 100
```

图 6.13 | 用于演示函数调用栈和活动记录的 square 函数。

规定函数 `print` 不接受参数且不返回值。图 6.17 展示了声明和使用空参数列表函数的两种方式。

```cpp
// Fig. 6.17: fig06_17.cpp
// Functions that take no arguments.
#include <iostream>
using namespace std;

void function1(); // function that takes no arguments
void function2( void ); // function that takes no arguments

int main()
{
    function1(); // call function1 with no arguments
    function2(); // call function2 with no arguments
} // end main

// function1 uses an empty parameter list to specify that
// the function1 receives no arguments
void function1()
{
    cout << "function1 takes no arguments" << endl;
} // end function1

// function2 uses a void parameter list to specify that
// the function2 receives no arguments
void function2( void )
{
    cout << "function2 also takes no arguments" << endl;
} // end function2
```

```text
function1 takes no arguments
function2 also takes no arguments
```

**图 6.17** | 不接受参数的函数。

> **常见编程错误 6.10**
> 
> *除非为每个函数提供函数原型，或者每个函数在调用之前已经定义，否则 C++ 程序无法编译。*

![](img/023f159fdd47d944d48e08843cea732d_275_0.png)

## 6.13 内联函数

从软件工程的角度来看，将程序实现为一组函数是良好的做法，但函数调用会涉及执行时开销。C++ 提供内联函数来帮助减少函数调用开销——尤其是对于小型函数。在函数定义中将限定符 `inline` 放在函数的返回类型之前，会“建议”编译器在适当情况下就地生成函数代码的副本，以避免函数调用。权衡之处在于，程序中会插入函数代码的多份副本（通常会使程序更大），而不是只保留一份函数代码，并在每次调用函数时将控制权传递给它。编译器可以忽略 inline 限定符，并且对于除最小函数之外的所有函数通常都会这样做。

### 软件工程观察 6.10

对内联函数的任何更改都要求重新编译该函数的所有使用方。在某些程序开发和维护场景中，这可能很重要。

![](img/023f159fdd47d944d48e08843cea732d_276_0.png)

### 良好编程实践 6.5

`inline` 限定符应仅用于小型且频繁使用的函数。

![](img/023f159fdd47d944d48e08843cea732d_276_1.png)

### 性能提示 6.4

使用内联函数可以减少执行时间，但可能增加程序大小。

![](img/023f159fdd47d944d48e08843cea732d_276_2.png)

图 6.18 使用内联函数 cube（第 9—12 行）计算立方体的体积。函数 cube 的参数列表（第 9 行）中的关键字 const 告诉编译器，该函数不修改变量 side。这确保在计算过程中 side 的值不会被该函数更改。（关键字 const 将在第 7、8 和 10 章详细讨论。）注意，函数 cube 的完整定义出现在程序中使用它之前。这是必需的，以便编译器知道如何将 cube 函数调用展开为其内联代码。因此，可复用的内联函数通常放在头文件中，以便其定义可以包含在使用它们的每个源文件中。

### 软件工程观察 6.11

应使用 const 限定符来实施最小权限原则。使用最小权限原则正确设计软件可以大大减少调试时间和不适当的副作用，并使程序更易于修改和维护。

![](img/023f159fdd47d944d48e08843cea732d_276_3.png)

```cpp
// Fig. 6.18: fig06_18.cpp
// Using an inline function to calculate the volume of a cube.
#include <iostream>
using namespace std;

// Definition of inline function cube. Definition of function appears
// before function is called, so a function prototype is not required.
// First line of function definition acts as the prototype.
inline double cube( double side )
{
   return side * side * side; // calculate cube
} // end function cube

int main()
{
   double sideValue; // stores value entered by user
   cout << "Enter the side length of your cube: ";
   cin >> sideValue; // read value from user

   // calculate cube of sideValue and display result
   cout << "Volume of cube with side "
        << sideValue << " is " << cube( sideValue ) << endl;
} // end main
```

**图 6.18** | 计算立方体体积的内联函数。（第 1 部分，共 2 部分。）


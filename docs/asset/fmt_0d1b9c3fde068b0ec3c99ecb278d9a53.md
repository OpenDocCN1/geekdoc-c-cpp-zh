
在某些参数始终具有相同值的情况下，提供默认参数很有用。例如，银行利息在特定存款期间对所有客户可能保持不变。它还为程序员提供了更大的灵活性。函数可以用比其最常见应用所需的更多的参数编写。使用默认参数，程序员只能使用对特定情况有意义的参数。程序 4.2 说明了默认参数的使用。

### DEFAULT ARGUMENTS

```
#include <iostream>

using namespace std;

int main()
{
    float amount;

    float value(float p, int n, float r=0.15);  // prototype
    void println(char ch='*', int len=40);      // prototype

    println();                  // uses default values for arguments

    amount = value(5000.00,5);          // default for 3rd argument

    cout << "\n      Final Value = " << amount << "\n\n";

    println('=');       // use default value for 2nd argument

    return 0;
}
/*------------------------------------------------------------*/
float value(float p, int n, float r)
{
    int year = 1;
    float sum = p;

    while(year <= n)
    {
        sum = sum*(1+r);
        year = year+1;
    }
    return(sum);
}

void println(char ch, int len)
{
    for(int i=1; i<=len; i++) printf("%c",ch);
    printf("\n");
}
```

程序 4.2 的输出为

```
***********************************

    Final Value = 10056.8

===================================
```

提供默认参数的优点是：

- 1. 我们可以使用默认参数为现有函数添加新参数。

- 2. 默认参数可用于将相似函数合并为一个。

## 4.8 const Arguments

在 C++ 中，函数的参数可以声明为 const，如下所示。

```
int strlen(const char *p);
int length(const string &s);
```

限定符 const 告诉编译器函数不应修改参数。当此条件被违反时，编译器会生成错误。这种类型的声明只有在我们通过引用或指针传递参数时才有意义。

## 4.9 Function Overloading

如前所述，重载是指对不同目的使用同一事物。C++ 也允许函数重载。这意味着我们可以使用相同的函数名创建执行各种不同任务的函数。这在 OOP 中称为函数多态性。

使用函数重载的概念，我们可以用一个函数名设计一组函数，但参数列表不同。函数将根据函数调用中的参数列表执行不同的操作。要调用的正确函数是通过检查参数的数量和类型而不是函数类型来确定的。例如，重载的 `add()` 函数处理不同类型的数据，如下所示：

```
// Declarations
int add(int a, int b);                      // prototype 1
int add(int a, int b, int c);               // prototype 2
double add(double x, double y);             // prototype 3
double add(int p, double q);                // prototype 4
double add(double p, int q);                // prototype 5

// Function calls
cout << add(5, 10);                         // uses prototype 1
cout << add(15, 10.0);                      // uses prototype 4
cout << add(12.5, 7.5);                     // uses prototype 3
cout << add(5, 10, 15);                     // uses prototype 2
cout << add(0.75, 5);                       // uses prototype 5
```

函数调用首先匹配具有相同数量和类型参数的原型，然后调用适当的函数执行。最佳匹配必须是唯一的。函数选择涉及以下步骤：

- 1. 编译器首先尝试找到完全匹配，其中实际参数的类型相同，并使用该函数。

- 2. 如果找不到完全匹配，编译器会使用对实际参数的整型提升，例如，

- 3. 当两者都失败时，编译器会尝试使用内置转换（隐式赋值转换）对实际参数进行转换，然后使用匹配唯一的函数。如果转换可能产生多个匹配，则编译器会生成错误消息。假设我们使用以下两个函数：

- 4. 如果所有步骤都失败，则编译器会尝试用户定义的转换结合整型提升和内置转换来找到唯一的匹配。用户定义的转换通常用于处理类对象。

```
char to int
float to double
```

```
long square(long n)
double square(double x)
```

函数调用例如

```
square(10)
```

会引起错误，因为 int 参数可以转换为 long 或 double，从而造成应使用 `square()` 的哪个版本的不明确情况。

程序 4.3 说明了函数重载。

### FUNCTION OVERLOADING

```
// Function volume() is overloaded three times

#include <iostream>

using namespace std;

// Declarations (prototypes)
int volume(int);
double volume(double, int);
long volume(long, int, int);

int main()
{
    cout << volume(10) << "\n";
    cout << volume(2.5,8) << "\n";
    cout << volume(100L,75,15) << "\n";
    return 0;
}

// Function definitions

int volume(int s)  // cube
{
    return(s*s*s);
}

double volume(double r, int h)  // cylinder
{
    return(3.14519*r*r*h);
}

long volume(long l, int b, int h) // rectangular box
{
    return(l*b*h);
}
```

PROGRAM 4.3

程序 4.3 的输出为：

1000

157.26

112500

函数重载应谨慎进行。我们不应重载不相关的函数，而应将函数重载保留给执行密切相关任务的函数。有时，默认参数可代替重载使用。这可减少需要定义的函数数量。

重载函数被广泛用于处理类对象。当在下一章讨论类时，将对其进行说明。

## 4.10 Friend and Virtual Functions

C++ 引入了两种新型函数，即友元函数和虚函数。它们基本上是为了处理与类对象相关的某些特定任务而引入的。因此，对这些函数的讨论已推迟到类对象讨论之后。友元函数在下一章的第 5.15 节中讨论，虚函数在第 9 章的第 9.5 节中讨论。

## 4.11 数学库函数

标准 C++ 支持许多数学函数，可用于执行某些常用的计算。最常用的数学库函数已在表 4.1 中汇总。

### 表 4.1 常用数学库函数

| Function | Purposes |

|---|---|

| `ceil(x)` | Rounds x to the smallest integer not less than x `ceil(8.1)` = 9.0 and `ceil(-8.8)` = -8.0 |

| `cos(x)` | Trigonometric cosine of x (x in radians) |

| `exp(x)` | Exponential function e^x. |

| `fabs(x)` | Absolute value of x. If x>0 then `abs(x)` is x If x=0 then `abs(x)` is 0.0 If x<0 then `abs(x)` is -x |

| `floor(x)` | Rounds x to the largest integer not greater than x `floor(8.2)` = 8.0 and `floor(-8.8)` = -9.0 |

| `log(x)` | Natural logarithm of x(base e) |

| `log10(x)` | Logarithm of x(base 10) |

| `pow(x,y)` | x raised to power y(x^y) |

| `sin(x)` | Trigonometric sine of x (x in radians) |

| `sqrt(x)` | Square root of x |

| `tan(x)` | Trigonometric tangent of x (x in radians) |

> note

> The argument variables x and y are of type double and all the functions return the data type double.

要使用数学库函数，我们必须在传统的 C++ 中包含头文件 `math.h`，在 ANSI C++ 中包含 `cmath`。

## SUMMARY

+ 可以通过在程序的不同位置调用和使用函数来减小程序的大小。

+ 在 C++ 中 `main()` 向操作系统返回类型为 int 的值。由于函数的返回类型默认为 int，因此 `main()` 头中的关键字 int 是可选的。如果没有 return 语句，大多数 C++ 编译器会发出警告。

函数原型为编译器提供了有关函数的详细信息，例如参数的数量和类型以及返回值的类型。

C++ 中的引用变量允许我们通过引用将参数传递给函数。函数还可以返回对变量的引用。

当函数声明为 inline 时，编译器会用相应的函数代码替换函数调用。通常，将小型函数设为 inline。

如果函数声明过长或过于复杂，编译器可能会忽略 inline 声明，从而将函数作为普通函数编译。

C++ 允许我们在声明函数时为函数参数分配默认值。在这种情况下，我们可以在不指定所有参数的情况下调用函数。默认值始终从右到左添加。

在 C++ 中，函数的参数可以声明为 const，表示函数不应修改该参数。

C++ 允许函数重载。也就是说，我们可以在程序中拥有多个同名函数。编译器通过检查参数的数量和类型，将函数调用与确切的函数代码匹配。

C++ 支持两种新型函数，即友元函数和虚函数。

许多数学计算都可以使用 C++ 标准库支持的库函数进行。

## Key Terms

+ actual arguments

+ argument list

+ bubble sort

+ call by reference

+ call by value

+ called function

+ calling program

+ calling statement

+ cmath

+ const arguments

+ declaration statement

+ default arguments

+ default values

+ dummy variables

+ ellipses

+ empty argument list

+ exit value

+ formal arguments

+ friend functions

+ function call

+ function definition

+ function overloading

+ function polymorphism

+ function prototype

+ indirection

+ inline

+ inline functions

+ macros

+ main()

+ math library

+ math.h

+ overloading

+ pointers

+ polymorphism

+ prototyping

+ reference variable

+ return by reference

+ return statement

+ return type

+ return()

+ template

+ virtual functions

## Review Questions

4.1 State whether the following statements are TRUE or FALSE.

(a) A function argument is a value returned by the function to the calling program.

(b) When arguments are passed by value, the function works with the original arguments in the calling program.

(c) When a function returns a value, the entire function call can be assigned to a variable.

(d) A function can return a value by reference.

(e) When an argument is passed by reference, a temporary variable is created in the calling program to hold the argument value.

(f) It is not necessary to specify the variable name in the function prototype.

4.2 What are the advantages of function prototypes in C++?

4.3 Describe the different styles of writing prototypes.

4.4 Find errors, if any, in the following function prototypes.

(a) `float average(x,y);`

(b) `int mul(int a,b);`

(c) `int display(...);`

(d) `void Vect(int? &V, int & size);`

(e) `void print(float data [], size = 20);`

4.5 What is the main advantage of passing arguments by reference?

4.6 When will you make a function inline? Why?

4.7 How does an inline function differ from a preprocessor macro?

4.8 When do we need to use default arguments in a function?

4.9 What is the significance of an empty parenthesis in a function declaration?

4.10 What do you meant by overloading of a function? When do we use this concept?

4.11 Comment on the following function definitions:

```
(a) int *f()
{
    int m = 1;
    ....
    ....
    return(&m);
}
```

```
(b) double f()
{
    ....
    ....
    return(1);
}
```

```
(c) int & f()
{
    int n = 10;
    ....
    ....
    return(n);
}
```

## Debugging Exercises

4.1 Identify the error in the following program.

```
#include <iostream.h>
int fun()
{
    return 1;
}
float fun()
{
    return 10.23;
void main()
{
    cout << (int)fun() << ' ';
    cout << (float)fun() << ' ';
}
```

4.2 Identify the error in the following program.

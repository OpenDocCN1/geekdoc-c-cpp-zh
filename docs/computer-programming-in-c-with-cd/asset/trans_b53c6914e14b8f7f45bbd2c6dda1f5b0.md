

## 调用函数

在 C++ 程序中声明并定义的函数，可以在程序中的任何位置被调用。在 C++ 中，调用函数的方式是使用函数名加一对括号，并在括号内提供参数列表（如果有的话）。如果函数返回某个值，则在调用函数时必须使用相同数据类型的变量来接收该值。如果你需要直接显示返回值，也可以使用 `cout` 对象，而无需将值赋给任何其他变量。以下代码片段演示了如何调用函数：

```cpp
largest = maximum(i,j);
```

在上述代码片段中，调用了在 *定义函数* 一节中定义的 maximum(i, j) 方法。参数 i 和 j 作为函数参数传递给 maximum() 函数。maximum(i, j) 函数也返回一个值，该值存储在整型变量 largest 中。完整的程序包括声明函数原型、定义函数以及调用函数，如清单 9 所示（你可以在随书 CD 的 code/chapter3 文件夹中找到 Func4.cpp 文件）：

### 清单 9：声明、定义和调用函数

```cpp
#include <iostream.h>
int main()
{
    int i, j, largest;
    int maximum(int a, int b); // function prototype
    cout<<"Enter the value of i: ";
    cin>>i;
    cout<<endl;
    cout<<"Enter the value of j: ";
    cin>>j;
    cout<<endl;
    largest = maximum(i,j); // calling a function
    cout<<"The value that is greater between "<<i<<" and "<<j<<" is :"<<largest;
    return 0;
}
// Defining a function
int maximum(int a, int b)
{
    int temp=0;
    if(a > b)
        temp = a;
    else
        temp = b;
    return temp;
}
```

**输出：**

```
Enter the value of i: 5
Enter the value of j: 10
The value that is greater between 5 and 10 is: 10
```

在清单 9 中，我们通过 `int maximum(int a, int b);` 语句在 main() 函数内部定义了 maximum() 函数的原型。然后我们从用户那里接受两个数字，并调用 maximum() 函数传入这两个数字。maximum() 函数返回的值通过 `largest = maximum(i,j);` 语句存储在另一个整型变量 largest 中。最后，显示 largest 变量的值。你还可以看到 maximum() 函数是在 main() 函数外部定义的。

## 向函数传递参数

在 C++ 中，函数的参数用于初始化函数定义中的形参。参数可以是变量、常量或表达式。当向函数传递参数时，必须记住参数的个数和类型必须与函数定义中的形参一致。调用函数时传递的参数称为实际参数，定义函数时传递的参数称为形式参数。清单 10 演示了向 sub() 函数传递参数。在清单 10 中，value1 和 value2 是调用函数 sub(value1, value2) 的实际参数，num1 和 num2 是定义 void sub(int num1, int num2) 函数时的形式参数。你可以在随书 CD 的 code/chapter3 文件夹中找到 Func5.cpp 文件：

### 清单 10：向函数传递参数

```cpp
#include <iostream.h>
void sub(int num1, int num2) // Arguments num1 and num2 are formal arguments
{
    int num3;
    num3 = num1 - num2;
    cout<<"The subtraction of two numbers is : "<<num3;
}
int main()
{
    int value1, value2;
    cout<<"Enter value1 :";
    cin>>value1;
    cout<<endl;
    cout<<"Enter value2 :";
    cin>>value2;
    cout<<endl;
    sub(value1, value2); //value1 and value2 are actual arguments of sub()
    return 0;
}
```

**输出：**

```
Enter value1 :8
Enter value2 :5
The subtraction of two numbers is : 3
```

在清单 10 中，从用户那里接受两个整数值，并分别存储在变量 value1 和 value2 中。然后，`value1` 和 `value2` 作为参数传递给 `sub()` 函数。sub() 函数将 value2 变量的值从 value1 变量的值中减去，并将结果显示给用户。

## 从函数返回值

从函数返回值意味着函数必须返回一个值。返回值可以是 int、float、char 或数组。这意味着当函数被调用时，函数体被执行，执行完成后，函数返回一个值。以下是从函数返回值的语法：

```text
<return_type> <function-name>(<argument>)
{
    return <variable_name> or value;
}
```

在上述语法中，`return_type` 可以是任何数据类型，例如 char、int 和数组。return 语句必须放在函数体的末尾，即函数定义的右花括号之前。当函数返回一个值时，其数据类型必须与函数原型中的数据类型相同。清单 11 演示了 `sub()` 函数如何返回一个值。你可以在随书 CD 的 code/chapter3 文件夹中找到 Func6.cpp 文件：

### 清单 11：函数返回值

```cpp
#include <iostream.h>
int sub(int num1, int num2)
{
    int num3;
    num3 = num1 - num2;
    return num3;  // function returns a value
}

int main()
{
    int value1, value2, value3;
    cout<<"Enter value1 :";
    cin>>value1;
    cout<<endl;
    cout<<"Enter value2 :";
    cin>>value2;
    cout<<endl;
    value3 = sub(value1, value2); // function call
    cout<<"The subtraction of two number is :"<<value3;
    return 0;
}
```

**输出：**

```
Enter value1 :7
Enter value2 :2
The subtraction of two number is :5
```

在清单 11 中，定义了 `sub()` 函数，该函数接受两个整型变量作为参数，并返回它们之间的差。在 `main()` 函数中，从用户那里接受整数值（value1 和 value2），并将其作为参数传递给 `sub()` 函数。`sub()` 函数返回的值存储在 value3 变量中，并显示给用户。

## 测试你的知识

- 问题5. 编写一个程序，演示如何使用递归函数计算 2 的 n 次幂的乘法，其中 n 由用户提供。

答案：

```cpp
#include <iostream.h>
int power2n(int n)
{
    if (n > 1)
        return 2*power2n(n-1);
    return 2;
}
int main()
{
    int n;
    cout<<"Enter a number : ";
    cin>>n;
    cout<<"2 to the power of "<<n<<" is :"<<power2n(n);
    return 0;
}
```

**输出：**

```
Enter a number : 6
2 to the power of 6 is :64
```

- 问题6. 编写一个程序，求数字 m 的 n 次幂的乘积，其中 m 和 n 由用户提供。

答案：

```cpp
#include <iostream.h>
double power(double m, int n);   //function prototype
void main()
{
    int m, n;
    cout<<"Enter any number ";
    cin>>m;
    cout<<" Enter any integer number to calculate power ";
    cin>>n;
    cout<<"power("<<m<<", "<<n<<") = "<<power(m, n);
}
double power(double m, int n)
{
    double d1 = 1;
    for(int i=1;i<=n;i++)
    {
        d1 *= m;
    }
    return d1;
}
```

**输出：**

```
Enter any number 5
Enter any integer number to calculate power 4
power(5, 4) = 625
```

- 问题7. 编写一个程序，使用递归生成给定数字的斐波那契数列。

答案：

```cpp
#include<iostream.h>
int fibonacci(int n)
{
    if((n == 1) || (n == 0))
        return 1;
    else
        return fibonacci(n-1) + fibonacci(n-2);
}
void main()
{
    int n;
    cout<<"Enter any integer number :";
    cin>>n;
    cout<<"Fibonacci of "<<n<<" is :"<<fibonacci(n);
}
```

**输出：**

```
Enter any integer number :5
Fibonacci of 5 is :8
```

也可以使用 void 关键字创建一个执行结束后不返回值的函数。让我们在下一节中讨论返回 void 的函数。

## 描述返回 void 的函数

在程序中，如果你希望函数不返回任何值，可以将 void 关键字作为函数返回类型。不返回任何值的函数称为返回 void 的函数。函数在函数体末尾没有 return 语句的情况下终止，程序的执行将转移到调用函数的下一条语句。清单 12 演示了使用 void 关键字定义函数（convert()）。你可以在随书 CD 的 code/chapter3 文件夹中找到 Func7.cpp 文件：

### 清单 12：从函数返回 void

```cpp
#include <iostream.h>
void convert(float cel) // function definition with void
{
  float fahrenheit;
  fahrenheit = (cel*9)/5 + 32 ;
  cout<<"The equivalent temperature in fahrenheit is :"<<fahrenheit;
}

int main()
{
  float celsius;

  cout<<"Enter Celsius :";
  cin>>celsius;
  cout<<endl;
  convert(celsius); // function call
  return 0;
}
```

**输出：**

```
Enter Celsius :33.56
The equivalent temperature in fahrenheit is :92.408005
```

在清单 12 中，convert(float cel) 函数的返回类型被定义为 void，这意味着当该函数终止时，它不会向调用程序返回任何值。这就是为什么你可以看到在函数末尾没有使用 return 语句的原因。

现在，让我们学习函数的默认参数。

## 指定默认参数

默认参数是在定义函数时提供值的函数参数。调用函数时，不必为默认参数传递值。如果你为默认参数传递了值，函数将以




![](img/d68f6199646ca63591a6d8419e0ed4ba_244_0.png)

图 6.8 展示了 *main* 函数与 *greeting* 函数之间的通信。尽管 *main* 函数与 *greeting* 函数之间没有交换数据，但存在副作用。*main* 函数首先调用 *greeting* 函数。*greeting* 函数在屏幕上打印问候语（副作用）。随后控制权返回 *main* 函数（void 返回）。

## 带参数的 void 函数

下一个选择是创建带参数的函数。传给函数的值（实参）位于形参的位置。该函数有副作用，但不向调用者返回数据。当我们只需要函数的副作用，但还需要传递一些信息（例如每次调用函数时要输出的内容）时，就会使用这种类型的函数。正如稍后将看到的，带参数的 void 函数是输入-处理-输出设计中输出模块的良好选择。

## 示例 6.11

程序 6.9 展示了一个示例，其中参数告诉函数在每次执行时如何格式化图案。第 14 行到第 25 行是函数定义；第 38 行是函数调用。

## 程序 6.9——带参数的 void 函数

```cpp
/************************************************************
 * This program shows how we can create different patterns using     *
 * a void function with a parameter.                                  *
 ************************************************************/
#include <iostream>
using namespace std;

/************************************************************
 * Function definition for the pattern function. This is a void      *
 * function with one parameter that accepts its size from the        *
 * user each time the program is called. The parameter is used       *
 * to create a different size for the pattern.                       *
 ************************************************************/
void pattern (int size)
{
    for (int i = 0; i < size; i++)
    {
        for (int j = 0; j < size; j++)
```

## 图 6.9 主函数与 pattern 函数之间的通信

## 程序 6.10 无参数的有返回值函数

```cpp
/******************************************************
 * This program shows how to define a function to get a positive   *
 * integer from the keyboard and print its right-most digit.      *
 ******************************************************/
#include <iostream>
using namespace std;

/******************************************************
 * The getdata function is a returning-value function with         *
 * no parameters. It takes the user input (side effect) from      *
 * the keyboard and returns the value to the main function         *
 * after validating that the number is positive.                   *
 ******************************************************/
int getData()
{
    int data;
    do
    {
        cout << "Enter a positive integer: ";
        cin >> data;
    } while (data <= 0);
    return data;
}

int main()
{
    int number = getData(); // function call with no argument
    cout << "Right-most digit: " << number % 10;
    return 0;
}
```

```text
Run
Enter a positive integer: 56
Right-most digit: 6
```

## 程序 6.10 无参数的有返回值函数（续）

```text
Run
Enter a positive integer: -72
Enter a positive integer: 72
Right-most digit: 2
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_247_0.png)

**图 6.10** 主函数与 pattern 函数之间的通信

图 6.10 展示了 *main* 函数与 *getData* 函数之间的通信。每次运行程序时，我们从键盘获取一个整数，验证它为正数，然后将其返回给 *main* 函数。

## 带参数的有返回值函数

程序 6.11 展示了如何拥有一个带参数并返回值的函数。*larger* 函数从 *main* 函数接收两个值，找出两者中较大的一个，并返回结果。

## 程序 6.11 带参数的有返回值函数

```cpp
1  /*************************************************************
2  * This program shows how to define a function to find the    *
3  * larger of any two positive integers given by the user.     *
4  *************************************************************/
5  #include <iostream>
6  using namespace std;
7
8  /*************************************************************
9  * The larger function is a value-returning function with two    *
10 * parameters that gets two values from the calling function  *
11 * and returns the larger one. The function has no side effect.*
12 *************************************************************/
13 int larger (int fst, int snd)
14 {
15   int max;
16   if (fst > snd)
17   {
18      max = fst;
19   }
20    else
21    {
22        max = snd;
23    }
24    return (max);
25 } // End larger

27 int main()
28 {
29    // Declaration
30    int first, second;
31    // Get inputs
32    cout << "Enter the first number: ";
33    cin >> first;
34    cout << "Enter the second number: ";
35    cin >> second;
36    // Function call
37    cout << "Larger: " << larger (first, second); // Function call
38    return 0;
39 }

Run
Enter the first number: 56
Enter the second number: 71
Larger: 71

Run
Enter the first number: -10
Enter the second number: 8
Larger: 8
```

图 6.11 展示了 *main* 函数与 *larger* 函数之间的通信。*main* 函数向 *larger* 发送两个值（实参）。*larger* 函数找出两者中较大的一个并返回它。

## 6.3.2 使用声明

在之前的所有示例中，我们都将函数定义放在函数调用之前。另一种方法是将函数的声明（原型）放在函数调用之前。

![](img/d68f6199646ca63591a6d8419e0ed4ba_248_0.png)

**图 6.11** 函数调用、返回和副作用

![](img/d68f6199646ca63591a6d8419e0ed4ba_249_0.png)

图 6.12 将函数定义放在函数调用之后

并将函数定义放在函数调用之后，如图 6.12 所示。注意声明末尾必须有一个分号。

> 函数声明末尾需要有一个分号。

## 示例 6.12

程序 6.12 遵循模块化编程的原则：输入-处理-输出。main 函数只负责三个调用：输入调用、处理调用和输出调用。其余工作由三个函数完成：*input*、*process*、*output*。程序 6.12 旨在从用户处获取年份值（输入），检查该年份是否为闰年（处理），并打印结果（输出）。我们之前讨论过，一个年份要成为闰年需要满足两个条件。第一，它必须能被 4 整除。第二，如果它能被 100 整除，那么它还必须能被 400 整除。

## 程序 6.12 判断某一年是否为闰年

```cpp
/**************************************************************
 * This program shows how to use three functions: input an     *
 * integer representing a year, check if it is a leap year,   *
 * and print the result.                                       *
 **************************************************************/
#include <iostream>
using namespace std;

// Declarations (prototypes)
int input();
bool process (int year);
void output (int year, bool result);

int main()
{
    // Input, processing, output
    int year = input();
    bool result = process (year);
    output (year, result);
}
```

*（续）*

## 程序 6.12 判断某一年是否为闰年（续）

```cpp
/******************************************************************
 * The definition of the input function. It is called in the       *
 * main function. It takes the value of the year from the user     *
 * (side effect), validates the year to be greater than 1582,      *
 * and returns the result to the main function. The function is    *
 * value-returning, with no parameters, but with a side effect.    *
 *******************************************************************/
int input()
{
    int year;
    do
    {
        cout << "Enter a year after 1582: ";
        cin >> year;
    } while (year <= 1582);
    return year;
}
/******************************************************************
 * The definition of the process function. It takes the value of  *
 * the year from the main function. It checks to                  *
 * to see if it is a leap year and returns a boolean value back   *
 * to main. It is a value-returning function with a parameter      *
 * and no side effect.                                            *
 *******************************************************************/
bool process (int year)
{
    bool criteria1 = (year % 4 == 0);
    bool criteria2 = (year % 100 != 0) || (year % 400 == 0);
    return (criteria1) && (criteria2);
}
/******************************************************************
 * The output function takes the year value and the Boolean value  *
 * returned from the process function. It prints the results on   *
 * the monitor. It is a void function with two parameters.        *
 *******************************************************************/
void output (int year, bool result)
{
    if (result)
    {
        cout << "Year " << year << " is a leap year.";
    }
    else
    {
```

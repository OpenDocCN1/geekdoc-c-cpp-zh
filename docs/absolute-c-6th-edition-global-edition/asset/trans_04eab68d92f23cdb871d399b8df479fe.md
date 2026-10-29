

你的程序应允许用户输入任意日期并输出对应的星期几（英文）。

## 13.

你有四个相同的奖品要发放，候选人池有 25 名决赛选手。决赛选手的编号为 1 到 25。编写一个程序随机选择 4 名决赛选手的编号以获得奖品。确保不要重复挑选同一个号码。例如，挑选决赛选手 3、15、22 和 14 是有效的，但挑选 3、3、31 和 17 是无效的，因为决赛选手编号 3 被列出了两次且 31 不是有效的决赛选手编号。

## 14.

编程项目 2.9 要求你实现巴比伦算法来计算一个数的平方根。将此算法放入一个函数中并通过用它计算若干个数的平方根来测试它。该函数应以 double 返回平方根，并且也应将数字 n 作为 double 处理。

## 15.

社会保障局维护了一张精算生命表，其中包含美国某人死亡的概率（http://www.ssa.gov/OACT/STATS/table4c6.html）。2009 年的死亡概率存储在文件 LifeDeathProbability.txt 中，该文件包含在本书的网站上。每行有三个值：年龄、男性的死亡概率和女性的死亡概率。例如，前五行是

```
0 0.006990 0.005728
1 0.000447 0.000373
2 0.000301 0.000241
3 0.000233 0.000186
4 0.000177 0.000150
```

对第四行的解释是，3 岁女性在 3 岁到 4 岁期间死亡的概率为 0.000186。

编写一个程序，从键盘在主函数中输入年龄和性别。主函数应调用一个名为 simulate 的函数（你必须编写），将年龄和性别作为参数传递。函数应模拟一个人将活到什么年龄，通过从给定年龄和性别的死亡概率开始。你可以通过逐行读取文件中的数据来实现。跳过小于输入年龄的行。一旦达到输入年龄，生成一个介于 0 和 1 之间的随机数，如果该数小于或等于相应的死亡概率，则预测该人将活到当前年龄并返回该年龄。如果随机数大于死亡概率，则将年龄增加一并对文件中的下一行重复计算。如果模拟达到 120 岁，则停止并预测用户将活到 120 岁。主函数应输出模拟的死亡年龄。此程序只是一个模拟，每次运行结果会不同，前提是你更改随机数生成器的种子。

## Parameters and Overloading 4

### 4.1 PARAMETERS 176

Call-by-Value Parameters 176

A First Look at Call-by-Reference Parameters 178

Call-by-Reference Mechanism in Detail 181

Constant Reference Parameters 183

Example: The swapValues Function 183

Tip: Think of Actions, Not Code 184

Mixed Parameter Lists 185

Tip: What Kind of Parameter to Use 186

Pitfall: Inadvertent Local Variables 188

Tip: Choosing Formal Parameter Names 189

Example: Buying Pizza 190

### 4.2 OVERLOADING AND DEFAULT ARGUMENTS 193

Introduction to Overloading 193

Pitfall: Automatic Type Conversion and Overloading 196

Rules for Resolving Overloading 197

Example: Revised Pizza-Buying Program 199

Default Arguments 201

### 4.3 TESTING AND DEBUGGING FUNCTIONS 203

The assert Macro 203

Stubs and Drivers 204

## 4 Parameters and Overloading

Just fill in the blanks.

Common instruction

# Introduction

本章讨论了 C++ 用于在函数调用中为参数插入参数的机制的细节。它还讨论了重载，这是一种为同一个函数名提供两个（或更多）不同函数定义的方法。最后，它介绍了测试函数的一些基本技术。

## 4.1 Parameters

你不能把方形的楔子塞进圆形的孔里。

Common saying

本节描述了 C++ 用于在函数被调用时为形式参数插入参数的机制的细节。C++ 中有两种基本参数类型，因此有两种基本插入机制。两种基本参数类型是传值参数和传引用参数。书中到目前为止出现的所有参数都是传值参数。

对于传值参数，只插入参数的值。对于传引用参数，参数是一个变量，并且变量本身被插入；因此，变量的值可以被函数调用更改。传引用参数是通过在参数类型后加上与号 & 来表示的，如以下函数声明所示：

```
void getInput(double& variableOne, int& variableTwo);
```

传值参数是通过不使用与号来表示的。关于传值和传引用参数的细节在以下小节中给出。

## Call-by-Value Parameters

传值参数不仅仅是被函数参数值填入的空白。传值参数实际上是一个局部变量。当函数被调用时，传值参数的值被计算，并且相应的传值参数，即一个局部变量，被初始化为该值。

在大多数情况下，你可以将传值参数视为一种空白或占位符，由函数调用中对应参数的值填充。然而，在某些情况下，将传值参数用作局部变量并在函数体内部更改参数的值是很有用的

call-by-value parameter

call-by-reference parameter

definition。例如，程序在 Display 4.1 中说明了传值参数用作局部变量，其值在函数定义体中被更改。注意 fee 函数定义中的形式参数 minutesWorked。它被用作变量，其值被函数定义体内的以下行更改：

```
minutesWorked = hoursWorked*60 + minutesWorked;
```

## Display 4.1 Formal Parameter Used as a Local Variable (part 1 of 2)

```
//Law office billing program.
#include <iostream>
using namespace std;

const double RATE = 150.00; //Dollars per quarter hour.

double fee(int hoursWorked, int minutesWorked);
//Returns the charges for hoursWorked hours and
//minutesWorked minutes of legal services.

int main()
{
    int hours, minutes;
    double bill;

    cout << "Welcome to the law office of\n"
         << "Dewey, Cheatham, and Howe.\n"
         << "The law office with a heart.\n"
         << "Enter the hours and minutes"
         << " of your consultation:\n";
    cin >> hours >> minutes;

    bill = fee(hours, minutes);

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "For " << hours << " hours and " << minutes
         << " minutes, your bill is $" << bill << endl;

    return 0;
}
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;

    minutesWorked = hoursWorked*60 + minutesWorked;
    quarterHours = minutesWorked/15;
    return (quarterHours*RATE);
}
```

minutes 的值不会被对 fee 的调用更改。

minutesWorked 是初始化为 minutes 值的局部变量。

## Display 4.1 Formal Parameter Used as a Local Variable (part 2 of 2)

# Sample Dialogue

```
Welcome to the law office of
Dewey, Cheatham, and Howe.
The law office with a heart.
Enter the hours and minutes of your consultation:
5 46
For 5 hours and 46 minutes, your bill is $3450.00
```

传值参数就像你在函数体内部声明的变量一样是局部变量。然而，你不应该为形式参数添加变量声明。在函数头中列出形式参数 minutesWorked 也充当了变量声明。以下是以错误方式开始 fee 函数定义的方法，因为它声明了 minutesWorked 两次：

```
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;
    int minutesWorked;
    ...
```

当 minutesWorked 是参数时不要这样做！

## Self-Test Exercises

- 1. 仔细描述传值参数机制。
- 2. 以下函数本应以英尺和英寸表示的长度作为参数并返回总英寸数。例如，totalInches(1, 2) 本应返回 14，因为 1 英尺 2 英寸等于 14 英寸。以下函数是否能正确执行？如果不能，为什么？

```
double totalInches(int feet, int inches)
{
    inches = 12*feet + inches;
    return inches;
}
```

## A First Look at Call-by-Reference Parameters

我们到目前为止使用的传值机制对于你可能希望函数执行的所有任务来说是不够的。例如，函数的一个常见任务是从用户那里获取输入值并将参数变量的值设置为该输入值。使用我们到目前为止使用的传值形式参数，


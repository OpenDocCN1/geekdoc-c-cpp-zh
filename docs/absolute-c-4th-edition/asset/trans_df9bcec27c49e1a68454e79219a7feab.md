

## 展示 4.1 将形式参数用作局部变量（第 2 部分，共 2 部分）

```
26 double fee(int hoursWorked, int minutesWorked)
27 {
28     int quarterHours;
29     minutesWorked = hoursWorked*60 + minutesWorked;
30     quarterHours = minutesWorked/15;
31     return (quarterHours*RATE);
32 }
```

minutesWorked 是一个局部变量，其初始值为 minutes 的值。

### 示例对话

```
Welcome to the law office of
Dewey, Cheatham, and Howe.
The law office with a heart.
Enter the hours and minutes of your consultation:
5 46
For 5 hours and 46 minutes, your bill is $3450.00
```

按值传递的参数与你在函数体内声明的变量一样，都是局部变量。但是，你不应为形式参数添加变量声明。在函数头中列出形式参数 minutesWorked 本身就充当了变量声明。以下是定义 fee 函数的错误方式，因为它重复声明了 minutesWorked：

```
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;
    int minutesWorked;
    ...
```

当 minutesWorked 是参数时，切勿这样做！

### 自测练习

1. 仔细描述按值传递的参数机制。

2. 以下函数本应以英尺和英寸表示的长度作为参数，并返回该长度对应的总英寸数。例如，totalInches(1, 2) 应返回 14，因为 1 英尺 2 英寸等于 14 英寸。以下函数能否正确执行？如果不能，原因是什么？

```
double totalInches(int feet, int inches)
{
    inches = 12*feet + inches;
    return inches;
}
```

## 初步了解按引用传递的参数

我们迄今为止使用的按值传递机制，并不足以完成你可能希望函数执行的所有任务。例如，函数的一个常见任务是从用户处获取输入值，并将该输入值赋给一个参数变量。使用我们迄今所用的按值传递形式参数时，函数调用中的对应实参可以是变量，但函数只取该变量的值，而不会以任何方式改变该变量。对于按值传递的形式参数，只有实参的值被替换为形式参数。而对于输入函数，你希望将变量（而非变量的值）替换为形式参数。按引用传递机制正是以这种方式工作的。对于按引用传递的形式参数，函数调用中的对应实参必须是变量，并且该实参变量会被替换为形式参数。这几乎就像实参变量被字面复制到函数定义体中，取代了形式参数的位置。实参被替换后，函数体中的代码被执行，并可以改变实参变量的值。

按引用传递的参数必须以某种方式标记，以便编译器能将其与按值传递的参数区分开来。指示按引用传递参数的方法是在形式参数列表中的类型名末尾附加与号 &。这在函数声明（函数原型）和函数定义的头部都要进行。例如，以下函数定义有一个形式参数 receiver，它是一个按引用传递的参数：

```
void getInput(double& receiver)
{
    cout << "Enter input number:\n";
    cin >> receiver;
}
```

在包含此函数定义的程序中，以下函数调用会将 double 变量 inputNumber 设置为从键盘读取的值：

```
getInput(inputNumber);
```

C++ 允许你将与号放在类型名旁边或参数名旁边，因此你有时会看到

```
void getInput(double &receiver);
```

这与以下写法等价：

```
void getInput(double& receiver);
```

展示 4.2 演示了按引用传递的参数。该程序读入两个数字，然后以相反顺序写出相同的数字。在

## 展示 4.2 按引用传递的参数（第 1 部分，共 2 部分）

```
//Program to demonstrate call-by-reference parameters.
#include <iostream>
using namespace std;

void getNumbers(int& input1, int& input2);
//Reads two integers from the keyboard.

void swapValues(int& variable1, int& variable2);
//Interchanges the values of variable1 and variable2.

void showResults(int output1, int output2);
//Shows the values of variable1 and variable2, in that order.

int main()
{
    int firstNum, secondNum;

    getNumbers(firstNum, secondNum);
    swapValues(firstNum, secondNum);
    showResults(firstNum, secondNum);
    return 0;
}

void getNumbers(int& input1, int& input2)
{
    cout << "Enter two integers: ";
    cin >> input1
        >> input2;
}

void swapValues(int& variable1, int& variable2)
{
    int temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}

void showResults(int output1, int output2)
{
    cout << "In reverse order the numbers are: "
         << output1 << " " << output2 << endl;
}
```

## 展示 4.2 按引用传递的参数（第 2 部分，共 2 部分）

### 示例对话

```
Enter two integers: 5 6
In reverse order the numbers are: 6 5
```

函数 getNumbers 和 swapValues 中的参数是按引用传递的参数。输入操作由以下函数调用执行：

```
getNumbers(firstNum, secondNum);
```

变量 firstNum 和 secondNum 的值由该函数调用设置。之后，以下函数调用反转了两个变量 firstNum 和 secondNum 中的值：

```
swapValues(firstNum, secondNum);
```

接下来的几个小节将更详细地描述按引用传递机制，并解释展示 4.2 中使用的特定函数。

### 按引用传递的参数

要将形式参数设为按引用传递的参数，请在其类型名后附加与号 &。函数调用中的对应实参应为变量，而非常量或其他表达式。当函数被调用时，对应的变量实参（而非其值）将被替换为形式参数。在函数体中对形式参数所做的任何更改，都会在函数调用时作用于实参变量。替换机制的具体细节将在本章正文中给出。

#### 示例

```
void getData(int& firstInput, double& secondInput);
```

### 按引用传递机制的详细说明

在大多数情况下，按引用传递机制的工作方式就像函数实参中给出的变量名被字面替换为按引用传递的形式参数一样。然而，这个过程比这更微妙一些。在某些情况下，这种微妙之处很重要，因此我们需要更详细地考察这种按引用传递的替换过程。

程序变量以内存位置实现。每个内存位置都有一个唯一的地址，该地址是一个数字。编译器为每个变量分配一个内存位置。例如，当展示 4.2 中的程序被编译时，变量 firstNum 可能被分配位置 1010，而变量 secondNum 可能被分配位置 1012。就所有实际用途而言，这些内存位置就是变量。

例如，考虑展示 4.2 中的以下函数声明：

```
void getNumbers(int& input1, int& input2);
```

按引用传递的形式参数 input1 和 input2 是函数调用中实际实参的占位符。

现在考虑同一程序中的如下函数调用：

```
getNumbers(firstNum, secondNum);
```

当函数调用被执行时，函数并不会获得实参名称 firstNum 和 secondNum。相反，它获得的是与每个名称关联的内存位置列表。在此示例中，该列表由以下位置组成：

1010
1012

这些是按顺序分配给实参变量 firstNum 和 secondNum 的位置。与形式参数关联的正是这些内存位置。第一个内存位置与第一个形式参数关联，第二个内存位置与第二个形式参数关联，依此类推。用图示表示，在这种情况下对应关系为：

```
firstNum ⟶ 1010 ⟶ input1
secondNum ⟶ 1012 ⟶ input2
```

当函数语句被执行时，函数体对形式参数所做的任何操作，实际上都会对与该形式参数关联的内存位置中的变量执行。在此示例中，getNumbers 函数体中的指令表明应使用 cin 语句将一个值存储到形式参数 input1 中，因此该值被存储到内存位置 1010 中的变量中（恰好是变量 firstNum）。类似地，getNumbers 函数体中的指令表明随后应使用 cin 语句将另一个值存储到形式参数 input2 中，因此该值被存储到内存位置 1012 中的变量中（恰好是变量 secondNum）。因此，函数指示计算机对 input1 和 input2 所做的任何操作，实际上都会作用于变量 firstNum 和 secondNum。


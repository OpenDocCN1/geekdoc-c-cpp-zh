
## 程序 9.2 使用按引用传递的交换函数（续）

```cpp
int temp = rX;
rX = rY;
rY = temp;
}
```

运行：
交换前 x 和 y 的值。
x: 10 y: 20
交换后 x 和 y 的值。
x: 20 y: 10

## 按引用返回

在第二种情况下，**按引用返回**，被调用函数有一个必须返回给调用函数的对象。

**按值返回的特性** 在按值返回中，被调用函数使用以下原型返回所需类型的对象。

```cpp
type function (...);
```

按值返回简单且可在任何地方使用。我们可以返回参数或局部变量的值。唯一的缺点是复制的开销。如果要返回的对象是基本类型，我们不必担心；如果是类类型的对象，我们知道将调用复制构造函数，开销可能很高。

**按引用返回的特性** 在**按引用返回**中，要返回的对象的类型是对另一个对象的引用，如下原型所示。

```cpp
type& function (...);
```

这种方法消除了复制的开销，但有一个缺点：如果对象是值参数或局部变量（静态除外），我们就不能按引用返回它。原因将在本章后面讨论：当函数终止时，所有局部变量和值参数都被销毁。当对象被销毁时，我们不能拥有它的别名，但可以返回对引用参数的引用。

## 示例 9.9

假设我们要编写一个函数来找出两个整数中较大的一个。我们可以使用按值传递和按值返回的组合，也可以使用按引用传递和按引用返回的组合。下面并排展示两个程序以进行比较。

```cpp
#include <iostream>                    #include <iostream>
using namespace std;                   using namespace std;

// Return-by-value                                      // Return-by-reference
int larger (int x, int y)                              int& larger (int& x, int& y)
{                                                     {
    if (x > y)                                            if (x > y)
    {                                                     {
        return x;                                            return x;
    }                                                     }
    return y;                                              return y;
}                                                     }
int main ()                                            int main ()
{                                                     {
    int x = 10;                                             int x = 10;
    int y = 20;                                             int y = 20;
    int z = larger (x, y);                                  int z = larger (x, y);
    cout << z;                                              cout << z;
    return 0;                                               return 0;
}                                                     }

Run:                                                  Run:
20                                                    20
```

我们看到在这类情况下两种做法的示例，因为在按值传递和按值返回中复制开销很小。

## 示例 9.10

在本例中，我们找出两个类类型对象中较大的一个。在第7章中，我们创建了一个分数类。这里不再重复接口和实现文件（分离编译）。我们只创建一个应用程序文件，它使用按引用传递和按引用返回找出两个分数中较大的一个。程序9.3展示了该应用程序文件。

## 程序 9.3 找出两个分数中较大的一个

```cpp
/***************************************************************
 * The program creates two pairs of fractions and then calls a  *
 * function named larger to find the larger in each pair        *
 ***************************************************************/
#include "fraction.h"

Fraction& larger (Fraction&, Fraction&);  // Prototype

int main ( )
{
    // Creating first pair of fractions and finding the larger
    Fraction fract1 (3, 13);
    Fraction fract2 (5, 17);
    cout << "Larger of the first pair of fractions: ";
    larger (fract1, fract2).print ();
    // Creating second pair of fractions and finding the larger
    17    Fraction fract3 (4, 9);
    18    Fraction fract4 (1, 6);
    19    cout << "Larger of the second pair of fractions: ";
    20    larger (fract3, fract4).print ();
    21    return 0;
    22 }
    23 /********************************************************
    24  * The function gets two fractions by reference, compares them *
    25  * and returns the larger.                                  *
    26  ********************************************************/
    27 Fraction& larger (Fraction& fract1, Fraction& fract2)
    28 {
    29    if (fract1.getNumer() * fract2.getDenom() >
    30          fract2.getNumer() * fract1.getDenom())
    31    {
    32        return fract1;
    33    }
    34    return fract2;
    35 }
```

运行：
第一对分数中较大者：5/17
第二对分数中较大者：4/9

有趣的是，在每次调用中，返回的项是一个*左值*，即发送给函数的对象之一。这就是为什么我们可以将类中定义的*print*函数应用于该对象（第17行和第22行）。

## 9.2 指针

**指针类型**是一种复合类型，表示内存位置的地址。指针变量是其内容为指针类型的变量。在本节中，我们讨论地址、指针类型、指针变量以及一些相关问题。

### 9.2.1 地址

当我们谈论地址时，必须考虑两个独立的概念：内存中的地址和变量的地址。

### 内存中的地址

正如我们在第1章中简要讨论的，计算机内存是字节的序列。换句话说，最小可访问单元是*字节*。当我们说一台计算机有1千字节的内存（随机存取存储器，或RAM）时，我们是指内存由2<sup>10</sup>即1024字节组成。今天的计算机内存范围从兆字节（2<sup>20</sup>）、吉字节（2<sup>30</sup>）甚至太字节（2<sup>40</sup>）。

每个内存字节都有一个地址。地址以十六进制格式显示。例如，在一台有1千字节内存的计算机中，字节编号从0x000到0x3ff（十进制0到1023），如图9.7所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_410_0.png)

### 变量的地址

在我们的程序中，我们定义不同类型的变量：布尔型、字符型、整型、浮点型和类。每个变量占用一个或多个内存字节。*bool*或*char*类型的变量通常占用一个内存字节。*int*类型的变量可能占用四个或更多内存字节。*double*类型的变量也可能占用四个或更多内存字节（可以使用*sizeof*运算符确定字节数）。变量的地址是它所占用第一个字节的地址。这是我们在处理地址或指针时必须记住的重要一点，正如我们将看到的。要获取变量的地址，我们在变量前使用**地址运算符（&）**。

> 变量的地址是该变量所占用的第一个字节的地址。

## 示例 9.1

在本例中，我们编写一个简单程序，打印三个变量的地址：*bool*、*int*和*double*（程序9.4）。

### 程序 9.4 打印大小、值和地址

```cpp
/**************************************************************
 * The program to define three variables and to print their    *
 * values and their addresses in the memory                    *
 **************************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Declaration of three data variables
    bool flag = true;
    int score = 92;
    double average = 82.56;
    // Printing size, value, and address of the flag variable
    cout << "A variable of type bool" << endl;
    cout << "Size: " << sizeof (flag) << " " ;
    cout << "Value: " << flag << " " ;
    cout << "Address: " << &flag << endl << endl;
```

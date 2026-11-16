

```cpp
// main.cpp

#include <iostream>
#include <iomanip>

#include "ZipCode.h"

using namespace std;

int main() {
    ZipCode zip1(99504);
    ZipCode zip2(12345);
    ZipCode zip3(67890);
    ZipCode zip4("10010101001110000110011001001");
    ZipCode zip5("1101000001011100001100010011");
    ZipCode zip6("10000110001101010000111100101");

    cout << "Digits" << " " << "Bar Code" << endl;
    cout << zip1.getZipCode() << setw(35) << zip1.getBarCode() << endl;
    cout << zip2.getZipCode() << setw(35) << zip2.getBarCode() << endl;
    cout << zip3.getZipCode() << setw(35) << zip3.getBarCode() << endl;
    cout << endl;
    cout << zip4.getZipCode() << setw(35) << zip4.getBarCode() << endl;
    cout << zip5.getZipCode() << setw(35) << zip5.getBarCode() << endl;
    cout << zip6.getZipCode() << setw(35) << zip6.getBarCode() << endl;

    return 0;
}
```

国际奥委会需要你的帮助。用于根据每条赛道的计时数据确定比赛获胜者的计算机程序需要重写为面向对象风格。你被选中担任这项工作。幸运的是（或者也许不幸的是），一些初步设计工作已经完成，用于输入数据并将其打印出来的主程序也已经编写好了。你的工作是编写两个 C++ 类，`Competitor` 和 `Ranker`，包括声明（.h）和实现（.cpp），用于存储比赛中每个参赛者的信息，并按完成时间从低到高对这些参赛者进行排名。此代码应分为四个文件：`competitor.h`、`competitor.cpp`、`ranker.h` 和 `ranker.cpp`。

`Competitor` 类的对象在初始化时使用该人的姓名和赛道分配，分别指定为字符串和整数。该人的姓名应复制到 `Competitor` 对象自己的内存中；也就是说，不要只记录传入的指针。请注意，该人的姓名不应有预定义的大小。还要注意，对于本实验，你不应使用任何 C++ 预定义的 `String` 类。由于一开始不知道该人的时间，此值通过名为 `setTime()` 的单独成员函数设置，该函数接受一个双精度浮点值。还应有成员函数来检索姓名、赛道和时间，以及一个成员函数将对象作为单行文本打印出来。完成时间应保留一位小数。最后，不要忘记让类析构函数在该类的对象超出作用域时释放任何存储。

`Ranker` 类的对象在初始化时使用要排名的项目（`Competitor` 对象）的数量。指向 `Competitor` 对象的指针逐个传递给 `addList()` 成员函数。如果传入 `NULL` 指针，或者传入的对象总数超过预定义的项目数，`addList()` 应返回 0；否则，它返回传入的 `Competitor` 对象总数。项目通过两个成员函数从列表中检索（但不删除）：`getLane()` 和 `getFinish()`。每个函数接受一个从 1 到列表中项目数的整数。`getLane()` 返回指向指定赛道中 `Competitor` 对象的指针，而 `getFinish()` 返回指向在指定位置（第一名、第二名等）完成比赛的参赛者的指针。最后，当 `Ranker` 对象被销毁时，它会释放为自己分配的任何内存，但不会删除 `Competitor` 对象的内存（因为它无法知道这些对象是如何创建的）。

使用以下驱动程序测试你的类。你应该能够在不做任何更改的情况下将代码编译并链接到它：

```
// olympic.h

#ifndef _OLYMPIC_H
#define _OLYMPIC_H

#include "competitor.h"
#include "ranker.h"

#endif
```

```
// olympic.cpp

#include <iostream>
#include <fstream>
#include "olympic.h"

using namespace std;

ofstream csis;

int main() {
   const int lanes = 4;
   Ranker rank(lanes);

   csis.open("csis.txt");

   // First make a list of names and lane assignments
   Competitor* starters[lanes];

   starters[0] = new Competitor("Emmylou Harris", 1);
   starters[1] = new Competitor("Nanci Griffith", 2);
   starters[2] = new Competitor("Bonnie Raitt", 3);
   starters[3] = new Competitor("Joni Mitchell", 4);

   // The race is run; now assign a time to each person
   starters[0]->setTime((float)12.0);
   starters[1]->setTime((float)12.8);
   starters[2]->setTime((float)11.0);
   starters[3]->setTime((float)10.3);

// Put everyone into the ranker
for (int i = 0; i < lanes; i++)
    rank.addList(starters[i]);

// Now print out the list to make sure it's right
cout << "Competitors by lane are:" << endl;
csis << "Competitors by lane are:" << endl;
for (int i = 1; i <= lanes; i++)
    rank.getLane(i)->print();

// Finally, show how they finished
cout << "Rankings by finish are:" << endl;
csis << "Rankings by finish are:" << endl;
for (int i = 1; i <= lanes; i++)
    rank.getFinish(i)->print();
for (int i = 0; i < lanes; i++)
    delete starters[i];

csis.close();
// rank's destructor will be called automatically here
```

- 内联函数
- const 修饰符

## 内联函数

C 程序员通常使用预处理器通过宏和值替换来使代码更易于编写和阅读。我们将看到这种过程会引入错误，因为：

- 宏看起来像函数但不像函数一样工作
- 值替换看起来像表达式但不像表达式一样工作

然后我们将看到 C++ 如何通过内联函数和 const 来纠正这个问题。

### 函数或子程序

函数或子程序的目的或优势有很多：

- 使程序模块化
- 更容易调试程序
- 更容易维护程序
- 通常内存利用率较低

函数节省内存空间，因为对函数的所有调用都会导致执行相同的代码。因此，函数体不需要在内存中重复。

但是，请记住，使用函数也有缺点。C 和 C++ 等编程语言的一个令人遗憾的事实是，函数调用会浪费时间。要调用函数，编译后的程序必须：

- 将当前位置的返回地址保存在堆栈上
- 将函数所需的任何参数值压入堆栈
- 保存寄存器内容
- 执行汇编语言调用指令以调用函数
- 返回某个函数值
- 清除堆栈并返回到起始位置
- 恢复寄存器

所有这些指令都会减慢程序速度。虽然这些事件序列可能节省内存空间，但它们需要一些额外的时间。虽然单个函数调用发生得相当快，但大量函数调用会削弱程序的性能。但是，避免使用函数并不是解决这个问题的可接受方案！函数使程序模块化，更容易维护和调试。如果没有函数，要编写即使是中型程序且能正确运行，也极其困难，甚至不可能。事实上，如果函数非常短，调用它所需的指令甚至可能占用与函数体内的指令一样多的空间。在这种情况下，不仅有时间惩罚，还有空间惩罚。

## 宏

解决函数开销的一个可能方案是使用预处理器并定义使用代码替换的宏。例如，这里有一个检查其参数范围并在参数超出范围时调用 error() 的函数：

```
void test(int a) {
    if (a < 0 || a > 10)
        error(a);
}
```

现在，这里有一个执行相同范围检查的相应宏：

```
#define TEST(a) if (a < 0 || a > 10) error(a)
```

这里的问题是，预处理器宏看起来像函数但不像函数一样工作！如果我们进行以下相当无害的调用，就会得到一些意外的结果：

```
int main() {
    int x = 0;
    int y = 0;
    int u = 10;
    int v = 10;

    test(--x);    // error: -1 out of range
    TEST(--y);    // error: -2 out of range
    test(++u);    // error: 11 out of range
    TEST(++v);    // error: 13 out of range
}
```


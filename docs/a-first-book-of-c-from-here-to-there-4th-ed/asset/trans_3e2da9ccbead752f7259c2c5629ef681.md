

## 图 8.2 变量 num 存储在内存中的某处

![](img/e9bf940282dfb289356f077151cc69dd_362_0.png)

C++ 允许你更进一步，并显示任何变量对应的地址。所显示的地址对应于计算机内存中为该变量预留的第一字节的地址。

要确定变量的地址，必须使用地址运算符 &。你在声明引用变量时已经见过这个符号。当用于显示地址时，它表示“的地址”，并且放在变量名前面时，翻译为该变量的地址。² 例如，&num 表示“num 的地址”，&total 表示“total 的地址”，&price 表示“price 的地址”。程序 8.2 使用地址运算符来显示变量 num 的地址。

## 程序 8.2

```
#include <iostream>
using namespace std;

int main()
{
    int num;

    num = 22;
    cout << "The value stored in num is " << num << endl;
    cout << "The address of num = " << &num << endl;

    return 0;
}
```

这是程序 8.2 的输出：

```
The value stored in num is 22
The address of num = 0012FED4
```

> ²当在引用变量的声明中使用时（参见第 6.3 节），& 符号指的是其前面的数据类型。例如，声明 int &num 可读作“num 是 int 的地址”或更常见地“num 是 int 的引用。”

图 8.3 显示了程序 8.2 输出提供的额外地址信息。

![](img/e9bf940282dfb289356f077151cc69dd_363_0.png)

图 8.3 变量 num 的更完整图示

显然，程序 8.2 输出的地址取决于运行程序所使用的计算机以及程序运行时内存中其他程序或数据文件的情况。然而，每次运行程序 8.2 时，它都会显示用于存储 num 的第一个内存位置的地址。如程序 8.2 的输出所示，地址以十六进制表示法显示（参见第 2.6 节）。这种显示不会影响程序内部使用地址的方式；它只提供了一种比计算机内部使用的二进制系统更紧凑的表示地址的方式。正如你在以下各节中看到的，使用地址（而不是仅仅显示它们）为 C++ 程序员提供了一个强大的编程工具。

## 存储地址

除了像程序 8.2 中那样显示变量的地址外，你还可以将地址存储在适当声明的变量中。例如，语句

```
numAddr = &num;
```

将变量 num 对应的地址存储在变量 numAddr 中，如图 8.4 所示。

![](img/e9bf940282dfb289356f077151cc69dd_363_1.png)

图 8.4 将 num 的地址存储在 numAddr 中

同样，语句

```
d = &m;
tabPoint = &list;
chrPoint = &ch;
```

将变量 m、list 和 ch 的地址存储在变量 d、tabPoint 和 chrPoint 中，如图 8.5 所示。

## 图 8.5 存储更多地址

| 变量 | 内容 |
|---|---|
| d | m 的地址 |
| tabPoint | list 的地址 |
| chrPoint | ch 的地址 |

变量 numAddr、d、tabPoint 和 chrPoint 正式称为指针变量或指针。指针只是用于存储其他变量地址的变量。

## 使用地址

要使用存储的地址，C++ 提供了间接运算符 *。* 符号在后面跟随一个指针时（* 前后允许有空格），表示“地址存储在其中的变量”。因此，如果 numAddr 是一个指针（存储地址的变量），*numAddr 表示地址存储在 numAddr 中的变量。同样，*tabPoint 表示地址存储在 tabPoint 中的变量，*chrPoint 表示地址存储在 chrPoint 中的变量。图 8.6 显示了指针变量中包含的地址与变量之间的关系。

## 图 8.6 使用指针变量

指针变量 y
y 的内容是一个地址
地址 mmmm 处的内容是 qqqq

尽管 *d 表示“地址存储在 d 中的变量”，但它通常简称为“d 所指向的变量”。同样，参考图 8.6，*y 可读作“y 所指向的变量”。最终获得的值，如该图所示，是 qqqq。

在使用指针变量时，最终获得的值总是首先通过指针获取地址。然后使用指针中包含的地址来获取变量的内容。当然，这种获取最终值的方法相当间接，因此使用该术语间接寻址来描述它。

由于使用指针需要计算机进行双重查找（先检索地址，然后使用地址检索实际数据），你可能会想知道为什么要存储地址。答案在于指针与数组之间的共享关系以及指针在程序运行时动态创建和删除变量存储位置的能力。两个主题都在下一节中讨论。然而，就目前而言，鉴于每个变量都有一个与其关联的内存地址，存储地址的想法不应该显得不寻常。

## 声明指针

像所有变量一样，指针必须在用于存储地址之前声明。当你声明一个指针变量时，C++ 还要求指定所指向的变量的类型。例如，如果指针 numAddr 中的地址是整数的地址，则指针的正确声明为：

```
int *numAddr;
```

此声明可读作“numAddr 所指向的变量（声明中的 *numAddr）是一个整数”。³

请注意，声明 int *numAddr; 指定了两件事：首先，numAddr 所指向的变量是一个整数，其次，numAddr 必须是一个指针（因为它是用星号 * 声明的）。同样，如果指针 tabPoint 指向（包含）双精度数，chrPoint 指向字符变量，则这些指针所需的声明如下：

```
double *tabPoint;
char *chrPoint;
```

这两个声明可以读作“tabPoint 所指向的变量是一个 double”以及“chrPoint 所指向的变量是一个 char”。由于所有地址看起来都相同，编译器需要此额外信息来知道在使用指针中存储的地址时访问多少个存储位置。

以下是其他指针声明示例：

```
char *inkey;
int *numPt;
double *numPtr
```

要理解指针声明，从星号 * 开始向后阅读是有帮助的，将其翻译为“地址存储在其中的变量”或“所指向的变量”。应用此方法到指针声明，例如声明 char *inkey; 可以读作“地址存储在 inkey 中的变量是一个 char”或“inkey 所指向的变量是一个 char”。这两种说法通常都简化为更简单的“inkey 指向一个 char”。这三种对声明语句的解释都是正确的，因此你可以选择并使用对你最有意义的描述。程序 8.3 将这些信息放在一起构建一个使用指针的程序。

## 程序 8.3

```
#include <iostream>
using namespace std;

int main()
{
    int *numAddr;      // declare a pointer to an int
    int miles, dist;   // declare two integer variables

    dist = 158;        // store the number 158 in dist
    miles = 22;        // store the number 22 in miles
    numAddr = &miles;  // store the "address of miles" in numAddr

    cout << "The address stored in numAddr is " << numAddr << endl;
    cout << "The value pointed to by numAddr is " << *numAddr << "\n\n";

    numAddr = &dist; // now store the address of dist in numAddr
    cout << "The address now stored in numAddr is " << numAddr << endl;
    cout << "The value now pointed to by numAddr is " << *numAddr << endl;

    return 0;
}
```

程序 8.3 的输出如下：

```
The address stored in numAddr is 0012FEC8
The value pointed to by numAddr is 22

The address now stored in numAddr is 0012FEBC
The value now pointed to by numAddr is 158
```

程序 8.3 的唯一用途是帮助你理解存储在哪里，因此请回顾该程序以了解输出是如何产生的。声明语句 int *numAddr; 声明 numAddr 为用于存储整数变量地址的指针。语句 numAddr = &miles; 将变量 miles 的地址存储在指针 numAddr 中。第一个 cout 语句导致此地址被显示。第二个 cout 语句使用间接运算符 (*) 检索并显示 numAddr 所指向的值，即存储在 miles 中的值。

由于 numAddr 已声明为指向整数变量的指针，你可以使用此指针存储任何整数变量的地址。语句 numAddr = &dist 说明了这种用法，通过将变量 dist 的地址存储在 numAddr 中。最后两个 cout 语句验证了 numAddr 值的变化，并确认新的存储地址指向变量 dist。如程序 8.3 所示，只有地址应存储在指针中。


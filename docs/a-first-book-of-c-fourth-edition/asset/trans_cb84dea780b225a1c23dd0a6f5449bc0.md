

4. (练习) a. 编写一个包含以下声明语句的 C++ 程序。让程序使用地址运算符和 cout 语句显示每个变量对应的地址。
int num, count;
long date;
float slope;
double yield;

b. 运行练习 4a 编写的程序后，画出计算机为程序中的变量分配存储的示意图。在你的示意图上填入程序显示的地址。

c. 修改练习 4a 中编写的程序（使用第 2.1 节讨论的 sizeof() 运算符）以显示计算机为每种数据类型保留的存储量。利用这些信息和练习 4b 提供的地址信息，确定计算机是否按声明的顺序为变量分配存储。

5. (复习) 如果一个变量被声明为指针，该变量中必须存储什么？

6. (练习) 使用间接运算符，写出以下表达式：
a. xAddr 所指向的变量
b. 地址在 yAddr 中的变量
c. ptYld 所指向的变量
d. ptMiles 所指向的变量
e. mptr 所指向的变量
f. 地址在 pdate 中的变量
g. distPtr 所指向的变量
h. tabPtr 所指向的变量
i. 地址在 hoursPt 中的变量

7. (练习) 为以下内容编写声明语句：
a. yAddr 所指向的变量是一个整数。
b. chAddr 所指向的变量是一个字符。
c. ptYr 所指向的变量是一个长整数。
d. amt 所指向的变量是一个双精度变量。
e. z 所指向的变量是一个整数。
f. qp 所指向的变量是一个单精度变量。
g. datePt 是一个指向整数的指针。
h. yldAddr 是一个指向双精度变量的指针。
i. amtPt 是一个指向单精度变量的指针。
j. ptChr 是一个指向字符变量的指针。

8. (复习) a. 练习 7 中使用的变量 yAddr、chAddr、ptYr、amt、z、qp、datePt、yldAddr、amtPt 和 ptChr 分别被称为什么？
b. 为什么练习 7 中使用的变量名 amt、z 和 qp 不是指针名的好选择？

9. (练习) 写出以下声明变量包含内容的英文句子：
a. char *keyAddr;
b. int *m;
c. double *yldAddr;
d. long *yPtr;
e. double *pCou;
f. int *ptDate;

10. (练习) 以下哪个是指针的声明？
a. long a;
b. char b;
c. char *c;
d. int x;
e. int *p;
f. double w;
g. float *k;
h. float l;
i. double *z;

11. (练习) 对于以下声明，
int *xPt, *yAddr;
long *dtAddr, *ptAddr;
double *ptZ;
int a;
long b;
double c;
判断以下哪个语句是有效的：
a. yAddr = &a;    b. yAddr = &b;    c. yAddr = &c;
d. yAddr = a;     e. yAddr = b;    f. yAddr = c;
g. dtAddr = &a;   h. dtAddr = &b;  i. dtAddr = &c;
j. dtAddr = a;    k. dtAddr = b;   l. dtAddr = c;
m. ptZ = &a;      n. ptAddr = &b;  o. ptAddr = &c;
p. ptAddr = a;    q. ptAddr = b;   r. ptAddr = c;
s. yAddr = xPt;   t. yAddr = dtAddr;   u. yAddr = ptAddr;

12. (练习) 对于图 8.10 中的变量和地址，填入以下语句确定的数据：
a. ptNum = &m;
b. amtAddr = &amt;
c. *zAddr = 25;
d. k = *numAddr;
e. ptDay = zAddr;
f. *ptYr = 2011;
g. *amtAddr = *numAddr;

## 8.2 数组名作为指针

尽管指针按定义只是用于存储地址的变量，但数组名与指针之间也存在直接且密切的关系。本节详细描述这种关系。图 8.11 说明了名为 grade 的一维数组的存储，该数组包含五个整数。每个整数需要 4 字节的存储。

![](img/202cface8244f523c2641baa2e00d7dd_373_0.png)

使用下标，grade 数组中的第四个元素被称为 grade[3]。然而，使用下标掩盖了计算机对地址的广泛使用。内部，计算机立即使用下标根据

![](img/202cface8244f523c2641baa2e00d7dd_373_1.png)

数组的起始地址和每个元素使用的存储量来计算数组元素的地址。调用第四个元素 `grade[3]` 迫使编译器进行此地址计算：

`&grade[3] = &grade[0] + (3 * sizeof(int))`

记住地址运算符 (`&`) 的含义是“的地址”，此语句读作“`grade[3]` 的地址等于 `grade[0]` 的地址加上 3 倍整数的大小（即 12 字节）。”图 8.12 显示了用于定位 `grade[3]` 的地址计算。

![](img/202cface8244f523c2641baa2e00d7dd_374_0.png)

**图 8.12**  使用下标获取地址

因为指针是用于存储地址的变量，你可以创建一个指针来存储数组第一个元素的地址。这样做可以让你模拟计算机在访问数组元素时的操作。在此之前，先看一下程序 8.5。

# 程序 8.5

```
#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\\nElement " << i << " is " << grade[i];

    cout << endl;

    return 0;
}
```

当程序 8.5 运行后，它会产生以下显示：

```
Element 0 is 98
Element 1 is 87
Element 2 is 92
Element 3 is 79
Element 4 is 85
```

程序 8.5 通过使用标准下标表示法显示 grade 数组的值。通过先将数组元素 0 的地址存储在指针中，你可以使用指针中的地址访问每个数组元素。例如，如果你使用赋值语句 gPtr = &grade[0]; 将 grade[0] 的地址存储在名为 gPtr 的指针中，表达式 *gPtr（表示“gPtr 所指向的变量”）可用于访问 grade[0]，如图 8.13 所示。

![](img/202cface8244f523c2641baa2e00d7dd_375_0.png)

图 8.13 *gPtr 所指向的变量是 grade[0]

指针的一个独特特性是，可以在指针表达式中包含偏移量。例如，表达式 *(gPtr + 1) 中的 1 是一个偏移量。完整的表达式引用的是 gPtr 所指向变量之后的一个整数。同样，如图 8.14 所示，表达式 *(gPtr + 3) 引用的是 gPtr 所指向变量之后三个整数的变量：变量 grade[3]。

![](img/202cface8244f523c2641baa2e00d7dd_375_1.png)

图 8.14 gPtr 中地址的偏移量为 3

表 8.1 显示了通过下标引用的元素与通过指针和偏移量引用的元素之间的对应关系。图 8.15 说明了该表中列出的关系。

### 表 8.1 数组元素可以用两种方式引用

| 数组元素 | 下标表示法 | 指针表示法 |
|---|---|---|
| 元素 0 | grade[0] | *gPtr or (gPtr + 0) |
| 元素 1 | grade[1] | *(gPtr + 1) |
| 元素 2 | grade[2] | *(gPtr + 2) |
| 元素 3 | grade[3] | *(gPtr + 3) |
| 元素 4 | grade[4] | *(gPtr + 4) |

![](img/202cface8244f523c2641baa2e00d7dd_376_0.png)

# 图 8.15 数组元素与指针之间的关系

使用图 8.15 中显示的指针与下标之间的对应关系，程序 8.5 中使用下标访问的数组元素现在可以用指针访问，这在程序 8.6 中完成。

当程序 8.6 运行后会产生以下显示：

```
Element 0 is 98
Element 1 is 87
Element 2 is 92
Element 3 is 79
Element 4 is 85
```

## 数组和指针

```
Program 8.6

#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int *gPtr;          // declare a pointer to an int
    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    gPtr = &grade[0];        // store the starting array address
    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\nElement " << i << " is " << *(gPtr + i);

    cout << endl;

    return 0;
}
```

请注意，此显示与程序 8.5 的显示相同。程序 8.6 中用于访问数组元素的方法模拟了编译器在内部引用数组元素的方式。编译器会自动将程序员使用的任何下标转换为等效的指针表达式。在此情况下，由于 gPtr 的声明包含指向整数的信息，添加到 gPtr 地址中的任何偏移量都会自动按整数的大小进行缩放。因此，例如，*(gPtr + 3) 引用 grade[0] 的地址加上 12 字节的偏移量（3 × 4），假设 sizeof(int) = 4。这就是图 8.15 中显示的 grade[3] 的地址。

表达式 *(gPtr + 3) 中的括号对于正确引用数组元素是必要的。省略括号会导致表达式 *gPtr + 3。由于运算符优先级，此表达式将 3 加到“gPtr 所指向的变量”上。因为 gPtr 指向 grade[0]，此表达式将 grade[0] 的值和 3 相加。请注意，表达式 *(gPtr + 3) 不会改变 gPtr 中存储的地址。在计算机使用偏移量从 gPtr 存储的地址定位正确的变量后，偏移量会被丢弃，gPtr 中的地址保持不变。

尽管程序 8.6 中使用的指针 gPtr 是专门为存储 grade 数组的起始地址而创建的，但这样做是不必要的。当数组被创建时，编译器会为数组创建一个内部指针常量，并将数组的起始地址存储在此指针中。在几乎所有方面，指针常量与程序员创建的指针变量相同，但正如你将看到的，存在一些差异。

对于每个创建的数组，数组名成为编译器为数组创建的指针常量的名称，并且第一个位置的起始地址为数组保留


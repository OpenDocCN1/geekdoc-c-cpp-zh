
**程序 9.7** 找出两个对象中较大者

```cpp
10
11 int main ( )
12 {
13    // Creating the first pair of fractions
14    Fraction fract1 (3, 13);
15    Fraction fract2 (5, 17);
16    cout << "Larger of the first pair of fractions: ";
17    larger (&fract1, &fract2) -> print ();
18    // Creating the second pair of fractions
19    Fraction fract3 (4, 9);
20    Fraction fract4 (1, 6);
21    cout << "Larger of the second pair of fractions: ";
22    larger (&fract3, &fract4) -> print ();
23    return 0;
24 }
25 /************************************************************
26  * The function gets two fractions by pointer, compares them  *
27  * and returns the larger of the two.                         *
28  ************************************************************/
29 Fraction* larger (Fraction* fract1, Fraction* fract2)
30 {
31    if (fract1 -> getNumer() * fract2 -> getDenom() >
32        fract2 -> getNumer() * fract1 -> getDenom())
33    {
34        return fract1;
35    }
36    return fract2;
37 }
```

**运行：**

```text
Larger of the first pair of fractions: 5/17
Larger of the second pair of fractions: 4/9
```

## 9.3 数组与指针

在 C++ 中，数组和指针彼此交织。本节学习如何用指针表示一维数组和二维数组。

### 9.3.1 一维数组与指针

当我们声明一个名为 *arr*、类型为 t、容量为 N 的数组时，系统会创建 N 个类型为 t 的内存位置。系统随后创建一个类型为 t 的常量指针，指向第一个元素，如图 9.15 所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_424_0.png)

指针是常量意味着其内容（地址）不能改变。它始终指向第一个元素。由于第一个元素的地址是固定的，我们就知道所有元素的地址。索引为 0 的元素的地址是 `arr`（或 `arr + 0`）；索引为 1 的元素的地址是 `arr + 1`；依此类推。

> **数组名是指向第一个元素的常量指针。**

为了演示，我们编写一个程序，并打印图 9.15 中定义的数组元素的地址。我们同时使用指针的值和地址运算符来证明它们相同（程序 9.8）。该程序演示了我们可以使用常量指针或索引访问每个元素的地址。事实上，索引是一种符号表示，使访问元素更加容易。

**程序 9.8** 检查每个数组元素地址的程序

```cpp
/****************************************************
 * The program proves that the system stores the address of each       *
 * element in the array in a constant pointer.                         *
 *************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration of an array of five int
    int arr[5];
    // Printing the addresses through pointers and the & operator
    for (int i = 0; i < 5; i++)
    {
        cout << "Address of cell " << i << " Using pointer: ";
        cout << arr + i << endl;
        cout << "Address of cell " << i << " Using & operator: ";
        cout << &arr[i] << endl;
    }
    return 0;
}
```

**运行：**

```text
Address of cell 0 Using pointer: 0x28fee8
Address of cell 0 Using & operator: 0x28fee8

Address of cell 1 Using pointer: 0x28feec
Address of cell 1 Using & operator: 0x28feec

Address of cell 2 Using pointer: 0x28fef0
Address of cell 2 Using & operator: 0x28fef0

Address of cell 3 Using pointer: 0x28fef4
Address of cell 3 Using & operator: 0x28fef4

Address of cell 4 Using pointer: 0x28fef8
Address of cell 4 Using & operator: 0x28fef8
```

这意味着 `arr[0]` 与 `*(arr + 0)` 相同，但我们必须小心使用括号，因为星号运算符的优先级高于加法运算符，而使用括号可以改变这一点。同样有趣的是，每个地址增加 4 字节，这证明整数的大小为 4。

> 使用指针引用数组元素时，我们需要用括号让加法运算符优先。

**例 9.19**

程序 9.9 表明，使用索引和指针引用数组元素可以得到相同的结果。

**程序 9.9** 对数组使用索引和指针

```cpp
1 /**********************************************************
2 * The program shows how to access the elements of an array       *
3 * using either the indexes or pointers to elements.             *
4 **********************************************************/
5 #include <iostream>
6 using namespace std;
7
8 int main ( )
9 {
10   // Declaration and initialization of an array
11   int numbers [5] = {10, 11, 12, 13, 14};
12   // Accessing elements through the indexes
13   cout << "Accessing elements through indexes" << endl;
14   for (int i = 0; i < 5; i++)
15   {
16       cout << numbers [i] << " ";
17    }
18    cout << endl;
19    // Accessing elements through the pointers
20    cout << "Accessing elements through pointers" << endl;
21    for (int i = 0; i < 5; i++)
22    {
23        cout << *(numbers + i) << " ";
24    }
25    return 0;
26    }
```

**运行：**

```text
Accessing elements through indexes
10  11  12  13  14
Accessing elements through pointers
10  11  12  13  14
```

### 指针算术

指针类型不是整数类型。然而，指针算术允许将有限数量的算术运算符应用于指针类型。我们必须带着新的定义来看待这些运算符。使用这些运算符时，我们必须记住：由于结果是另一个指针值，该值必须指向我们控制的内存位置；否则结果毫无意义。这就是为什么将这些运算符应用于指向数组元素的指针时是有意义的：当我们声明数组时，所涉及的内存位置处于我们的控制之下。

**整数加法或减法**  我们可以使用加法运算符将整数加到指针上，或使用减法运算符从指针中减去一个整数：

| 加法 | 减法 |
|---|---|
| `ptr1 = ptr + n` | `ptr2 = ptr - n` |

以这种方式使用加法和减法运算符，会为它们创建新的定义。它会创建一个向前或向后移动 *n × m* 字节的新指针；*m* 是被指向变量的大小，其中 *m* 是每个元素占用的字节数。因此，该操作将指针向前或向后移动 *n* 个元素，如图 9.16 所示。加法创建的指针离数组开头更远；减法创建的指针离数组开头更近。红色箭头表示原始指针。

![](img/d68f6199646ca63591a6d8419e0ed4ba_426_0.png)

**图 9.16** 指针的整数加法和减法

**自增和自减** 这两个运算符设计用于变量（*值*）。它们不能用于数组名，因为数组名是一个常量值。`ptr++` 的含义与 `ptr = ptr + 1` 相同，`ptr--` 的含义与 `ptr = ptr - 1` 相同。在这些情况下，原始指针会如图 9.17 所示移动。自增操作后，原始指针指向 `arr[3]`。自减操作后，它指回 `arr[2]`。

![](img/d68f6199646ca63591a6d8419e0ed4ba_427_0.png)

**图 9.17** 自增和自减运算符应用于指针

**复合加法和减法** 我们也可以对指针变量使用复合加法和减法运算符。如果 *ptr* 是一个指针变量，表达式（`ptr += 3`）等价于（`ptr = ptr + 3`），表达式（`ptr -= 3`）等价于（`ptr = ptr - 3`）。这些操作与自增和自减运算符一样，会将指针移向开头或移向末尾，如图 9.18 所示。

![](img/d68f6199646ca63591a6d8419e0ed4ba_427_1.png)

**图 9.18** 复合加法和减法

**指针减法** 我们可以从一个指针中减去另一个指针。如果 *ptr1* 和 *ptr2* 是指针，其中 *ptr1* 指向索引较低的元素，*ptr2* 指向索引较高的元素，那么表达式（`ptr2 - ptr1`）返回一个正整数，而（`ptr1 - ptr2`）返回一个负整数，如图 9.19 所示。换句话说，这些运算的结果是整数，而不是指针。

**指针不能相加** C++ 中不允许指针值相加，因为这没有意义。


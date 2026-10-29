

## 显示 10.8 返回指向数组的指针

```
#include <iostream>
using namespace std;

int* doubler(int a[], int size);
//Precondition: size is the size of the array a.
//All indexed variables of a have values.
//Returns: a pointer to an array of the same size as a in which
//each indexed variable is double the corresponding element in a.

int main()
{
    int a[] = {1, 2, 3, 4, 5};
    int* b;

    b = doubler(a, 5);

    int i;
    cout << "Array a:\n";
    for (i = 0; i < 5; i++)
        cout << a[i] << " ";
    cout << endl;
    cout << "Array b:\n";
    for (i = 0; i < 5; i++)
        cout << b[i] << " ";
    cout << endl;

    delete[] b;
    return 0;
}

int* doubler(int a[], int size)
{
    int* temp = new int[size];

    for (int i =0; i < size; i++)
        temp[i] = 2*a[i];

    return temp;
}
```

此处的 delete 调用其实并不真正需要，因为程序即将结束，但在其他上下文中包含此 delete 可能是很重要的。

示例对话

```
Array a:
1 2 3 4 5
Array b:
2 4 6 8 10
```

## 自测练习

9. 编写一个指针变量的类型定义，该指针变量将用于指向动态分配的数组。数组元素类型为 char。将该类型命名为 CharArray。

10. 假设你的程序包含以下代码来创建一个动态分配的数组：

```
int *entry;
entry = new int[10];
```

使得指针变量 entry 指向此动态分配的数组。编写代码用键盘输入的十个数填充此数组。

11. 假设你的程序包含如自测练习 10 中创建动态分配数组的代码，并且假设指针变量 entry 的指针值未被更改。编写代码销毁此动态分配的数组并将其使用的内存返回给 freestore 管理器。

12. 以下代码片段的输出是什么？

```
int a[10];
int arraySize = 10;
int *p = a;
int i;
for (i = 0; i < arraySize; i++)
    a[i] = i;
for (i = 0; i < arraySize; i++)
    cout << p[i] << " ";
cout << endl;
```

## 指针算术

你可以对指针执行一种算术运算，但它是地址的算术，而不是数字的算术。例如，假设你的程序包含以下代码：

```
typedef double* DoublePtr;
DoublePtr d;
d = new double[10];
```

在此语句之后，d 包含索引变量 d[0] 的地址。表达式 d + 1 求值为 d[1] 的地址，d + 2 是 d[2] 的地址，以此类推。请注意，尽管 d 的值是一个地址，而地址是一个数字，但 d + 1 并不是简单地将 1 加到 d 中的数字上。如果 double 类型的变量需要八个字节（八个内存位置）并且 d 包含地址 2000，则 d + 1 求值为内存地址 2008。当然，类型 double 可以被任何其他类型替换，然后指针加法以该类型变量的单位移动。

addresses, not numbers

这种指针算术为你提供了一种操作数组的替代方法。例如，如果 arraySize 是 d 所指向的动态分配数组的大小，则以下代码将输出动态数组的内容：

```
for (int i = 0; i < arraySize; i++)
    cout << *(d + i)<< " ";
```

前者等价于以下代码：

```
for (int i = 0; i < arraySize; i++)
    cout << d[i] << " ";
```

你不能对指针进行乘法或除法运算。你能做的只是将整数加到指针上、从指针中减去整数，或减去两个相同类型的指针。当你减去两个指针时，结果是两个地址之间索引变量的数量。记住，对于两个指针值的减法，这些值必须指向同一个数组！从指向一个数组的指针中减去指向不同数组的指针几乎没有意义。

你也可以使用自增和自减运算符 ++ 和 -- 来执行指针算术。例如，d++ 将使 d 的值前进，使其包含下一个索引变量的地址，而 d-- 将使 d 包含前一个索引变量的地址。

## 多维动态数组

你可以拥有多维动态数组。你只需要记住，多维动态数组是数组的数组，或数组的数组的数组等等。例如，要创建一个二维动态数组，你必须记住它是一个数组的数组。要创建整数的二维数组，你首先创建一个 int* 类型的指针的一维动态数组，这是 int 的一维数组的类型。然后你为数组的每个元素创建一个 int 的动态数组。

类型定义可能有助于理清思路。以下是一个普通一维动态整数数组的变量类型：

```
typedef int* IntArrayPtr;
```

要获得一个三乘四的整数数组，你需要一个基类型为 IntArrayPtr 的数组。例如，

```
IntArrayPtr *m = new IntArrayPtr[3];
```

这是一个包含三个指针的数组，每个指针都可以命名一个整数的动态数组，如下所示：

```
for {int i = 0; i < 3; i++}
m[i] = new int[4];
```

由此产生的数组 m 是一个三乘四的动态数组。一个简单的程序来说明这一点在显示 10.9 中给出。

## 如何使用动态数组

- **定义指针类型：** 定义一种指向与数组元素类型相同变量的指针的类型。例如，如果动态数组是一个 double 数组，你可能会使用以下定义：
  
  ```
  typedef double* DoubleArrayPtr;
  ```

- **声明指针变量：** 声明此定义类型的指针变量。指针变量将指向内存中的动态分配数组，并将作为动态数组的名称。
  
  ```
  DoubleArrayPtr a;
  ```
  （或者，如果没有定义指针类型，使用 double *a；）。

- **调用 new：** 使用 new 运算符创建动态数组：
  
  ```
  a = new double [arraySize];
  ```
  
  动态数组的大小在方括号中给出，如前例所示。大小可以用 int 变量或其他 int 表达式给出。在前例中，arraySize 可以是类型为 int 的变量，其值在程序运行时确定。

- **像普通数组一样使用：** 指针变量，例如 a，与普通数组一样使用。例如，索引变量以通常的方式书写：a[0]、a[1] 等等。指针变量不应有任何其他指针值分配给它，而应像数组变量一样使用。

- **调用 delete []：** 当你的程序完成对动态分配数组变量的使用时，使用 delete 和空方括号以及指针变量来消除动态数组并将它占用的存储返回给 freestore 管理器以供重用。例如，
  
  ```
  delete [] a;
  ```

请注意显示 10.9 中 delete 的使用。由于动态数组 m 是一个数组的数组，在 for 循环第 13 行和 14 行中使用 new 创建的每个数组都必须使用 delete [] 调用返回给 freestore 管理器；然后，数组 m 本身必须使用另一个 delete [] 调用返回给 freestore 管理器。必须为每个使用 new 创建数组的调用提供一次 delete [] 调用。（由于程序在 delete [] 调用后立即结束，我们可以安全地省略 delete [] 调用，但我们想说明其用法。）

## 显示 10.9 一个二维动态数组

```
#include <iostream>
using namespace std;

typedef int* IntArrayPtr;

int main() {
    int d1, d2;
    cout << "Enter the row and column dimensions of the array:\n";
    cin >> d1 >> d2;

    IntArrayPtr *m = new IntArrayPtr[d1];
    int i, j;
    for (i = 0; i < d1; i++)
        m[i] = new int[d2];
    // m is now a d1-by-d2 array.

    cout << "Enter " << d1 << " rows of "
         << d2 << " integers each:\n";
    for (i = 0; i < d1; i++)
        for (j = 0; j < d2; j++)
            cin >> m[i][j];

    cout << "Echoing the two-dimensional array:\n";
    for (i = 0; i < d1; i++) {
        for (j = 0; j < d2; j++)
            cout << m[i][j] << " ";
        cout << endl;
    }

    for (i = 0; i < d1; i++)
        delete[] m[i];
    delete [] m;

    return 0;
}
```

请注意，必须为每个使用 new 创建数组的调用提供一次 delete[] 调用。（由于程序即将结束，这些 delete[] 调用其实并不真正需要，但在其他上下文中包含它们可能是很重要的。）

## 示例对话

```
Enter the row and column dimensions of the array:
3 4
Enter 3 rows of 4 integers each:
1 2 3 4
5 6 7 8
9 0 1 2
Echoing the two-dimensional array:
1 2 3 4
5 6 7 8
9 0 1 2
```


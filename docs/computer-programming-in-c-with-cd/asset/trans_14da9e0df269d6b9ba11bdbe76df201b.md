
清单 6 展示了 C++ 程序中 `new` 和 `delete` 运算符的使用（可在 CD 的 `code\chapter4` 文件夹中找到 `NewDelete.cpp` 文件）：

### 清单 6：使用 new 和 delete 运算符分配和释放内存

```cpp
#include <iostream.h>
void main()
{
    double * pi = new double;//declare the double pointer variable
    *pi = 3.14159;//assign a value to the referenced pointer variable
    cout<<"Value stored at newly allocated memory(pi) is:"<< * pi << endl;
    delete pi;//delete the memory held by pointer variables
    cout<<"The memory for the pointer 'pi' has been de-allocated"<<endl;
}
```

### 输出：

```text
Value stored at newly allocated memory(pi) is: 3.14159
The memory for the pointer 'pi' has been de-allocated
```

在清单 6 中，我们声明了一个由 double 指针变量 `pi` 引用的变量，并为其赋值。在显示变量 `pi` 的值之后，我们使用 `delete` 运算符释放了分配给变量 `pi` 的内存。最后，打印一条消息，确认已删除变量 `pi` 占用的内存。

## 4.2 使用指针探索数组

数组是相同数据类型变量的线性集合。在程序中创建数组时，其大小是有限的，可以包含 n 个元素，其中 n 是数组的大小。此外，可以使用元素的索引号来操作数组元素。索引号也称为下标号。数组中每个元素的索引号比它在数组中的实际位置小 1。例如，如果你想访问数组的第五个元素，索引号应为 4。你可以使用索引值在数组范围内逐个遍历元素。

指针也可用于引用数组。当指针处理数组时，它们存储数组类型变量中某个元素的地址。让我们看一个示例，其中创建了一个包含 11 个元素的整型数组 `arr`。该数组通过以下代码片段创建：

```cpp
int arr[11];
```

创建数组后，数组的所有元素在内存中彼此相邻地表示，如图 3 所示：

![](img/8a6886c00caa6a1651a6c0e62bff341f_235_0.png)

然后，可以使用以下代码片段表示该数组第一个元素的地址：

```cpp
&arr[0]; // we have used address operator to denote the address of first element
```

或者，可以使用以下代码片段表示数组的任意元素：

```cpp
&arr[i]; // for any element at the given index location denoted by i
```

现在，使用以下代码片段声明一个整型指针变量：

```cpp
int * ptr; // an integer pointer
```

声明整型指针变量后，我们可以使用以下代码片段，将数组第一个元素或任意其他元素的地址显式赋给新创建的指针变量：

```cpp
ptr = &arr[0];               //ptr points to address of arr[0]
```

或者，

```cpp
ptr = &arr[i]; // ptr points to the address of the element referenced by i
```

此外，还可以仅通过传入数组名（也可以说，不指定任何索引号），使用以下代码片段将数组第一个元素的地址赋给指针变量：

```cpp
ptr = arr;                   //ptr points to address of arr[0]
```

在 C++ 中，可以使用数组名以及指向数组的指针来访问和操作数组元素的值。然而，数组和指针的工作方式相当不同。由于指针是变量，可以使用运算符（+、-、++、--）进行操作；而数组是变量的线性集合，不能使用诸如 arr++ 这样的操作进行操作，其中 arr 是数组名。清单 7 展示了如何使用指针处理数组（可在 CD 的 `code\chapter4` 文件夹中找到 ArrayPointer.cpp 文件）：

### ▶ 清单 7：使用指针处理数组

```cpp
#include<iostream.h>
void main()
{
    int myarray [5] = {10,11,12,13,14};      //declare an integer array
    int i;
    for(i=0;i<5;i++)//using for loop traverse through it
    {
        cout<<"address of element"<<i<<": " <<(myarray + i) <<endl;
        //print addresses of all elements using (myarray)
    }
    for(i=0;i<5;i++)
    {
        cout<<"element at address"<< " "<<(myarray + i) <<" is "<<*(myarray + i)<<endl;
        //print contents at the addresses
    }
}
```

**输出：**

```text
address of element0:0x0012ff40
address of element1:0x0012ff44
address of element2:0x0012ff48
address of element3:0x0012ff4c
address of element4:0x0012ff50
element at address 0x0012ff40 is 10
element at address 0x0012ff44 is 11
element at address 0x0012ff48 is 12
element at address 0x0012ff4c is 13
element at address 0x0012ff50 is 14
```

在清单 7 中，我们声明了一个整型数组（myarray）。由于数组名保存其第一个元素的地址，我们使用其名称（myarray）来打印地址。最后，我们使用 *(myarray) 打印指定地址处的值。

接下来，让我们解释如何对指针变量执行算术运算、如何使用指针变量处理字符串，并讨论动态数组。

### 使用指针算术

C++ 允许对指针变量进行算术运算。指针算术用于对内存地址而不是简单变量执行算术运算。算术运算主要用于快速、准确地操作由变量（包括数组）分配的地址。对指针执行算术运算的主要目的是在指针变量引用的地址区域内前后移动。

当你想访问数组中的一系列值时，指针算术很有用。为此，需要将指针变量（引用该数组）加 1，以从一个值移动到下一个值。指针算术中使用以下类型的算术运算符：

- 递增（++）和递减（--）运算符
- 加法（+）和减法（-）运算符
- 星号（*）运算符

### 递增（++）和递减（--）运算符

指针变量充当指向变量地址的索引。当存储的变量为整型时，它在内存中占用 4 字节。当应用递增（++）运算符时，指针变量在跳过 4 字节的间隔后指向下一个元素。当数据为 double、float 或字符类型时，索引会根据其大小移动。可以使用递减（--）运算符移动到数组的前一个元素。

### 加法（+）和减法（-）运算符

加法（+）运算符按指定数据类型的大小增加指针的值，并使指针变量指向指定元素。减法（-）运算符按指定数据类型的大小减小指针的值，并使指针变量指向指定元素。

### 星号（*）运算符

`*` 运算符用于指针变量之前，以检索变量的值。在对指针执行算术运算时，还会考虑与指针变量一起使用的数据类型的大小。让我们考虑一个示例，其中指针 ptr 存储一个名为 arr 的 float 类型数组的引用，该数组包含 5 个元素。假设数组 arr 的第一个元素位于内存位置 2000。当使用 ++ 运算符递增指针 ptr 时，指针的地址会增加四个字节而不是一个字节，因为 float 数据类型占用的大小是 4 字节。图 4 展示了对指针变量执行算术运算的方式：

![](img/8a6886c00caa6a1651a6c0e62bff341f_237_0.png)

清单 8 展示了指针算术的使用（可在 CD 的 `code\chapter4` 文件夹中找到 `ArithmeticPointer.cpp` 文件）：

### 清单 8：使用指针算术打印数组元素

```cpp
#include<iostream.h>
void main()
{
    int myarray [5] = {10,11,12,13,14};//declare an array of integers
    int* ptr = &myarray[0];//declare a pointer and assign the address of the first element of array
    cout<<"<ptr> prints value at the first memory location:";
```

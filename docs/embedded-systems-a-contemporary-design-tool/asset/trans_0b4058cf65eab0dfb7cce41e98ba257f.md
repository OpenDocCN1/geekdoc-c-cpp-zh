

## 示例 7.7

从声明和赋值开始，

```
int *myData0Ptr = &myData0;
```

赋值运算符左侧的代码片段从右向左分几步读取：

- 1. myData0Ptr – 第一部分。
- 2. 是指针 – * 第二部分。
- 3. 指向整数 – int 第三部分。
- 4. myData0Ptr 是指向整数的指针。

再来一次，

```
float *anOtherPtr = &myFloatVar;
```

我们读取

- 1. anOtherPtr – 第一部分。
- 2. 是指针 – * 第二部分。
- 3. 指向浮点数 – float 第三部分。
- 4. anOtherPtr 是指向浮点数的指针。

如果我们假设编译器将指针变量 myData0Ptr（记住，它只是另一个变量）放在内存地址 0xCD00，我们现在有如图 7.9 所示的图景。

myData0Ptr，解引用运算符

![](img/679b8d2d47f1bf86e17aca48f596f5cc_350_0.png)

图 7.9 指针引用内存中的变量

我们可以通过在指针变量前使用解引用运算符 * 来获取 myData0Ptr 所引用的值。因此，如果我们写

```
int myData1 = *myData0Ptr;
```

myData1 值 0x3 被赋给 myData1，步骤如图 7.10 所示。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_351_0.png)

- 1. 获取指针变量 myData0Ptr 中包含的值，0x3000。
- 2. 转到该值所指定、指向或引用的地址（0x3000）。
- 3. 获取内存地址 0x3000 处变量 myData0 的值——这将是值 0x3。
- 4. 将该值（0x3）赋给变量 myData1。

图 7.10 使用指针获取内存中变量的值

同样，如果我们写

```
myData3 = 0x4;
*myData0Ptr = myData3;
```

myData0Ptr 值 0x4 被赋给指针变量 myData0Ptr 所引用的内存位置，步骤如图 7.11 列出。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_352_0.png)

- 1. 将值 0x4 赋给变量 myData3。
- 2. 获取变量 myData3=0x4 中包含的值。
- 3. 获取指针变量 myData0Ptr 的值，0x3000。
- 4. 转到该值所指定或指向的地址（0x3000）。
- 5. 将变量 myData3 中包含的值赋给内存地址 0x3000 处的变量 myData0——这将是值 0x4。

图 7.11 使用指针更改内存中的变量

让我们试试这个（见图 7.12）。

## 示例 7.8

```
/* A First Look at Pointers */
#include <stdio.h>
void main(void)
{
 int myData0 = 0x3;
 int myData1 = 0;
 int myData2 = 0;
 int myData3 = 0;
 int *myData0Ptr = &myData0; // myData0Ptr is a pointer to int
 // initialized to point to myData0
 myData1 = *myData0Ptr; // myData1 now contains the value 3
 printf("The value of myData1 is: %d\n", myData1);
 *myData3 = 4; // myData3 now contains the value 4
 *myData0Ptr = myData3; // myData0 now contains the value 4 as well
 printf("The value of myData3 is: %d\n", *myData0Ptr);
 return;
}
```

图 7.12 使用指针

该程序将打印

```
The value of myData1 is: 3
The value of myData3 is: 4
```

## 7.3.2 简单指针运算

我们已经学习过，各种算术运算符可以应用于 C 变量。合理地询问，这些相同的运算符是否可以应用于指针变量。答案是既是也不是。让我们先看看不能做什么。

指针不能相加、相乘或相除。稍加思考，这些限制是有道理的。指针不能由标量相加、相乘或相除。这也是有道理的。在这两种情况下，人们不得不问：如果这些操作是合法的，算术运算的结果是否给出有意义的答案？

另一方面，指针变量和标量可以相加。结果是一个指针变量——具体来说，是指向内存地址的指针变量，该地址相对于原始地址偏移了以字节为单位的偏移量大小。相反，两个指针可以相减；结果是一个标量。标量的值是分隔两个指针的偏移量大小（以字节为单位）。

表面上看，这一切似乎都很简单。表面之下，只要认识到有一些小的指针魔法在进行，它仍然很简单。让我们看看那种魔法是什么，以及在这一点上，它是否真的只是小魔法。

正如我们所学，不同的变量类型占用不同的内存量。存储类型所需的字节数可以通过将 C 的 sizeof 运算符应用于该类型来确定。

```
sizeof (type)
```

运算符的应用返回存储指定类型操作数所需的字节数。操作数可以是内置类型或用户定义类型。

当写入以下表达式时，底层发生了什么

```
myPointer0 = myPointer1 + anInteger
```

编译器实际上计算的是

```
myPointer0 = myPointer1 + anInteger * sizeof( type of myPointer1)
```

这种操作给出一个新的指针值，该值引用与原始值由指定类型的标量数个变量实例分隔的内存位置。让我们看看内存。

## 示例 7.9

设 myPointer1 为指向整数的指针类型，并放置在内存位置 0x3000。我们进一步假设整数为 16 位——在该机器上为两个字节。如果我们写：

```
int* myPointer0 = myPointer1 + 4;
```

代码片段被解释为：

```
int* myPointer0 = myPointer1 + 4 * ( sizeof ( int ) );
= 0x3000 + 4*2
= 0x3008
```

变量 myPointer0 现在将引用地址 0x3008。

## 示例 7.10

让我们重复前一个示例；这次我们将使用负整数。再次，设 myPointer1 为指向整数的指针类型，并放置在内存位置 0x3000。我们写：

```
int* myPointer0 = myPointer1 - 4;
```

代码片段被解释为：

```
int* myPointer0 = myPointer1 - 4 * ( sizeof ( int ) );
= 0x3000 - 4*2
= 0x2FF8
```

变量 myPointer0 现在将引用地址 0x2FF8。

回到指针相减的问题，我们现在应该看到，两个指针之间的差由编译器计算为：

```
pointer_1 - pointer_2 / sizeof (type)
```

记住，当我们写变量名时——在这里是指针——它等同于写它的值，而该值是一个地址。

以下任何代码片段的含义和结果现在应该开始变得清晰。

```
int* myPtr = anAddress;
myPtr*1;
myPtr++;
myPtr*3;
myPtr -= 1;
--myPtr;
```

每个操作都将标量值代数地加到指针上。但是，使用自增（自减）运算符时必须小心，并知道何时对指针进行解引用。对于自增（自减）运算符，前缀位置表示先进行算术运算，然后再求值指针变量，而后缀位置表示先求值指针变量，然后再进行算术运算。

图 7.13 中的代码片段并非都完成相同的事情，也不会使指针保持相同的状态。让我们假设指针的初始值为 0x3000，值 0x3 存储在位置 0x3000，并且我们正在使用 16 位整数。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_354_0.png)

图 7.13 指针与指针运算的优先级

```
int aVal = *(myPtr++);
```

### 求值

- 1. 括号内的操作将首先求值。myPtr 将被求值为 0x3000，这将是操作的返回值。
- 2. 在返回之前，myPtr 将按一个整数的大小递增到 0x3002。
- 3. 返回值 0x3000——即递增*之前*的值。
- 4. 0x3 将被赋给 aVal，因为这是内存位置 0x3000 处存储的值。

```
int aVal = *myPtr + 1;
```

### 求值

- 1. myPtr 将被求值为 0x3000 并解引用。
- 2. 将返回内存位置 0x3000 处的值。
- 3. 将 1 加到从内存位置 0x3000 返回的值上，得到 0x4。
- 4. 0x4 将被赋给 aVal。

```
int aVal = *(myPtr + 1);
```

### 求值

- 1. myPtr 将被求值为 0x3000。
- 2. 将 1 加到 0x3000 上得到 0x3002。
- 3. 将返回内存位置 0x3002 处的值并赋给 aVal。


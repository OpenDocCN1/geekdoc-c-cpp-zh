

```cpp
int main()
{
    int i = 11,
        j = 22,
        k = 33;

    int * iPtr = &i;
    int * jPtr = &j;
    int * kPtr = &k;

    cout << "\nAt address " << iPtr
         << ", the value " << *iPtr << " is stored.\n"
         << "\nAt address " << jPtr
         << ", the value " << *jPtr << " is stored.\n"
         << "\nAt address " << kPtr
         << ", the value " << *kPtr << " is stored.\n";
}
```

# SAMPLE RUN:

At address 0xbffff970, the value 11 is stored.

At address 0xbffff96c, the value 22 is stored.

At address 0xbffff968, the value 33 is stored.

## 15.1.1 声明和初始化指针

我们从示例 15.1 中程序的第二组声明开始：

```cpp
int * iPtr = &i;
int * jPtr = &j;
int * kPtr = &k;
```

这些语句中有两项新内容：

- 1. *在形如*
  
      ```cpp
      type * variableName;
      ```
  
      的声明中跟在类型名之后的一个星号 (*)，*
  
      声明 `variableName` 可以存储一个存储指定 `Type` 值 的内存位置的地址。这类变量通常称为 **指针变量**，或简称为指针。因此，声明
  
      ```cpp
      int * iPtr;
      int * jPtr;
      int * kPtr;
      ```

  声明 iPtr、jPtr 和 kPtr 为指针变量，每个都可以存储一个存储 int 的内存位置的地址。这三个变量的类型均为 int *。

2. 取地址运算符（&）可作为变量名上的前缀一元运算符使用，

```
&variableName
```

返回与 variableName 关联的地址，因此 & 被称为取地址运算符。因此，表达式 &i、&j 和 &k 分别返回与变量 i、j 和 k 关联的地址（或引用³）。

将这两条信息结合起来，我们看到声明

```
int * iPtr = &i;
int * jPtr = &j;
int * kPtr = &k;
```

将 iPtr、jPtr 和 kPtr 声明为指针变量，每个都可以存储包含 int 的内存位置的地址，并且它们将 iPtr 初始化为变量 i 的地址，jPtr 初始化为变量 j 的地址，kPtr 初始化为变量 k 的地址。在示例 15.1 的示例运行中，与变量 i 关联的地址是十六进制值 0xbffff970，j 的地址是 0xbffff96c，k 的地址是 0xbffff968。我们可以按如下方式可视化程序数据的内存布局：⁴

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_611_0.png)

必须记住，在声明中，星号运算符 * 必须位于要作为指针的每个标识符之前。因此，

```
double * ptr1,
    * ptr2;
```

是正确地将 ptr1 和 ptr2 声明为指向 double 的指针的声明。如果我们写成

```
double * ptr1,
    ptr2;
```

> ¹ 术语 reference 用作 address 的同义词。事实上，这就是引用参数一词的由来——引用参数的值实际上是其参数的地址，而不是参数的副本。

> ¹ 请注意（使用十六进制算术）
> 0xbffff970 - 0xbffff96c = 4
> 且
> 0xbffff96c - 0xbffff968 = 4
> 这表明在此特定机器上 int 的大小为 4 字节（32 位）。

则只有 ptr1 是指针变量；ptr2 将是一个普通的 double 变量。为了避免犯此错误，我们通常会对每个指针变量使用单独的声明：

```
double * ptr1;
double * ptr2;
```

### 15.1.1.1 使用 typedef 提高可读性

一种不需要在指针声明中重复使用星号的替代记法是使用 typedef 重命名类型。例如，我们可以在示例 15.1 中首先声明

```
typedef int * IntPointer;
```

然后使用 IntPointer 声明指针：

```
IntPointer iPtr = &i,
    jPtr = &j,
    kPtr = &k;
```

此类声明提高了指针声明的可读性，尤其是在声明指针参数时。

## 15.1.2 基本指针操作

C++ 支持对指针的多种操作，包括初始化、解引用、I/O、赋值、比较和算术。我们依次检查这些操作。

### 15.1.2.1 初始化

当指针变量被初始化为一个地址时，如

```
int * iPtr = &i;
```

该地址必须是其类型与指针指向的类型相同的对象的地址。指针据说已绑定到该类型。例如，声明

```
double doubleVar;
int * iPtr = &doubleVar; // ERROR
```

将导致编译器错误，因为整数指针只能存储整数对象的地址。

一个重要的例外是 0 可以赋给任何指针变量。由此得到的值称为该类型的空指针值，而 0 通常称为空地址。因此，声明

```
char * cPtr = 0;
int * iPtr = 0;
double * dPtr = 0;
```

都是使用空地址的有效初始化。
空地址还可以在布尔表达式中用来指示指针是否指向任何东西：

```
if (dPtr == 0)
    // dPtr 当前未指向任何东西
else
    // dPtr 指向一个内存位置
```

正如我们将看到的，当指针用于存储执行期间分配的内存块的地址时，此类比较尤其重要。

### 15.1.2.2 间接寻址和解引用

指针变量不仅存储地址，还提供对存储在这些地址处的值的访问。形如

```
*pointerVariable
```

的表达式可用于访问存储在 pointerVariable 中的地址处的值。它可以被认为是在 pointerVariable 中存储的引用（地址）处转到并访问存储在该地址处的值。为了说明，在示例 15.1 的示例运行中，表达式

```
iPtr
```

的值为 0xbffff970，而表达式

```
*iPtr
```

的值为 11，因为 11 是存储在地址 0xbffff970 处的值：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_613_0.png)

出于同样的原因，表达式 *jPtr 和 *kPtr 的值分别为 22 和 33。因此，变量 i 的值可通过表达式 *iPtr 访问，j 的值可通过 *jPtr 访问，k 的值可通过 *kPtr 访问。一般来说，变量 v 的值可以通过将 * 运算符应用于其值为 v 的地址的指针变量 vPtr 来间接访问。因此，* 运算符称为间接运算符。因为引用是地址的另一个术语，并且将间接运算符应用于指针变量会访问存储在该指针变量中的地址处的值，所以将间接运算符应用于指针变量称为解引用该指针变量。

我们已经在前几章中使用了这种间接访问技术。例如，在第 12.6 节中对 vector<T> 对象的研究中，我们看到解引用迭代器

可提供对 vector<T> 对象中迭代器所指向位置处存储的值的访问。此外，虽然我们在上一章研究类时没有讨论它，但每个类对象都包含一个指针变量 this，其值为包含它的对象的地址，解引用 this 提供了一种（间接）访问该对象的方法。我们可以如下想象它：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_614_0.png)

间接运算符可以多次应用以产生额外的间接级别。例如，声明

```
typedef int * IntPointer;    // 或不使用 typedef：
IntPointer * ptr;            //     int ** ptr;
```

声明 ptr 为指向包含指向可存储 int 的另一内存位置的指针的内存位置的指针。

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_614_1.png)

间接运算符可在赋值语句的两侧使用。如果将语句

```
i = *jPtr;
```

添加到示例 15.1 中的程序中，i 的值将从 11 变为 22，因为解引用 jPtr 会产生存储在地址 0xbffff96c 处的 22 值，并且该值将被赋给 i。语句

```
*iPtr = j;
```

会产生相同的结果。*iPtr 指的是地址为 0xbffff970 的内存位置，赋值运算符将 j 的值（22）复制到此内存位置。因为此地址与变量 i 关联，所以效果是改变 i 的值。

如前所述，示例 15.1 中程序的目的是介绍指针和间接寻址的基础知识。指针并不经常用于存储地址


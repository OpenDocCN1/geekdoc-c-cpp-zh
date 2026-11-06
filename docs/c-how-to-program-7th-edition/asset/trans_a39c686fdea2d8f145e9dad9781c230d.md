
函数的可重用性——只有处理特定大小的一维 int 数组、且该大小被“硬编码”到函数中的程序才能使用该函数。

**软件工程观察 8.4**

*将数组传递给函数时，还要传递数组的大小（而不是将数组大小的知识内建到函数中）——这会使函数更具可重用性。*

## 8.7 sizeof 运算符

一元运算符 `sizeof` 在程序编译期间确定数组（或任何其他数据类型、变量或常量）的大小（以字节为单位）。当应用于数组名时，如图 8.14（第 13 行）所示，`sizeof` 运算符返回数组中的总字节数，作为 `size_t` 类型的值（一种至少与 `unsigned int` 一样大的无符号整数类型）。例如，这与 `vector<int>` 的大小不同，后者是向量中整数元素的个数。我们用来编译此程序的计算机将 `double` 类型的变量存储在 8 字节内存中，而 `array` 被声明为具有 20 个元素（第 11 行），因此 `array` 在内存中使用 160 字节。当应用于接收数组作为实参的函数中的指针形参（第 22 行）时，`sizeof` 运算符返回指针的字节大小（在我们使用的系统上为 4）——而不是数组的大小。

**常见编程错误 8.7**

*在函数中使用 `sizeof` 运算符求数组形参的字节大小，得到的是指针的字节大小，而不是数组的大小。*

```cpp
1  // Fig. 8.14: fig08_14.cpp
2  // sizeof operator when used on an array name
3  // returns the number of bytes in the array.
4  #include <iostream>
5  using namespace std;
6  
7  size_t getSize( double * ); // prototype
8  
9  int main()
10 {
11     double array[ 20 ]; // 20 doubles; occupies 160 bytes on our system
12 
13     cout << "The number of bytes in the array is " << sizeof( array );
14 
15     cout << "\nThe number of bytes returned by getSize is "
16        << getSize( array ) << endl;
17 } // end main
18 
19 // return size of ptr
20 size_t getSize( double *ptr )
21 {
22     return sizeof( ptr );
23 } // end function getSize
```

**图 8.14** | 当 `sizeof` 运算符作用于数组名时，返回数组中的字节数。（第 1 部分，共 2 部分）

```cpp
23   << "sizeof(int) = " << sizeof( int )
24   << "\nsizeof 1 = " << sizeof 1
25   << "\nsizeof(long) = " << sizeof( long )
26   << "\nsizeof f = " << sizeof f
27   << "\nsizeof(float) = " << sizeof( float )
28   << "\nsizeof d = " << sizeof d
29   << "\nsizeof(double) = " << sizeof( double )
30   << "\nsizeof ld = " << sizeof ld
31   << "\nsizeof(long double) = " << sizeof( long double )
32   << "\nsizeof array = " << sizeof array
33   << "\nsizeof ptr = " << sizeof ptr << endl;
34 } // end main
```

```text
sizeof c = 1        sizeof(char) = 1
sizeof s = 2        sizeof(short) = 2
sizeof i = 4        sizeof(int) = 4
sizeof l = 4        sizeof(long) = 4
sizeof f = 4        sizeof(float) = 4
sizeof d = 8        sizeof(double) = 8
sizeof ld = 8       sizeof(long double) = 8
sizeof array = 80
sizeof ptr = 4
```

**图 8.15** | 使用 sizeof 运算符确定标准数据类型的大小。（第 2 部分，共 2 部分。）

> **可移植性提示 8.2**
>
> *用于存储特定数据类型的字节数可能因系统而异。编写依赖于数据类型大小且将在多个计算机系统上运行的程序时，请使用 sizeof 确定用于存储这些数据类型的字节数。*

运算符 sizeof 可应用于任何表达式或类型名。当 sizeof 应用于变量名（不是数组名）或其他表达式时，返回用于存储该表达式值的特定类型所占用的字节数。只有当类型名（例如 int）作为其操作数提供时，才需要使用与 sizeof 一起使用的圆括号。当 sizeof 的操作数是表达式时，不需要使用与 sizeof 一起使用的圆括号。请记住，sizeof 是运算符，而不是函数，并且它在编译时而非执行时起作用。

> **常见编程错误 8.8**
>
> *当操作数是类型名时，在 sizeof 运算中省略圆括号是编译错误。*

> **性能提示 8.2**
>
> *由于 sizeof 是编译时一元运算符，而不是执行时运算符，因此使用 sizeof 不会对执行性能产生负面影响。*

> **错误预防提示 8.3**
>
> *为避免因省略 sizeof 运算符操作数周围的圆括号而导致的错误，请在每个 sizeof 操作数周围都加上圆括号。*

## 8.8 指针表达式和指针算术

指针是算术表达式、赋值表达式和比较表达式中的有效操作数。然而，这些表达式中通常使用的并非所有运算符都对指针变量有效。本节介绍可以将指针作为操作数的运算符，以及这些运算符如何与指针一起使用。

C++ 支持指针算术——可以对指针执行某些算术运算。指针可以递增（++）或递减（--），可以将整数加到指针上（+ 或 +=），可以从指针中减去整数（- 或 -=），也可以从同一类型的另一个指针中减去一个指针。

假设已声明数组 `int v[5]`，并且其第一个元素位于内存位置 3000。假设指针 `vPtr` 已初始化为指向 `v[0]`（即 `vPtr` 的值为 3000）。图 8.16 展示了在整数为四字节的机器上的这种情况。变量 `vPtr` 可以用以下任一语句初始化为指向数组 `v`（因为数组名等价于其第一个元素的地址）：

```cpp
int *vPtr = v;
int *vPtr = &v[ 0 ];
```

> **可移植性提示 8.3**
>
> 如今大多数计算机使用两字节或四字节整数。一些较新的机器使用八字节整数。由于指针算术的结果取决于指针所指向对象的大小，因此指针算术是机器相关的。

![](img/023f159fdd47d944d48e08843cea732d_401_0.png)

**图 8.16** — 数组 `v` 和指向 `v` 的指针变量 `int *vPtr`。

在常规算术中，加法 3000 + 2 得到的值是 3002。指针算术通常并非如此。当整数加到指针上或从指针中减去时，指针并不是简单地增加或减少该整数，而是增加或减少该整数乘以指针所指向对象的大小。字节数取决于对象的数据类型。例如，语句

```cpp
vPtr += 2;
```

将得到 3008（3000 + 2 * 4），假设 `int` 存储在 4 字节内存中。在数组 `v` 中，`vPtr` 现在将指向 `v[2]`（图 8.17）。如果整数存储在 2 字节内存中，那么前面的计算将得到内存位置 3004（3000 + 2 * 2）。如果数组元素是不同数据类型，前面的语句将使指针增加存储该数据类型对象所需字节数的两倍。对字符数组执行指针算术时，结果将与常规算术一致，因为每个字符长一字节。

![](img/023f159fdd47d944d48e08843cea732d_402_0.png)

**图 8.17** 指针算术后的指针 vPtr。

如果 vPtr 已递增到 3016，即指向 v[4]，那么语句

```cpp
vPtr -= 4;
```

会将 vPtr 重新设置为 3000——数组的开头。如果指针要递增或递减 1，可以使用递增（++）和递减（--）运算符。以下每条语句

```cpp
++vPtr;
vPtr++;
```

都会使指针递增以指向数组的下一个元素。以下每条语句

```cpp
--vPtr;
vPtr--;
```

都会使指针递减以指向数组的前一个元素。

指向同一数组的指针变量可以相互相减。例如，如果 vPtr 包含地址 3000，v2Ptr 包含地址 3008，那么语句

```cpp
x = v2Ptr - vPtr;
```

会将从 vPtr 到 v2Ptr 之间的数组元素个数赋给 x——在本例中为 2。除非对指向数组的指针执行指针算术，否则指针算术没有意义。除非两个相同类型的变量是数组中的相邻元素，否则我们不能假定它们在内存中连续存储。

> **常见编程错误 8.9**  
> *对不指向数组的指针使用指针算术是逻辑错误。*

> **常见编程错误 8.10**  
> *对不指向同一数组元素的两个指针进行相减或比较是逻辑错误。*

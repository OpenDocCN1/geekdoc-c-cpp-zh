

## 第4章

如果你尝试用如下语句修改字符数组：

```
*pstr[0] = "Stan Laurel";
```

程序将无法编译。

如果你尝试用如下语句将数组中的一个元素重新设置为指向一个字符：

```
*pstr[0] = 'X';
```

程序可以编译，但在执行该语句时会崩溃。

你肯定不希望出现程序在运行时崩溃这类意外行为，而你可以避免这种情况。更好的声明方式如下：

```
const char* pstr[] = { "Robert Redford",  // Array of pointers
    "Hopalong Cassidy",  // to constants
    "Lassie",
    "Slim Pickens",
    "Boris Karloff",
    "Oliver Hardy"
};
```

在这种情况下，关于指针数组元素所指向字符串的常量性没有歧义。如果你现在试图修改这些字符串，编译器会在编译时将其标记为错误。

然而，你仍然可以合法地编写如下语句：

```
pstr[0] = pstr[1];
```

那些本应得到雷德福先生的幸运儿将改领卡西迪先生，因为两个指针现在指向同一个名字。请注意，这并没有改变指针数组元素所指向对象的值——而是改变了存储在 pstr[0] 中的指针值。因此，你也应该禁止这种修改，因为有些人可能认为老好人霍皮并没有罗伯特那样的性感魅力。你可以通过如下语句实现这一点：

```
// Array of constant pointers to constants
const char* const pstr[] = { "Robert Redford",
    "Hopalong Cassidy",
    "Lassie",
    "Slim Pickens",
    "Boris Karloff",
    "Oliver Hardy"
};
```

总而言之，你可以区分与 const、指针以及它们所指向对象相关的三种情况：

- 指向常量对象的指针
- 指向对象的常量指针
- 指向常量对象的常量指针

在第一种情况下，所指向的对象不能被修改，但我们可以将指针设置为指向其他对象：

```
const char* pstring = "Some text";
```

在第二种情况下，指针中存储的地址不能被改变，但所指向的对象可以被修改：

```
char* const pstring = "Some text";
```

最后，在第三种情况下，指针和所指向的对象都被定义为常量，因此两者都不能被修改：

```
const char* const pstring = "Some text";
```

*当然，所有这些都适用于指向任意类型的指针。这里使用指向 char 类型的指针纯粹是为了说明问题。*

### 指针与数组

在某些情况下，数组名的行为可以像指针一样。在大多数情况下，如果你单独使用一维数组的名称，它会自动转换为指向数组首元素的指针。请注意，当数组名用作 sizeof 运算符的操作数时，情况并非如此。

如果我们有以下声明：

```
double* pdata;
double data[5];
```

你可以编写如下赋值语句：

```
pdata = data;      // Initialize pointer with the array address
```

这是将数组 data 的第一个元素的地址赋给指针 pdata。单独使用数组名表示数组的地址。如果你将数组名 data 与索引值一起使用，则表示该索引值对应元素的内容。因此，如果你想将该元素的地址存储在指针中，必须使用取地址运算符：

```
pdata = &data[1];
```

这里，指针 pdata 包含数组第二个元素的地址。

### 指针算术

你可以对指针执行算术运算。在算术运算方面，你仅限于加法和减法，但你也可以比较指针值以产生逻辑结果。对指针进行算术运算隐式地假定指针指向一个数组，并且算术运算作用于指针中包含的地址。例如，对于指针 pdata，我们可以使用如下语句将数组 data 的第三个元素的地址赋给一个指针：

```
pdata = &data[2];
```

在这种情况下，表达式 pdata+1 将指向 data[3] 的地址，即 data 数组的第四个元素，因此你可以通过编写如下语句使指针指向该元素：

```
pdata += 1;      // Increment pdata to the next element
```

该语句将 pdata 中包含的地址增加数组 data 中一个元素所占的字节数。一般情况下，表达式 pdata+n（其中 n 可以是任何结果为整数的表达式）将 n*sizeof(double) 加到指针 pdata 所含的地址上，因为 pdata 被声明为指向 double 的指针类型。如图 4-8 所示。

double data[5];

![](img/2359b0c604600c58fba3539c738a356e_227_0.png)

图 4-8

换句话说，指针的递增或递减是根据所指向对象的类型进行的。将指向 long 的指针加一，会将其内容改为下一个 long 地址，因此地址增加四。类似地，将指向 short 的指针加一，地址增加二。递增指针更常见的写法是使用递增运算符。例如：

```
pdata++;      // Increment pdata to the next element
```

这等同于 += 形式（而且比 += 形式更常用）。不过，我前面使用 += 形式是为了说明：虽然增量值实际指定为 1，但效果通常是大于 1 的增量，除非是指向 char 类型的指针。

> 对指针进行算术运算所得的地址，其取值范围可以是从数组首元素的地址到超出最后一个元素一个位置的地址。超出这些限制，指针的行为是未定义的。

当然，你可以解引用已经执行过算术运算的指针（否则，这样做就没有什么意义了）。例如，假设 pdata 仍然指向 data[2]，如下语句：

```
*(pdata + 1) = *(pdata + 2);
```

等同于：

```
data[3] = data[4];
```

当你希望在递增指针所含地址后对其进行解引用时，括号是必需的，因为间接寻址运算符（*）的优先级高于算术运算符 + 或 -。如果你写成表达式 *pdata + 1（而不是 *(pdata + 1)），这会将 pdata 所含地址处的值加 1，相当于 data[2] + 1。由于这不是左值，在之前的赋值语句中使用它会导致编译器生成错误消息。

你可以将数组名当作指针来寻址数组的元素。如果你有和之前相同的一维数组，声明如下：

```
long data[5];
```

使用指针表示法，你可以将元素 data[3] 表示为 *(data + 3)。这种表示法可以通用，因此对于元素 data[0]、data[1]、data[2]，你可以分别写成 *data、*(data + 1)、*(data+2) 等。

### 数组名作为指针

你可以用一个计算质数的程序来练习数组寻址的这一方面（质数只能被自身和 1 整除）。

```
// Ex4_09.cpp
// Calculating primes
#include <iostream>
#include <cmath>
using std::cout;
using std::endl;
using std::setw;

int main()
{
  const int MAX = 100; // Number of primes required
  long primes[MAX] = { 2,3,5 }; // First three primes defined
  long trial = 5; // Candidate prime
  int count = 3; // Count of primes found
  int found = 0; // Indicates when a prime is found

  do
  {
    trial += 2; // Next value for checking
    found = 0; // Set found indicator
    for(int i = 0; i < count; i++) // Try division by existing primes
    {
      found = (trial % *(primes + i)) == 0; // True for exact division
      if(found) // If division is exact
        break; // it's not a prime
    }
    if (found == 0) // We got one...
  }


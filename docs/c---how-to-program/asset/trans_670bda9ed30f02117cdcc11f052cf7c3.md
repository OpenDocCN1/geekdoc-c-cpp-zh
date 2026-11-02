
数组会自动按引用传递；单个数组元素是标量，通常按值传递。因此，bubbleSort 在 swap 调用（第 46 行）中使用地址运算符（&）对每个数组元素进行操作，以实现按引用传递，如下所示：

```c
swap(&array[j], &array[j + 1]);
```

函数 swap 在 element1Ptr（第 54 行）中接收 &array[j]。即使由于信息隐藏，swap 不被允许知道名称 array[j]，swap 仍可使用 *element1Ptr 作为 array[j] 的同义词——当 swap 访问 *element1Ptr 时，它实际上是在引用 bubbleSort 中的 array[j]。类似地，当 swap 访问 *element2Ptr 时，它实际上是在引用 bubbleSort 中的 array[j + 1]。即使 swap 不被允许写

```c
int hold = array[j];
array[j] = array[j + 1];
array[j + 1] = hold;
```

精确相同的效果由第 56 行至第 58 行实现：

```c
int hold = *element1Ptr;
*element1Ptr = *element2Ptr;
*element2Ptr = hold;
```

### 函数 bubbleSort 的数组参数

函数 bubbleSort 的几个特性应予注意。函数头（第 34 行）将 array 声明为 int * const array 而不是 int array[]，以表明 bubbleSort 接收一个一维数组作为参数（再次，这两种记法是可以互换的）。参数 size 被声明为 const 以强制执行最小权限原则。尽管参数 size 在 main 中接收一个值的副本，并且修改副本不能改变 main 中的值，但 bubbleSort 无需更改 size 即可完成其任务。数组的大小在函数 bubbleSort 执行期间保持固定。因此，size 被声明为 const 以确保它不会被修改。

### 函数 bubbleSort 体内的函数 swap 的原型

函数 swap 的原型（第 36 行）包含在函数 bubbleSort 的体内，因为 bubbleSort 是唯一调用 swap 的函数。将原型放在 bubbleSort 中将 swap 的正确调用限制为从 bubbleSort（或源代码中出现在 swap 之后的任何函数）发出的调用。在 swap 之前定义的尝试调用 swap 的其他函数无法访问正确的函数原型，因此编译器会自动生成一个原型。这通常会导致一个与函数头不匹配的原型（并生成编译警告或错误），因为编译器假定返回类型和参数类型为 int。

> **软件工程观察 7.2**
>
> 将函数原型放在其他函数的定义中，通过将正确的函数调用限制在原型出现的函数中来强制执行最小权限原则。

### 函数 bubbleSort 的 size 参数

函数 bubbleSort 将数组的大小作为参数接收（第 34 行）。该函数必须知道数组的大小才能对数组进行排序。当数组传递给函数时，函数的接收的是数组第一个元素的内存地址。地址，当然，*不* 传达数组中元素的数量。因此，你必须将数组大小传递给函数。另一种常见做法是传递指向数组开头的指针和指向数组末尾之后位置的指针——正如你在第 7.8 节中将要学习的那样，这两个指针之差是数组的长度，并且 resulting 代码更简单。

在程序中，数组的大小被显式传递给函数 bubbleSort。这种方法有两个主要好处——*软件可重用性* 和 *适当的软件工程*。通过定义函数以将数组大小作为参数接收，我们使该函数能够被任何对任意大小的一维整数数组进行排序的程序使用。

> **软件工程观察 7.3**
>
> *当将数组传递给函数时，也传递数组的大小。这有助于使函数在许多程序中可重用。*

我们本可以将数组的大小存储在对整个程序可访问的全局变量中。这会更高效，因为传递给函数的不是 size 的副本。然而，其他需要整数数组排序功能 的程序可能没有相同的全局变量，因此该函数无法在这些程序中使用。

> **软件工程观察 7.4**
>
> *全局变量通常违反最小权限原则，并可能导致糟糕的软件工程。全局变量应仅用于表示真正共享的资源，例如一天中的时间。*

数组的大小本可以直接编程到函数中。这将使用该函数的限制为特定大小的数组，并显著降低其可重用性。只有处理函数中编码的特定大小的一维整数数组的程序才能使用该函数。

## 7.7 `sizeof` 运算符

C 提供了特殊的 unary 运算符 `sizeof` 来确定数组（或任何其他数据类型）的字节大小。此运算符在编译时应用，除非其操作数是变长数组（第 6.12 节）。当应用于数组名称时，如图 7.16（第 15 行）所示，`sizeof` 运算符以类型 `size_t`⁴ 返回数组的总字节数。在这台计算机上，类型为 `float` 的变量占用 4 字节内存，而 array 被定义为有 20 个元素。因此，array 中共有 80 字节。

> **性能提示 7.2**
>
> *`sizeof` 是一个编译时运算符，因此不会产生任何执行时开销。*

```c
// Fig. 7.16: fig07_16.c
// Applying sizeof to an array name returns
// the number of bytes in the array.
#include <stdio.h>
#define SIZE 20

size_t getSize(float *ptr); // prototype

int main(void)
{
    float array[SIZE]; // create array

    printf("The number of bytes in the array is %u\n"
           "The number of bytes returned by getSize is %u\n",
           sizeof(array), getSize(array));
}

// return size of ptr
size_t getSize(float *ptr)
{
    return sizeof(ptr);
}
```

```text
The number of bytes in the array is 80
The number of bytes returned by getSize is 4
```

**图 7.16** | 将 sizeof 应用于数组名称会返回数组的字节数。

数组中的元素数量也可以用 sizeof 确定。例如，考虑以下数组定义：

```c
double real[22];
```

类型为 double 的变量通常占用 8 字节内存。因此，数组 real 包含总共 176 字节。要确定数组中的元素数量，可以使用以下表达式：

```c
sizeof(real) / sizeof(real[0])
```

该表达式确定数组 real 中的字节数，并将该值除以在内存中存储数组 real 的第一个元素（一个 double 值）所使用的字节数。

即使函数 getSize 作为参数接收一个包含 20 个元素的数组，函数的参数 ptr 只是指向数组第一个元素的指针。当你对参数使用 sizeof 时，它返回指针的大小，而不是它所指向项的大小。在我们的 Windows 和 Linux 测试系统上，指针的大小为 4 字节，因此 getSize 返回 4；在我们的 Mac 上，指针的大小为 8 字节，因此 getSize 返回 8。此外，使用 sizeof 确定数组元素数量的上述计算仅在使用实际数组时有效，而在使用指向数组的指针时无效。

### *确定标准类型、数组和指针的大小*

图 7.17 计算存储每种标准数据类型的字节数。此程序的结果是实现相关的，并且在不同平台上以及有时在同一平台上的不同编译器之间有所不同。输出显示了我们使用 Visual C++ 编译器的 Windows 系统的结果。在我们使用 GNU gcc 编译器的 Linux 系统上，long double 的大小为 12 字节。在我们使用 Xcode 的 LLVM 编译器的 Mac 系统上，long 的大小为 8 字节，long double 的大小为 16 字节。

```c
// Fig. 7.17: fig07_17.c
// Using operator sizeof to determine standard data type sizes.
#include <stdio.h>

int main(void)
{
    char c;
    short s;
    int i;
    long l;
    long long ll;
    float f;
    double d;
    long double ld;
    int array[20]; // create array of 20 int elements
    int *ptr = array; // create pointer to array

    printf("\n    sizeof c = %u\t sizeof(char) = %u"
    "\n    sizeof s = %u\t sizeof(short) = %u"
    "\n    sizeof i = %u\t sizeof(int) = %u"
    "\n    sizeof l = %u\t sizeof(long) = %u"
    "\n    sizeof ll = %u\t sizeof(long long) = %u"
    "\n    sizeof f = %u\t sizeof(float) = %u"
    "\n    sizeof d = %u\t sizeof(double) = %u"
    "\n    sizeof ld = %u\t sizeof(long double) = %u"
    "\n    sizeof array = %u"
    "\n    sizeof ptr = %u",
    sizeof c, sizeof(char), sizeof s, sizeof(short), sizeof i,
    sizeof(int), sizeof l, sizeof(long), sizeof ll,
    sizeof(long long), sizeof f, sizeof(float), sizeof d,
    sizeof(double), sizeof ld, sizeof(long double),
    sizeof array, sizeof ptr);
}
```

|  |  |
|---|---|
| sizeof c = 1 | sizeof(char) = 1 |
| sizeof s = 2 | sizeof(short) = 2 |
| sizeof i = 4 | sizeof(int) = 4 |
| sizeof l = 4 | sizeof(long) = 4 |
| sizeof ll = 8 | sizeof(long long) = 8 |
| sizeof f = 4 | sizeof(float) = 4 |
| sizeof d = 8 | sizeof(double) = 8 |
| sizeof ld = 8 | sizeof(long double) = 8 |
| sizeof array = 80 |  |
| sizeof ptr = 4 |  |

**图 7.17** | 使用 sizeof 运算符确定标准数据类型大小。


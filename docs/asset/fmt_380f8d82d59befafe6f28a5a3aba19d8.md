
参数名 `nm1Addr` 和 `nm2Addr` 的选择与所有参数一样，由程序员决定。然而，声明 `double *nm1Addr` 表明参数 `nm1Addr` 用于存储双精度数值的地址。同样，声明 `double *nm2Addr` 指定 `nm2Addr` 也存储双精度数值的地址。

在编写 `swap()` 来交换 `firstnum` 和 `secnum` 中的值之前，首先检查 `nm1Addr` 和 `nm2Addr` 中地址使用的值是否正确。程序 10.performance 演示了这一点

# 指针

## 程序 10.10

```
#include <iostream>
using std;

void swap(double *, double *); //函数原型

int main() {
    double firstnum = 20.5, secnum = 6.25;

    swap(&firstnum, &secnum);    // 调用 swap

    return 0;
}

// 此函数说明传递指针参数
void swap(double *nm1Addr, double *nm2Addr) {
    cout << "The number whose address is in nm1Addr is " << *nm1Addr << endl;
    cout << "The number whose address is in nm2Addr is " << *nm2Addr << endl;

    return;
}
```

当程序 10.10 运行时，显示以下输出：

The number whose address is in nm1Addr is 20.5

The number whose address is in nm2Addr is 6.25

在检查此程序时，请注意两点。首先，`swap()` 的函数原型

`swap(double *, double *)`

声明 `swap()` 直接返回值，且参数是两个指向双精度数值的指针。当调用函数时，它要求传递两个地址，且每个地址都是双精度数值的地址。

其次，`swap()` 中使用了间接操作符来访问存储在 `firstnum` 和 `secnum` 中的值。`swap` 函数并不知道这些变量名，但它拥有存储在 `nm1Addr` 中的 `firstnum` 地址和存储在 `nm2Addr` 中的 `secnum` 地址。第一个语句 `*nm1Addr` 意味着“nm1Addr 处的值”，这当然是第一个变量。同样，第二个语句 `*nm2Addr` 获取存储在“nm2Addr 处的值”。指针已成功用于允许 `swap()` 访问 `main()` 中的变量。图 10.18 显示了在参数中存储地址。

参数名：nm1Addr    `swap(&firstnum, &secnum)`

![](img/d5a225ca53b347501e86d72212077531_622_0.png)

图 10.18 在参数中存储地址

在验证 `swap()` 可以访问 `main()` 的局部变量 `firstnum` 和 `secnum` 后，你可以扩展 `swap()` 来交换这些变量的值。通过第 6.3 节描述的三步算法，可以在 `swap()` 交换 `main()` 变量 `firstnum` 和 `secnum` 的值：

1. 将 `firstnum` 的值存储在临时位置。
2. 将 `secnum` 的值存储在 `firstnum` 中。
3. 将临时值存储在 `secnum` 中。

在 `swap()` 中使用指针的形式如下：

1. 使用语句 `temp = *nm1Addr;` 将 `nm1Addr` 指向的临时位置的值（见图 10.19）。

![](img/d5a225ca53b347501e86d72212077531_622_1.png)

图 10.19 间接存储 firstnum 的值

2. 使用语句 `nm1Addr = *nm2Addr;` 将地址为 `nm2Addr` 的变量的值存储在变量 `nm1Addr` 中（见图 10.20）。

![](img/d5a225ca53b347501e86d72212077531_623_0.png)

图 10.20 间接改变 firstnum 的值

3. 使用语句 `*nm2Addr = temp;` 将临时位置的值移动到变量 `nm2Addr` 中（见图 10.21）。

![](img/d5a225ca53b347501e86d72212077531_623_1.png)

图 10.21 间接改变 secnum 的值

程序 10.11 根据此描述编写了 `swap()` 的最终形式。

```
#include <iostream>
using namespace std;

void swap(double *, double *); // 函数原型

int main() {
    double firstnum = 20.5, secnum = 6.25;

    cout << "The value stored in firstnum: " << firstnum << endl;
    cout << "The value stored in secnum: " << secnum << endl;

    swap(&firstnum, &secnum); // 调用 swap

    cout << "The value stored in firstnum is now: " << firstnum << endl;
    cout << "The value stored in secnum is now: " << secnum << endl;

    return 0;
}

// 此函数交换参数中的值
void swap(double *nm1Addr, double *nm2Addr) {
    double temp;

    temp = *nm1Addr; // 保存 firstnum 的值
    *nm1Addr = *nm2Addr; // 将 secnum 的值移入 firstnum
    *nm2Addr = temp; // 改变 secnum 的值
}
```

程序 10.11 的示例运行产生了输出：

The value stored in firstnum is: 20.5

The value stored in secnum is: 6.25

The value stored in firstnum is now: 6.25

The value stored in secnum is now: 20.5

正如输出所示，`main()` 变量中存储的值在 `swap()` 中被修改了，这是通过指针实现的。确保你理解，可以将此版本的 `swap()` 与程序 6.10 中使用引用的版本进行比较。使用指针而不是引用的优点是函数指定了正在使用的地址，并提醒函数可能会修改调用者的变量。使用引用的优点是语法简单得多。通常，对于像 `swap()` 这样的函数，语法占优，并使用引用。但在向函数传递数组时（这是下一个主题），编译器会完整传递地址，这要求使用指针来存储地址。

## 传递数组

当数组传递给函数时，它的地址是实际传递的唯一项。“地址”意味着存储数组的第一个位置的地址；如图 10.22 所示。因为数组的第一个位置对应于数组的元素 0，所以“数组的地址”就是元素 0 的地址。

![](img/d5a225ca53b347501e86d72212077531_624_0.png)

图 10.22 数组的地址是为数组保留的第一个位置的地址

关于向函数传递数组的具体示例，请查看程序 10.12。在此程序中，`nums` 数组使用常规符号传递给 `findMax()` 函数。

![](img/d5a225ca53b347501e86d72212077531_625_1.png)

## 程序 10.12

（注：代码块已在原文中提供，此处不再重复）

## 第 10 章

`findMax` 函数头中名为 `vals` 的参数实际上接收的是 `nums` 数组的地址。因此，`vals` 实际上是一个指针，因为指针是存储地址的变量（或参数）。由于传递给 `findMax()` 的地址是一个整数地址，以下 `findMax()` 函数头是合适的：

```
int findMax(int *vals, int nums) // vals 被声明为
// 指整数的指针
```

函数头中的声明 `int *vals` 表明 `vals` 用于存储一个整数的地址。存储的地址当然是该数组的位置。以下是 `findMax()` 函数的重写版本，它使用了新的指针 `vals`，但保留了使用下标来引用数组元素的方法：

```
int findMax(int *vals, int nums) // 寻找最大值
{
  int i, max = vals[0];
  for (i = 1; i < nums; i++)
    if (max < vals[i])
      max = vals[i];
  return max;
}
```

无论 `vals` 在函数头中如何声明，或者在函数体中如何使用，这对于名称 `nums` 都不成立。因为 `nums` 是原始创建的数组的名称，它是一个指针变量。`vals` 中的地址是可以修改的。正如第 10.2 节所述，这意味着 `nums` 中的地址不能更改，且无法获取 `nums` 的地址。然而，对指针变量没有没有任何限制。你在第 10.3 节中学学会的所有指针算术都可以应用于 `vals`。

接下来，你将学习如何编写两个版本的 `findMax()`，使用指针而不是下标。在第一个版本中，你可能会用指针表示法代替下标符号。在第二个版本中，你使用指针算术来更改指针中的地址。如前所述，可以使用 `array[i]` 访问数组元素，并且始终可以替换为指针表示法 `*(arrayName + i)`。

在 `findMax()` 的第一次修改中，你可以通过将所有对 `vals[i]` 的引用替换为表达式 `*(vals + i)` 来使用这种对应关系：

```
int findMax(int *vals, int nums) // 寻找最大值
{
  int i, max = *vals;
  for (i = 1; i < nums; i++)
    if (max < *(vals + i))
      max = *(vals + i);
  return max;
}
```

## 指针

`findMax()` 的第二次修改利用了更改存储在 `vals` 中的地址的能力。在通过 `vals` 中的地址获取每个数组元素后，该地址在 `for` 语句的修改列表中加了 1。之前用于将 `max` 设置为 `vals[0]` 值的表达式 `max * vals` 被表达式 `max = *vals++` 替换，这会调整 `vals` 的地址指向第二个数组元素。元素赋值在递增之前将数组元素 `vals` 赋值给 `max`。后置递增运算符 `++` 在地址被用于获取第一个数组元素之后，不会改变 `vals` 中的地址。

```
int findMax(int *vals, int numels) // 寻找最大值
{
    int i; // 获取第一个元素并对其进行递增
    for (i = 1; i < numels; i++, vals++)
    {
        if (max < *vals)
            max = *vals;
    }
    return max;
}
```

复习这个版本的 `findMax()`。最初，最大值被设置为“指针所指向的内容”。因为 `vals` 初始包含分配给 `findMax()` 的第一个数组元素的地址，所以这个元素元素被存储在 `max` 中。`vals` 中的地址加了 1。加到 `vals` 的值会自动根据存储整数的字节数进行缩放。因此，递增后，`vals` 中存储的地址是下一个数组元素的地址，如图 10.23 所示。这个下一个元素的值与 `max` 进行比较，并在 `for` 语句的修改列表中递增地址。这个过程一直持续直到所有数组元素都检查完毕。

![](img/d5a225ca53b347501e86d72212077531_627_0.png)

图 10.23 指向不同的元素

你选择哪个 `findMax()` 版本取决于个人风格。通常，初级程序员觉得使用下标比指针更自在。此外，如果程序使用数组作为应用程序的自然结构，并且使用下标访问数组能更清晰地实现程序的意图。然而，随着你学习数据结构，下标将没有等价替代物。

从这次讨论中，你可以学到一个巧妙的小技巧：由于向函数传递数组涉及涉及传递一个数组，所以你可以传递任何有效地址。例如，调用 `findMax(&nums[2],3)` 将 `nums[2]` 的地址传递给 `findMax()`。在 `findMax()` 中，指针存储了该地址，函数开始搜索与该地址对应的最大元素。因此，从 `findMax()` 的角度来看，它接收了一个地址并据此进行。

## 高级指针表示法^9

你也可以通过指针表示法访问多维数组，尽管随着数组维度的增加，这种表示法会变得更加晦涩。指针表示法对于二维字符数组特别有用，本节讨论了二维数值数组的指针表示法。例如，考虑这个声明：

```
int nums[2][3] = {16, 18, 20,
{0, 25, 27} };
```

此声明创建了一个元素数组和一组名为 `nums`、`nums[0]` 和 `nums[1]` 的指针。图 10.24 显示了这些指针常量与元素之间的关系。

| nums | nums[0] | nums[1] | | | |

|---|---|---|---|---|---|

| nums[0] 的地址 | nums[0][0] | nums[1][0] | 16 | 18 | 20 |

| | | nums[1][0] 的地址 | 25 | 26 | 27 |

| | | | nums[1][0] | nums[1][1] | nums[1][2] |

图 10.24 nums 数组及其指针常量的存储

关联数组的指针常量允许你访问访问元素。一种方法是将二维数组视为行的数组，每行都是一个包含三个元素的数组。从这个观点来看，第一行第一个元素的地址是 `nums[0]`，因此 `nums` 指向的变量是 `nums[0][0]`。同样，`nums[1]` 就是 `nums[1]`。在阅读时可以省略这些而不影响连续性。

## 指针

当向函数传递二维数组时，同样的概念适用。例如，通过 `calc(nums)` 将二维数组传递给 `calc()` 函数；与所有数组一样，传递的是地址。`calc()` 函数合适的函数头如下：

```
calc(int pt[2])
```

正如你所见，`pt` 的参数声明也可以是：

```
calc(int pt[3])
```

使用指针表示法，这是另一种合适的声明：

```
calc(*pt[3])
```

在此声明中，需要内层括号来创建一个指向三个整数数组的单个指针。每个数组当然等于数组的一行。通过设置指针，可以访问数组中的每个元素。注意，如果没有括号，声明将变为

```
int *pt[3]
```

这创建了一个包含三个指针的数组，每个指针指向一个整数。在对 `cale()` 进行正确的声明（这三个声明中的任何一个都是有效的）后，`wale()` 函数中的所有后续表示法都是等价的：

| 指针表示法 | 下标表示法 | 值 |

| :--- | :--- | :--- |

| (*pt) | pt[0][0] | 16 |

| (*pt + 1) | pt[0][1] | 18 |

| (*pt + 2) | pt[0][2] | 20 |

| (*pt + 1) + 1 | pt[1][1] | 25 |

| (*pt + 1) + 2) | pt[1][2] | 27 |

最后两个使用指针的用法在高级的 C++ 程序中常见。第一个出现在函数返回任何 C++ 标量数据类型时，包括指向这些类型中任意指针。如果函数返回指针，则所指向的数据类型必须在函数的声明中定义。例如，如下声明

```
int cale()
```

声明 `cale()` 返回一个指向整数值的指针，这意味着返回了一个整数变量的地址。同样，如下声明

```
double *taxes()
```

声明 `taxes()` 返回一个指向双精度值的指针，这意味着返回了一个双精度值的地址。

除了声明指向整数、双精度数字以及 C++ 其他数据类型的指针外，你还可以还可以声明指向函数（包含函数地址）的指针。函数指针是可能的，因为函数名像数组名一样，是指针常量。例如，如下声明

```
int (*cale)()
```

声明 `cale` 为一个指向返回整数的函数的指针。这意味着该变量包含一个函数的地址，而位于变量 `cale` 中地址的函数返回一个整数值。例如，函数 `sum()` 返回一个整数，则赋值 `cale = sum;` 是有效的。

![](img/d5a225ca53b347501e86d72212077531_630_0.png)

## 练习题 10.4

- 1. (练习) 使用以下声明创建了 `prices` 数组：

```
double price[500];
```

为名为 `sortArray()` 的函数编写三个不同的函数头，该函数接受名为 `index` 的价格参数且不返回任何值。

## 610 指针

- 2. (练习) 使用以下声明创建了 `keys` 数组：

```
char keys[256];
```

为名为 `findKey()` 的函数编写三个函数头，该函数接受名为 `select` 的数组参数且返回任何值。

- 3. (练习) 使用以下声明创建了 `rates` 数组：

```
double rates[256];
```

为名为 `maximum()` 的函数编写不同的函数头，该函数接受名为 `speed` 的数组参数并返回双精度值。

- 4. (修改) 修改 `findMax()` 函数以定位传递数组的最小值。

仅使用指针编写该函数。

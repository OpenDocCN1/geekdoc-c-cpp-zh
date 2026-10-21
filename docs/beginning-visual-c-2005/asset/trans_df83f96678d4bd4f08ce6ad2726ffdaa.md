

![](img/2359b0c604600c58fba3539c738a356e_280_0.png)

图 5-2

像这样编码语句可以避免原始版本引起的编译器警告信息。使用静态转换并不会消除在一种数据类型转换为另一种数据类型时可能丢失数据的可能性。但由于是你指定的，很清楚这是你所期望的，承认数据丢失可能会发生。

## 向函数传递参数

了解参数如何传递给函数非常重要，因为它会影响你编写函数的方式以及它们最终的运行方式。还有许多需要避免的陷阱，因此我们将对此机制进行仔细研究。

你在调用函数时指定的参数通常应在类型和顺序上与函数定义中出现的参数相对应。正如你在上一个示例中看到的，如果在函数调用中指定的参数的类型与函数定义中参数的类型不对应，（如果可能）它会转换为所需类型，遵守第 2 章中讨论的关于转换操作数的相同规则。如果这证明是不可能的，你会从编译器得到错误信息；然而，即使转换是可能的并且代码可以编译，它也可能导致数据丢失（例如从 long 类型到 short 类型），因此应避免这种情况。

在 C++ 中，一般使用两种机制向函数传递参数。第一种机制适用于你在函数定义中将参数指定为普通变量（不是引用）的情况。这称为按值传递数据到函数的方法，所以我们先来看看这一点。

## 按值传递机制

使用这种机制，你指定的变量或常量作为参数并不会真正传递给函数。相反，会创建参数的副本，这些副本被用作要传输的值。图 5-3 使用我们的 power() 函数的例子以图表形式展示了这一点。

```
int index = 2;
double value = 10.0;
double result = power(value, index);
```

![](img/2359b0c604600c58fba3539c738a356e_281_0.png)

每次你调用函数 power() 时，编译器都会安排将你指定的参数的副本存储在内存中的临时位置。在函数执行期间，对函数参数的所有引用都映射到这些参数的临时副本。

按值传递机制的一个后果是，函数不能直接修改传递进来的参数。你可以通过故意尝试在示例中这样做来证明这一点：

```
// Ex5_02.cpp
// A futile attempt to modify caller arguments
#include <iostream>
using std::cout;
using std::endl;

int incr10(int num);      // Function prototype

int main(void)
{
    int num = 3;

    cout << endl
        << "incr10(num) = " << incr10(num)
        << endl
        << "num = " << num;

    cout << endl;
    return 0;
}

// Function to increment a variable by 10
int incr10(int num)          // Using the same name might help...
{
    num += 10;               // Increment the caller argument - hopefully

    return num;              // Return the incremented value
}
```

当然，这个程序注定要失败。如果你运行它，会得到以下输出：

```
incr10(num) = 13
num = 3
```

## 其工作原理

输出证实了 num 的原始值保持不变。递增操作是在为 num 生成的副本上进行的，并在退出函数时最终被丢弃。

显然，按值传递机制为你提供了很高的保护，防止调用者参数被 rogue 函数破坏，但可以设想你可能确实想安排修改调用者参数。当然，有办法做到这一点。你难道没有预料到指针会变得非常有用吗？

## 作为函数参数的指针

当你使用指针作为参数时，按值传递机制仍然像以前一样运行；然而，指针是另一个变量的地址，如果你复制这个地址，副本仍然指向同一个变量。这就是指定指针作为参数使你的函数能够访问调用者参数的方式。

## 试一试 按指针传递

你可以将上一个示例更改为使用指针来演示效果：

```
// Ex5_03.cpp
// A successful attempt to modify caller arguments
#include <iostream>
using std::cout;
using std::endl;

int incr10(int* num);            // Function prototype

int main(void)
{
    int num = 3;

    int* pnum = &num;            // Pointer to num

    cout << endl
         << "Address passed = " << pnum;

    cout << endl
         << "incr10(pnum) = " << incr10(pnum);

    cout << endl
         << "num = " << num;

    cout << endl;
    return 0;
}

// Function to increment a variable by 10
int incr10(int* num)            // Function with pointer argument
{
    cout << endl
         << "Address received = " << num;

    *num += 10;                  // Increment the caller argument
                               // - confidently
    return *num;                 // Return the incremented value
}
```

此示例的输出为：

```
Address passed = 0012FF6C
Address received = 0012FF6C
incr10(pnum) = 13
num = 13
```

你的计算机产生的地址值可能与上面显示的不同，但两个值彼此应该是相同的。

## 其工作原理

在此示例中，与上一个版本相比，主要的更改与传递指针 pnum 而不是原始变量 num 有关。函数的原型现在将参数类型指定为指向 int 的指针，而 main() 函数已声明并用 num 的地址初始化指针 pnum。函数 main() 和函数 incr10() 分别输出发送的地址和接收的地址，以验证在两个位置确实使用的是相同的地址。

输出显示这次变量 num 已被递增，其值现在与函数返回的值相同。

在重写的 incr10() 函数中，递增传递给函数的值的语句和 return 语句现在都取消引用指针以使用存储的值。

## 向函数传递数组

你也可以向函数传递数组，但在这种情况下，数组不会被复制，即使仍然适用按值传递参数的方法。数组名被转换为指针，并将指向数组开头的指针的副本按值传递给函数。这非常有利，因为复制大型数组非常耗时。正如你可能已经推断出的那样，数组的元素可以在函数内部被更改，因此数组是唯一一种不能按值传递的类型。

## 试一试 传递数组

你可以通过编写一个函数来计算传递给函数的数组中的多个值的平均值来说明其中的来龙去脉。

```
// Ex5_04.cpp
// Passing an array to a function
#include <iostream>
using std::cout;
using std::endl;

double average(double array[], int count);      //Function prototype

int main(void)
{
    double values[] = { 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0 };

    cout << endl
         << "Average = "
         << average(values, (sizeof values)/(sizeof values[0]));

    cout << endl;
    return 0;
}

// Function to compute an average
double average(double* array, int count)
{
    double sum = 0.0;                // Accumulate total in here
    for(int i = 0; i < count; i++)
        sum += *array++;             // Sum array elements

    return sum/count;                // Return average
}
```

输出与上一个示例完全相同。

## 其工作原理

正如你所见，该程序只需很少的更改即可使用数组作为指针工作。原型和函数头已被更改，尽管两者都不是绝对必要的。如果你将两者都改回原始版本，将第一个参数指定为 double 数组，并保留函数体以指针形式编写，它同样有效。此版本最有趣的方面是 for 循环语句的主体：

```
sum += *array++;                 // Sum array elements
```

在这里，你似乎违反了不能修改指定为数组名的地址的规则，因为你正在递增存储在 array 中的地址。事实上，你并没有违反规则。记住，按值传递机制会复制原始数组地址并传递该副本，所以你在这里只是修改副本（原始数组地址完全不受影响）。因此，每当你将一维数组传递给函数时，你就可以在任何意义上将传递的值视为指针，并以任何你想要的方式更改地址。

## 向函数传递多维数组

向函数传递多维数组相当直接。以下语句声明了一个二维数组 beans：

```
double beans[2][4];
```

然后你可以像这样编写一个假设的函数 yield() 的原型：

```
double yield(double beans[2][4]);
```


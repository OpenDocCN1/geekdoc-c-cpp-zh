

将图 3.7 中的图示与清单 3.6 中的结构进行比较，我们可以很容易地发现后者并不包含函数，甚至没有构造函数。对于保存一对简单的对象（如 fName 和 fDays）来说，这完全没有问题，前提是这两个对象具有初始化机制。如前所述，每个数据项都是通过初始化列表 `{}` 来初始化的。因此，我们不需要实现构造函数——这被称为 *零规则*。关于特殊成员函数（例如构造函数）的更多规则将在第 4 章中讨论。

另一方面，下面的 `SimpleCalendar` 函数（其定义从第 [8] 行开始）展示了包含 `MonthDays` 对象的 vector 的应用。存储 `MonthDays` 对象的 `std::vector` 类型的 calendar 对象在第 [10] 行定义，其初始化在第 [10–23] 行。请注意，对于每个 `MonthDays` 对象，都需要在初始化列表 `{}` 中提供一对值——一个 string 值和一个整数值，例如 `{ "May", 31 }`。此外，字符串常量 `"May"` 足以初始化 `std::string` 对象。

```cpp
// Creates and displays a simple calendar
void SimpleCalendar( void )
{
    const std::vector< MonthDays > calendar {
                                      { "January",   31 },
                                      { "February",  28 },
                                      { "March",     31 },
                                      { "April",     30 },
                                      { "May",       31 },
                                      { "June",      30 },
                                      { "July",      31 },
                                      { "August",    31 },
                                      { "September", 30 },
                                      { "October",   31 },
                                      { "November",  30 },
                                      { "December",  31 }
                                    };

    // Print them on the screen
    auto sum_days { 0 };
    for( auto month : calendar )
    {
        sum_days += month.fDays;
        std::cout << month.fName << " has " << month.fDays << " days\\n";
    }

    std::cout << "\\nTotal days: " << sum_days << std::endl;
}
```

存储在 calendar vector 中的对象在循环中被逐一访问，这通过第 [27–31] 行的基于范围的 `for` 循环完成。更准确地说，calendar 中的每个对象依次被复制到 month 对象中，month 对象虽然用 `auto` 声明，但其类型也是 `MonthDays`。在此基础上，第 [29] 行借助点 `.` 运算符访问 `fDays` 字段，并将其累加到变量 `sum_days` 中。第 [30] 行从 month 对象中同时访问 `fName` 和 `fDays`，并将它们输出到屏幕。当 calendar 中的所有月份都显示完毕，且总天数已累加到 `sum_days` 中之后，`sum_days` 也在第 [33] 行显示。

运行上述代码后（例如，在某个在线编译器中，并添加相应的 `#include`），将得到以下输出：

```
January has 31 days
February has 28 days
March has 31 days
```

到目前为止，我们只在结构中看到了数据成员。很快我们将开始添加成员函数。然后，我们将学习如何对成员数据和函数的访问施加限制（第 4.3 节）。不过，struct 或 class 中所有不受限制的数据成员和成员函数都可以通过成员访问运算符在对象层面进行访问，其语法如图 3.8 所示。

图 3.8a 展示了使用点运算符从对象调用成员的常见方式。当不是直接提供对象，而是提供对象的引用时（第 3.11 节），也会使用这种调用方式。为完整起见，图 3.8b 也展示了通过对象指针进行调用的方式。在这种情况下，使用 -> 运算符。两者都属于第 2 组运算符（表 3.15）。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_94_0.png)

关于指针的讨论将推迟到第 3.12 节。

数据成员也可以通过将初始化放在构造函数中来初始化，这将在下一节讨论。如果没有显式编写构造函数，编译器就会自动为数据成员提供默认行为。此处的默认行为是通过调用合适的构造函数（例如 std::string 的构造函数）来初始化和复制对象。然而，基本内建类型会被保留为未初始化状态；如果被复制，则会逐字节复制。因此，在这种情况下进行正确的初始化非常重要。

正如我们已经看到的，C++ 定义了类（class），它在语义上与 struct 非常相似。主要区别在于，在类中，所有成员默认对直接访问隐藏，而 struct 则相反：即 struct 的所有成员都可以被外部组件自由读写。这一区别尽管乍看之下很微妙，却会对编程产生影响，我们将在后续章节中回到这个问题。但两者有很多相似之处，尤其是在初始化数据成员方面。

第 [24] 行创建了与 theArray 大小相同的 theDbArray。这一次，它保存的是 double 类型的元素。我们已经知道它不会被自动初始化。因此，在第 [27] 行，使用 std::copy 函数将 theArray 的元素复制到 theDbArray 对象中。请注意，这些元素会在复制过程中即时地从 unsigned int 转换为 double。

```cpp
// Make the same size as theArray
array< double, theArray.size() > theDbArray;

// Copy and convert int to double
copy( theArray.begin(), theArray.end(), theDbArray.begin() );

copy(    theDbArray.begin(), theDbArray.end(),
         ostream_iterator< double >( cout, " " ) );
```

最后，在第 [29–30] 行再次使用 std::copy 来显示 theDbArray 数组的所有元素。更准确地说，输出由针对 double 的 ostream_iterator 执行，它连接到 std::cout 流。

值得注意的是，std::array 是内建固定大小数组的包装类，后者将在附录 A.2.1 中讨论。包装类将在第 3.15 节中介绍。

# 3.10.1  多维固定大小数组

我们可以直接创建包含其他数组的数组，从而得到多维固定大小数组。让我们看一下清单 3.8，它展示了如何创建一个简单的二维结构——两行三列（即矩阵），其中保存浮点对象。

# 清单 3.8  使用 std::array 定义多维固定大小数组的示例（位于 CppBookCode, VectorsStringsArrays.cpp）。

```cpp
enum ArrayDims { kCols = 3, kRows = 2 };   // Define two constants

using ArrayElem = double;

// Declare a single array of kCols elems
using _1D_Array = std::array< ArrayElem, ArrayDims::kCols >;

// Declare a matrix with kRows
using _2D_Array = std::array< _1D_Array, ArrayDims::kRows >;

_2D_Array matrix { 0.0 };   // Create a matrix and init with zeros
```

固定大小数组的维度需要在编译时已知。为此，我们可以定义一个 const int 对象；但在这个示例中，我们使用了另一种方式，即枚举类型 ArrayDims 及其常量值 kCols 和 kRows，如第 [1] 行所定义。这是一种 *无作用域枚举* 类型，在本上下文中已经足够。较新的 *有作用域枚举* 类型将在第 3.14.6 节中介绍。

现在，我们可以用选定的维度来定义 `std::array`。然而，在处理由命名空间、类等组成的长名称时，使用 `using` 指令声明名称别名会非常有用，如第 [3, 6, 9] 行所示。很快我们就会看到，用 `using` 创建合适的别名可以使代码更简短、更清晰、更灵活。例如，如果我们想改变元素的类型，只需要修改第 [3] 行——所有后续元素将在编译期间自动调整。借助这些别名，我们在第 [12] 行定义了 matrix 对象。通过提供初始化列表 `{ 0.0 }`，其元素立即被初始化为 0.0。

```cpp
13    double val { 0.0 };    // Initial value
14
15    // Initialize matrix with increasing values
16    for (auto & r : matrix )
17      for( auto & c : r )
18        c = val ++;         // Each element gets 1 higher value
```

我们可以访问二维结构以写入新值，如第 [13–18] 行所示。在第 [16] 行，通过引用 `r` 访问 `matrix` 的行。然后，在第 [17] 行，借助引用 `c` 访问该行的每个元素，并为其赋当前值 `val`。使用引用（将在下一节讨论）有两个好处：

+   - 我们避免了复制行和元素
+   - 我们修改的是 `matrix` 的真实元素，而不是它们的局部副本

运行上述代码后，二维结构的内存布局如图 3.9 所示。我们可以看到，`kCols` 定义了最内层数组的维度，而 `kRows` 是这类数组的数量：即矩阵的行数。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_98_0.png)

**图 3.9** 具有两行三列的多维数组的内存布局与索引。



另一个有趣的构造是第[11]行的编译期不变量。它确保所提供参数`i`的类型属于“无符号”整数类型。换句话说，我们不允许其他类型被字节反转。但这个条件必须在编译期间检查，而不是在运行时。因此，在这种情况下，我们需要使用`static_assert`，而不是在运行时检查的`assert`。为了检查提供给模板函数的类型`T`是否无符号，我们使用`std::is_unsigned_v<T>`构造。如果`T`确实属于无符号类型之一，它计算结果为`true`。否则，编译将被中止，并显示编译器提供的适当错误消息。`std::is_unsigned_v`属于类型支持库，其对应的头文件已在第[2]行包含。更多关于使用`constexpr`和`static_assert`的示例将在第6.4节和第7.3.2节中介绍。

`RevertEndianness`模板版本的操作在以下`RevertEndianness_Test`函数中得到验证，其定义从第[22]行开始：

```cpp
inline void RevertEndianness_Test( void )
{
    // RevertEndianness can be computed at compilation time
    // Notice 'u' in 0xABCDu - this makes 0xABCD an unsigned constant
    std::cout << std::hex << std::uppercase << "0xABCD" << "\t <-> "
              << RevertEndianness( 0xABCDu ) << std::endl;

    // Compilation time since argument is constexpr
    constexpr unsigned int ui { 0xABCDu };
    std::cout << std::hex << std::uppercase   << ui << "\t <-> "
              << RevertEndianness( ui ) << std::endl;

    long l { 0x01234567 };
    // This will not compile since l is not an 'unsigned' type
    //std::cout  << std::hex << std::uppercase << l << "\t <-> "
    //          << RevertEndianness( l ) << std::endl;

    unsigned long ul { 0x01234567ul };
    std::cout << std::hex << std::uppercase   << ul << "\t <-> "
              << RevertEndianness( ul ) << std::endl;

    unsigned long long ull { 0x0123456789ABCDEFull };
    std::cout << std::hex << std::uppercase   << ull << "\t <-> "
              << RevertEndianness( ull ) << std::endl;
}
```

如前所述，如果向`RevertEndianness`传递`constexpr`类型参数（如第[26–32]行所示），该函数将被编译并执行，之后结果值将包含在代码中。但当提供可变对象时，`RevertEndianness`可以像任何其他函数一样被调用。然而，对于第[34]行定义的`long`类型参数，由于第[11]行的类型验证条件未满足，`RevertEndianness`将无法编译。

还要注意第[30, 39, 43]行上的特殊后缀，如`u`、`ul`和`ull`，它们用于定义整数字面量常量（https://en.cppreference.com/w/cpp/language/integer_literal）。

运行`RevertEndianness_Test`后的输出如下：

```text
ABCD        <-> CDAB0000
ABCD        <-> CDAB0000
1234567     <-> 67452301
123456789ABCDEF  <-> EFCDAB8967452301
```

字节的顺序被反转，但每个字节内部的位顺序保持不变。

## 4.8.4 示例项目 – 使用*TStack*设计模板类

在本节中，我们将学习如何定义和实现一个非常有用的数据结构，称为*栈*。我们在组织函数的嵌套调用时已经见过这个重要的数据结构（第3.14.3节）。回想一下，函数调用时，返回地址会自动压入栈顶。函数返回时，该地址会被弹出。由于调用可以嵌套，因此从另一个函数内部调用的函数需要先被处理。因此，栈反转了访问顺序——最后压入的将最先弹出，依此类推。这种方法被称为后进先出（LIFO），如前所述（第3.14.3节）。然而，我们将看到，栈数据结构的应用远不止存储返回地址（第6.6.9节）。在本节中，我们将学习以下内容：

- 栈及其功能
- 如何通过创建*模板*类来定义可以存储*任意*类型元素的栈类
- 如何在模板定义中添加数值参数
- 如何组织包含模板类定义的文件

栈是一种数据结构，允许我们以类似于桌子上堆放书籍的方式存储对象，如图4.12所示。新对象N只能被压入栈顶。同样，只能从栈顶弹出对象。无法访问结构中更深处的对象，例如图4.12a中的Z和Q。如果栈上有三个对象，名为Q、Z和N，那么要访问Z，首先需要弹出N。还要注意，如果对象按Q、Z、N的顺序放入栈，那么取出时的顺序将是相反的：N、Z、Q。最后，栈可以为空或已满。

图4.12a展示了栈数据结构。必须有存储数据的支持，由`fData`表示。还有一个直接或间接的栈指针的概念，它指向栈上的第一个空闲位置。这就是我们需要了解的栈底层数据存储区域。但栈真正独特的是其功能（动态性）。只可能有两种操作：*压入*，将新对象放到栈顶；以及*弹出*，从栈顶取出一个元素。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_300_0.png)

**图 4.12** (a) 栈数据结构的结构和操作。栈只能从顶部访问——新元素可以通过将其压入栈顶来添加。同样，栈顶的元素可以被弹出。示例栈包含两个元素，Q和Z。元素N可以被压入栈顶。之后它可以通过弹出操作从栈中移除。除了弹出所有前面的元素，无法访问栈中更深的元素（如Q）。(b) 适配器（包装器）模式。内部对象嵌入在外部对象中。仅暴露外部接口。

这些操作需要为两种特殊情况做好准备：空栈（用于*弹出*）和满栈（用于*压入*），这将在我们实现表示栈的类时看到。

栈可以存储相同类型的对象。然而，我们希望为许多不同类型定义栈，例如*size_t*和*double*。我们已经见过能够以相同方式处理各种类型数据的对象——`std::vector`是最好的例子（第3.2节）。这种功能是通过设计模板类获得的：在需要创建特定对象时，可以指定一个或多个类型的类，例如`std::vector<double>`。

STL也包含栈的实现（`std::stack`）。但在本节中，我们将出于两个原因实现自己的版本（清单4.17）：(i) 学习如何编写模板类；(ii) 因为未来应用需要略有不同的栈接口，如第6.6.6节所述。

为了更好地保护一个流行类的名称，首先重新打开了`CppBook`命名空间。模板类`TStackFor`的定义占用了第[13–14]行。首先，`T`被引入为表示参数化类型的名称，而`MaxElems`是一个数值参数，也可以在模板定义中提供。定义的第二行引入了名称`TStackFor`。

像往常一样，为存储的类型定义别名很方便，如第[18]行的公有部分和第[22]行的私有部分所示。我们很容易猜到，底层数据支持将是一个`std::vector`对象，保存`value_type`类型的对象，如第[24]行定义。如图4.12b所示，由于`fData`是私有数据成员，`TStackFor`可以被解释为*对`std::vector`的包装器*，大大缩小了其功能（第3.15节）。然后，在第[29]行，创建了`size_type`别名。有趣的是，需要在`DataContainer::size_type`之前放置一个额外的`typename`关键字，以明确告诉编译器我们指定的是一个类型。这在处理依赖于模板参数的类型名时是必要的，我们将在第6.6.6节中讨论。

`TStackFor`的主要接口由两个函数组成：在第[54]行声明的`Push`，以及在第[71]行声明的`Pop`。简单的`GetStackSize`函数返回栈上的对象数量，它仅在第[34]行以单行形式完全定义为一个内联成员。

### 清单4.17 TStackFor模板类的定义（在*TheStack*、*TheStack.h*中）

```cpp
#pragma once
#include <cassert>
#include <vector>

namespace CppBook {

// Definition of the stack data structure
template < typename T, auto MaxElems = 1000 >
class TStackFor
{
    public:
    using value_type = T;
};
```

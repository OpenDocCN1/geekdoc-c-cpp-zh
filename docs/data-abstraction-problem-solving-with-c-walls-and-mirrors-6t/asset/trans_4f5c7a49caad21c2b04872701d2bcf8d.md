

## 图 C2-6 (a) 创建第一个对象；(b) 创建第二个对象；(c) 赋值导致不可访问的对象

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_150_0.png)

我们有几种方法来修复这个函数。第一种是在函数终止前删除对象。我们可以通过添加以下行来实现：

```
delete someBoxPtr;
someBoxPtr = nullptr;
```

在函数末尾。如果由 someBoxPtr 指向的 ToyBox 对象仅由该函数需要，那么更好的实现选择是不从自由存储区分配内存，而是使用局部变量，如以下语句所示：

```
ToyBox<double> someBox(); // someBox is not a pointer variable
someBox.setItem(someItem);
```

如果在该函数中创建的对象在函数外部也需要，则该函数可以返回指向它的指针，以便调用者可以访问该对象。要实现此选项，我们将把函数的返回类型从 void 改为 ToyBox<double>* 并返回 someBoxPtr，它是指向 ToyBox<double> 对象的指针。结果函数定义如下：

```
ToyBox<double>* pluggedLeakyFunction(const double& someItem)
{
    ToyBox<double>* someBoxPtr = new ToyBox<double>();
    someBoxPtr->setItem(someItem);
    return someBoxPtr;
} // end pluggedLeakyFunction
```

你可以通过编写诸如下面的语句来调用此函数：

```
double boxValue = 4.321;
ToyBox<double>* toyPtr = pluggedLeakyFunction(boxValue);
```

现在 toyPtr 指向由 pluggedLeakyFunction 中的 ToyBox 构造函数创建的对象。当函数返回指向它在自由存储区中创建的对象的指针时，使用该指针的程序段必须负责删除该对象。否则，仍可能发生内存泄漏。在记录此类函数时，你应该添加注释以指明此责任。例如，你可以在 pluggedLeakyFunction 的定义前加上这些注释：

```
/* Creates an object in the free store and returns a pointer
to it. Caller must delete the object when it is no longer
needed. */
```

当然，此注释并不能防止内存泄漏，但它会提醒你的函数的用户注意潜在的泄漏风险。该函数仍可能被误用，并通过诸如下面的语句来调用：

```
pluggedLeakyFunction(boxValue); // Misused; returned pointer is lost
```

在这种情况下，指向自由存储区中对象的返回指针丢失，并发生内存泄漏。

防止内存泄漏的最佳方法是不使用函数来返回指向新创建对象的指针。相反，你应该定义一个具有用于此任务的方法的类。该类负责删除自由存储区中的对象，并确保没有内存泄漏。至少，这样的类将有三个部分：一个在自由存储区中创建对象的方法、一个指向对象的数据字段，以及一个方法——析构函数——在类实例不再需要时删除对象。虽然 C++ Interlude 1 介绍了类析构函数，但我们现在必须更多地讨论它们。

> 要防止内存泄漏，请勿使用函数来返回指向新创建对象的指针

每个 C++ 类都有一个析构函数，其名称与类相同，但前面带有波浪号 (~) 字符。对于作为局部变量的对象，当包含该对象的激活记录从运行时堆栈中移除时，会调用析构函数。如果对象是使用 new 创建并存储在自由存储区中，则当客户使用 delete 运算符释放分配给对象的内存时，会调用析构函数。

通常，编译器生成的析构函数对于一个类来说就足够了，但如果类本身通过使用 new 运算符在自由存储区上创建对象，那么实现析构函数以确保释放该对象的内存是一种安全可靠的编程实践。

清单 C2-2 给出了 GoodMemory 类的头文件，演示了如何避免内存泄漏。我们之前函数 pluggedLeakyFunction 中的指针变量现在是 GoodMemory 中的数据字段。只要该字段指向自由存储区中的现有对象，我们就可以访问该对象。

```
LISTING C2-2 Header file for the class GoodMemory
/** @file GoodMemory.h */
#include <string>
#include "ToyBox.h"
using namespace std;
class GoodMemory
{
(continues)
```

```
private:
ToyBox<string>* someBoxPtr;
public:
GoodMemory(); // Default constructor
~GoodMemory(); // Destructor
void fixedLeak(const double& someItem);
}; // end GoodMemory
```

因为类 GoodMemory 有一个用作数据字段的指针变量，我们应该定义一个默认构造函数来将指针初始化为 nullptr。该类的析构函数只需删除指针所指向的对象。清单 C2-3 显示了该类的实现文件。

```
LISTING C2-3 Implementation file for the class GoodMemory

/* @file GoodMemory.cpp */
#include "GoodMemory.h"

GoodMemory::GoodMemory() : someBoxPtr(nullptr)
{ // end default constructor

GoodMemory::~GoodMemory()
{ delete someBoxPtr;
} // end destructor

void GoodMemory::fixedLeak(const double& someItem)
{ someBoxPtr = new ToyBox<double>();
someBoxPtr->setItem(someItem);
} // end fixedLeak
```

与原始函数 myLeakyFunction 不同，如清单 C2-1 所示，以下客户端函数使用 GoodMemory 类来保证不会发生内存泄漏：

```
void goodFunction()
{ double boxValue = 4.321; // Original statement
GoodMemory gmObject; // Create a safe memory object
gmObject.fixedLeak(boxValue); // Perform the task
} // end goodFunction
```

编译器在此方面大有帮助。首先，编译器可以检查以确保在调用 fixedLeak 方法之前已创建 GoodMemory 对象。这保证了安全的内存分配和释放。然后，由于变量 gmObject 是局部变量，编译器会在 goodFunction 函数执行结束时自动调用 GoodMemory 析构函数。因此，在自由存储区中分配的内存被释放。

## C2.3.3 避免悬空指针

如前所述，悬空指针是不再引用有效对象的指针变量。四种情况可能导致悬空指针，但我们只讨论其中三种，因为我们认为第四种是一种不安全的做法。2

- 如第 C2.3.1 节所讨论，如果在使用 delete 后不将指针变量设置为 nullptr，则会使指针悬空。

可能导致悬空指针的情况

- 同样，如果你声明一个指针变量但不为其赋值，结果就是一个悬空指针。与任何 C++ 变量一样，当 C++ 创建指针变量时，其值是未定义的。也就是说，C++ 不会自动初始化或清除变量所代表的内存。编译器和程序员都无法检查指针变量中的值是否实际指向自由存储区中的对象。该值可能只是创建指针时内存中原本的内容。例如，假设你编写了诸如下面的语句：

```
MagicBox<int>* myMagicBoxPtr;
myMagicBoxPtr->getItem();
```

在这里，指针变量 myMagicBoxPtr 未被分配指向的对象。当调用 getItem 方法时，程序将中止——通常伴随段错误——因为程序将 myMagicBoxPtr 中的值视为 MagicBox<int> 对象的地址，并尝试在该地址查找 getItem 方法。由于 MagicBox<int> 对象极不可能碰巧位于那里，程序将异常结束。

如果你需要创建一个指针变量但没有对象让它指向，则应始终将其设置为 nullptr：

```
MagicBox<int>* myMagicBoxPtr = nullptr;
```

然后你的代码可以将指针变量与 nullptr 进行比较，以查看它是否指向自由存储区中的有效对象，如下例所示：

```
if (myMagicBoxPtr != nullptr)
    myMagicBoxPtr->getItem();
```

如果指针不是 nullptr，则可以使用该指针来调用方法。

- 第三种可能导致悬空指针的情况比较微妙，防范它的最佳方法是仔细编程。考虑我们在讨论内存泄漏时之前见过的以下语句：

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
MagicBox<string>* yourBoxPtr = myBoxPtr;
```

执行此代码会导致图 C2-7 所示的内存配置，其中 yourBoxPtr 和 myBoxPtr 都指向同一个对象。我们说 yourBoxPtr 是 myBoxPtr 的别名，因为它们都引用同一个对象。到目前为止，这段代码没有问题，也没有任何内存泄漏。

假设我们随后执行以下语句：

```
delete myBoxPtr;
myBoxPtr = nullptr;
yourBoxPtr->getItem();
```



```cpp
~Test()
{
    cout << "Destructor is called";
};

void *operator new(size_t size);
void operator delete(void *P, size_t size);
};

char *Test::CurrentPtr;
char *Test::OldPtr;
char *Test::TableSpace;
bool Test::FirstTime = true;

void *Test::operator new(size_t size)
{
    if(Test::FirstTime)
    {
        /* First time! Allocating memory large enough to hold the entire tablespace */
        Test::TableSpace = (char *)::new char[TABLESPACE_SIZE];
        Test::CurrentPtr = Test::TableSpace;
        printf("\n Test::TableSpace pointer is %u", Test::TableSpace);
        printf("\n Current pointer is %u", Test::CurrentPtr);
        printf("\n Old pointer is %u", Test::OldPtr);
        Test::FirstTime = false;
    }

    /* When we want memory space that goes beyond the tablespace available */
    if((Test::CurrentPtr + size) > (Test::TableSpace + TABLESPACE_SIZE))
    {
        cout << "\n Memory allocation failure";
        getchar();
        exit(0);
    }

    Test::OldPtr = Test::CurrentPtr;
    /* Old pointer to be returned. New pointer would be useful for allocation of new memory in the next cycle */
    Test::CurrentPtr = Test::CurrentPtr + size;
    cout << "\n Memory allocated \n";
    printf("Current pointer is %u", Test::CurrentPtr);
    printf("\n Old pointer is %u", Test::OldPtr);
    return Test::OldPtr;
}

void Test::operator delete(void *p, size_t size)
{
    ::delete p;
}

int main()
{
    while(true)
        new Test;  // Continue allocating until it runs out of memory
}
```

```
Output
Test::TableSpace pointer is 48770560
Current pointer is 48770560
Old pointer is 0
Memory allocated

Current pointer is 48770564
Old pointer is 48770560
Constructor is called
Memory allocated

Current pointer is 48770568
Old pointer is 48770564
Constructor is called
Memory allocated

Current pointer is 48770572
Old pointer is 48770568
Constructor is called
Memory allocated

Current pointer is 48770576
Old pointer is 48770572
Constructor is called
Memory allocated

Current pointer is 48770580
Old pointer is 48770576
Constructor is called
Memory allocated

Current pointer is 48770584
Old pointer is 48770580
Constructor is called
Memory allocated

Current pointer is 48770588
Old pointer is 48770584
Constructor is called
Memory allocated

Current pointer is 48770592
Old pointer is 48770588
Constructor is called
Memory allocation failure
```

## 程序如何工作

为了演示，我们定义了一个 32 字节的小型表空间，每次操作将从该表空间分配 4 字节。程序围绕表空间设计和内存分配展开。表空间在开始时通过为其分配足够的内存（32 字节）进行初始化。

### 初始化表空间

让我们尝试理解这个程序。让我们从表空间大小的定义开始。

```
#define TABLESPACE_SIZE 32
```

程序包含一个 32 字节的小型表空间。它有一个类 `Test`，只有一个数据成员 `int i`，其大小为 4 字节。`Test` 类的对象存储在大小为 32 的表空间中。因此，在 32 字节的内存中最多可以容纳八个这样的对象。我们重载了 `new`，它做两件事：

- 1. 它在开始时向静态字符指针 `TableSpace` 分配 32 字节。然后，从这 32 字节中，为第一个对象分配 4 字节。
- 2. 从此以后，每次内存耗尽（32 字节）时，它为下一个对象再分配 4 字节。

这如图 6.1、6.2 和 6.3 所示。图 6.1 显示了第一次插入之前和之后内存的外观。它还揭示了操作前后变量如何被设置为各自的值。图 6.2 显示了在相同位置进行第三次插入的情况。它还指出了该操作之后变量值是如何变化的。图 6.3 显示了内存完全占满的情况。

第一次调用为整个表空间分配内存，即 32 字节，也就是四个字节的八个块。

此后不可能再分配内存，因此分配失败。

## 使用静态成员

我们在类 `Test` 中定义了四个静态变量。了解为什么在这里使用静态成员是很重要的。我们需要跟踪内存位置，而不管对象的数量如何。这些成员真正意义上属于类，而不是对象。

![](img/0da15892b2796544fb447dc5727e9ab4_283_0.png)

![](img/0da15892b2796544fb447dc5727e9ab4_283_1.png)

![](img/0da15892b2796544fb447dc5727e9ab4_284_0.png)

让我们绕个弯来理解这一点。假设我们有以下两个陈述：

- 1. 萨钦是一个男人。
- 2. 男人分布在世界各地。

这些陈述意味着萨钦分布在世界各地。

为什么这个推断是错误的？这是因为当类属性被继承到一个元素中时，它必须是对象的属性，而不是类本身的属性。这里给出的例子是一个与类有关的属性（类分布在世界各地，而不是单个对象）。静态变量代表类的属性（这些属性不会被类的元素，即对象所继承）。这是一个例子，可以看到此类成员的必要性以及程序员如何使用它们。

第一个静态变量保存指向我们想要自行分配的内存的指针。所以，当我们第一次获得内存分配时，我们必须从堆中分配内存（在我们的例子中是 32 字节），并让该指针指向的内存作为表空间。随后，每次需要分配时，从该块中取出四个字节进行分配。接下来，两个指针用于在内存中遍历。当前指针指向下一个内存将被分配的位置，而旧指针指向当前内存被分配的位置。在第一次 `new` 操作中，完整的表空间内存从堆中分配；对于所有后续操作，内存都是从这个 `new` 调用所分配的内存中获取的，而不是从其他调用中获取。布尔变量 `firstTime` 告诉我们 `new` 是否是第一次被调用。当前指针和旧指针的分配和移动过程也如图 6.1、6.2 和 6.3 所示。

我们也为 `Test` 类定义了构造函数和析构函数。有趣的是，尽管我们没有从重载的 `new` 中调用构造函数，但构造函数会被自动调用。构造函数调用是由编译器在重载的 `new` 函数中添加的。此外，看看 `operator new()` 函数体内的 `::new` 调用。它将调用系统定义的全局 `new`。我们使用 `::new` 在堆上获取表空间所需的内存。

`delete` 运算符被重载为带有两个参数，即 `void` 指针和 `size_t` 类型的变量 `size`。这里的第二个参数并不重要。我们可以使用两种版本调用 `delete`，即一个参数（仅 `void *`）和两个参数（`void *` 和 `size_t`）。如果未提供第二个参数，对象的大小会自动确定。当定义 `delete` 运算符的类被继承时，我们需要第二个参数。另一个有趣的点是，`::delete` 在析构函数中被调用。`::delete` 用于撤销重载 `new` 所做的工作，即释放 `P` 指向的内存。

### 分阶段释放内存

为了避免复杂性，这里没有实现与分配例程类似的复杂释放过程。如果编写了类似分配的释放例程，则很难找到哪些块是已分配的，哪些是空闲的。我们需要一个额外的数组，用 `bool` 值指示哪些槽位已分配、哪些空闲。从该列表中，就可以分配任何空闲槽位。我们为演示重载 `new` 和 `delete` 而设计的解决方案并不复杂。请看下面重载 `new` 中的条件。

### 测试内存分配失败

下面的分配算法检查我们要分配的内存是否在表空间限制内。如果超出表空间限制，它会显示一条失败消息，程序执行将被终止。

```
if((Test::CurrentPtr + size) > (Test::TableSpace + TABLESPACE_SIZE))
{
    cout << "\n Memory allocation failure";
    getchar();
    exit(0);
}
```

输出显示了当前指针和旧指针是如何递增的。当当前指针到达末尾时，我们得到内存分配失败消息。

## 6.11 用户定义转换

如果所涉及的两个对象类型相同，对象赋值是简单的。被赋值对象成员被复制到被赋值的对象。我们称之为逐成员复制。然而，当它们的类型不同时，例如，用两种不同类型的对象表示的两种不同格式的时间，那么我们需要用户定义转换。为什么？由于对象不同且成员不同，编译器无法进行逐成员复制。在深入讨论用户定义转换的细节之前，让我们了解一下隐式转换的含义，隐式转换由编译器自动提供。

> 注意 普通的赋值涉及逐成员复制。然而，当赋值语句两边有不同类型的对象时，必须指示编译器如何复制。用户定义转换是解决此问题的一种方法。

### 6.11.1 隐式转换

有时需要从一种类型转换为另一种类型。C 自动提供了大量转换。此外，强制类型转换也可以用于提供类型转换。这两种转换在 C++ 中也都可能。此外，还可以提供用户定义转换（从一个类的对象转换为另一个类、从类对象转换为内置类型，或从内置类型转换为类对象）。

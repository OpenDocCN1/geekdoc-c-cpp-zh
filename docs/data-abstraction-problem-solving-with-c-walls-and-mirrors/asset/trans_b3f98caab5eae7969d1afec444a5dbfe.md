

## 图 C2-3 当 myboxPtr 指向 MagicBox 对象且其数据成员被设置后的运行时栈和自由存储区

在运行时栈上创建变量 | 在自由存储区创建对象

```
MagicBox<string>* myboxPtr = new MagicBox<string>();
string someItem = "Something"
```

设置字段 item 的值

![](img/d0cb86b2f18b2db569968ad7c743510e_147_0.png)

与运行时栈上的变量不同（后者的内存会自动分配和释放），自由存储区中的变量即使在创建它的函数或方法结束后，仍然存在于内存中。这意味着，当程序员从自由存储区为变量分配内存时，程序员有责任在变量不再需要时释放该内存。未能这样做会导致**内存泄漏**。内存泄漏是指已分配但不再需要，且无法访问或释放的内存。

如果你在自由存储区上分配了内存，你必须释放它

为了表示一个变量是指针，我们在该指针所引用的数据类型之后放置一个星号 `*`。例如，以下语句

通过在数据类型后编写星号来指示指针类型

```
MagicBox<string>* myboxPtr = new MagicBox<string>();
```

在自由存储区中创建一个 MagicBox 对象，并将该对象的地址存储在局部变量 `myboxPtr` 中。我们说 `myboxPtr` 指向一个 MagicBox 对象。要调用自由存储区中对象的方法，我们使用运算符 `->` 

```
string someItem = "Something Free";
myboxPtr->setItem(someItem);
```

图 C2-3 显示了执行上述语句后内存和局部变量的状态。

请注意，这个新创建的对象没有程序员定义的名称。访问其方法的唯一方法是通过我们创建的指针直接访问，如在上一个例中使用 `myboxPtr->`。我们通常会简化图表，只画出自由存储区中的对象及其指针，如图 C2-4 所示。

有些程序员会将 `*` 放在变量名旁边。本教材的作者认为这能清晰地表明该变量是指针类型。

## 图 C2-4 myBoxPtr 和它所指向的对象

![](img/d0cb86b2f18b2db569968ad7c743510e_148_0.png)

指针变量只是另一种类型的变量，遵循与其他变量类型相同的规则。例如，如果你声明了一个指向 `ToyBox<string>` 对象的指针变量，它可以只能指向 `ToyBox<string>` 对象，而不能指向 `MagicBox<string>` 对象或 `ToyBox<double>` 对象，如下语句所示：

```
ToyBox<string>* toyPtr = new ToyBox<string>(); // OK
ToyBox<string>* boxPtr = new MagicBox<string>(); // 错误！
ToyBox<string>* somePtr = new ToyBox<double>(); // 错误！
```

如果你有两个可以指向相同类型对象的指针变量，可以使用赋值运算符 `=` 让它们指向同一个对象。例如，语句
`somePtr = toyPtr;`

使变量 `somePtr` 指向与 `toyPtr` 指向相同的 `ToyBox` 对象。在这些情况下，将赋值操作理解为将右侧指针变量中存储的值复制到左侧指针变量是有帮助的。由于指针存储的是对象的地址，因此复制的值是对象在自由存储区中的位置。对象本身并没有被复制。结果是两个指针变量都指向同一个对象，如图 C2-5 所示。

如果你声明了一个指针变量但没有立即为它创建引用的对象，你应该将指针设置为 `nullptr`。像下面的赋值是必要的，因为 C++ 不会为你初始化指针：

```cpp
ToyBox<int>* myToyPtr = nullptr;
```

## 图 C2-5 指向同一个对象的两个指针变量

![](img/d0cb86b2f18b2db569968ad7c743510e_148_1.png)

### C2.3.1 释放内存

当指针指向的内存不再需要时，你使用 `delete` 运算符来释放它。然后你应该将指针变量设置为 `nullptr`，作为其不再引用或指向某个对象的信号：

```cpp
delete somePtr;
somePtr = nullptr;
```

## 指针与程序的自由存储区 123

如果我们在这个示例中没有将 `somePtr` 设置为 `nullptr`，那么 `somePtr` 将是一个**悬空指针**（dangling pointer）示例，因为它仍然包含一个已释放对象的地址。悬空指针可能是严重错误的根源。

始终记住，如果一个类使用 `new` 创建对象，则该类的某个方法必须删除该对象的内存。安全可靠的编程的一个特征是，任何从自由存储区分配内存的行为都伴随着在不再需要时释放内存的责任。

指针对内存如何使用以及何时发生绑定提供了巨大的控制，我们将稍后讨论这一点。如果使用不当，它们也会导致严重的问题和难以发现的错误。涉及指针的最常见错误是内存泄漏和悬空指针，正如本节所示。让我们看看这些问题在程序中是如何发生的，以便你可以在代码中防止它们。

如果你使用 `new` 运算符分配内存，你必须使用 `delete` 运算符释放它

## C.3.2 避免内存泄漏

内存泄漏发生于在自由存储区中创建了对象，但程序不再有方法访问它。由于无法访问该对象，它无法被删除并占用内存，尽管它无法被使用。如果程序有多个内存泄漏，可能会导致内存耗尽并崩溃。

考虑以下语句：

```cpp
MagicString* myBoxPtr = new MagicBox<string>();
MagicString* yourBoxPtr = new MagicBox<string>();
yourBoxPtr = myBoxPtr; // 导致不可访问的对象
```

图 2-6 追踪了这些语句的执行过程。最终，`yourBoxPtr` 指向与 `myBoxPtr` 相同的对象，而 `yourBoxPtr` 原指向的对象不再可访问，导致了图中所示的内存泄漏。

为了防止这种情况，我们不应该创建第二个对象。相反，要么将 `yourBoxPtr` 初始化为 `nullptr`，要么将其设置为 `myBoxPtr`：

```cpp
MagicString* myBoxPtr = new MagicBox<string>();
MagicString* yourBoxPtr = myBoxPtr;
```

细微的内存泄漏发生在：函数或方法在自由存储区创建了对象，但由于没有返回该指针或将其存储在类成员中而丢失了它的指针。这就是列表 C2-1 中函数发生的情况。列表 C2-1 错误的函数在自由存储区分配内存

```cpp
void leakyFunction(const double& someItem)
{
    ToyBox<double>* someBoxPtr = new ToyBox<double>();
    someBoxPtr->setItem(someItem);
} // 结束 leakyFunction
```

参数 `someItem` 和指针 `someBoxPtr` 都存储在运行时栈上，并在函数结束后自动销毁。在自由存储区通过 `new ToyBox<double>` 创建的对象仍然存在，但由于我们对其唯一的引用被销毁了，我们导致了内存泄漏。

## C++ 间插 2 指针、多态与内存分配

图 C2-6 (a) 创建第一个对象；(b) 创建第二个对象；(c) 赋值导致不可访问的对象

+ (a) `MagicBox<string>* myboxPtr = new MagicBox<string>();`

![](img/d0cb86b2f18b2db569968ad7c743510e_150_0.png)

+ (b) `MagicBox<string>* yourBoxPtr = new MagicBox<string>();`

![](img/d0cb86b2f18b2db569968ad7c743510e_150_1.png)

+ (c) `yourBoxPtr = myBoxPtr;`

![](img/d0cb86b2f18b2db569968ad7c743510e_150_2.png)

我们有几种方案来修复此函数。第一种是在函数终止前删除对象。我们可以通过在末尾添加以下行来实现：

```cpp
delete someBoxPtr;
someBoxPtr = nullptr;
```

如果 `someBoxPtr` 指向的 Box 对象只需要此函数，更好的实现方式是不从自由存储区分配内存，而是使用局部变量，如下语句所示：

```cpp
ToyBox<double> someBox(); // someBox 不是指针变量
someBox.setItem(someItem);
```

如果创建的对象在函数外部，函数可以返回一个指针供调用者访问该对象。要实现这一点，我们将函数的返回类型从 `void` 改为 `ToyBox<double>*` 并返回 `someBoxPtr`。结果定义如下：

```cpp
ToyBox<double>* leakyFunction(const double& someItem)
{
    ToyBox<double>* someBoxPtr = new ToyBox<double>();
    someBoxPtr->setItem(someItem);
    return someBoxPtr;
} // 结束 leakyFunction
```


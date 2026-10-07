
请记住，使用 `operator new` 操作符动态分配的指针，即使你使用了类似于静态数组的语法，仍然需要使用 `operator delete` 操作符对其进行释放。

如果你忘记了这一点，你的应用程序就会内存泄漏，这是不好的。

# 使用指针时的常见编程错误

C++ 允许你进行动态分配，以便你的应用程序的内存消耗达到最优。与 C# 和 Java 等基于运行时环境的较新语言不同，C++ 并不具备自动垃圾回收器来清理程序已分配但无法使用的内存。由于指针可能会变得有点复杂，程序员有许多机会犯错。

## 内存泄漏

这可能是 C++ 应用程序中最常见的问题之一：程序运行得越长，消耗的内存越多，系统就会变得越慢。这通常发生在程序员没有确保应用程序在内存块不再需要后，通过匹配的 `delete` 调用来释放使用 `new` 动态分配的内存时。

由你——程序员——来确保所有分配的内存都被你的应用程序释放。这种情况永远不应该发生在：

```
int* numbers = new int [5]; // 初始分配
// 使用指针 numbers
...
// 忘记释放 delete[] pnumbers;
...
// 再次进行分配并覆盖指针
pnumbers = new int[0]; // 泄漏了之前分配的内存
```

# 当指针未指向有效的内存位置时

当使用操作符 `*` 解引用指针时，必须 100% 确定指针指向有效的内存位置，否则将会崩溃。

# 错误的编程演示

```
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     int* pointer;
6:     char input;
7: 
8:     cout << "Enter y to allocate memory: ";
9:     cin >> input;
10:    if (input == 'y') {
11:        pointer = new int;
12:        *pointer = 42;
13:    }
14: 
15:    cout << "Enter y to delete memory: ";
16:    cin >> input;
17:    if (input == 'y') {
18:        delete pointer;
19:    }
20: 
21:    cout << "Pointer value: " << *pointer << endl;
22:    return 0;
23: }
```

输出：

```
Enter y to allocate memory: y
Enter y to delete memory: n
Pointer value: [崩溃]
```

### 分析

上面的程序崩溃是因为如果用户没有输入 'y' 来分配内存，`pointer` 就没有被初始化。当程序在第 22 行尝试解引用指针时，即使指针在此之前是有效的，它也会访问无效位置。

# 列表 8.13 程序的安全版本

```
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     int* pointer = nullptr;
6:     char input;
7: 
8:     cout << "Enter y to allocate memory: ";
9:     cin >> input;
10:    if (input == 'y') {
11:        pointer = new int;
12:        *pointer = 42;
13:    }
14: 
15:    cout << "Enter y to delete memory: ";
16:    cin >> input;
17:    if (input == 'y' && pointer != nullptr) {
18:        delete pointer;
19:        pointer = nullptr;
20:    }
21: 
22:    if (pointer != nullptr) {
23:        cout << "Pointer value: " << *pointer << endl;
24:    } else {
25:        cout << "Pointer not valid." << endl;
26:    }
27:    return 0;
28: }
```

输出：

```
Enter y to allocate memory: n
Enter y to delete memory: n
Pointer not valid.
Enter y to allocate memory: y
Enter y to delete memory: n
Pointer value: 42
Enter y to allocate memory: y
Enter y to delete memory: y
Pointer not valid.
```

### 分析

程序的安全版本通过将指针初始化为 `nullptr` 避免了崩溃。在解引用指针之前，程序检查它是否不为 `nullptr`。此外，在删除内存后，将其设置为 `nullptr` 以防止其变成悬空指针。

# 悬空指针（也称为野指针）

注意，任何有效指针在通过 `delete` 释放后都是无效的。因此，如果在第 22 行使用指针，即使它在此之前有效，也会崩溃。为了避免这个问题，许多程序员在初始化或删除指针后将其赋值为 NULL，在使用前检查其有效性。

# 指针编程最佳实践

在应用程序中使用指针时，有一些基本规则可以让你处理它们变得更容易。

| 应该 | 不应该 |
|--- |--- |
| **应该** 始终初始化指针变量，否则它们将包含垃圾值。这些垃圾值会被解释为地址位置，但你的应用程序无权访问。如果你无法将指针初始化为由 `new` 或其他有效变量返回的地址，请初始化为 NULL<br>**应该** 在使用指针之前检查它们是否为 NULL。检查 NULL 可以确保在声明后的语句中（初始化为 NULL）未分配有效地址的指针无法被使用（如列表 8.13 中危险的操作所示）。<br>**应该** 确保指针的编程方式使其在有效性得到保证时被使用，否则你的程序可能会崩溃。<br>**应该** 记得使用 `delete` 释放通过 `new` 分配的内存，否则你的应用程序将内存泄漏并降低系统性能。 | **不应该** 在通过 `delete` 释放内存块后访问该指针。<br>**不应该** 对同一个内存地址多次调用 `delete`。<br>**不应该** 在用完分配的内存块后忘记调用 `delete` 导致内存泄漏。 |

在学习了一些关于指针使用的编程最佳实践后，现在是时候纠正列表 8.13 中极其错误的代码，并使用列表 8.14 所示的代码了。

# 列表 8.14 更安全的指针编程，对列表 8.13 的修正

```
0 #include <iostream>
1 using namespace std;
2:
3 int main()
4 {
5 cout << "Is it sunny (y/n)? ";
6 char UserInput = 'y';
7 cin >> UserInput;
8:
9 if (UserInput == 'y')
10 {
11 // 已初始指针（良好）
12 int *pTemperature = new int;
13 *pTemperature = 30;
14
15 cout << "Temperature is: " << *pTemperature << endl;
16
17 // 使用指针完成？delete
18 delete pTemperature;
19 }
20
21 return 0;
22 }
```

### 输出

Is it sunny (y/n)? y

Temperature is: 30

下一次运行：

Is it sunny (y/n)? n

（无崩溃地结束）

### 分析

主要的区别在于指针是在需要时创建的——即当用户按下 y 时——并且如第 12 行所示，在创建时就进行了初始化。内存的释放也发生在同一个块中，因此不会出现在指针未分配有效内存位置时就被使用（在解引用中或在调用 delete 处）的情况。

# 检查使用 new 的分配请求是否成功

`new` 总是会成功，除非请求的内存量异常巨大，或者系统处于可用内存极少的关键状态。某些应用程序需要请求大块内存（例如数据库应用程序），因此，不要假设内存分配一定会成功。C++ 为你提供了两种可能的方法来确保你的指针有效。默认方法使用异常，除非分配失败并以 `std::bad_alloc` 的形式抛出。这将导致你的应用程序执行被中断，除非你编写了异常处理程序，否则你的程序将带有类似于“handled exception”的错误消息并崩溃。

第 28 节“异常处理”详细讨论了这个问题。8.15 为你预览了如何使用异常处理来检查失败的分配请求。

# 列表 8.15 处理异常，当 new 失败时优雅地退出

```
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:   try
6:   {
7:     // 请求大量的内存空间
8:     int* pAge = new int [536870911];
9:
10:    // 使用分配的内存
11:
12:    delete [pAge];
13:  }
14:  catch (bad_alloc)
15:  {
16:    cout << "Memory allocation failed. Ending program" << endl;
17:  }
18:  return 0;
19: }
```

### 输出

Memory allocation failed. Ending program

### 分析

此程序在你的计算机上执行结果可能不同。我的环境无法为 536870911 个整数成功分配所需的空间。我没有编写异常处理程序（第 14-17 行中的 catch 块），程序将非常狼狈地结束。当使用 Microsoft Visual Studio 构建的调试模式二进制文件时，程序执行将产生如图 8.2 所示的输出。

图 8.2

程序崩溃

在缺少

异常处理

在列表 8.15 中

（使用 MSVC 编译器构建的调试版本）。

![](img/fd01f923cb963a04200115e3b215851c_214_0.png)

调试模式二进制文件包含开发环境插入的异常处理程序，这些程序会介入并显示上述消息。在发布模式下，操作系统（在本例中为 Windows）将如图 8.3 所示非常粗鲁地终止应用程序。

图 8.3

程序崩溃

在缺少

异常处理

在列表 8.15 中

（发布版本）。

![](img/fd01f923cb963a04200115e3b215851c_214_0.png)

当你的应用程序如上所示崩溃时，异常处理程序的存在允许程序优雅地退出。在没有异常处理程序的情况下，操作系统将粗鲁地终止应用程序。

# 输出 ▼

输入一个想要平方的数字： 5

平方结果为： 25

# 分析 ▼

执行平方操作的函数位于第 3–6 行。注意它是如何通过引用接收要平方的数字作为参数，并返回相同结果的。如果你忘记将参数 `Number` 标记为引用 (`&`)，结果将无法传递给调用函数 `main()`，因为 `ReturnSquare()` 此时将在 `Number` 的本地拷贝上执行操作，而该拷贝在函数退出时会被销毁。使用引用，你可以确保 `ReturnSquare()` 在与 `main()` 定义相同的地址空间内进行操作。因此，即使函数 `ReturnSquare()` 已退出，`main()` 中仍然可以使用该操作的结果。

在此示例中，包含用户发送数字的输入参数被修改了。如果你需要两个值（原始值和平方值），你可以让函数接受两个参数：一个包含输入值，另一个提供平方值。

# 在引用上使用关键字 const

你可能需要某些不允许改变所别名原始值的引用。在声明此类引用时使用 `const` 是实现这一目标的方法：

```cpp
int Original = 30;
const int ConstRef = Original;
ConstRef = 40; // 不允许：ConstRef 不能改变 Original 的值
int &ConstRef2 = ConstRef; // 不允许：ConstRef2 不是 const
const int ConstRef2 = ConstRef; // 正确
```

# 通过引用向函数传递参数

引用的许多优点之一是它们允许被调用函数在未从调用函数拷贝的参数上进行工作，从而显著提高性能。然而，由于被调用函数是直接在调用函数的栈上使用参数工作的，因此确保被调用函数无法更改调用端变量的值是非常重要的。定义为参数引用不能作为左值（l-value），因此任何对其进行赋值的尝试都会导致编译失败。

# 什么是引用？ 19

**列表 8.19** 使用 const 引用确保调用函数无法修改通过引用发送的值

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: void CalculateSquare(const int& Number, int& Result) // 注意 "const"
4: {
5:     Result = Number*Number;
6: }
7:
8: int main()
9: {
10:    cout << "Enter a number you wish to square: ";
11:    int Number; cin >> Number;
12:
13:    int Square = 0;
14:    CalculateSquare(Number, Square);
15:    cout << Number << "^2 = " << Square << endl;
16:
17:    return 0;
18: }
```

# 输出 ▼

输入一个想要平方的数字： 27

27^2 = 729

# 分析 ▼

与之前的程序（发送要平方数字的变量也持有结果）不同，这里使用了两个变量——一个用于发送要平方的数字，另一个用于存储操作的结果。为了确保发送的数字不能被修改，它使用 `const` 关键字被标记为常量引用，如第 3 行所示。这自动使参数 `Number` 成为输入参数——一个值不能被修改的参数。

作为一个实验，你可以修改第 5 行，使用列表 8.18 所示的逻辑返回平方值：

Number *= Number;

你肯定会遇到一个编译错误，提示 `const` 值不能被修改。这些 `const` 引用是 C++ 提供的一种强大工具，它们表示参数是一个输入参数，同时确保通过引用传递的内容不会被调用函数修改。初看起来这可能很平凡，但在多处理器环境中，编写第一个版本的人与增强或修正它的人可能不同，使用 `const` 引用对编程质量有重要影响。

# 第 8 节：指针和引用的解释

## 总结

在本节中，你学习了指针和引用。你学习了如何使用指针访问和操作内存，以及它们是如何辅助动态内存分配的工具。你学习了可以为元素分配内存的 `new` 和 `delete` 运算符。你学习了它们的变体 `new[]` 和 `delete[]` 如何帮助你为数据数组分配内存。你接触了指针编程和动态分配中的陷阱，并发现释放动态内存对于避免泄漏至关重要。引用是别名，当向函数传递保证有效的参数时，它们是使用指针的强大替代方案。你学习了在使用指针和引用时使用“const 正确性”，从以后将尽可能使用最严格的 `const` 级别来声明函数。

## 问答

- Q 既然可以使用不需要担心释放的静态数组，为什么还要动态分配？

- 静态数组具有固定大小，如果你的应用程序需要更多内存，它们不会向上扩展；如果你的应用程序需要差异，它们也不会进行优化。

- Q 我有两个指针：

`int* pNumber = new int;`

`int* pCopy = pNumber;`

在对两个都调用 `delete` 以确保内存消失后我不是更好吗？

-- 那是错误的。你只允许对 `new` 返回的地址调用一次 `delete`。此外，理想情况下，你应该避免两个指针指向同一个地址，因为对其中任何一个执行 `delete` 都会导致另一个失效。你的程序编写方式也不应该对所用指针的有效性产生任何不确定性。

问答 199

# 我什么时候应该使用 new(nothrow)？

## 我什么时候应该使用 new(nothrow)？

如果你不想处理 `std::bad_alloc` 异常，使用 `nothrow` 版本的 `operator`，它在分配失败时返回 `NULL`。

# 我什么时候应该使用 new(nothrow)？

## 我什么时候应该使用 new(nothrow)？

如果你不想处理 `std::bad_alloc` 异常，使用 `nothrow` 版本的 `operator`，它在分配失败时返回 `NULL`。

（注：由于原文中存在重复的段落，如“我什么时候应该使用 new(nothrow)”，已按要求完整翻译）

# 之前的分析重复部分翻译如下：

与之前的程序（发送要平方数字的变量也持有结果）不同，这里使用了两个变量——一个用于发送要平方的数字，另一个用于存储操作的结果。为了确保发送的数字不能被修改，它使用 `const` 关键字被标记为常量引用，如第 3 行所示。这自动使参数 `Number` 成为输入参数——一个值不能被修改的参数。

作为一个实验，你可以修改第 5 行，使用列表 8.18 所示的逻辑返回平方值：

Number *= Number;



# 示例代码和附加信息

你可以通过其网站访问所有示例程序并了解有关本书的更多信息，该网站的 URL 如下：
http://www.cppmove.com

# 反馈

我欢迎你的建设性意见——无论是负面还是正面。我已竭尽全力为你带来我希望你会认为是一本优秀的书。然而，在某个时间点，我不得不停止写作、审阅和微调以“发布新修订版”。因此，你可能会发现错误、不一致、可以改进的呈现方式，或完全缺失的主题。你的反馈给了我一个机会来修复这些问题，通过本书的网站通知所有读者变更情况，并改进后续的修订版或版本。

联系我的最佳方式是通过电子邮件。你可以在本书的网站上找到电子邮件地址：
http://www.cppmove.com

如果你使用电子书，你可能希望确保拥有本书的最新版本（请记住它是以增量方式编写和发布的）。你还应该在提交报告前查看本书的网站以了解当前已知的勘误表。在任何情况下，请在提供反馈时参考此版本的出版日期。当前出版日期为 2022-04-19（你也可以在第 ii 页找到它，即封面之后的页面）。

非常感谢。

# 第一部分

# 移动语义的基础特性

本书的这一部分介绍了移动语义的基础特性，这些特性不特定于通用编程（即模板）。它们对应用程序程序员在日常编程中特别有帮助，因此每个使用现代 C++ 的 C++ 程序员都应该了解它们。
移动语义在通用编程方面的特性将在第二部分中介绍。

此页 intentionally left blank

# 第 1 章

# 移动语义的力量

本章使用简短的代码示例演示移动语义的基本原理和优势。

# 1.1 移动语义的动机

为了理解移动语义的基本原理，让我们先看看一段小代码的执行情况，首先不使用移动语义（即使用仅支持 C++03 的旧 C++ 编译器编译），然后使用移动语义（使用支持 C++11 或更高版本的现代 C++ 编译器编译）。

# 1.1.1 使用 C++03 的示例（移动语义之前）

假设我们有以下程序：

```
```cpp
#include <string>
#include <vector>

std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;  // create vector of strings
    coll.reserve(3);                // reserve memory for 3 elements
    std::string s = "data";         // create string object

    coll.push_back(s);              // insert string object
    coll.push_back(s+s);            // insert temporary string
    coll.push_back(s);              // insert string

    return coll;                    // return vector of strings
}
```
```

- 下一步是将字符串插入到向量 coll 中的命令：
  coll.push_back(s);

C++ 标准库中的所有容器都具有值语义，这意味着它们会创建传递给它们的值的副本。因此，我们在向量中得到了第一个元素，它是传递的值/对象 s 的完整（深）副本：

![](img/c6f2c4fe3e0701d95a17354ad517147a_22_0.png)

![](img/c6f2c4fe3e0701d95a17354ad517147a_22_1.png)

- • 现在让我们看看下一个语句，它创建一个新的临时字符串并再次将其插入到向量中：
  coll.push_back(s+s);

此语句分为三个步骤执行：

- 1. 我们创建临时字符串 s+s：

```
std::vector<std::string> createAndInsert()
{
	std::vector<std::string> coll;
	coll.reserve(3);
	std::string s = "data";
	coll.push_back(s);
	coll.push_back(s+s);
	coll.push_back(s);
	return coll;
}

std::vector<std::string> v;
...

v = createAndInsert();
```

![](img/c6f2c4fe3e0701d95a17354ad517147a_23_0.png)

2. 我们将此临时字符串插入到向量 coll 中。正如始终一样，容器会创建传递值的副本，这意味着我们创建了临时字符串的深拷贝，包括为其值分配内存：

![](img/c6f2c4fe3e0701d95a17354ad517147a_23_1.png)

# 1.1 移动语义的动机

```
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(s);

    return coll;
}

std::vector<std::string> v;
...
v = createAndInsert();
```

![](img/c6f2c4fe3e0701d95a17354ad517147a_24_0.png)

- 3. 在语句结束时，临时字符串 s+s 被销毁，因为我们不再需要它：

```
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(s);

    return coll;
}

std::vector<std::string> v;
...
v = createAndInsert();
```

![](img/c6f2c4fe3e0701d95a17354ad517147a_24_1.png)

在这里，我们遇到了第一个生成性能不佳的代码的时刻：我们复制了一个临时字符串，并在其后立即销毁了副本的源，这意味着我们不必要地分配并释放了本可以从源移动到副本的内存。

- • 接下来，使用下一个语句，我们再次将 s 插入到 coll 中：

```
coll.push_back(s);
```

再次，coll 复制 s：

```
```cpp
std::vector<std::string> createAndInsert()
{
    std::vector<std::string> coll;
    coll.reserve(3);
    std::string s = "data";

    coll.push_back(s);

    coll.push_back(s+s);

    coll.push_back(s);

    return coll;
}

std::vector<std::string> v;
...
v = createAndInsert();
```
```

![](img/c6f2c4fe3e0701d95a17354ad517147a_25_0.png)

这也是需要改进的地方：因为 s 的值不再需要，某种优化可以使用 s 的内存作为向量中新元素的内存。

- - 在 `createAndInsert()` 结束时，我们来到 return 语句：
  
  ```cpp
  return coll;
  } 
  ```

这里，程序的行为变得有点复杂。我们按值返回（返回类型不是引用），这应该是 return 语句中值 coll 的副本。复制 coll 意味着我们必须创建整个向量及其所有元素的深拷贝。因此，我们必须为向量中元素的数组分配堆内存，并为每个字符串为其值分配的堆内存分配内存。在这里，我们必须分配内存 4 次。

然而，由于同时 coll 被销毁，因为我们离开了它声明的作用域，编译器允许执行命名返回值优化（NRVO）。这意味着编译器可以生成代码，使 coll 仅用作返回值。

即使这会改变程序的功能行为，此优化也是允许的。如果我们在 vector 或 string 的拷贝构造函数中有打印语句，我们会看到程序不再有来自打印语句的输出。这意味着此优化会改变程序的功能行为。然而，这是可以的，因为我们明确允许 C++ 标准中即使有副作用也进行此优化。没有人应该期望这里会进行拷贝，就像没有人应该期望不会进行拷贝一样。它完全取决于编译器是否执行命名返回值优化。

让我们假设我们有命名返回值优化。在这种情况下，在 return 语句结束时，coll 现在成为返回值，并且 s 的析构函数被调用，从而释放其声明时分配的内存：


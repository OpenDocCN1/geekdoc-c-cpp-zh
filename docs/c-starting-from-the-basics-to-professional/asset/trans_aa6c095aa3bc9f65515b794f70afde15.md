
你甚至可以在类型定义可达的对象上调用函数。用正式的话说，我们说可达类定义中成员的名字是可见的。因此，在 `Ex11_03.cpp` 的下面两行中，我们可以对 `to_roman()` 返回的 `std::string` 对象调用 `c_str()` 和 `size()` 函数，尽管我们从未导入 `<string>` 模块：

```cpp
std::cout << "1234 in Roman numerals is " << to_roman(1234).c_str() << std::endl;
std::cout << "This consists of " << to_roman(1234).size() << " numerals" << std::endl;
```

为了避免无意的名称冲突，并避免使用者依赖不同的内部名称，实体名称的*可见性*不会随意逃逸出模块。因此，`std::string` 和 `std::string_view` 这些名称在 `Ex11_03.cpp` 中不可见，因而无需在那里使用。

```cpp
// std::string_view sv{ "MXX" };  /* Error: the name std::string_view is not visible */
// std::string roman{ to_roman(567) };  /* Error: the name std::string is not visible */
```

不过幸运的是，你不需要访问函数返回类型的名称就能使用它们。你始终可以使用 `auto` 或 `const auto&` 作为该名称的占位符来捕获函数的结果。

```cpp
auto roman{ to_roman(567) };
std::cout << "567 in Roman numerals is " << roman.c_str() << std::endl;
```

与类型名称（`std::string`、`std::string_view` 等）的可见性一样，函数名称的可见性也不会随意越过模块边界。因此，诸如 `std::stoi()` 和 `std::to_string()` 这样的函数根本无法从 `Ex11_03.cpp` 内部调用。

```cpp
// std::cout << std::stoi("1234") << std::endl;  // Error: std::stoi() is not visible
```

这也至少部分解释了为什么我们之前在 `Ex11_02.cpp` 中必须导入 `<string>` 模块。没有该导入，下面这行就无法工作，因为 `<<` 运算符不可见。正如你将在第 13 章学到的，这个流输出运算符实际上也不过是一个函数，只不过它可以用不同的语法调用。

```cpp
// std::cout << "1234 in Roman numerals is " << to_roman(1234) << std::endl;
```

总之，声明的*可达性*和传递可见性会传播到模块的所有使用者——无论这种传播多么间接——但所声明名称的*可见性*不会。不过幸运的是，可达定义通常就足以让你使用模块接口而无需导入任何额外模块，尤其是如果你乐于使用 `auto`。

## 导出导入声明

与模块接口文件中的大多数声明一样，你也可以在导入声明前添加 `export`。任何导入模块接口文件的文件，也可以导入从该模块导出的声明。例如，假设在 `Ex11_02` 的 `roman.cppm` 中，你在其两个导入声明前添加 `export`，如下所示：

```cpp
// roman.cppm
export module roman;
export import <string>;
export import <string_view>;

export std::string to_roman(unsigned int i);
export unsigned int from_roman(std::string_view roman);
```

然后你就可以安全地移除 `Ex11_02.cpp` 中对 `<string>` 的导入声明，因为该文件随后通过导入 roman 间接导入了 `<string>`。

不过，你不应系统性地导出在模块内使用的所有模块导入。只有当你知道模块的每个使用者都将需要依赖模块所暴露的函数和/或类型名称时，才应导出某个导入声明。如你在上一节中所记得的，类型定义的可达性通常就足以使用模块接口，为此你不需要导出相应的导入。

导出导入声明的另一个可行原因是形成所谓的子模块。我们将在下一节讨论该策略。

## 管理更大的模块

模块越大，其功能越复杂，就越可能需要进一步将其代码划分为更小、更易管理的组件。

当然，你的首选方案是将模块拆分为若干更小的模块。如果其接口可以拆分为清晰、互不相交的子接口，并且这些子接口的实现也相互独立，那么这种方法就很有效。那么一种特别有趣的方法是将较大的模块拆分为若干所谓的子模块。我们在第一小节讨论该方案。

然而，有时你确实希望将所有内容捆绑在一个自包含的单一模块中。也许拆分其功能没有意义。或者也许模块接口已经相当小，而你只是需要大量内部机制来实现它。并非所有代码都需要始终导出到整个应用程序。将代码保持在模块局部有一个优势：你可以更灵活地修改它，而无需担心外部使用。C++20 为此类场合提供的答案是模块分区。我们将在第二个小节中简要讨论分区。

### 模拟子模块

尽管 C++ 并不正式支持嵌套子模块的概念，但你可以很容易地模拟它们。最好通过示例来解释这一原理。通过创建以下三个模块接口文件（为简洁起见，我们将省略函数定义），你可以将俗称的 roman 模块拆分为两个更小的子模块，分别称为 roman.from 和 roman.to。

```cpp
// roman.cpp - Module interface file of the roman module
export module roman;
export import roman.from;        // Not: 'export import .from;' (cf. partitions later)
export import roman.to;

// roman.from.cpp - Module interface file of the roman.from module
export module roman.from;
import <string_view>;
export unsigned int from_roman(std::string_view roman);

// roman.to.cpp - Module interface file of the roman.to module
export module roman.to;
import <string>;
export std::string to_roman(unsigned int i);
```

值得注意的是，就 C++ 而言，`roman.from` 和 `roman.to` 只是像其他任何模块名一样的模块名。如果你愿意，完全可以把这些（子）模块重命名为 `from_roman` 和 `to_roman`，甚至 `cattywampus` 和 `codswallop`。该语言根本不会强制任何层级命名方案。只是采用一种方案能让你更容易地看到模块与其子模块之间的关系，而且点号正是专门为了便于这种层级命名而允许在模块名中使用的。

有了这三个模块文件，在应用程序的剩余部分你就有如下选择：要么分别导入各个子模块，要么一次性全部导入。如果你只需要输出罗马数字，可以添加 `import roman.to;` 并仅访问 `to_roman()`。或者你只需添加 `import roman;` 就能一次性访问所有子模块。

> **提示** 从功能上讲，一次性导入所有子模块与只导入你实际需要的那部分之间没有区别。事实上，从功能角度看，前者更方便得多。不过，更细粒度地导入子模块的潜在优势包括：编译速度提升（源文件之间的依赖更少意味着有更多机会并行编译），以及在开发期间缩短增量构建时间（当你更改某个子模块的接口时，只有导入该特定子模块的文件需要重新构建）。

### 模块分区

如果将一个模块拆分成多个（子）模块并不适合你，*模块分区*为你提供了将原本庞大、单体式模块更好地结构化的手段。

> **注意** 子模块和分区之间的关键区别在于，子模块可以被应用程序的其余部分单独导入，而分区仅在模块内部可见。对于应用程序的其余部分，分区模块仍然表现为一个自包含的模块。你甚至可以在完全重新分区一个模块的同时，不更改应用程序中任何其他地方。

### 模块实现分区

你从 Ex11_02 中已经知道，可以将模块的实现划分到多个模块实现文件中。但这并不总是足够；有时你希望在多个源文件内使用相同的模块局部实体——最好不要在共享的模块接口文件中声明这些实现细节。这正是*模块实现分区*的用途。

一个示例是以下分区，摘自我们庞大的 `roman` 模块。它定义了 `from_roman(char)` 辅助函数，该函数此前已在 `from_roman.cpp` 中定义（这个重新分区后的 `roman` 模块的完整源代码见 Ex11_04）。

```cpp
// roman-internals.cpp - Module implementation file for the
//                    internals partition of the roman module
module roman:internals;

unsigned int from_roman(char c)
{
    // Same switch statement as before...
}
```

*模块分区文件*的模块声明与任何其他模块文件类似，不同之处在于，*分区*的名称添加在模块名称之后，并用冒号分隔。在我们的示例中，分区名因此是 internals，显然它是 roman 模块的一个分区。模块声明中缺少 export 关键字，表明这是一个*模块实现分区*，因此它不允许导出任何实体。名称 internals 唯一标识这个特定文件。

> ⚠️ **注意** 任意两个模块分区文件都不能共享同一个*分区名*——即使其中一个文件包含模块*接口*分区，而另一个包含模块*实现*分区也不行。因此，分区名始终唯一标识一个文件。

然后，要在定义 `from_roman(string_view)` 的模块实现文件中使用 internals 分区及其函数，你必须导入该分区，如下所示。

```cpp
// from_roman.cpp - Implementation of the from_roman() function
module roman;
import :internals;  // Caution: never 'import roman:internals;'

unsigned int from_roman(std::string_view roman)
{
    // Same as before... (uses from_roman(char) function from the :internals partition)
}
```

> ⚠️ **注意** 模块分区只能导入到同一模块的其他文件中，并且只能使用 `import :partition_name;`。看似诱人的语法 `import module_name:partition_name;` 永远无效（无论是在模块外部——那里无法访问该分区，还是在模块内部——那里 *模块名* 限定反正只会是多余的）。

当然，只有当这些分区随后被同一模块的多个其他实现文件和/或分区文件复用时，将模块局部功能分组到实现分区文件中才真正值得。如果像 `internals` 这样的分区只被另一个文件使用，那可能就不值得付出这种努力。

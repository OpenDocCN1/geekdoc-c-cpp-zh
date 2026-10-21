

- 3. 可以稍后存储和检索的对象被称为 ________。
    - (a) serial objects
    - (b) serialized objects
    - (c) persistent objects
    - (d) persisted objects

- 4. 当我们写入二进制流时，________ 不会发生。
    - (a) insertion
    - (b) conversion
    - (c) Both
    - (d) None

- 5. 我们在程序中引用一个文件时所使用的名称被称为 ________。
    - (a) logical file name
    - (b) physical file name
    - (c) file handle
    - (d) program file name

- 6. 文本文件存储和检索可能需要 ________。
    - (a) character conversions
    - (b) numeric conversions
    - (c) Both
    - (d) None

- 7. 库函数的 ________ 越多，对程序员来说就越容易。
    - (a) dependency
    - (b) independency
    - (c) standardization
    - (d) modularization

- 8. 将文件指针移动到我们想要的位置的操作被称为 ________。
    - (a) jump operation
    - (b) seek operation
    - (c) Both
    - (d) None

- 9. 设备驱动程序接受来自 ________ 的命令。
    - (a) the user
    - (b) the operating system
    - (c) the programmer
    - (d) the device

- 10. Unix 中的文件结束标记是 ________。
    - (a) ^Z (ctrl Z)
    - (b) ^D (ctrl D)
    - (c) Any of the above depending on the programmer
    - (d) Any of the above depending on the compiler

### Conceptual Exercises

- 1. 为什么需要 I/O 库？
- 2. 讨论程序员、C++ I/O 库和操作系统在 I/O 中的作用。
- 3. 解释文件打开、读取、写入和关闭的过程。
- 4. 解释文本流和二进制流的区别。
- 5. 如何打开一个文本文件并从中读取？
- 6. 如何打开一个二进制文件并写入？
- 7. 解释使用 `get()` 和 `put()` 函数以及使用 `getline()` 的读写方法。
- 8. 解释在二进制流中使用 `read()` 和 `write()` 函数的读写方法。
- 9. 解释 `seekg()`、`seekp()`、`tellg()` 和 `tellp()` 函数在二进制文件随机访问过程中的作用。
- 10. 如何在处理文件时确定错误？

### Practical Exercises

- 1. 编写一个程序读取文本文件并统计其中的字符数。
- 2. 编写一个程序读取文本文件并将其复制到另一个文本文件。
- 3. 编写一个程序读取文本文件并在整个文件中将特定单词转换为另一个单词。
- 4. 选取前面章节中定义的任意员工类。按员工编号的排序顺序将员工信息存储到文件中。从键盘读取一个员工编号并显示相应的员工详细信息。
- 5. 为客户类编写类似的程序。选取前面定义的任意客户类。

## Chapter 14 — Namespaces

### Learning Objectives

- The name conflict problem
- Fully qualified names
- Logical grouping
- `using` declarations and directives
- Defining inside and outside the namespace
- Extending the namespace
- Unnamed namespaces
- Nested namespaces
- Namespace aliases
- `std` namespace
- Koenig lookup

### 14.1 Name Conflict Problem

当最初版本的 C++ 被引入时，厂商开始向程序员提供第三方库供其使用。这些库帮助程序员将例行的工作函数直接拿来使用。例如，统计学家需要用于查找回归、众数等的额外函数。同样，图形设计师需要用于绘制基本形状如线条和正方形的函数，有时还需要更高级的函数，如三维图像、阴影和投影。库通过提供基本构建块来减轻程序员的负担，使他们能够专注于核心设计。

当程序员使用其中一个这样的库时，他/她不会遇到任何问题。问题开始出现于当使用多个定义了同名函数的库时。让我们考虑一个例子。我们有一个数学库，其中包含一个函数 `abs()`，它返回传递给它的数字的绝对值。我们也可能在使用一个库，其中 `abs()` 返回班级中缺席的学生人数。当我们在程序中使用 `abs()` 时，编译器无法识别需要使用哪个 `abs()`。如果我们能够为这两个函数命名不同，这个问题就可以很容易避免。不幸的是，我们无法选择不冲突的名称，因为这些名称是由开发该库的开发者决定的。每当我们使用任何第三方库时，我们都可能与之前安装的库发生名称冲突。这种问题无法在本地解决。第三方库设计者也无法解决这个问题，因为他/她不知道我们计算机上安装了哪些其他库。这就是所谓的名称冲突问题。

> **Note:** 名称冲突问题类似于把一所学校的所有学生都放在一个大房间里。如果你只喊一个学生的名字，比如“Arun”，就很可能有不止一个学生回应。

为了解决名称冲突问题，我们需要为函数提供封闭。每个封闭应有一个唯一名称并包含唯一的函数。然而，相同的名称可能存在于不同的封闭中。每个这样的封闭被称为命名空间。

### 14.1.1 Global Namespace

全局命名空间是程序运行的封闭。它是程序在执行时可访问的环境。任何函数、变量或类都必须被带入全局命名空间才能被访问。

> 当我们使用两个具有相同名称的第三方库时，至少有一个元素的名称相同，我们就会遇到名称冲突问题。
>
> 通过将不同库的元素放在不同的命名空间中，可以避免名称冲突问题。

每个程序都可以在不加限定符的情况下使用全局命名空间元素。

命名空间标识逻辑组。

`namespace::element` 是一个完全限定名称，例如，`std::cout` 和 `math::abs()` 分别是 `std` 和 `math` 命名空间元素的完全限定名称。`math` 在这里是一个用户定义的命名空间。

使用命名空间有很多种方法：`using` 指令、`using` 声明和完全限定名称是例子。

问题产生的原因是所有安装的库都将其函数插入到全局命名空间中。简单来说，所有函数都被无差别地汇集到一个单一空间中。一旦库被安装，就无法在库元素名称之间进行区分。因此，在名称冲突的情况下，全局命名空间无法唯一标识一个库元素。

### 14.1.2 Logical Grouping

全局命名空间问题的解决方案在于逻辑分组。这类似于把特定年级的学生放在单独的房间。现在，人们可以很容易地唯一识别三年级的 Arun。也可以发现三年级的“Arun”与六年级的 Arun 不同。

引入命名空间是为了提供这种名称的逻辑分组。一旦逻辑分组到位，只需担心在单个组中唯一标识一个名称即可。这又类似于确保单个年级中没有超过一个 Arun。在编程时，可以实际禁止在单个命名空间中存在相似名称的对象，也可以重命名它们。这不是一个大问题，因为单个库是由一个开发团队设计的；因此，负责人总能决定更好的无冲突命名约定。

因此，命名空间标识元素的逻辑组。这些元素可以是变量、类及其对象，以及非成员函数。

### 14.1.3 Fully Qualified Names

一旦使用命名空间对元素进行逻辑分组，任何名称都可以使用语法 `namespace::element` 进行限定。假设有两个 `abs()` 函数，一个在 `math` 命名空间中，另一个在 `Academic` 命名空间中。这里，可以使用 `math::abs()` 和 `Academic::abs()` 以无歧义的方式标识这两个 `abs()` 函数。

名称 `math::abs()` 被称为完全限定名称。当 `abs()` 函数被同一库的某个其他函数使用时，即 `math` 库，它位于与 `abs()` 相同的命名空间中。它不需要使用 `math::abs()`；它可以直接使用 `abs()`。如果某个在 `math` 命名空间之外定义的函数使用 `abs()`，那么它应该使用完全限定名称，即 `math::abs()`。

我们将在以下章节学习如何定义和使用命名空间。首先，让我们讨论如何以不同于我们迄今为止一直在使用的 `using namespace std` 的方式使用 `std` 命名空间。

### 14.2 Ways of Using Namespaces

#### 14.2.1 `using` Syntax

`using` 是一个关键字，当不想重复使用完全限定名称时使用。它有两种使用方式。


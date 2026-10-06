
```cpp

int constexpr cMember()

{

    return d_x;

}

int member() const

{

    return d_x;

}

```
```cpp
Data d1{ 0 }; // OK，但不是一个常量表达式
enum e1 {
  ERR = d1.cMember(); // ERROR: cMember(): 不再是一个常量
expression anymore
};
constexpr Data d2{ 0 }; // OK，常量表达式拥有enum e2 {
  OK = d2.cMember(), // OK: cMember(): 现在是一个常量
  expression
  ERR = d2.member(), // ERROR: member(): 不是一个常量
  expression
};
```

### 8.2 静态成员函数

除了静态成员之外，C++ 还允许我们定义静态成员函数。类似于由类中所有对象共享的静态数据，静态成员函数也可以在不与该类的任何关联对象的情况下而存在。

静态成员函数可以访问其所在类的静态成员，但如果它们被告知了这些对象的存在（如接下来的示例所示），也可以访问其类对象的成员（私有或公有）。静态成员函数与类的任何对象都没有关联，它们没有这个 `this` 指针。事实上，静态成员函数与全局函数完全具有比较性，但下一节将显示 `8.2.1` 关于一个细微点的说明。由于静态成员函数不需要关联对象，因此在类接口的公共部分声明的静态成员函数可以在不指定该类对象的情况下调用。下面的示例说明了静态成员函数的这一特性：

```cpp
class Directory {
    string d_currentPath;
    char s_path[];
public:
    static void setpath(char const *newpath);
    static void preset(Directory &dir, char const *newpath);
}
inline void Directory::preset(Directory &dir, char const *newpath)
{
  dir.d_currentPath = newpath; // 见下文文本
  // 1
}
char Directory::s_path[200] = "/usr/local"; // 2
void Directory::setpath(char const newpath) {
  if (strlen(newpath) >= 200) {
    throw "newpath too long";
  }
  strcpy(s_path, newpath); // 3
}
int main() {
  Directory dir;
  Directory::setpath("/etc"); // 4
  dir.setpath("/etc"); // 5
  Directory::preset(dir, "/usr/local/bin"); // 6
  dir.preset(dir, "/usr/local/bin"); // 7
}
```

- 在 `1` 处，静态函数修改了对象的私有数据成员。然而，必须修改其成员的对象作为引用参数传递给成员函数。注意，静态成员函数可以被定义为内联 `inline` 函数。
- 在 `2` 处，定义了一个较长的数组以容纳长路径。或者，可以使用字符串或内存指针。
- 在 `3` 处，一个（可能很长但不是过长）新路径被存储在静态成员 `s_path[]` 中。只使用了静态成员函数。
- 在 `4` 处，`setpath()` 是一个静态成员，因此不需要对象。但编译器需要知道该函数属于哪个类，因此使用作用域解析运算符提到了该类。
- 在 `5` 处，这里使用 `dir` 来告诉编译器我们正在讨论 `Directory` 类中的一个函数。静态成员函数可以像普通成员函数一样被调用，但这并不意味着静态成员函数接收对象的地址作为其 `this` 指针。这里使用了成员类语法作为类名加作用域解析运算符的替代方案。
- 在 `6` 处，`currentPath` 被更改了。与 `4` 类似，使用了类和作用域解析运算符。
- 在 `7` 处，这里使用 `dir` 来告诉编译器我们正在讨论 `Directory` 类中的一个函数。实现与 `6` 相同，但这里使用 `dir` 来告诉编译器我们正在讨论 `Directory` 类中的一个函数。在这种情况下，注意这并不是作为 `dir` 的普通成员函数使用的：函数仍然没有 `this` 指针，必须作为参数传递给静态成员以告知它要修改的 `currentPath`。

# 第 9 章：类与内存分配

- `this` 指针，允许显式引用调用其成员函数的对象；
- 拷贝构造函数：创建对象副本的构造函数；
- 移动构造函数：从匿名临时对象创建对象的构造函数。

## 9.1 运算符 ‘new’ 和 ‘delete’

C++ 定义了两个运算符来分配内存并将其返回“公共内存池”。这两个运算符分别是 `new` 和 `delete`。

下面是一个简单的示例，说明了它们的用法。一个 `int` 指针变量指向由运算符 `new` 分配和 `delete` 释放的内存。

```cpp
int *ip = new int;
delete ip;
```

以下是 `new` 和 `delete` 运算符的一些特性：

- `new` 和 `delete` 是运算符，因此不需要像函数 `malloc` 和 `free` 那样加括号；
- `new` 返回一个指向操作数所请求的内存类型的指针（例如，它返回一个指向 `int` 的指针）；
- `new` 使用类型作为其操作数，其重要优点是：根据要分配对象的类型，可以获得正确数量的内存；
- 结果是 `new` 是一个类型安全的运算符，因为它总是返回一个与操作数中提到的类型相同的指针。此外，接收的指针类型必须与运算符 `new` 指定类型匹配；
- `new` 可能会失败，但这通常对程序员来说不需要担心。程序不需要测试内存分配是否成功，而 `malloc` 及其它的函数要求这样做。`9.2.2` 节深入探讨了 `new` 的这一方面；
- `delete` 返回 `void`；
- 每调用一次匹配的 `delete` 且最终未被执行，就会发生一次内存泄漏；
- `delete` 可以安全地释放 `0` 指针（什么都不做）；
- 否则，`delete` 必须仅用于释放由 `new` 分配的内存。它不应该用于释放由 `malloc` 及其它的分配的内存。
- 在 C++ 中，`malloc` 及其它的已过时，应该避免使用。

运算符 `new` 可以用于分配原始类型，也可以用于分配对象。原始类型或没有构造函数的结构体 `struct` 所分配的内存不保证初始化为 `0`，但可以提供初始化表达式：

```cpp
int *v1 = new int; // 不保证初始化为 0
int *v1 = new int(); // 初始化为 0
int *v2 = new int(3); // 初始化为 3
int *v3 = new int(3 * *v2); // 初始化为 9
```

### 9.1 运算符 'NEW' 和 'DELETE'

当分配类类型对象时，其构造函数的参数（如果有的话）会紧跟在 `new` 表达式中的类型之后指定，并通过由此指定的构造函数对对象进行初始化。例如，分配 `string` 时可以使用以下语句：

```cpp
string *s1 =                   // 使用默认构造函数
string *s2 = new string();      // 相同
string *s3 = new string(4, ' ');     // 初始化为 4 个空格。
```

除了使用 `new` 为单个实体或实体数组分配内存外（见下节），还存在一种返回原始内存内存的变体运算符：`operator new(sizeInBytes)`。原始内存以 `void *` 的形式返回。在这里，`new` 为未指定的用途分配一块内存。原始内存可能包含多个字符，但不应被解释为字符数组。由于 `new` 返回的原始内存是 `void *`，因此其返回值可以赋值给 `void *` 变量。更多情况下使用类型转换将其赋值给 `char *` 变量。这里是一个示例：

```cpp
char *chPtr = static_cast<char*>(operator new(numberOfBytes));
```

原始内存的使用经常与第 `9.5` 节讨论的放置 `new`（placement new）结合使用。

#### 9.1.1 分配数组

运算符 `new[]` 用于分配数组。C++ 注释中使用通用表示法 `new[]`。要分配的元素数量必须在方括号内指定，反之，它必须由类型前缀。

```cpp
int *arr = new int[10]; // 分配 10 个整数
delete[] arr;          // 释放数组
```

运算符 `new[]` 用于分配数组。当分配类类型对象时，其构造函数的参数（如果有）会紧跟在 `new` 表达式中的类型之后指定，并通过由此指定的构造函数对对象进行初始化。例如，分配 `string` 数组时可以使用以下语句：

```cpp
string *s1 = new string[10];         // 使用默认构造函数初始化 10 个 string
string *s2 = new string[10]();      // 相同
string *s3 = new string[10](4, ' '); // 初始化为 10 个包含 4 个空格的 string
```

除了使用 `new` 为单个实体或实体数组分配内存外（见下节），还存在一种返回原始内存的变体运算符：`operator new(sizeInBytes)`。原始内存以 `void *` 的形式返回。在这里，`new` 为未指定的用途分配一块内存。原始内存可能包含多个字符，但不应被解释为字符数组。由于 `new` 返回的原始内存是 `void *`，因此其返回值可以赋值给 `void *` 变量。更多情况下使用类型转换将其赋值给 `char *` 变量。这里是一个示例：

```cpp
char *p = static_cast<char*>(operator new(size));
```

原始内存的使用经常与第 `9.5` 节讨论的放置 `new`（placement new）结合使用。

#### 9.1.1 分配数组

运算符 `new[]` 用于分配数组。C++ 注释中使用通用表示法 `new[]`。要分配的元素数量必须在方括号内指定，反之，它必须由类型前缀。

```cpp
int *arr = new int[10]; // 分配 10 个整数
delete[] arr;          // 释放数组
```

### 9.1.2 删除数组

动态分配的数组使用 `operator delete[]` 来进行删除。它期望一个指向内存块的指针，该内存块此前由 `operator new[]` 分配。

当 `operator delete[]` 的操作数是一个对象数组的指针时，会执行两个操作：

- 首先，为数组中的每个对象调用类的析构函数。正如在本章后部分解释的，析构函数会执行在对象不再存在时所需的所有清理操作。
- 其次，指针指向的内存被返回到公共池。

以下示例展示了如何分配和删除一个包含 `10` 个 `string` 对象的数组：

```cpp
std::string *sp = new std::string[10];
delete[] sp;
```

如果删除动态分配的原始类型值数组，不会执行任何特殊操作。执行 `it = new int[0]` 之后，`delete[] it` 语句只是返回 `it` 指向的内存。请注意，由于指针是一种原始类型，删除动态分配的指针数组不会导致指针所指向的数组元素被销毁。因此，下面的示例会导致内存泄漏：

```cpp
string *sp = new string[5];
for (size_t idx = 0; idx != 5; ++idx)
    sp[idx] = new string;
delete[] sp; // 内存泄漏！
```

在这个示例中，`delete[]` 执行的唯一操作是将指向五个 `string` 指针的区域返回到公共池。

在这些情况下，应该这样执行销毁：

- 为数组的每个元素调用 `delete`；
- 删除数组本身

示例：

```cpp
for (size_t idx = 0; idx != 5; ++idx)
    delete sp[idx];
delete[] sp;
```

其后果之一是，当内存要返回时，不仅指针必须可用，它包含的元素数量也必须可用。这可以通过在一个简单的类中存储指针和元素数量并使用该类的对象来轻松实现。

`Operator delete[]` 是与 `operator delete` 不同的运算符。经验法是：如果使用了 `new[]`，则也应使用 `delete[]`。

# 第 9 章：类与内存分配

#### 9.1.3 扩大数组

一旦分配，所有数组的大小都是固定的。目前没有简单的方法来扩大或缩小数组。C++ 没有 `renew` 运算符。扩大数组时需要采取的基本步骤如下：

- 分配一个更大的新内存块；
- 将旧数组的内容拷贝到新数组中；
- 删除旧数组；
- 让数组指针指向新分配的数组。

静态数组和局部数组无法调整大小。只有动态分配的数组可以进行大小调整。

示例：

```cpp
#include <string>
using namespace std;
string *enlarge(string *old, size_t oldsize, size_t newsize)
{
    string *tmp = new string[newsize]; // 分配更大的数组
    for (size_t idx = 0; idx < oldsize; ++idx)
        tmp[idx] = old[idx]; // 将旧的拷贝到 tmp
    delete old; // 删除旧数组
    return tmp;
}
int main() {
    string *arr = new string[4]; // 初始：包含 4 个 string 的数组
    arr = enlarge(arr, 4, 6); // 将 arr 扩大到 6 个元素。
}
```

示例中所示的过程也有几个缺点：

- 新数组需要调用新的构造函数；
- 在新数组中初始化字符串后，它们的旧大小 `oldsize` 立即被重新赋值为原始数组中对应的值；
- 旧数组中的所有对象都会被销毁。

根据具体情况，存在各种解决方案来提高这种相当低效过程的效率。可以使用指针数组（仅需拷贝指针，不需要析构，不需要多余的初始化），或者可以使用原始内存结合放置性 new 运算符（对象数组保持可用，不需要析构，不需要多余的构造）。

#### 9.1.4 管理“原始”内存

正如我们所见的，`operator new` 为对象分配内存，并随后通过调用其中一个构造函数对其进行初始化。同样，`operator delete` 调用对象的析构函数，并随后将 `operator new` 分配的内存返回到公共池。

## 9. 运算符 'NEW' 和 'DELETE'

在下一节中，我们将遇到 `new` 的另一种用法，它允许我们在所谓的“原始内存”中初始化对象：这种内存仅由通过静态或动态分配提供的字节组成。

原始内存通过 `operator new(sizeInBytes)` 和 `operator new[](size)` 提供。返回的内存不应被解释为任何类型的数组，而只是一系列动态可用的内存位置。这些 `new` 的变体不会进行任何初始化。

这两个变体都返回 `void *`；使用某些类型的内存返回值时需要 `static_cast`。

这里有两个示例：

```cpp
int *ip = static_cast<int *>(operator new(5 * sizeof(int)));
// 与上例相同：
int *ip2 = static_cast<int *>(operator new[](5 * sizeof(int)));
// 5 个 string 的内存：
string *sp = static_cast<string *>(operator new(5 * sizeof(string)));
```

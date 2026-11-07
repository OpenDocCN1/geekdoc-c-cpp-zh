
## 基于范围的 for 循环

基于范围的 for 循环（在第5章“循环和关系表达式”以及第16章中讨论）简化了为内置数组以及具有标识范围的 begin() 和 end() 方法的类（例如 std::string 和 STL 容器）编写循环的过程。该循环对数组或容器中的每个元素应用指定的操作：

```cpp
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices)
    std::cout << x << std::endl;
```

这里，x 依次取 prices 中每个元素的值。x 的类型应与数组元素的类型匹配。一种更简单、更安全的方法是使用 auto 声明 x；编译器将从 prices 声明中的信息推导出类型：

```cpp
double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (auto x : prices)
    std::cout << x << std::endl;
```

如果你的意图是让循环修改数组或容器中的元素，请使用引用类型：

```cpp
std::vector<int> vi(6);
for (auto & x : vi)          // use a reference if loop alters contents
    x = std::rand();
```

## 新的 STL 容器

C++11 将 forward_list、unordered_map、unordered_multimap、unordered_set 和 unordered_multiset 添加到其 STL 容器集合中（见第16章）。forward_list 容器是一个只能单向遍历的单向链表；它比双向链表容器更简单，也更节省空间。另外四个容器支持实现哈希表。

C++11 还添加了 array 模板（在第4章“复合类型”和第16章中讨论），使用它需要指定元素类型和固定的元素数量：

```cpp
std::array<int, 360> ar;    // array of 360 ints
```

这个模板类并不满足所有常见的模板要求。例如，由于大小是固定的，你不能使用任何会改变容器大小的方法，例如 push_back()。但 array 确实具有 begin() 和 end() 方法，这使你可以对 array 对象使用许多基于范围的 STL 算法。

## 新的 STL 方法

C++11 将 cbegin() 和 cend() 添加到 STL 方法列表中。与 begin() 和 end() 一样，这些新方法返回指向容器第一个元素和最后一个元素之后位置的迭代器，从而指定一个包含所有元素的范围。此外，这些新方法将元素视为 `const`。类似地，`crbegin()` 和 `crend()` 是 `rbegin()` 和 `rend()` 的 `const` 版本。

更重要的是，除了传统的复制构造函数和常规赋值运算符之外，STL 容器现在还拥有移动构造函数和移动赋值运算符。本章稍后将描述移动语义。

### valarray 升级

`valarray` 模板是独立于 STL 开发的，其原始设计阻止了将基于范围的 STL 算法用于 `valarray` 对象。C++11 添加了两个函数 `begin()` 和 `end()`，它们各自接受一个 `valarray` 参数。它们返回指向 `valarray` 对象第一个元素和最后一个元素之后位置的迭代器，从而允许使用基于范围的 STL 算法（见第16章）。

### export 退出历史舞台

C++98 引入了 `export` 关键字，希望创造一种将模板定义分离到接口文件和实现文件中的方法，接口文件包含原型和模板声明，实现文件包含模板函数和方法定义。事实证明这并不切实际，C++11 结束了 `export` 的这一角色。然而，标准仍保留 `export` 作为关键字，以备将来可能使用。

### 尖括号

为了避免与 `>>` 运算符混淆，C++ 曾要求在嵌套模板声明的括号之间加一个空格：

```cpp
std::vector<std::list<int> > vl; // > not ok
```

C++11 移除了该要求：

```cpp
std::vector<std::list<int>> vl; // >> ok in C++11
```

### *右值*引用

传统的 C++ 引用现在称为*左值引用*，它将标识符绑定到左值。左值是一种表达式，例如变量名或解引用的指针，它表示程序可以获取其地址的数据。最初，左值是可以出现在赋值语句左侧的表达式，但 `const` 修饰符的出现允许了不能赋值但仍可寻址的构造：

```cpp
int n;
int * pt = new int;
const int b = 101; // can't assign to b, but &b is valid
int & rn = n;       // n identifies datum at address &n
int & rt = *pt;     // *pt identifies datum at address pt
const int & rb = b; // b identifies const datum at address &b
```

C++11 添加了右值引用（在第8章中讨论），使用 `&&` 表示，它可以绑定到右值——也就是可以出现在赋值表达式右侧、但不能对其应用地址运算符的值。示例包括字面常量（C 风格字符串除外，它们会求值为地址）、诸如 x+y 的表达式，以及函数返回值（前提是该函数不返回引用）：

```cpp
int x = 10;
int y = 23;
int && r1 = 13;
int && r2 = x + y;
double && r3 = std::sqrt(2.0);
```

注意，r2 真正绑定的是 x + y 在当时求值得到的值。也就是说，r2 绑定到值 23，并且 r2 不受之后 x 或 y 变化的影响。

有趣的是，将右值绑定到右值引用会使该值存储在一个可以取地址的位置。也就是说，虽然你不能对 13 应用 & 运算符，但可以对 r1 应用它。正是这种将数据绑定到特定地址的机制，使得通过右值引用访问数据成为可能。

程序清单18.1提供了一个简短示例，说明关于右值引用的这些要点中的一部分。

### 程序清单18.1 rvref.cpp

```cpp
// rvref.cpp -- simple uses of rvalue references
#include <iostream>

inline double f(double tf) {return 5.0*(tf-32.0)/9.0;};
int main()
{
    using namespace std;
    double tc = 21.5;
    double && rd1 = 7.07;
    double && rd2 = 1.8 * tc + 32.0;
    double && rd3 = f(rd2);
    cout << " tc value and address: " << tc <<", " << &tc << endl;
    cout << "rd1 value and address: " << rd1 <<", " << &rd1 << endl;
    cout << "rd2 value and address: " << rd2 <<", " << &rd2 << endl;
    cout << "rd3 value and address: " << rd3 <<", " << &rd3 << endl;
    cin.get();
    return 0;
}
```

以下是一个示例输出：

```
tc value and address: 21.5, 002FF744
rd1 value and address: 7.07, 002FF728
rd2 value and address: 70.7, 002FF70C
rd3 value and address: 21.5, 002FF6F0
```

引入右值引用的主要原因之一是实现移动语义，这是本章的下一个主题。

## 移动语义与右值引用

现在让我们继续讨论尚未讨论的主题。C++11 启用了一种称为*移动语义*的技术。这会引出一些问题，例如什么是移动语义、C++11 如何启用它们，以及为什么我们需要它们？我们将从最后一个问题开始。

### 移动语义的必要性

让我们考察一下 C++11 之前的复制过程是如何工作的。假设我们从类似下面的代码开始：

```cpp
vector<string> vstr;
// build up a vector of 20,000 strings, each of 1000 characters
...
vector<string> vstr_copy1(vstr);  // make vstr_copy1 a copy of vstr
```

vector 类和 string 类都使用动态内存分配，因此它们会定义使用某种形式的 new 的复制构造函数。为了初始化 vstr_copy1 对象，vector<string> 复制构造函数将使用 new 为 20,000 个 string 对象分配内存，而每个 string 对象又会调用 string 复制构造函数，后者将使用 new 为 1000 个字符分配内存。然后，全部 20,000,000 个字符将从 vstr 控制的内存复制到 vstr_copy1 控制的内存。这是大量的工作，但如果必须完成，那就必须完成。

但它“必须完成”吗？有时答案是否定的。例如，假设我们有一个返回 vector<string> 对象的函数：

```cpp
vector<string> allcaps(const vector<string> & vs)
{
    vector<string> temp;
    // code that stores an all-uppercase version of vs in temp
    return temp;
}
```

接下来，假设我们这样使用它：

```cpp
vector<string> vstr;
// build up a vector of 20,000 strings, each of 1000 characters
vector<string> vstr_copy1(vstr);          // #1
vector<string> vstr_copy2(allcaps(vstr));  // #2
```

从表面上看，语句 #1 和 #2 相似；它们都使用一个现有对象来初始化一个新的 vector<string> 对象。如果我们按字面理解这段代码，allcaps() 会创建一个管理 20,000,000 个字符的 temp 对象，vector 和 string 复制构造函数会费力地创建一个包含 20,000,000 个字符的副本，然后程序

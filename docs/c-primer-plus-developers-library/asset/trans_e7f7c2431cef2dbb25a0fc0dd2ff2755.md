
如果你对Swap()做类似的操作呢？

```cpp
    int m = 5;
    double x = 14.3;
    Swap<double>(m, x);  // almost works
```

这会为double类型生成一个显式实例化。不幸的是，在这种情况下，代码不会工作，因为第一个形参是double &类型，不能引用int类型的变量m。

隐式实例化、显式实例化和显式特化统称为特化。它们的共同点是，它们都表示使用了特定类型的函数定义，而不是通用描述。

显式实例化的引入带来了声明中使用template和template <>前缀的新语法，以区分显式实例化和显式特化。正如许多其他情况一样，做更多事情的成本是更多的语法规则。以下片段总结了这些概念：

```cpp
    ...
    template <class T>
    void Swap (T &, T &);   // template prototype

    template <> void Swap<job>(job &, job &);   // explicit specialization for job
    int main(void)
    {
        template void Swap<char>(char &, char &); // explicit instantiation for char
        short a, b;
        ...
        Swap(a,b);   // implicit template instantiation for short
        job n, m;
        ...
        Swap(n, m);  // use explicit specialization for job
        char g, h;
        ...
        Swap(g, h);  // use explicit template instantiation for char
        ...
    }
```

当编译器到达char的显式实例化时，它使用模板定义生成Swap()的char版本。对于Swap()的其余使用，编译器将模板与函数调用中使用的实际参数匹配。例如，当编译器到达函数调用Swap(a,b)时，它生成一个Swap()的short版本，因为这两个参数是short类型。当编译器到达Swap(n,m)时，它使用为job类型提供的单独定义（显式特化）。当编译器到达Swap(g,h)时，它使用在处理显式实例化时已经生成的模板特化。

## 编译器会选择哪个函数版本？

由于函数重载、函数模板和函数模板重载的存在，C++需要并且确实有一个明确的策略来决定函数调用使用哪个函数定义，尤其是在有多个参数的情况下。这个过程称为*重载解析*。详细描述完整的策略需要一小章的篇幅，所以我们只大致看看这个过程是如何工作的：

-   **阶段1**——收集候选函数列表。这些是与被调用函数同名的函数和模板函数。
-   **阶段2**——从候选函数中收集可行函数列表。这些是参数数量正确的函数，并且存在隐式转换序列，包括每个实际参数类型与相应形式参数类型完全匹配的情况。例如，一个带有`float`类型参数的函数调用可以将该值转换为`double`以匹配`double`类型的形参，而模板可以为`float`生成实例化。
-   **阶段3**——确定是否存在最佳可行函数。如果存在，则使用该函数。否则，函数调用是一个错误。

考虑一个只有一个函数参数的情况——例如，下面的调用：

```cpp
may('B');    // actual argument is type char
```

首先，编译器会搜罗候选者，即名为`may()`的函数和函数模板。然后，它会找出那些可以用一个参数调用的函数。例如，下面这些就符合要求，因为它们有相同的名字，并且可以用一个参数调用：

```cpp
void may(int);                              // #1
float may(float, float = 3);                // #2
void may(char);                             // #3
char * may(const char *);                   // #4
char may(const char &);                     // #5
template<class T> void may(const T &);      // #6
template<class T> void may(T *);            // #7
```

注意，这里只考虑签名，而不考虑返回类型。然而，这些候选中（#4和#7）有两个不可行，因为整型不能隐式转换（即没有显式类型转换）为指针类型。剩下的模板是可行的，因为它可以用来生成一个特化，其中`T`被当作`char`类型。这样就剩下五个可行函数，每个函数如果单独声明的话都可以使用。

接下来，编译器必须确定哪个可行函数是最佳的。它会查看使函数调用参数与可行候选参数匹配所需的转换。一般来说，从最佳到最差的排名如下：

-   **1.** 完全匹配，普通函数优于模板
-   **2.** 提升转换（例如，char和short到int的自动转换，以及float到double的自动转换）
-   **3.** 标准转换（例如，将int转换为char或将long转换为double）
-   **4.** 用户定义的转换，例如类声明中定义的转换

例如，函数#1优于函数#2，因为char到int的转换是提升转换（参见第3章“处理数据”），而char到float是标准转换（参见第3章）。函数#3、#5和#6优于#1或#2，因为它们是完全匹配。函数#3和#5都优于#6，因为#6是模板。这一分析引发了几个问题。什么是完全匹配？如果出现两个完全匹配（如#3和#5）会发生什么？通常，如此例中的情况，两个完全匹配是一个错误；但有一些特殊情况是此规则的例外。显然，我们需要进一步调查此事！

## 完全匹配与最佳匹配

C++允许在进行完全匹配时进行一些“平凡转换”。表8.1列出了这些转换，其中Type代表某种任意类型。例如，int实际参数与int &形式参数是完全匹配。注意Type可以是类似于char &的类型，因此这些规则包括将char &转换为const char &。Type (argument-list)条目意味着，只要函数名作为实际参数与函数指针作为形式参数具有相同的返回类型和参数列表，它们就是匹配的。（回顾第7章中的函数指针。还要记住，你可以将函数名作为参数传递给期望函数指针的函数。）我们将在第9章后面讨论volatile关键字。

**表8.1 — 完全匹配允许的平凡转换**

| 实际参数 | 形式参数 |
|---|---|
| Type | Type & |
| Type & | Type |
| Type [] | Type * |
| Type (argument-list) | Type (*) (argument-list) |
| const Type | const Type |
| Type | volatile Type |
| Type * | const Type * |
| Type * | volatile Type * |

假设包含这些模板的程序还包含以下代码：

```cpp
struct blot {int a; char b[10];};
blot ink = {25, "spots"};
...
recycle(&ink);  // address of a structure
```

recycle(&ink)调用匹配模板#1，其中类型被解释为blot *。recycle(&ink)函数调用也匹配模板#2，这次Type为blot类型。这种组合将两个隐式实例化，recycle<blot *>(blot *)和recycle<blot>(blot *)，送入可行函数池。

在这两个模板函数中，recycle<blot *>(blot *)被认为更特化，因为它在生成时经历了更少的转换。也就是说，模板#2已经明确说明函数参数是指向Type的指针，因此Type可以直接与blot对应。然而，模板#1将Type作为函数参数，因此必须将Type解释为指向blot的指针。也就是说，在模板#2中，Type已经被特化为指针，因此它“更特化”。

用于查找最特化模板的规则称为函数模板的偏序规则。与显式实例化一样，它们是C++98对C++语言的补充。

## 一个偏序规则示例

让我们检查一个完整的程序，该程序使用偏序规则来确定使用哪个模板定义。程序清单8.14有两个用于显示数组内容的模板定义。第一个定义（模板A）假定作为参数传递的数组包含要显示的数据。第二个定义（模板B）假定数组元素是指向要显示的数据的指针。

**程序清单8.14** `tempover.cpp`

```cpp
// tempover.cpp -- template overloading
#include <iostream>

template <typename T>             // template A
void ShowArray(T arr[], int n);

template <typename T>             // template B
void ShowArray(T * arr[], int n);

struct debts
{
    char name[50];
    double amount;
};

int main()
```

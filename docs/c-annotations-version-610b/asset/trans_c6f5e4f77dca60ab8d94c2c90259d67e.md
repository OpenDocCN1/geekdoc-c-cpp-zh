

程序中源代码里模板被实例化的位置称为其*实例化点*。在实例化点，编译器推导出模板参数的实际类型。此时，它会检查模板中依赖于模板类型参数的语句的语法正确性。这意味着编译器*仅在实例化点*才必须看到所需的声明。通常的经验法则是，你应该确保编译器在模板的每个实例化点都已经读取了所有必需的声明（通常是头文件）。对于模板定义本身，可以提出一个更宽松的要求。当读取定义时，只需提供那些*不*依赖于模板类型参数的语句所需的声明。

## 20.14 函数选择机制

当编译器遇到函数调用时，如果有多个重载函数可用，它必须决定调用哪一个。之前我们已经遇到过诸如“选择最具体的函数”这样的原则。这是对编译器函数选择机制的一个相当直观的描述。在本节中，我们将仔细研究这一机制。

假设我们要求编译器编译下面的 `main` 函数：

```cpp
int main()
{
    process(3, 3);
}
```

进一步假设编译器在即将编译 `main` 时已经遇到了以下函数声明：

```cpp
template <class T>
void process(T &t1, int i);                  // 1

template <class T1, class T2>
void process(T1 const &t1, T2 const &t2);    // 2

template <class T>
void process(T const &t, double d);         // 3

template <class T>
void process(T const &t, int i);            // 4

template <>
void process<int, int>(int i1, int i2);     // 5

void process(int i1, int i2);               // 6

void process(int i, double d);              // 7

void process(double d, int i);              // 8

void process(double d1, double d2);         // 9

void process(std::string s, int i);          // 10

int add(int, int);                           // 11
```

编译器在读取了 `main` 的语句后，现在必须决定实际上应该调用哪个函数。其步骤如下：

-   首先，构造一个*候选函数*集合。该集合包含所有满足以下条件的函数：
    -   在调用点可见；
    -   与被调用函数同名。

    由于函数 11 名称不同，它被移出集合。编译器剩下的是一组 10 个候选函数。

-   其次，构造*可行函数*集合。可行函数是指存在可应用的类型转换、使得函数形参类型与实参类型相匹配的函数。

    这意味着至少实参的数量必须与可行函数的形参数量匹配。函数 10 的第一个实参是 `string`。由于 `string` 不能用 `int` 值初始化，因此不存在合适的转换，函数 10 从候选函数列表中被移除。`double` 参数可以保留。确实存在从 `int` 到 `double` 的标准转换，所以所有具有普通 `double` 参数的函数都可以保留。因此，可行函数集合由函数 1 到 9 组成。

此时，编译器尝试确定模板类型参数的类型。这一步骤将在下一小节中概述。

## 20.15 确定模板类型参数

在确定了候选函数集合，并从中确定可行函数集合之后，编译器现在必须确定模板类型参数的实际类型。

在尝试将实际类型与模板类型参数匹配时，它可以使用三种标准模板参数转换过程中的任何一种（参见第 20.4 节）。在这个过程中，它得出结论：对于函数 1 的参数 `T &t1`，无法确定类型 T，因为实参 3 是一个常量 int 值。因此，函数 1 从可行函数列表中被移除。编译器现在面对的是以下一组可能被实例化的函数模板和普通函数：

```cpp
void process(T1 [≡ int] const &t1, T2 [≡ int] const &t2);    // 2
void process(T [≡ int] const &t, double d);                  // 3
void process(T [≡ int] const &t, int i);                     // 4
void process<int, int>(int i1, int i2);                      // 5
void process(int i1, int i2);                                // 6
void process(int i, double d);                               // 7
void process(double d, int i);                               // 8
void process(double d1, double d2);                          // 9
```

编译器为每个可行函数关联一个*直接匹配计数*值。直接匹配计数统计的是无需自动类型转换即可与函数参数匹配的参数个数。例如，函数 2 的计数为 2，函数 7 的计数为 1，函数 9 的计数为 0。现在，函数按照其直接匹配计数值进行（递减）排序：

| 函数 | 匹配计数 |
|---|---|
| `void process(T1 [≡ int] const &t1, T2 [≡ int] const &t2); // 2` | 2 |
| `void process(T [≡ int] const &t, int i); // 4` | 2 |
| `void process<int, int>(int i1, int i2); // 5` | 2 |
| `void process(int i1, int i2); // 6` | 2 |
| `void process(T [≡ int] const &t, double d); // 3` | 1 |
| `void process(int i, double d); // 7` | 1 |
| `void process(double d, int i); // 8` | 1 |
| `void process(double d1, double d2); // 9` | 0 |

如果最高值不存在并列，则选择相应的函数，函数选择过程完成。

当多个函数出现在最高位时，编译器会验证是否遇到了歧义。如果（不）需要类型转换的参数序列不同，就会遇到歧义。以函数 3 和 8 为例。用 D 表示“直接匹配”，C 表示“转换”，那么实参对函数 3 的匹配为 D,C，对函数 8 的匹配为 C,D。假设函数 2、4、5 和 6 不可用，那么编译器将报告歧义，因为函数 3 和 8 的实参/参数匹配过程序列不同。比较函数 7 和 8 时也会遇到同样的差异，但比较函数 3 和 7 时不会遇到这样的差异。

此时，最高值出现并列，编译器继续处理相关函数的子集（函数 2、4、5 和 6）。对于这些函数中的每一个，都关联一个“普通参数计数”，用于统计函数中非模板参数的数量。函数按照此计数进行递减排序，结果如下：

| 函数 | 普通参数计数 |
|---|---|
| `void process(int i1, int i2); // 6` | 2 |
| `void process(T [= int] const &t, int i); // 4` | 1 |
| `void process(T1 [= int] const &t1, T2 [= int] const &t2); // 2` | 0 |
| `void process<int, int>(int i1, int i2); // 5` | 0 |

现在最高值没有并列。选择相应的函数（`process(int, int)`，函数 6），函数选择过程完成。函数 6 将用于 `main` 的函数调用语句。

如果函数 6 没有被定义，那么将使用函数 4。假设函数 4 和函数 6 都没有被定义，那么选择过程将继续处理函数 2 和 5：

| 函数 | 普通参数计数 |
|---|---|
| `void process(T1 [= int] const &t1, T2 [= int] const &t2); // 2` | 0 |
| `void process<int, int>(int i1, int i2); // 5` | 0 |

在这种情况下，再次出现并列，选择过程继续。对于具有最高普通参数计数的每个函数，关联一个“函数类型”值，这些函数按照其函数类型值进行递减排序。值 2 关联到普通函数，值 1 关联到模板显式特化，值 0 关联到普通函数模板。

如果最高值没有并列，则选择相应的函数，函数选择过程完成。如果出现并列，编译器报告歧义并且无法确定要调用哪个函数。假设只存在函数 2 和 5，那么此选择步骤将产生以下排序：

| 函数 | 函数类型 |
|---|---|
| `void process<int, int>(int i1, int i2); // 5` | 1 |
| `void process(T1 [= int] const &t1, T2 [= int] const &t2); // 2` | 0 |

函数 5，即模板显式特化，将会被选中。以下是函数模板选择机制的总结（参见图 **20.1**）：

-   构造候选函数集合：函数名相同；
-   构造可行函数集合：参数数量正确且存在可用的类型转换；
-   确定模板类型，丢弃无法确定其类型参数的模板；


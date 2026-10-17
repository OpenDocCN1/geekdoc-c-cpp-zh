
就足够了。处理 `iosfwd` 所需的时间仅处理 `string` 和 `istream` 头文件的一部分。

### 21.5.1 实例化声明

如果声明函数模板可以加速程序的编译和链接阶段，那么我们该如何确保在程序最终链接在一起时，函数模板所需的实例化是可用的呢？

为此可以使用模板声明的一种变体，即所谓的显式实例化（explicit declaration）。一个显式实例化声明由以下元素组成：

- 它以 `template` 关键字开头，省略模板参数列表。
- 接下来指定函数的返回类型和名称。
- 函数名后跟着一个类型指定列表。类型指定列表是一个用角括号括起来的类型名称列表。每个类型指定了模板参数列表中对应模板参数的实际类型。
- 最后指定函数的参数列表，并以分号结束。

尽管这是一个声明，但编译器将其理解为对实例化该函数模板的特定变体的请求。

使用显式实例化声明，可以将程序所需的所有模板函数实例化收集在一个文件中。该文件应该是一个普通的源文件，它应该包含模板头文件，随后指定所需的实例化声明。由于它是源文件，因此不会被其他源文件包含。一旦包含了所需的头文件，就可以安全地使用 `namespace` 声明。下面的示例展示了我们之前的 `add` 函数模板所需的实例化，针对 `double`、`int` 和 `std::string` 类型进行了实例化：

```cpp
#include "add.h"

#include <string>

using namespace std;

template int add<int>(const int &lhs, const int &rhs);

template double add<double>(double const &lhs, double const &rhs);

template string add<string>(string const &lhs, string const &rhs);
```

如果我们疏忽忘记提到程序所需的实例化，通过向列表中添加缺失的实例化声明即可轻松修复。重新编译文件并重新链接后，工作就完成了。

## 21.6 实例化函数模板

与编译器读取其定义后就会生成代码的普通函数不同，模板在读取其定义时并不会实例化。模板仅仅是一份配方，告诉编译器在需要时如何创建特定的代码。它非常像烹饪书中的配方。阅读如何烘蛋糕并不意味着你在读完配方时已经烘焙了蛋糕。

那么，函数模板实际上被实例化了吗？编译器在两种情况下决定实例化模板：

- 它们在被使用时被实例化（例如，用一对 `size_t` 值调用函数 `add`）；
- 当获取函数模板的地址时，它们会被实例化。

```cpp
char (*addptr)(const char &, const char &) = add;
```

导致编译器实例化模板的语句的位置称为模板的实例化点（point of instantiation）。实例化点对函数模板的代码有深远影响。这些影响将在第 21.13 节中讨论。

编译器并不总是能够无歧地推导出模板的类型。编译器会报告可能由软件工程师解决歧义。考虑以下代码：

```cpp
#include <iostream>

#include "add.h"

size_t fun((f)int *p, size_t n);

double fun(double((f)double *p, size_t n));

int main() {

{
  std::cout << fun(add);
}
```

### 21.6.2 实例化函数模板

当编译这个小程序时，编译器报告了一个它无法解决的歧义。它有两个候选函数，因为对于每个重载版本的 `fun`，`add` 函数都可以被实例化：

```
error: call of overloaded 'fun(<unknown type>' is ambiguous

candidate are: int fun(size_t (int*, size_t)

note: double fun(double) (double*, size_t)
```

这种情况应该被避免。如果没有歧义，函数模板是可以被实例化的。当多个函数从编译器的选择机制中涌现时，就会产生歧义（参见第 21.14 节）。解决歧义取决于我们。它们可以通过以下方式消除歧义（这在第 21.7 节中解释了这一点）：

```cpp
#include <iostream>

#include "add.h"

size_t fun(int *p, size_t n);

double fun(double *p, size_t n);

int main() {

{
  std::cout << fun(add<int>);
}
```

（注：原文代码中 `(f)int` 似乎有笔误，此处按意图理解为类型强制）

但是，尽可能避免这种转换是良好的做法。这样做将在下一节（21.7）中解释。

## 21.7. 使用显式模板类型

从我们的实验中，我们可以得出结论：链接器确实会从最终程序中移除相同的模板实例化。此外，我们得出结论，使用更多的模板声明不会导致模板的实例化。

## 21.7 使用显式模板类型

在上一节中，我们看到编译器在尝试实例化模板时可能会遇到歧义。在一个示例中，存在多个重载版本的函数（`fun`）以及已有的参数类型。这种歧义源于这样一个事实：这两个参数都可以由函数模板的实例化来提供。解决此类歧义的直观方法是使用 `static_cast`。但应该尽可能避免使用这种方法。

对于函数模板，可以使用显式模板参数来避免使用强制类型转换（casts）。使用显式模板参数的作用是告诉编译器在实例化模板时应该使用哪些类型。要使用显式模板参数，在函数名后紧跟一个实际的模板参数列表，之后可以是函数的参数列表。实际模板参数列表中意指的实际类型被编译器用于“推断”在实例化模板时使用什么类型。这里是之前一节的示例，现在改用显式模板类型参数。

```cpp
#include <iostream>

#include "add.h"

int (*f)(int const &lhs, int const &rhs);

double fun(double (*f)(double const &lhs, double const &rhs));

int main() {

  std::cout << fun(add<int>()) << '\n';
}
```

在编译器无法检测应该使用哪些类型的情况下，可以使用显式模板类型。例如，在 21.4 节定义了函数模板 `Type fun()`。为了为 `double` 类型实例化该函数，我们可以调用 `fun<double>()`。

## 21.8 重载函数模板

让我们回到 `add` 模板。该模板的设计目的是返回两个实体的和。如果我们想计算三个实体的和，可以写成：

```cpp
int main() {

  add(2, 3, 4);
}
```

对于偶尔出现的情况，这是一个可以的方案。然而，如果我们经常需要加三个实体，那么一个期望三个参数的 `add` 函数重载版本可能是一个非常有用的函数。这个问题有一个简单的解决方案：函数模板可以被重载。

要定义一个重载函数模板，只需在其头文件中放置该模板的多个定义。对于 `add` 函数，这将归纳为：

```cpp
template <typename Type>

Type add(const Type &lhs, Type const &rhs)

{

    return lhs + rhs;

}

template <typename Type>

Type add(const Type &lhs, Type const &mid, Type const &rhs)

{

    return lhs + mid + rhs;

}
```

重载函数不必非用简单的值来定义。像所有重载函数一样，一组唯一的参数就足够定义一个重载函数模板了。例如，这里有一个可以计算 `vector` 元素和的重载版本：

```cpp
template <typename Type>

Type add(std::vector<Type> const &vect)

{

    return accumulate(vect.begin(), vect.end(), Type(0));

}
```

在重载函数模板时，我们不需要局限于函数的参数列表。模板的参数列表本身也可以被重载。`add` 模板允许我们提供 `vector` 作为其第一个参数，但也可以 `deque` 或 `map`。可以为这些类型的容器构建重载版本，但我们应该做到到什么程度呢？如果我们可能基于这些共同特征定义一个重载函数模板。我们发现上述容器的一个共同特征是，它们都支持 `begin` 和 `end`，并返回迭代器。利用这一点，我们可以定义一个代表必须支持这些方法的容器的模板参数。但提到“容器”类型并没有告诉我们容器的数据类型是什么，从而对模板进行了重载。以下是 `add` 模板的结果版本：

```cpp
template <typename Container, typename Type>

Type add(Container const cont, Type const &init)

{

    return std::accumulate(cont.begin(), cont.end(), init);

}
```

人们可能会想 `init` 参数是否可以排除在参数列表中，因为 `init` 通常有一个默认初始化值。答案是“肯定的”，但存在复杂性。可以如下所示定义 `add` 函数：

```cpp
template <typename Type, typename Container>

Type add(Container const &cont)

{

    return std::accumulate(cont.begin(), cont.end(), Type(0));

}
```

但注意，模板的类型参数被重新排序了，这是必要的，因为编译器无法在如下调用中确定 `Type`：

```cpp
int x = add(vectorOfInts);
```

在重新排序类型参数并将 `Type` 放在第一个后，可以为第一个模板参数提供显式的模板类型参数：

```cpp
int x = add<int>(vectorOfInts);
```

在这个示例中，我们提供了一个 `vector<int>` 参数。人们可能会奇怪为什么必须明确指定 `int` 以允许编译器确定模板参数 `Type`。事实上，我们不需要。存在第三种模板参数，模板模板参数（template template parameter），允许编译器直接从实际容器确定 `Type`。模板模板参数在 23.4 节中讨论。

### 21.8.1 使用重载函数模板的示例

在有了这些重载版本后，我们现在可以启动编译器编译以下函数：

```cpp
using namespace std;

int main() {

    vector<int> v;

    add(3, 4);      // 1

    add(v);         // 2

    add(v, 0);      // 3

}
```

- 在语句 1 中，编译器识别出两个类型，都是 `int`。它实例化了第一个定义。
- 在语句 2 中，编译器找到了单个参数。因此，编译器寻找需要一个参数的重载版本。它找到了模板定义。
- 在语句 3 中，编译器遇到了不同的类型。然而，参数的类型并不相等，所以 `add` 模板支持不同的结尾。它实例化了最后一个定义。

### 21.8.2 重载函数模板时的歧义

虽然可以定义另一个函数模板，但这引入了歧义，因为编译器无法确定应该使用哪一个定义两个不同参数的重载版本。例如定义：

```cpp
#include "add.h"

template <typename T1, typename T2>

T1 add(const T1 const &lhs, T2 const &rhs)

{

    return lhs + rhs;

}

int main()

{

    add(3, 4.5);

}
```

编译器报告了如下歧义：

```
error: call of 'add(int, double)' is ambiguous

error: candidates are: Type add(const Container&, Type&)

    [with Container = int, Type = double]

error: T1 add(const T1, T2&)

    [with T1 = int, T2 = double]
```

现在回想接受三个参数的重载函数模板：

```cpp
template <typename Type>

add(const Type &lhs, Type const &mvalue, Type const &rhs)

{

    return lhs + mvalue + rhs;

}
```

人们可能认为，只接受相同类型的参数（三个 `int`、三个 `double` 等）是一个缺点。为了解决这个问题，我们定义了另一个重载函数模板，该模板只有在实际使用的类型之间定义了 `operator+` 时才能，但除此之外似乎没有问题。接受任何类型参数的重载版本：

```cpp
template <typename Type1, typename Type2, typename Type3>

add(Type1 const &lhs, Type2 const &mid, Type3 const &rhs)

{

    return lhs + mid + rhs;

}
```

现在我们定义了上述期望三个参数的重载函数模板，如下调用：

```cpp
add(1, 2, 3);
```

我们应该在这里遇到歧义吗？之后，编译器可能会选择前面的函数，推断出 `Type1 == int`，但它也可能选择后面的函数，推断出 `Type2 == int` 和 `Type3 == int`。令人惊讶的是，编译器没有报告歧义。

## 21.9. 为偏离类型特化模板

由于以下原因，没有报告歧义。如果使用较少和更多的特化模板参数定义了重载模板函数（例如：较少特化：全部不同 vs 更多特化：所有类型相等），那么编译器将尽可能选择更特化的函数。

从经验法则上来说：重载函数模板必须允许模板类型参数的唯一组合，以防止在选择重载函数模板进行实例化时产生歧义。函数模板参数列表中列表中类型参数的顺序并不重要。例如，尝试实例化以下函数模板中的一个会导致歧义：

```
template <typename T1, typename T2>

void binarg(T1 const &first, T2 const &second)

{}

template <typename T1, typename T2>

void binarg(T2 const &first, T1 const &second)

{}
```

这不应该让人意外。毕竟，模板类型参数只是形式名称。名称（`T1`、`T2` 或其他名称）没有具体的含义。

### 21.8.3 声明重载函数模板

像任何函数一样，重载函数可以使用普通声明或实例化声明来声明。也可以使用显式模板参数类型：

- 声明一个接受特定容器的函数模板：

```
template <typename Container, typename Type>

Type add(Container const &container, Type const &init);
```

- 使用实例化声明（编译器可能已经见过该模板的定义）：

```
template int add(std::vector<int>, int)

(std::vector<int> const &vector, int const &init);
```

- 使用显式模板类型：

```cpp
std::vector<int> vi;

int sum = add<std::vector<int>, int>(vi, 0);
```

### 21.9 为偏离类型特化模板

定义两个相同类型参数的初始 `add` 模板适用于所有支持 `operator+` 和拷贝构造函数的类型。然而，这些假设并不总是满足。例如，对于 `char *`，使用 `operator+` 或“拷贝构造函数”是有意义的。编译器尝试实例化函数模板，但编译失败，因为为指针没有定义 `operator+`。

在这些情况下，编译器可能解析模板参数，但（或我们……）可能会检测到标准实现毫无意义或会产生错误。

## 第 21 章 函数和变量模板

为了解决这个问题，可以定义一个模板显式特化。模板显式特化使用实际的模板类型参数为已经存在的通用定义定义函数。正如我们在上一节中看到的，编译器倾向于选择更特化的函数而不是较少特化的函数。因此，将尽可能选择模板显式特化。

模板显式特化为其模板类型参数（或参数）提供特化版本。特殊类型替换了模板代码中的类型参数。例如，如果模板定义中显式特化的类型是 `char const *`：

```
template <typename Type>

Type add(Type const &lhs, Type const &rhs)

{

    return lhs + rhs;

}
```

`Type` 必须被替换为 `char const *`，导致函数具有如下原型：

```cpp
char const *add(char const *const &lhs, char const *const &rhs);
```

现在我们尝试使用这个函数：

```cpp
int main(int argc, char **argv)

{

    add(argv[0], argv[1]);

}
```

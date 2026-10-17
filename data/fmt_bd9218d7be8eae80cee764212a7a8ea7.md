
请注意，即使 **CallOption** 没有实现任何接口，代码仍然可以运行。重要的是它拥有的方法，而不是它实现的接口。例如，**BlackScholesModel** 没有实现任何特定接口，我们只是假设传递给我们模板函数的模型类具有 **generateRiskNeutralPricePath** 方法。

与使用多态性给出的解决方案相比，此解决方案可能看起来更简单。然而，它存在几个严重的问题。

- 你需要编写清晰的文档来说明如何使用你的模板类。在这些文档中，你需要列出你期望在模板参数类中存在的所有函数及其返回类型。相比之下，接口类会自动记录这些信息。此外，编译器会检查接口是否正确。
- 所有代码必须放在头文件中。这使得封装更具挑战性，并增加了文件之间的耦合。一个实际的后果是，你的代码构建时间会更长。
- 当你在模板中犯错时出现的编译器错误消息非常令人困惑。特别是，编译器通常会告诉你错误在库文件中，而实际上错误在你的代码中。参见练习 17.3.1 中的一个例子。
- 当你使用模板时，编译器只在模板实际被使用时才找到错误。而在面向对象中，错误在代码编写时就会被发现。

模板在成熟、稳定且经过仔细设计和文档化的库中效果很好，例如 C++ 标准库和 Boost。它们在与必须不断适应变化的业务需求的金融软件中效果较差。

### 练习

17.3.1. 修改我们模板示例库中的 `CallOption` 类，使 `payoff` 这个词拼写错误。编译器说哪个文件包含错误？

17.3.2. 编写一个模板类 `ComplexNumber`，它可以用来存储形式为 $x + iy$ 的复数，其中 $x$ 和 $y$ 都可以是 doubles、floats 或 ints。该类应有一个接受单个实数参数的构造函数和一个默认构造函数。应该能够使用 `+` 将两个复数相加。

17.3.3. 重写第 10.6 节中的积分示例，不使用多态性，而是使用模板。

## 17.4 总结

模板为“一次且仅一次”原则提供了解决方案，这对于编写数据结构类非常有用。另一方面，使用模板编写不必要的通用代码违反了 YAGNI 原则（你暂时不需要它）。

模板可以作为虚函数的替代方案，但虚函数通常是更好的方法。

对于金融数学问题，利用使用模板构建的库类是一个好主意，但应避免编写自己的模板库。

# 第 18 章

# 标准模板库

我们在第 13 章开发的 `Portfolio` 类只能用于存储单只股票的期权。这是一个重大限制。在本章中，我们希望增强我们的类，以便能够处理包含多只股票的市场。

为此，我们需要使用比向量和矩阵更有趣的数据结构。特别是，我们将使用一种称为 `map` 的数据结构，它允许你按某种键存储数据。例如，假设你编写了一个名为 `CompanyInfo` 的类，其中包含大量关于公司的实用信息，例如总部地址和董事姓名。然后，你将希望为每只股票存储一个 `CompanyInfo` 对象，以便仅通过关联股票名称就能快速查找 `CompanyInfo`。`map` 类允许你高效地做到这一点。

在练习 18.12.3 中，相同的理念将使你能够应对对我们的 `Portfolio` 类的另一项批评。如果 `Portfolio` 中的多个期权具有相同的到期日和基础股票，那么我们可以使用同一组市场模拟来一次性为所有这些期权定价。`map` 类允许你方便地对数据分组，因此是开发更复杂算法的有用工具。

C++ 具有许多内置数据结构。`map` 是一个，`vector` 也是一个。这些标准数据结构被称为*容器*。包含这些数据结构的完整库称为标准模板库 `STL`。之所以称为标准模板库，是因为所有这些数据结构都是使用模板编写的。

在本章中，我们将研究如何使用标准模板库，并查看标准模板库中的数据如何被用来对包含多只股票的市场进行建模。

## 18.1 typedef

我们已经看到，C++ 中的类型名称可能会变得非常长。例如，我们之前已经不得不处理 `PortfolioImpl` 类的以下成员变量。

```cpp
vector<shared_ptr<Priceable>> securities;
```

C++ 包含一些有助于处理长类型名称的特性。其中一个就是 `typedef`，我们现在将讨论它；另一个是 `auto`，我们将在下一节中讨论。

`typedef` 允许你为复杂类型定义缩写。例如，我们可以如下定义 `shared_ptr` 指向 `Priceable` 的缩写。

```cpp
typedef std::shared_ptr<Priceable> SPPriceable;
```

这种语法看起来像是在声明一个名为 `SPPriceable`、类型为 `shared_ptr<Priceable>` 的变量，只是前面多了个关键字 `typedef`。换句话说，其语法是：

```cpp
typedef <<复杂类型>> <<缩写名>>;
```

定义了这个缩写后，我们现在可以将成员变量 `securities` 的声明重写为：

```cpp
vector<SPPriceable> securities;
```

`typedef` 在减少输入量方面的优势显而易见。通过使代码更短，它也使其更具可读性。然而，过度使用 `typedef` 会使你的代码更难理解和调试。每个 `typedef` 的使用都为代码阅读者引入了额外的记忆负担。

就个人而言，我发现使用 `SP` 开头表示 `shared_ptr` 的类型命名约定既方便又容易记忆。我也使用前缀 `SPC` 来表示 `const` 指针，例如：

```cpp
typedef std::shared_ptr<const Priceable> SPCPriceable;
```

从现在开始，我们将不再评论地沿用这些约定，尽管它们并非 C++ 的标准约定。

除非你有如此清晰的约定，否则最好避免在头文件中的顶层放置 `typedef` 声明。这是因为这往往比帮助更大的是一种困惑。在 `cpp` 文件内部，你可以允许自己更多的自由，因为你只需要记住在该文件内使用的缩写。

一种替代方案是将 `typedef` 放在类声明内部。通过将 `typedef` 明确地与另一个类关联，通常可以使其含义更清晰。这样做时，你正在创建所谓的 *成员类型*。例如，我们可以在类 `Priceable` 中添加成员类型 `sp`，以便于引用指向 `Priceable` 的共享指针。然后我们可以使用它来添加成员类型 `spVec`，这使得引用指向 `Priceable` 的共享指针的向量变得更加容易。随后，我们将能够使用缩写 `Priceable::spVec` 在其他类中引用该类型，如下所示。

```cpp
class Priceable {
public:
   typedef shared_ptr<Priceable> sp;
   typedef vector< sp > spVec;
   // ... 更多代码 ...
};

class Portfolio {
private:
   Priceable::spVec securities;
   // ... 更多代码 ...
};
```

有一种替代语法，有时是必要的，以帮助编译器判断诸如 `Priceable::spVec` 这样的术语是指静态成员变量还是成员类型。替代语法只是在前面添加单词 `typename`。

```cpp
typename Priceable::spVec securities;
```

在处理模板时，包含 `typename` 是一个好习惯，以确保你的代码能够无歧义地编译。

拥有 `SPPriceable` 这样类型名称的约定与拥有名为 `sp` 的成员类型的约定之间没有太多实际区别。你应该遵循你正在工作的项目的约定。

成员类型在标准模板库中被大量使用。这并不是因为它们提供了方便的缩写，而是因为它们让你更容易编写模板函数。

假设你想编写一个模板化的 `sumVector` 函数，该函数接受某种数值向量并计算总和。我们希望该函数能够累加整数向量、实数向量、复数向量，甚至矩阵向量的值。

我们的模板函数将有一个模板参数 `V`，它将是某种向量类。我们的函数 `sumVector` 将接受类型为 `V` 的向量的引用作为其参数。但是它的返回类型是什么？返回类型将取决于 `V` 的类型。对于复数向量，返回类型应该是复数；对于实数向量，它应该是实数。如果我们只知道 `V`，如何推导返回类型？

解决方案是 C++ 中的向量拥有成员类型 `value_type`，其中仅包含我们需要的信息。因此，我们的 `sumVector` 函数的返回类型应该是 `V::value_type`。由于可能存在导致编译器问题的歧义，我们在处理模板时必须完整写成 `typename V::value_type`。

完整的 `sumVector` 函数代码如下：

```cpp
template <typename V>
typename V::value_type sumVector(const V& vector) {
    typename V::value_type total = 0;
    for (int i = 0; i < (int)vector.size(); i++) {
        total += vector[i];
    }
    return total;
}
```

## 18.2 auto

`auto` 关键字允许你在可以自动推导类型时避免键入类型的完整名称。例如，如果你想在类型为 `double` 的变量中存储函数的返回值，你可以使用 `auto`。在下面的代码中，编译器可以推断出 `s` 必须是 `double` 类型，因此我们可以使用 `auto`。

```cpp
double d = 4.0;
auto s = sqrt(d);
```

你可以将 `auto` 与 `&` 和 `const` 结合使用，以表明你是否想要数据的副本还是引用，以及你是否希望修改数据。以下是一些示例：

```cpp
vector<double> vec(10, 0.0);
auto& dRef = vec[5];
dRef = -1.0;
ASSERT(vec[5] == -1.0);
auto d = vec[6];
d = -1.0;
ASSERT(vec[6] == 0.0);
const auto& dRef2 = vec[7];
ASSERT(dRef2 == 0.0);
```

在这个例子中，我们利用了 `vector` 的 `[]` 运算符实际上返回向量中单元格的引用这一事实。因此 `dRef` 包含一个引用，可用于修改变量。另一方面，`d` 包含向量中数据的副本，因此不能用于修改变量。最后，`dRef2` 是一个引用，但是 `const` 的，所以它只能用于向量的读取访问。

这些示例相当刻意，因为 `auto` 在输入速度上仅略快于 `double`。然而，如下面所示，`auto` 关键字可以节省大量的输入和脑力。你应该在代码中广泛使用它。

## 18.3 在向量中使用迭代器

到目前为止，在这本书中我们一直使用 `for` 循环递增整数索引 `i` 来遍历向量。

遍历向量元素的另一种方法，对于标准模板库中的所有数据存储类同样有效。这种方法就是使用 *迭代器*。

当你对向量调用 `begin()` 时，它会返回一个称为迭代器的对象。迭代器是行为很像指针的类，你通过诸如 `*`、`++` 和 `==` 这样的运算符来处理它们。下面是一个使用迭代器对向量所有元素求和的示例。

```cpp
vector<double> v({ 1.0, 2.0, 3.0 });
double sum = 0.0;
vector<double>::iterator i = v.begin();
while (i != v.end()) {
    sum += *i;
    i++;
}
ASSERT(sum == 6.0);
```

代码 *看起来* 就像 `begin` 返回指向向量第一个元素的指针，而 `end` 返回指向向量最后一个元素之后的指针。我们使用 `*` 访问迭代器引用的数据，就像处理指针一样。我们使用 `++` 增加迭代器，就像处理指针一样。我们通过将指针与 `end` 比较来决定何时终止循环，就像我们在第 16 章处理指针时所做的那样。我们实际上不是在处理指针的唯一线索是类型声明 `vector<double>::iterator`。

使用迭代器的优势在于它们可以与其他所有类一起用于标准模板库。这意味着你为一种容器编写的代码可以用于其他容器。这使得使用模板编写通用的算法成为可能，这些算法可以与任何容器一起工作。

你可以使用向量上的 `iterator` 来修改数据，如下例所示。这个函数使用迭代器将向量的每个元素设置为零。

```cpp
void setZero(vector<double>& v) {
    vector<double>::iterator i = v.begin();
    while (i != v.end()) {
        *i = 0;
        i++;
    }
}
```

如果你只想查看数据，可以使用 `const_iterator` 代替，如下例所示。

```cpp
double sumVector( const vector<double>& v ) {
    double sum = 0.0;
    vector<double>::const_iterator i = v.begin();
    while (i != v.end()) {
        sum += *i;
        i++;
    }
    return sum;
}
```

如果你在一个 `const` 引用上调用 `begin`，它将返回一个 `const_iterator`。因此，在上述代码中，必须指定 `i` 的类型为 `const_iterator`，否则代码将无法编译。

`iterator` 和 `const_iterator` 之间的区别有点令人困惑，而且确实很难记住。这正是 `auto` 大显身手的地方。下面的代码与上一个示例等效，但更容易理解且输入更快。

```cpp
double sumWithAuto(const vector<double>& v) {
    double sum = 0.0;
    auto i = v.begin();
    while (i != v.end()) {
        sum += *i;
        i++;
    }
    return sum;
}
```

## 18.4 for 循环与容器

容器只是一个存储数据并遵循标准库约定的类。至少，它应提供 `begin` 和 `end` 方法，这些方法返回迭代器，正如 `vector` 所做的那样。

这意味着我们已经编写了一个容器！第 16 章中的类 `Matrix` 具有返回指针的 `begin` 和 `end` 函数。指针定义了 `++`、`==` 和 `*` 等运算符，因此它们可以被视为迭代器。

C++ 包含一种遍历容器元素的特殊语法。例如，以下代码对 `Matrix` 的所有元素求和。

```cpp
Matrix matrix("1,3;2,4");
double total = 0.0;
for (auto d : matrix) {
  total += d;
}
ASSERT_APPROX_EQUAL(total, 10.0, 0.001);
```

这种 `for` 循环语法意味着，对于矩阵中的每个元素，我们将其值赋值给 `d`，然后执行循环体。虽然最终结果基本上相同，但这种语法通常比使用迭代器编写循环更方便得多。

拥有 `begin` 和 `end` 函数只是容器的最低要求。应遵循标准模板库中适用于您的容器的所有约定。

因此，我们在 `Matrix` 类中添加了一些成员类型，这些类型与 `vector` 中对应的成员具有完全相同的名称。

```cpp
typedef double value_type;
typedef double* iterator;
typedef const double* const_iterator;
```

如果我们遵循容器类的相同命名约定，就可以编写能同样适用于 `vector` 和我们 `Matrix` 类的函数。例如，这里有一个模板函数，可用于计算 `vector` 或 `Matrix` 中元素的总和。

```cpp
template <typename C>
typename C::value_type sumContainer(const C& c) {
  typename C::value_type total = 0;
  for (auto v : c) {
    total += v;
  }
  return total;
}
```

## 18.5 容器 set

`set` 是一个有用的容器类。要使用它，必须 `#include <set>`。

`set` 和 `vector` 之间的一个关键区别是，`set` 不包含重复元素（就像数学中的 set 概念一样）。另一个区别是，存储在 `set` 中的数据始终是排序的。

因此，你不能在 `set` 中存储任意数据，你必须能够使用 `<` 运算符比较两个元素。如果既非 `a<b` 也非 `b<a`，则两个元素 `a` 和 `b` 被视为相同。

如果你想在 `set` 中存储特定的数据类型，你需要重载 `<` 运算符。实际上，这并不完全正确。你可以选择告诉 `set` 使用除了 `<` 以外的其他函数来进行比较，但我们只讨论重载 `<` 的标准情况。

幸运的是，人们最常想在 `set` 中存储的数据类型，即数值类型和 `string`，已经具备了适当的 `<` 实现。

下面是一个示例，展示了如何使用 `insert` 向 `set` 中插入元素，确认 `set` 不包含重复项，并使用 `for` 语法打印 `set` 的内容。

```cpp
set<int> ints;
ints.insert(1);
ints.insert(3);
ints.insert(2);
ints.insert(3); // 重复项被忽略
ASSERT(ints.size() == 3);
for (auto i : ints) {
    std::cout << "Item " << i << "\n";
}
```

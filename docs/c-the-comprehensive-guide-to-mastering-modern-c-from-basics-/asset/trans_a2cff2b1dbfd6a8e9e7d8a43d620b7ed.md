

-   * 另一个命名空间

这两个类型别名旨在暗示你将来可能会将 `ConiferousTree` 和 `BroadleafTree` 从 `Tree` 中分离出来，并为它们编写自定义类，但目前它们仍然是相同的。

如果你觉得合理，可以几乎任意地嵌套命名空间，并以这种方式组织你的项目。我在嵌入的 `exampleNames` 命名空间中放入了另一个元素：例如 `oakName` 等变量。

你也可以将常量和模板放在命名空间中。只有宏不受命名空间的影响；请参见第 21 章。

`main` 必须在任何命名空间之外；否则编译器将找不到该函数作为入口点。在这个 `main` 函数中，我使用命名空间限定符引用了 `plant::ConiferousTree` 和 `plant::BroadleafTree`。或者，以下代码同样有效：

```
using plant::ConiferousTree; using plant::BroadleafTree;
ConiferousTree pine{ pineName };
BroadleafTree oak{ oakName };
```

或者简单地：

```
using namespace plant;
ConiferousTree pine{ pineName };
BroadleafTree oak{ oakName };
```

我在使用 `using namespace plant::exampleName` 时也选择了这种方法。提醒一下：你应该只在局部范围内通过 `using namespace` 引入整个命名空间——例如在函数内部——但绝对不要在 *.cpp 文件中全局引入——更不要在头文件中引入。

由于 `fir` 是 `main` 中的局部变量，你可以像方法一样调用 `print`：

```
fir.print(std::cout); std::cout << "\n";
```

对于 `operator<<` 则稍微复杂一些。如果你直接写 `std::cout << tanne`，它会导致错误，因为编译器会在所有可用命名空间中寻找合适的自由函数（对于运算符，也会搜索 `std`）。所以它会寻找以下内容：

-   operator(std::ostream&, const Tree&);—在全局范围内，即 `main` 所在的层

-   std::operator<<(std::ostream&, const Tree&);—在搜索 `std` 的地方

-   plant::exampleNames::operator<<(std::ostream&, const Tree&))—因为之前声明了 `using namespace plant::exampleNames`

`Tree` 的重载在 `plant` 命名空间中：

plant::operator<<(std::ostream&, const Tree&);

要使用定义在命名空间内的运算符，必须先使其可用，以便将其包含在搜索范围内。这里有两个选项：

-   `using plant::operator<<`—仅获取该运算符

-   `using namespace plant;`—获取命名空间中的所有内容

命名空间也用于分离可能冲突的内容。运算符在这里是很好的候选者。你可能会像如下列表所示拥有两个 `operator<<` 变体。

```
namespace plant {
  // 如前所示 ...
  std::ostream& operator<<(std::ostream&, const Tree&) {
  namespace debug {
    std::ostream& operator<<(std::ostream&, const Tree&) {
  }
}
plant::Tree tree("MyTree");
void run() {
  using namespace plant;
  cout << tree << "\n";
}
void diagnostic() {
  using namespace plant::debug;
  cout << tree << "\n";
}
int main() {
  run();
  diagnostic();
}
```

**列表 13.2** 在不同的命名空间中，你可以定义相同的运算符。

根据需要，你可以使用 `using` 指令包含所需的 `operator<<`。与函数或类型不同，你不能为运算符指定作用域；`plant::Tree tree("x");` 是有效的，但 `cout plant::<< tree` 是无效的。相反，你可以写 `plant::operator<<(cout, tree)`，但这会让运算符失去意义，因为你大可以定义一个函数或方法了。

所以，如果你想始终在全局命名空间中定义运算符，只要你知道 `using plant::operator<<` 也有帮助，你就不需要这样做。

## 使用命名空间

如果你想整洁地组织你的项目，请使用命名空间。我建议每个自定义库使用一个主命名空间。是否想要进一步细分此命名空间取决于需求。

顺便说一下，你以后可以毫无问题地扩展命名空间并将其拆分为两个或多个文件。只需将每个文件中想要的所有内容放入 `namespace plant {...}` 中，命名空间就会跨文件进行填充。

## 13.2 匿名命名空间

你也可以定义一个没有标识符的命名空间。这具有特殊含义。为了接下来的列表，假设这里有几个文件。

```
// https://godbolt.org/z/e3d55zvT8
// module.hpp
#include <string>
#include <iostream>
namespace plant {
    class Tree {
        std::string name;
    public:
        explicit Tree(const std::string_view name);
        void print(std::ostream& os) const;
    };
std::ostream& operator<<(std::ostream& os, const Tree& arg);
}

// module.cpp
#include "module.hpp"
namespace { // 匿名命名空间
    std::string PREFIX = "TREE:";
    void printInfo(std::ostream& os) {
        os << "Author: Torsten T. Willmann";
    }
}

bool debug = false; // 全局，无命名空间
namespace plant {
    Tree::Tree(const std::string_view name)
        : name(name) {}
    void Tree::print(std::ostream& os) const {
        os << PREFIX << name;
    }
std::ostream& operator<<(std::ostream& os, const Tree& arg) {
    if (debug) printInfo(os);
    arg.print(os);
    return os;
}
}

// main.cpp
#include "module.hpp"
```
int main() {
    plant::Tree x{"x"};
    x.print(std::cout);
    std::cout << "\n";
}
```

**列表 13.3** 匿名命名空间使得定义局部化。这里你有三个文件：

-   module.hpp—Tree 类的接口
-   module.cpp—Tree 类的实现，带有匿名命名空间中的辅助函数
-   main.cpp—使用接口

标识符集在大型项目中可能会变得非常混乱，尤其是当你使用第三方库时。你会获得大量的标识符，它们可能与你的标识符重叠。

这种情况的第一种预防措施是使用命名空间。命名空间的标识符是标识名的一部分。这样，`plant::Tree` 和 `algo::Tree` 就不会相互干扰。

第二种措施是对不需要其他模块的内容使用匿名命名空间。main.cpp 不需要关心 `PREFIX`。而且 `printInfo` 函数只在 `module.cpp` 中使用。将这两个标识符封装在命名空间 `{...}` 中，它们只对当前模块可见。它们不再与其他模块干扰。

## 13.3 “static” 使局部化

为了正是这一目的，你也可以使用 `static` 关键字。无需打开匿名命名空间，只需在变量和函数前编写 `static`。你实现了相同的效果：变量或函数的名称仅在该模块内可见。其他模块可以使用相同的名称而不会引起编译器报错。

对于 `module.cpp` 如下：

`debug` 变量还没有 `static`。结果是，任何其他模块无法定义全局函数或全局变量 `debug`，但这里是故意的。因为尽管 `debug` 不在 `module.hpp` 头文件中，但拥有足够知识的人（作者？）可以操纵该变量。考虑这个离题，因为通常的编程实践不应该是这种方式隐藏和更改变量。在项目的其他模块中，有人可以通过方式操纵变量：

```
extern bool debug;
```

并在声明后通过 `debug = true` 进行操纵；这可能有利也可以有坏处。对于调试开关，这可能是允许的。否则，将不应导出的标识符放入匿名命名空间中（或将其声明为 `static`）。匿名命名空间相比 `static` 有一个巨大的优势，它还可以保护自己的类型不溢出到其他模块中。你无法通过 `static` 保护 `struct, class` 或 `using X = Y` 不被导出。但在命名空间 `{...}` 中，这些内容是安全的。


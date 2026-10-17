
现在，又有人提供了另一个库，其中包含用于文本处理的功能：

```
// Text_lib:
class Glyph { /* ... */ }; class Word { /* ... */ }; class Line { /* ... */ }; class Text { /* ... */ };
// sequence of Glyphs // sequence of Words // sequence of Lines
File* open(const char*); // open text file
Word operator+(const Line&, const Line&); // concatenate
```

暂时忽略图形和文本处理方面的具体设计问题，只考虑如何在一个程序中同时使用 `Graph_lib` 和 `Text_lib` 所带来的问题。

假设（这是非常现实的）`Graph_lib` 中的功能定义在一个头文件（§2.4.1）`Graph_lib.h` 中，而 `Text_lib` 中的功能定义在另一个头文件 `Text_lib.h` 中。现在，我可以“无意地”同时 `#include` 这两个头文件，并尝试使用两个库中的功能：

```
#include “Graph_lib.h”
#include “Text_lib.h”
// …
```

仅仅 `#include` 这些头文件就会导致大量错误消息：`Line`、`Text` 和 `open()` 以编译器无法消除歧义的方式被定义了两次。尝试使用这些库还会产生更多错误消息。

处理这类名称冲突有许多技术。例如，有些问题可以通过将一个库的所有功能放入少数几个类中、使用自认为不常见的名称（例如使用 `Text_box` 而不是 `Text`），或者系统地为库中的名称添加前缀（例如 `gl_shape` 和 `gl_line`）来解决。这些技术（也称为“变通方案”和“技巧”）在某些情况下有效，但并不通用，而且使用起来可能不方便。例如，名称往往会变得很长，而使用许多不同的名称会妨碍泛型编程（§3.4）。

# 14.2 命名空间

命名空间这一概念用于直接表示一组直接相关的功能，例如某个库的代码。命名空间的成员处于同一个作用域中，可以相互引用而无需特殊表示法；而从命名空间外部访问它们则需要使用显式表示法。特别是，我们可以将不同的声明集合（例如库接口）分隔到不同的命名空间中，从而避免名称冲突。例如，我们可以将图形库命名为 `Graph_lib`：

```
namespace Graph_lib {
class Shape { /* … */ };
class Line : public Shape { /* … */ }; class Poly_line: public Shape { /* … */ }; class Text: public Shape { /* … */ };

// connected sequence of lines // text label
Shape operator+(const Shape&, const Shape&); // compose
Graph_reader open(const char*); // open file of Shapes }
```

同样，我们的文本库显然可以命名为 `Text_lib`：

```
namespace Text_lib { class Glyph { /* … */ }; class Word { /* … */ }; class Line { /* … */ }; class Text { /* … */ };

// sequence of Glyphs // sequence of Words // sequence of Lines
File* open(const char*); // open text file
Word operator+(const Line&, const Line&); // concatenate
}
```

只要我们能够选择不同的命名空间名称，例如 `Graph_lib` 和 `Text_lib`（§14.4.2），现在就可以将两组声明一起编译，而不会发生名称冲突。

命名空间应当表达某种逻辑结构：命名空间中的声明整体上应该提供一组在用户看来彼此统一的功能，并体现共同的设计决策。应当把它们视为一个逻辑单元，例如“图形库”或“文本处理库”，这类似于我们看待类的成员的方式。事实上，在命名空间中声明的实体被称为该命名空间的成员。

命名空间是一个（有名称的）作用域。你可以在后续声明中访问命名空间中较早定义的成员，但不能（除非采取特殊措施）从命名空间外部引用这些成员。例如：

```
class Glyph { /* ... */ };
class Line { /* ... */ };
```

```
namespace Text_lib {
class Glyph { /* ... */ };
class Word { /* ... */ }; // sequence of Glyphs
class Line { /* ... */ }; // sequence of Words
class Text { /* ... */ }; // sequence of Lines

File* open(const char*); // open text file
Word operator+(const Line&, const Line&); }
```

```
Glyph glyph(Line& ln, int i); // ln[i]
```

这里，`Text_lib::Line` 声明中的 `Word` 和 `Line` 采用局部名称查找。该局部名称查找不受全局 `Line` 的影响。相反，全局 `glyph()` 声明中的 `Glyph` 和 `Line` 指的是全局的 `::Glyph` 和 `::Line`。这种（非局部）查找不受 `Text_lib` 的 `Glyph` 和 `Line` 的影响。

要引用命名空间的成员，可以使用其完全限定名称。例如，如果我们希望定义一个使用 `Text_lib` 中定义的 `glyph()`，可以写成：

```
Text_lib::Glyph glyph(Text_lib::Line& ln, int i); // ln[i]
```

从命名空间外部引用其成员的其他方式包括 `using`-声明（§14.2.2）、`using`-指令（§14.2.3）和与实参相关的查找（§14.2.4）。

```
// concatenate Text_lib::operator+() refer to Text_lib::Word and
```

## 14.2.1 显式限定

可以在命名空间定义中声明某个成员，然后使用命名空间名称 :: 成员名称表示法在之后定义它。命名空间的成员必须使用这种表示法引入：

```
namespace namespace-name {
// declaration and definitions
}
```

例如：

```
std::istringstream iss(s);
for (std::string buf; iss>>buf;)
res.push_back(buf);
return res;
}
```

反复使用限定名 `std` 既烦琐又分散注意力。特别是在这个小例子中，我们重复了四次 `std::string`。为减轻这一问题，我们可以使用 `using`-声明，说明在这段代码中，string 表示 `std::string`：

```
using std::string; // use “string” to mean “std::string”
std::vector<string> split(const string& s)
// split s into its whitespace-separated substrings
{
std::vector<string> res; std::istringstream iss(s);
for (string buf; iss>>buf;)
res.push_back(buf);
return res;
}
```

`using`-声明会在某个作用域中引入一个同义名称。通常，最好让局部同义名称尽可能保持局部化，以避免混淆。

当 `using`-声明用于重载名称时，它适用于所有重载版本。例如：

```
namespace N {
void f(int);
void f(string);
};

void g() {
using N::f;
f(789); // N::f(int)
f("Bruce"); // N::f(string)
}
```

关于 `using`-声明在类层次结构中的使用，请参见 §20.3.5。

## 14.2.3 `using`-指令

在 `split()` 示例（§14.2.2）中，即使为 `std::string` 引入了同义名称，我们仍然使用了三次 `std::`。很多时候，我们希望无需限定就能使用命名空间中的每个名称。可以为命名空间中的每个名称分别提供 `using`-声明来实现这一点，但这很烦琐，而且每当命名空间中添加或删除名称时，都需要额外处理。另一种方法是使用 `using`-指令，请求命名空间中的每个名称都可以在当前作用域中无须限定地访问。例如：

```
using namespace std; // make every name from std accessible
```

```cpp
vector<string> split(const string& s)
// split s into its whitespace-separated substrings
{
vector<string> res;
istringstream iss(s);
for (string buf; iss>>buf;)
res.push_back(buf);
return res;
}
```

一个 `using`-directive 使命名空间中的名称几乎就像在命名空间之外声明的一样可用（另请参见 §14.4）。使用 `using`-directive 使来自常用且众所周知的库的名称无需限定即可使用，这是一种简化代码的流行技术。本书在整个书中使用该技术来访问标准库设施。标准库设施定义在命名空间 `std` 中。

在函数内部，`using`-directive 可以安全地用作记号便利，但在使用全局 `using`-directive 时应谨慎，因为过度使用会导致命名空间引入的正是为了避免的名称冲突。例如：

```cpp
namespace Graph_lib {
class Shape { /* ... */ };
class Line : Shape { /* ... */ }; class Poly_line: Shape { /* ... */ }; class Text: Shape { /* ... */ };

// connected sequence of lines // text label
Shape operator+(const Shape&, const Shape&); // compose
Graph_reader open(const char*); // open file of Shapes }

namespace Text_lib { class Glyph { /* ... */ }; class Word { /* ... */ }; class Line { /* ... */ }; class Text { /* ... */ }; }

// sequence of Glyphs // sequence of Words // sequence of Lines
File* open(const char*); // open text file
Word operator+(const Line&, const Line&); // concatenate }
using namespace Graph_lib; using namespace Text_lib;
Glyph gl; // Text_lib::Glyph
vector<Shape**> vs; // Graph_lib::Shape
```

到目前为止，一切都很好。特别是，我们可以使用不冲突的名称，例如 `Glyph` 和 `Shape`。然而，一旦我们使用其中一个冲突的名称，就会发生名称冲突——就好像我们没有使用命名空间一样。例如：

```cpp
Text txt;
File* fp = open("my_precious_data");
// error : ambiguous // error : ambiguous
```

因此，我们必须在全局范围内谨慎使用 `using`-directive。特别是，不要在头文件中放置 `using`-directive 到全局范围，除非在非常特殊的情形下（例如，为了便于过渡），因为你永远不知道头文件可能会被 `#include` 到哪里。

## 14.2.4 实参相关查找

一个接受用户定义类型 `X` 的参数的函数通常在与 `X` 相同的命名空间中定义。因此，如果在使用的上下文中找不到函数，我们会在其参数的命名空间中查找。例如：

```
namespace Chrono { class Date { /* ... */ };
bool operator==(const Date&, const std::string&);
std::string format(const Date&); // make string representation // ... }

void f(Chrono::Date d, int i) {
std::string s = format(d); std::string t = format(i);
}
```

```
// Chrono::format()
// error: no format() in scope
```

这种查找规则（称为 argument-dependent lookup 或简称为 ADL）与使用显式限定相比为程序员节省了大量输入，但它不会像 `using`-directive (§14.2.3) 那样污染命名空间。它对于操作数操作符 (§18.2.5) 和模板参数 (§26.3.5) 尤其有用，在这些情况下显式限定可能非常繁琐。

请注意，命名空间本身需要在作用域中，并且函数必须先声明才能被找到并使用。

自然地，一个函数可以接受来自多个命名空间的参数。例如：

```
void f(Chrono::Date d, std::string s)
{
if (d == s) {

// ...

}
else if (d == “August 4, 1914”) {

// ...

}
}
```

在这种情况下，我们在调用的作用域中查找函数（如同以往），并在每个参数的命名空间中查找（包括每个参数的类及其基类），然后对我们找到的所有函数进行通常的重载决议 (§12.3)。特别是，对于调用 `d == s`，我们将在包围 `f()` 的作用域中查找 `operator==`，在 `std` 命名空间中（其中为 `string` 定义了 `==`），以及在 `Chrono` 命名空间中。存在 `std::operator==( )`，但它不接受 `Date` 参数，因此我们使用接受的 `Chrono::operator==( )`。另请参见 §18.2.5。

当类成员调用命名函数时，同一类及其基类的其他成员优先于可能基于参数类型找到的函数（操作符遵循不同的规则；§18.2.1，§18.2.5）。例如：

```
namespace N {
struct S { int i };
void f(S);
void g(S);
void h(int);
}
```

```
struct Base {
void f(N::S);
};

struct D : Base { void mf();

void g(N::S x) {
f(x); // call Base::f()
mf(x); // call D::mf()
h(1); // error :no h(int) available
}
};
```

在标准中，参数相关查找的规则以关联命名空间 (§iso.3.4.2) 的形式表述。基本上：

- 如果参数是类成员，则关联命名空间为该类本身（包括其基类）及其封闭命名空间。
- 如果参数是命名空间的成员，则关联命名空间为封闭命名空间。
- 如果参数是内置类型，则没有关联命名空间。

参数相关查找可以节省大量繁琐且分散注意力的输入，但有时会产生令人惊讶的结果。例如，搜索函数 `f()` 的声明时，并不会优先考虑在 `f()` 被调用的命名空间中的函数（类中调用 `f()` 的函数则会这样）。

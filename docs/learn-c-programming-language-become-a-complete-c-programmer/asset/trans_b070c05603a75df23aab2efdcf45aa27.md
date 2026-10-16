

+   - 组合问题
+   - 命名空间
+     显式限定；**using**-声明；**using**-指令；与实参相关的查找；命名空间是开放的
+   - 模块化与接口
+     命名空间作为模块；实现；接口与实现
+   - 使用命名空间进行组合
+     便利性与安全性；命名空间别名；命名空间组合；组合与选择；命名空间与重载；版本控制；嵌套命名空间；未命名命名空间；C 头文件
+   - 建议

## 14

## 命名空间

> 现在是 787 年！公元？
> ——蒙提·派森

## 14.1 组合问题

任何现实的程序都由若干相互独立的部分组成。函数（§2.2.1，第 12 章）和类（§3.2，第 16 章）提供了相对细粒度的关注点分离，而“库”、源文件和翻译单元（§2.4，第 15 章）则提供了更粗粒度的分离。逻辑上的理想状态是模块化，也就是说，让相互独立的事物保持独立，并且只允许通过定义明确的接口访问某个“模块”。C++ 没有提供一个支持模块概念的单一语言特性；它没有模块构造。相反，模块化是通过函数、类和命名空间等其他语言设施的组合，以及源代码组织来表达的。

本章和下一章讨论程序的粗粒度结构及其作为源文件的物理表示。也就是说，这两章更多关注“大规模编程”，而不是单个类型、算法和数据结构的优雅表达。

考虑一下当人们没有针对模块化进行设计时可能出现的一些问题。例如，一个图形库可能提供不同种类的图形 **Shape**，以及帮助使用这些图形的函数：

```
// Graph_lib:
class Shape { /* ... */ };
class Line : public Shape { /* ... */ }; class Poly_line: public Shape { /* ... */ }; class Text : public Shape { /* ... */ };
// connected sequence of lines // text label
Shape operator+(const Shape&, const Shape&); // compose
Graph_reader open(const char *); // open file of Shapes
```

现在，又有人提供了另一个库，其中包含用于文本处理的功能：

```
// Text_lib:
class Glyph { /* ... */ }; class Word { /* ... */ }; class Line { /* ... */ }; class Text { /* ... */ };
// sequence of Glyphs // sequence of Words // sequence of Lines
File* open(const char*); // open text file
Word operator+(const Line&, const Line&); // concatenate
```

暂时忽略图形和文本处理方面的具体设计问题，只考虑如何在一个程序中同时使用 Graph_lib 和 Text_lib 所带来的问题。

假设（这是非常现实的）**Graph_lib** 中的功能定义在一个头文件（§2.4.1）**Graph_lib.h** 中，而 **Text_lib** 中的功能定义在另一个头文件 **Text_lib.h** 中。现在，我可以“无意地”同时 **#include** 这两个头文件，并尝试使用两个库中的功能：

```
#include “Graph_lib.h”
#include “Text_lib.h”
// …
```

仅仅 **#include** 这些头文件就会导致大量错误消息：**Line**、**Text** 和 **open()** 以编译器无法消除歧义的方式被定义了两次。尝试使用这些库还会产生更多错误消息。

处理这类*名称冲突*有许多技术。例如，有些问题可以通过将一个库的所有功能放入少数几个类中、使用自认为不常见的名称（例如使用 **Text_box** 而不是 **Text**），或者系统地为库中的名称添加前缀（例如 **gl_shape** 和 **gl_line**）来解决。这些技术（也称为“变通方案”和“技巧”）在某些情况下有效，但并不通用，而且使用起来可能不方便。例如，名称往往会变得很长，而使用许多不同的名称会妨碍泛型编程（§3.4）。

**第 14.2 节 命名空间 391**

## 14.2 命名空间

*命名空间*这一概念用于直接表示一组直接相关的功能，例如某个库的代码。命名空间的成员处于同一个作用域中，可以相互引用而无需特殊表示法；而从命名空间外部访问它们则需要使用显式表示法。特别是，我们可以将不同的声明集合（例如库接口）分隔到不同的命名空间中，从而避免名称冲突。例如，我们可以将图形库命名为 **Graph_lib**：

```
namespace Graph_lib {
class Shape { /* … */ };
class Line : public Shape { /* … */ }; class Poly_line: public Shape { /* … */ }; class Text: public Shape { /* … */ };

// connected sequence of lines // text label
Shape operator+(const Shape&, const Shape&); // compose
Graph_reader open(const char*); // open file of Shapes }
```

同样，我们的文本库显然可以命名为 **Text_lib**：

```
namespace Text_lib { class Glyph { /* … */ }; class Word { /* … */ }; class Line { /* … */ }; class Text { /* … */ };

// sequence of Glyphs // sequence of Words // sequence of Lines
File* open(const char*); // open text file
Word operator+(const Line&, const Line&); // concatenate
}
```

只要我们能够选择不同的命名空间名称，例如 **Graph_lib** 和 **Text_lib**（§14.4.2），现在就可以将两组声明一起编译，而不会发生名称冲突。

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

Glyph glyph(Line& ln, int i); // ln[i]

这里，**Text_lib::Line** 声明中的 **Word** 和 **Line** 采用局部名称查找。该局部名称查找不受全局 **Line** 的影响。相反，全局 **glyph()** 声明中的 **Glyph** 和 **Line** 指的是全局的 **::Glyph** 和 **::Line**。这种（非局部）查找不受 **Text_lib** 的 **Glyph** 和 **Line** 的影响。

要引用命名空间的成员，可以使用其完全限定名称。例如，如果我们希望定义一个使用 **Text_lib** 中定义的 **glyph()**，可以写成：

```
Text_lib::Glyph glyph(Text_lib::Line& ln, int i); // ln[i]
```

从命名空间外部引用其成员的其他方式包括 **using**-声明（§14.2.2）、**using**-指令（§14.2.3）和与实参相关的查找（§14.2.4）。

```
// concatenate Text_lib::operator+() refer to Text_lib::Word and
```

### 14.2.1 显式限定

可以在命名空间定义中声明某个成员，然后使用*命名空间名称 :: 成员名称*表示法在之后定义它。命名空间的成员必须使用这种表示法引入：

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

反复使用限定名 **std** 既烦琐又分散注意力。特别是在这个小例子中，我们重复了四次 **std::string**。为减轻这一问题，我们可以使用 using-声明，说明在这段代码中，string 表示 **std::string**：

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

using-声明会在某个作用域中引入一个同义名称。通常，最好让局部同义名称尽可能保持局部化，以避免混淆。
当 using-声明用于重载名称时，它适用于所有重载版本。例如：

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

关于 using-声明在类层次结构中的使用，请参见 §20.3.5。

### 14.2.3 using-指令

在 split() 示例（§14.2.2）中，即使为 **std::string** 引入了同义名称，我们仍然使用了三次 **std::**。很多时候，我们希望无需限定就能使用命名空间中的每个名称。可以为命名空间中的每个名称分别提供 using-声明来实现这一点，但这很烦琐，而且每当命名空间中添加或删除名称时，都需要额外处理。另一种方法是使用 using-指令，请求命名空间中的每个名称都可以在当前作用域中无须限定地访问。例如：

```
using namespace std; // make every name from std accessible
```


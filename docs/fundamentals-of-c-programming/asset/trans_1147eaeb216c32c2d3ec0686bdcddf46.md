

{TextType::Fancy, "Wee", "[", "]", "-"},
{TextType::Fixed},
{TextType::Fancy, "Whoa", "[", "]", "-", "-" } };
for (auto t : texts)
    std::cout << t.get() << " \n";
for (auto& t : texts) {
    t.append("A");
    t.append("B");
    t.append("C");
}
for (auto t : texts)
    std::cout << t.get() << " \n";
}

从用户的角度来看，清单17.13（testalltext.cpp）的工作方式与清单17.10（polymorphicvector.cpp）完全相同。然而，从程序员的角度来看，这两个程序有很大不同。清单17.13（testalltext.cpp）在一个类中封装了清单17.10（polymorphicvector.cpp）中三个不同类的所有功能。这种非多态代码使用TextType自定义枚举类型来区分文本对象。请注意，我们之前示例中具有多态性的每个方法现在都使用条件逻辑（switch语句）来执行适合我们希望建模的实际文本对象类型的代码。

这种避免继承和多态的方法存在几个不同的问题：

- 1. 每个Text对象都承载着每种可能文本对象的负担。普通文本对象持有花哨文本对象所需的左括号、右括号和分隔符字符串。字符串占用的内存量取决于其长度（它持有的字符数），但即使是空的std::string对象也需要一些内存。管理许多主要为普通文本对象的应用程序可能会消耗比实际需要多得多的内存。

- 2. 使用继承时，开发人员可以在不修改现有文本类代码的情况下引入新的文本类型。希望在此示例中引入一种避免继承的新文本对象的程序员必须对代码进行相当大的更改，涉及以下内容：
  - 向枚举类型添加标识新文本对象类型的新元素，
  - 添加新文本对象可能需要的新字段，以及
  - 在继承版本中曾经具有多态性的每个方法的switch语句中添加与新文本对象类型匹配的case标签。

- 3. 没有继承，我们需要访问原始源代码才能扩展数据类型。如果它是预编译库的一部分，我们就无法进行必要的修改。然而，使用继承时，即使我们无法访问或控制其实现的源代码，也可以从现有类派生出新类。

为了说明这些问题，假设我们希望添加一种限制文本长度的新文本对象。清单??（alttext2.h）扩展了非多态Text类。

## Listing 17.14: alttext2.cpp

```cpp
#ifndef ALT_TEXT2_H_INCLUDED
#define ALT_TEXT2_H_INCLUDED

#include <string>

// The kinds of text objects supported (added Bounded)
enum class TextType { Plain, Fancy, Fixed, Bounded };

class AltText2 {
  TextType type;
  std::string text;
  std::string left_bracket;
  std::string right_bracket;
  std::string connector;
  size_t length_limit; // Maximum number of characters in the text

public:
  AltText2(TextType type, const std::string& t);
  AltText2(TextType type, const std::string& t, const std::string& left,
           const std::string& right, const std::string& conn);
  AltText2(TextType type);

  // Constructor for a length-bounded text object
  AltText2(TextType type, const std::string& t, size_t limit);
  std::string get() const;
  void append(const std::string& extra);
};

#endif
```

我们将枚举扩展为包含TextType::Bounded。我们向Text类添加了一个额外字段（limit），这意味着每个Text对象都会有一个limit字段，无论是否需要。我们还添加了一个额外的构造函数重载，以正确初始化有界文本对象。

清单17.14（alttext2.cpp）实现了新Text类中的方法。

## Listing 17.15: alttext2.cpp

```cpp
#include "alttext2.h"

AltText2::AltText2(TextType type, const std::string& t): type(type), text(t) {}

AltText2::AltText2(TextType type, const std::string& t, const std::string& left,
                   const std::string& right, const std::string& conn)
  : type(type), text(t), left_bracket(left), right_bracket(right),
    connector(conn) {}

AltText2::AltText2(TextType type): type(type), text("FIXED") {}

AltText2::AltText2(TextType type, const std::string& t, size_t limit):
  type(type),
  text(t.substr(0, limit)), // Ensure text initially does not exceed bound
  length_limit(limit) {}

std::string AltText2::get() const {
  switch (type) {
  case TextType::Plain:
case TextType::Fixed:
case TextType::Bounded:
    return text;
case TextType::Fancy:
    return left_bracket + text + right_bracket;
default:
    return "UNKNOWN TYPE";
}
}

void AltText2::append(const std::string& extra) {
switch (type) {
case TextType::Plain:
    text += extra; // Just concatenate
    break;
case TextType::Fancy:
    text += connector + extra; // Join with connector
    break;
case TextType::Fixed:
    break; // Ignore attempt to append
case TextType::Bounded:
    // Ensure the length does not exceed the established limit
    int avail = length_limit - text.length();
    text += extra.substr(0, avail);
    break;
}
}
```

清单17.16（testalttext2.cpp）表明，我们的新有界文本对象确实限制了其封装字符串字段的长度。

## Listing 17.16: testalttext2.cpp

```cpp
#include <string>
#include <vector>
#include <iostream>
#include "alttext2.h"

int main() {
std::vector<AltText2> texts { {TextType::Plain, "Wow"},
{TextType::Fancy, "Wee", "[", "]", "-"},
{TextType::Fixed},
{TextType::Bounded, "XYZ", 5},
{TextType::Fancy, "Whoa", "-:", "-:", "-:"} };

for (auto t : texts)
std::cout << t.get() << " \n";
for (auto& t : texts) {
t.append("A");
t.append("B");
t.append("C");
t.append("D");
t.append("E");
t.append("F");
}
for (auto t : texts)
    std::cout << t.get() << '\n';
}
```

清单17.16（testalttext2.cpp）显示

```
Wow
[Wee]
FIXED
XYZ
:Whoa:
WowABCDEF
[Wee-A-B-C-D-E-F]
FIXED
XYZAB
:Whoa:A:B:C:D:E:F:
```

请注意，尽管我们的新有界文本对象不需要特殊的get方法，但我们仍然必须添加`case`标签以匹配`TextType::Bounded`类型。如果不添加这个`case`标签，意味着每个有界文本对象都将响应"UNKNOWN TYPE"字符串。我们肯定必须在附录中添加新代码，以确保连接操作不会使有界文本对象过长。

即使在引入这种新文本对象之前，`get`和`append`方法已知能完美工作，现在它们也变得可疑。我们对它们的修改可能引入了微妙的错误，因此必须彻底重新测试。

我们的非多态`Text`类相对较小，仅包含两个方法。考虑一个提供更多方法的更大型类。引入该类型的变体可能需要进行大量代码修改。

现在假设我们无法访问清单17.14（alttext2.cpp）中的源代码。它可能已编译并作为库的一部分。在这种情况下，我们无法修改`Text`类来引入我们需要的自定义行为。

与这些挑战形成对比的是，考虑向我们的多态`Text`类层次结构中添加有界文本类型。清单17.17（boundedtext.h）为我们的新类提供了接口。

## Listing 17.17: boundedtext.h

```cpp
#ifndef BOUNDEDTEXT_H_INCLUDED
#define BOUNDEDTEXT_H_INCLUDED

// Compiler needs to know specifics of the Text class in order to
// derive a new class from it
#include "text.h"

// Provides minimal decoration for the text
class BoundedText: public Text {
    size_t text_length_limit;
public:
    // Client supplies the string to wrap plus the limit on
    // how many characters it can hold
    BoundedText(const std::string& t, size_t limit);
    // Concatenate another string onto the back of the existing text,
    // but do not exceed the predetermined limit on the text's length.
```

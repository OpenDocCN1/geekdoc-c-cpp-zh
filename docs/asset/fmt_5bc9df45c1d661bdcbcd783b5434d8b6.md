
为了区分左值和右值，我们必须找到可以利用的左值和右值的区分特征。这些区分特征是 `operator=`（作为左值使用）和转换运算符（始终作为右值使用）。与其让 `operator()` 返回一个 `string &`，不如让它返回一个 `Proxy` 对象，该对象始终用于区分其左值和右值。

`Proxy` 类需要 `operator=(const string const &)`（作为左值作用）和 `operator std::string const() const`（作为右值作用）。我们需要更多的运算符吗？`std::string` 类也提供了 `operator=`，所以我们可能应该实现 `operator=`，因为普通字符可以赋值给字符串（即使使用它们的数值我们时也是如此）。作为 `string=`，如果右侧是 `char`，则普通字符不能与 `operator=(string&)` 使用。也可以考虑一个将 `char` 提升的运算符 `operator=(char value)`。这些额外的运算符未包含构造函数的实现中，但“现实生活中”的 `Proxy` 类应该考虑实现额外的运算符。另一个微妙之处是，当在使用 `ostream` 插入或提取运算符时，不会使用 `Proxy` 的 `operator std::string const&`，因为这些实现并没有识别我们的 `Proxy` 类类型。因此，当需要流插入和提取时（这很可能），`Proxy` 将拥有它自己的重载插入和提取运算符。然而，重载插入运算符的实现将为 `Proxy` 替身的那个对象进行插入。

```cpp
inline std::ostream& operator<<(std::ostream& out, Lines::Proxy const &proxy)
{
    return out << static_cast<std::string const &>(proxy);
}
```

除了 `Lines` 之外，不需要任何代码来创建 `Proxy` 对象。`Proxy` 的构造函数应该放在 `private` 之前，并且 `Proxy` 可以声明 `Lines` 为其成员。事实上，`Proxy` 与 `Lines` 紧密相关，可以定义为嵌套类。修改后的 `Lines operator[]` 不再返回 `string`，而是返回一个 `Proxy`。这里是修改后的 `Lines` 类，包括其嵌套的 `Proxy` 类：

```cpp
class Lines{
    std::vector<std::string> d_line;
public:
    class Proxy;
    Proxy operator[](size_t idx);
    class Proxy
        {
            friend Lines::Proxy::operator[](size_t idx);
            std::string& d_str;
            Proxy(std::string const& str);
            public:
                std::string& operator=(std::string const &rhs);
                operator std::string const &() const;
        }
    Lines(std::istream& in);
```

## 26.5. 实现“反向迭代器”

`Proxy` 的成员是轻量级的，可以内联实现：

```cpp
inline Lines::Proxy::Proxy(std::string const &str)
    : d_str(str)
{}
inline std::string& Lines::Proxy::operator=(std::string const &rhs)
{
    d_str = rhs;
    return d_str;
}
inline std::string const& Lines::Proxy::operator std::string() const
{
    return static_cast<std::string const&>(d_str);
}
inline Lines::Proxy Lines::operator[](size_t idx)
{
    return Proxy(d_line[idx]);
}
```

现在我们有了 `Proxy` 类，就可以实现一个反向迭代器。反向迭代器仅仅向相反方向移动的迭代器。

```cpp
class ReverseIterator
{
    Lines::Proxy const it;
public:
    ReverseIterator(Lines::Proxy const it) : it(it) {}
    operator std::string const() const { return *it; }
    ReverseIterator& operator++() { /* implementation */ return *this; }
    ReverseIterator& operator--() { /* implementation */ return *this; }
};
```

在本节中，我们关注如何让这些迭代器与标准库算法兼容。

## 26.5. 实现“反向迭代器”

```cpp
friend auto operator<=>(RandomPtrIterator const &lhs,
RandomPtrIterator const &rhs);
friend int operator->(RandomPtrIterator const &lhs,
RandomPtrIterator const &rhs);
private:
BaseIterator d_current;
public:
``````cpp
int operator-(RandomPtrIterator const &rhs) const;
RandomPtrIterator operator++(int step) const;
value_type& operator*() const;
RandomPtrIterator operator--();
RandomPtrIterator operator--(int);
RandomPtrIterator operator++();
RandomPtrIterator operator++(int);
RandomPtrIterator operator-(int step) const;
RandomPtrIterator operator+=(int step);
RandomPtrIterator operator+=(int step);
value_type* operator->() const;
```

private:

```cpp
RandomPtrIterator(BaseIterator const &current);
};
```

```cpp
template <typename Class, typename BaseIterator, typename value_type>
PtrIteratorValue::RandomPtrIterator(BaseIterator const &current)
{
  d_current(current)
}
```

观察友元声明，我们可以看到 Class 的起始和结束成员返回类型为 Class、BaseIterator 和 Type 的 RandomPtrIterator 对象，它们被授予了访问 RandomPtrIterator 私有构造函数的权限。这正是我们想要的。Class 的 begin 和 end 成员被声明为友元。

RandomPtrIterator 的其余成员都是公共的（public）。由于 RandomPtrIterator 是第 22.14.1 节中开发的嵌套迭代器的泛化，重新实现所需的函数是很容易的，只需要将 `iterator` 更改为 `RandomPtrIterator`并将 `std::string` 更改为 `Type` 即可。例如，在 `iterator` 类中定义的 `operator<`：

现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename Type>
inline auto operator<=>(PtrIterator const &lhs, PtrIterator const &rhs)
{
  return ++lhs.d_current == rhs.d_current;
}
```

一些额外的示例：在 `iterator` 类中定义的 `operator*`：

```cpp
inline std::string::StringPtr::iterator::operator() const
{
  return **d_current;
}
```

现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename value_type>
value_type &PtrIteratorValue::operator() const
{
    return **d_current;
}
```

前置和后置增运算符现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename value_type>
PtrIteratorValue &PtrIteratorValue::operator++ ()
{
    ++d_current;
    return *this;
}
template <typename Class, typename BaseIterator, typename value_type>
PtrIteratorValue PtrIteratorValue::operator++(int)
{
    return RandomPtrIterator(d_current);
}
```

其余成员可以相应地实现；它们的具体实现是留给读者的练习（当然，也可以从 `cplusplus.yo` 压缩包中获取）。

重新实现 22.14.1 节中开发的 `StringPt` 类也不困难。除了包含定义类模板 `RandomPtrIterator` 的头文件外，它只需要单处修改。我们使用 `using` 声明语法的迭代器现在必须与 `RandomPtrIterator` 关联。以下是完整的接口和类的内部定义：

```cpp
#ifndef INCLUDED_STRINGPT_H_
#define INCLUDED_STRINGPT_H_

#include <vector>
#include <string>
#include "iterator.h"

class StringPt : std::vector<std::string> *
{
public:
    using iterator = RandomPtrIterator<
        StringPtr,
        std::vector<std::string>::iterator,
        std::string
    >;

    using reverse_iterator = std::reverse_iterator<iterator>;

    iterator begin();
```

```cpp
iterator end();
reverse_iterator rbegin();
reverse_iterator rend();

inline StringPtr::iterator StringPtr::begin()
{
    return iterator(this->std::vector<std::string>::begin());
}
inline StringPtr::iterator StringPtr::end()
{
    return iterator(this->std::vector<std::string>::end());
}
inline StringPtr::reverse_iterator StringPtr::rbegin()
{
    return reverse_iterator(end());
}
inline StringPtr::reverse_iterator StringPtr::rend()
{
    return reverse_iterator(begin());
}
#endif
```

将 22.14 节中修改后的 StringPtr 头文件引入程序，程序的行为将与之前的版本相同。在这种情况下，`StringPtr::begin` 和 `StringPtr::end` 返回从模板定义构造的迭代器对象。

## 26.6 使用‘bisonc++’和‘flexc++’

下文讨论的示例深入了使用生成解析器和扫描器的 C++ 源码的特殊性。一旦程序的复杂度超过某个水平，使用扫描器-解析器生成器来生成执行输入识别的代码就会变得非常有吸引力。本节及后续章节中的示例确保读者知道如何使用扫描器生成器 flex 和解析器生成器 bison。bison 和 flex 在其他地方都有详尽的文档。bison 和 flex 的前身 yacc 和 lex 已在多本书（如 O'Reilly 出版）中进行了描述。

### 26.6.1 使用‘flex++’创建扫描器

在本节开发的词法扫描器用于监控从几个子集生成文件的过程。设置如下：输入语言的 `#include` 指令，随后是指定文件（路径）的文本，该文件应位于 `#include`所在的位置。

为了避免与当前示例相关的复杂性，`#include` 语句的格式限制为 `#include <filepath>` 形式。括号之间指定的文件应该在 `filepath` 指出的位置可用。如果未找到文件，程序将在发布错误消息后终止。

程序启动时带有一个或两个文件名。如果启动时仅带一个文件名，输出将写入输出流 `out`，该流名称由程序的第二个参数给出。否则，输出将写入指定的流名称。

程序定义了最大嵌套深度。一旦超过此最大值，程序将在发布错误消息后终止。在这种情况下，指示我们所在位置的文件栈

## 26.6. 使用 'BISONC++' 和 'FLEXC++'

文件被包含在输出中。

该程序的另一个额外功能是会忽略（标准 C++）注释行。注释行中的直接指令也会被忽略。

程序的创建分为五个主要步骤：

- 首先，构建文件词法分析器（lexer），其中包含输入语言的规范。
- 根据词法分析器中的规范生成 `Scanner` 类的要求。`Scanner` 继承自由 flexc++ 生成的基类 `ScannerBase`。
- 接下来，构建 `main` 函数。通过检查命令行参数创建一个 `Scanner` 对象。如果成功，调用扫描器的成员函数 `lex` 来产生程序的输出。
- 现在，扫描器的全局设置已完成，实现了各种类的成员函数。
- 最后，对程序进行编译和链接。

### 26.6.1.1 派生类 'Scanner'

匹配表达式规则 (lex) 的函数是 `Scanner` 类的成员。由于 `Scanner` 继承自 `ScannerBase`，它可以访问 `Scanner` 的所有执行扫描器正则表达式匹配算法的保护成员。

观察正则表达式本身，注意我们需要识别注释、#include 指令以及所有剩余字符。这些都是非常标准的做法。当检测到 #include 指令时，该指令将由扫描器解析。这是非常常见的做法。我们的词法扫描器执行以下任务：

- 像往常一样，预处理器指令不是由解析器分析，而是由词法扫描器分析；
- 扫描器将使用一个微扫描器从目录中提取文件名，如果失败则抛出异常；
- 如果提取了文件名，处理将切换到下一个流，并控制最大嵌套深度。
- 一旦处理完当前文件的末，会自动返回上一个文件，恢复之前的文件名和行号。如果所有文件都处理完毕，扫描器返回 0。

### 26.6.1.2 扫描器规范文件

词法规范文件的顺序与在 C 环境下用于 flex 的文件相似。然而，在 C++ 环境下，flex++ 创建的是 `Scanner` 类，而不仅仅是一个扫描器函数。

Flex++ 的规范文件包含两个部分：

- 规范文件的第一部分是 flex++ 的符号区域，用于定义符号（类似于微扫描器）或选项。建议使用以下选项：

  `%debug`: 在 flexc++ 生成的代码中包含调试代码。调用成员函数 `setDebug(true)` 可以在运行时激活这些调试代码。当激活时，有关匹配过程的信息将写入标准输出流。

在调用成员函数 `Debug(false)` 后，调试代码的执行将被抑制。

- `%filenames` 定义了 flexc++ 生成的类头文件的基名。如果未指定文件名，则使用默认类名（其本身使用默认的 `Scanner`）。

以下是规范字段区域：

```
%filenames scanner
%debug
%max-depth 3

%x           comment
      include
```

- 规范的第二部分是规则部分，在示例中定义了正则表达式及其关联的操作。在开发的示例中，词法分析器应该从标准输入流 (std::cin) 复制信息到标准输出流 (std::cout)。对于这个预定义宏，可以使用 `ECHO`。以下是规则：

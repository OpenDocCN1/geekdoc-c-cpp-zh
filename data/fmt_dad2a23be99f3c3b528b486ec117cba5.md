
```
// dc.h:
#include <map>
#include <string>
#include <iostream>

namespace Parser { double expr(bool); double term(bool); double prim(bool);
}

namespace Lexer {
enum class Kind : char {
    name, number, end,
    plus='+', minus='-', mul='*', div='/', print=';', assign='=', lp='(', rp=')'
};

struct Token {
    Kind kind;
    string string_value; double number_value;
};

class Token_stream {
public:
    Token(istream& s) : ip{&s}, owns{false}, ct{Kind::end} { }
    Token(istream* p) : ip{p}, owns{true}, ct{Kind::end} { }
    ~Token() { close(); }
    Token get();
    Token& current();
    // read and return next token
    // most recently read token
    void set_input(istream& s) { close(); ip = &s; owns=false; }
    void set_input(istream* p) { close(); ip = p; owns = true; }
private:
    void close() { if (owns) delete ip; }
    istream *ip; // pointer to an input stream
    bool owns; // does the Token_stream own the istream?
    Token ct {Kind::end}; // current_token
};
}

extern Token_stream ts;
namespace Table {
extern map<string,double> table;
}

namespace Error {
extern int no_of_errors; double error(const string& s);
}

namespace Driver {
void calculate();
}
```

关键字`extern`用于每个变量声明，以确保我们在各个`.cpp`文件中`#include dc.h`时不会发生多次定义。相应的定义可以在适当的`.cpp`文件中找到。

我根据`dc.h`中的声明需要添加了标准库头文件，但我没有添加仅为单个`.cpp`文件方便而需要的声明（例如`using`-声明）。

```
// lexer.cpp:

#include "dc.h"
#include <cctype>
#include <iostream> // redundant: in dc.h

Lexer::Token_stream ts;
Lexer::Token Lexer::Token_stream::get() { /* ... */ }
Lexer::Token& Lexer::Token_stream::current() { /* ... */ }
```

我对定义使用了显式限定，`Lexer::`，而不是简单地将它们全部封闭在`namespace Lexer { /* ... */ }`中

这避免了意外向`Lexer`添加新成员的可能性。另一方面，如果我想向`Lexer`添加不是其接口一部分的成员，我就必须重新打开命名空间 (§14.2.5)。

以这种方式使用头文件可确保头文件中的每个声明最终都会包含在包含其定义的`.cpp`文件中。例如，编译`lexer.cpp`时，编译器将看到：

```
namespace Lexer { // from dc.h
// …
class Token_stream {
public:
    Token get();
// …
};
// …

Lexer::Token Lexer::Token_stream::get() { /* ... */ }
```

这确保编译器会检测到为名称指定的类型不一致。例如，如果`get()`被声明为返回`Token`，但定义为返回`int`，则`lexer.cpp`的编译将因类型不匹配错误而失败。如果缺少定义，链接器会捕获该问题。如果缺少声明，一些`.cpp`文件将无法编译。

文件`parser.cpp`将如下所示：

```
// parser.cpp:
#include "dc.h"

double Parser::prim(bool get) { /* ... */ }
double Parser::term(bool get) { /* ... */ }
double Parser::expr(bool get) { /* ... */ }
```

文件`table.cpp`将如下所示：

```
// table.cpp:

#include "dc.h"

std::map<std::string,double> Table::table;
```

符号表是一个标准库的`map`。

文件`error.cpp`变为：

```
// error.cpp:

#include "dg.h"
// anymore #includes or declarations
int Error::no_of_errors;
double Error::error(const string& s) { /* ... */ }
```

最后，文件`main.cpp`将如下所示：

```
// main.cpp:

#include "dc.h"

#include <sstream>

#include <iostream> // redundant: in dc.h

void Driver::calculate() { /* ... */ }

int main(int argc, char * argv[]) { /* ... */ }
```

要被识别为程序的`main()`，`main()`必须是一个全局函数（§2.2.1, §15.4），因此这里没有使用命名空间。

系统的物理结构可以这样呈现：

```
<sstream> <map> <string> <cctype> <iostream>

dc.h

table.cpp parser.cpp main.cpp lexer.cpp error.cpp
```

顶部的头文件都是标准库设施的头文件。对于许多形式的程序分析，这些库可以被忽略，因为它们是众所周知且稳定的。对于微小的程序，结构可以通过将所有`#include`指令移到公共头文件中来简化。同样，对于小型程序，将`error.cpp`和`table.cpp`从`main.cpp`中分离出来通常是过度的。

这种单头文件的物理划分方式在程序很小且其各部分不打算单独使用时最有用。注意当使用命名空间时，程序的逻辑结构仍然在`dc.h`中表示。如果不使用命名空间，结构就会被掩盖，尽管注释可以提供帮助。

对于大型程序，在传统的基于文件的开发环境中，单头文件方法是不可行的。对公共头文件的更改会强制重新编译整个程序，并且由多个程序员更新该单个头文件容易出错。除非在编程风格上强烈强调依赖命名空间和类的使用，否则随着程序的增长，逻辑结构会恶化。

# 15.3.2 多头文件组织

一种替代的物理组织方式让每个逻辑模块都有自己的头文件来定义其提供的设施。每个`.cpp`文件然后都有一个对应的`.h`文件来指定它提供的内容（其接口）。每个`.cpp`文件包含其自己的`.h`文件，并且通常还包含其他`.h`文件，这些文件指定了它为了实现接口中宣传的服务而需要从其他模块获得的内容。这种物理组织对应于模块的逻辑组织。用户接口放在其`.h`文件中，实现者接口放在后缀为`_impl.h`的文件中，而模块对函数、变量等的定义则放在`.cpp`文件中。这样，解析器就由三个文件表示。解析器的用户接口由`parser.h`提供：

```
// parser.h:
namespace Parser { // interface for users
double expr(bool get);
}
```

为函数`expr()`、`prim()`和`term()`实现解析器所共享的环境由`parser_impl.h`呈现：

```
// parser_impl.h:

#include "parser.h" #include "error.h" #include "lexer.h"

using Error::error;

using namespace Lexer;

namespace Parser { // interface for implementers

double prim(bool get);

double term(bool get);

double expr(bool get);

}
```

如果我们使用了`Parser_impl`命名空间（§14.3.3），用户接口和实现者接口之间的区别会更清晰。

用户接口在头文件`parser.h`中被`#include`，以便编译器有机会检查一致性（§15.3.1）。

实现解析器的函数存储在`parser.cpp`中，并附带解析器函数所需的头文件的`#include`指令：

```
// parser.cpp:
#include "parser_impl.h" #include "table.h"
using Table::table;

double Parser::prim(bool get) {/*...*/}
double Parser::term(bool get) {/*...*/}
double Parser::expr(bool get) {/*...*/}
```

图形上，解析器及其驱动程序的使用如下所示：

```
parser.h lexer.h error.h table.h

parser_impl.h

# main.cpp parser.cpp
```

正如预期的那样，这与 §14.3.1 中描述的逻辑结构非常接近。为了简化此结构，我们本可以在`parser_impl.h`中`#include table.h`而不是在`parser.cpp`中。然而，`table.h`是不需要表达解析器函数共享上下文的东西的一个例子；它仅由其实现需要。事实上，它仅被一个函数`prim()`使用。

### Section 15.3.2 Multiple-Header Organization 437

因此，如果我们真的想最小化依赖关系，我们可以将`prim()`放在它自己的`.cpp`文件中并仅在那里`#include table.h`：

- `parser.h` `lexer.h` `error.h` `table.h`

- `parser_impl.h`

- `parser.cpp` `prim.cpp`

这种细化除非对于更大的模块，否则是不合适的。对于实际大小的模块，通常在需要为单个函数的地方`#include`额外的文件。此外，不少见的是有多个`_impl.h`，因为模块的不同函数子集需要不同的共享上下文。

请注意，`_impl.h`记法不是标准或甚至常见的约定；它只是我喜欢的命名方式。

为什么要费心使用这种更复杂的多个头文件方案？显然，把所有声明都扔进一个单一头文件，如对`dc.h`所做的那样，只需要远少得多的思考。

多头文件组织可扩展到比我们的玩具解析器大几个数量级的模块，以及比我们的计算器大几个数量级的程序。使用这种组织类型的根本原因是它提供了更好的关注点定位。在分析和修改大型程序时，程序员必须专注于相对较小的代码块。多头文件组织使得很容易确定解析器代码依赖于什么并忽略程序的其余部分。单头文件方法迫使我们查看任何模块使用的每个声明并决定它是否相关。简单事实是，代码的维护不可避免地是在不完整的信息和局部视角下进行的。多头文件组织使我们能够仅凭局部视角“由内而外”成功地工作。单头文件方法——像每个以全局信息存储为中心的组织一样——需要自上而下的方法，并且永远让我们怀疑到底什么依赖于什么。更好的定位导致编译模块所需的信息更少，从而编译更快。效果可能非常显著。我见过编译时间因简单的依赖分析导致更好的头文件使用而下降 1000 倍。

## 15.3.2.1 其他计算器模块

剩余的计算器模块可以像解析器一样组织。然而，这些模块太小，不需要自己的`_impl.h`文件。这样的文件仅在逻辑模块的实现由许多需要共享上下文的函数组成（除了提供给用户的内容）时才需要。

错误处理程序在`error.h`中提供其接口：

```
// error.h:

#include<string>

namespace Error {

int number_of_errors;

double error(const std::string&);

}
```

实现在`error.cpp`中找到：

```
// error.cpp:

#include "error.h"

int Error::number_of_errors;

double Error::error(const std::string&) { /* ... */ }
```

词法分析器提供了一个相当庞大且杂乱的接口：

```
// lexer.h:

#include<string> #include<iostream>

namespace Lexer {

enum class Kind : char { /* ... */ };

class Token { /* ... */ };

class Token_stream { /* ... */ };

extern Token_stream is;

}
```

除了`lexer.h`，词法分析器的实现还依赖于`error.h`以及`<cctype>`中的字符分类函数（§36.2）：

```
// lexer.cpp:
#include "lexer.h"
#include "error.h"
#include <iostream> // redundant: in lexer.h #include <cctype>
Lexer::Token_stream is; // defaults to "read from cin"
Lexer::Token Lexer::Token_stream::get() { /* ... */ };
Lexer::Token& Lexer::Token_stream::current() { /* ... */ };
```

我们本可以将`error.h`的`#include`指令提取为词法分析器的`_impl.h`文件。然而，我认为对于这个微小的程序来说这是过度的。

### Section 15.3.2.1 Other Calculator Modules 439

像往常一样，我们在模块的实现中`#include`模块提供的接口——在本例中为`lexer.h`——以便给编译器一个检查一致性的机会。

符号表本质上是自包含的，尽管标准库头文件`<map>`可能拖入各种有趣的东西来为高效的`map`模板类实现：

```
// table.h:

#include <map> #include <string>

namespace Table {

extern std::map<std::string,double> table;

}
```

因为我们假设每个头文件都可能被多个`.cpp`文件`#include`，所以必须将`Table`的声明与其定义分开：

```
// table.cpp:

#include "table.h"

std::map<std::string,double> Table::table;
```

我只是把驱动程序塞进了`main.cpp`：

```
// main.cpp:

#include "parser.h"

#include "lexer.h" // to be able to set ts

#include "error.h"

#include "table.h" // to be able to predefine names

#include <sstream> // to be able to put main()’s arguments into a string stream

namespace Driver {

void calculate() {/*...*/}

}

int main(int argc, char* argv[]) {/*...*/}
```

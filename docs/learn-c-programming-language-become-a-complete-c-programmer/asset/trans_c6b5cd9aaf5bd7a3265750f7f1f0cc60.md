

to going to the very end of a loop.

## 10.2.6 头文件

计算器使用标准库设施。因此，必须包含适当的头文件来完成程序：

```
#include<iostream> // I/O
#include<string> // strings
#include<map> // map
#include<cctype> // isalpha(), etc.
```

所有这些头文件都提供 std 命名空间中的设施，因此要使用它们提供的名称，我们必须使用 std:: 进行显式限定，或者通过以下方式将名称引入全局命名空间

```
using namespace std;
```

为了避免将表达式的讨论与模块化问题混淆，我采用了后者。第 14 章和第 15 章讨论了如何使用命名空间将此计算器组织成模块，以及如何将其组织成源文件。

## 10.2.7 命令行参数

程序编写并测试后，我发现先启动程序，然后输入表达式，最后退出很麻烦。我最常见的用途是计算单个表达式。如果该表达式可以作为命令行参数提供，则可以避免几次按键。

程序通过调用 main() 开始 (§2.2.1, §15.4)。执行此操作时，main() 会获得两个参数，指定参数数量，通常称为 argc，以及参数数组，通常称为 argv。参数是 C 风格字符字符串 (§2.2.5, §7.3)，因此 argv 的类型为 char*[argc+1]。程序名（在命令行中出现的形式）作为 argv[0] 传递，因此 argc 始终至少为 1。参数列表以零结尾；也就是说，argv[argc]==0。例如，对于命令

```
dc 150/1.1934
```

参数具有以下值：

```
argc: 2 argv: 0
"dc" "150/1.1934"
```

由于调用 main() 的约定与 C 共享，因此使用了 C 风格的数组和字符串。想法是以与从输入流读取相同的方式从命令字符串读取。读取字符串的流不出所料地称为

istringstream (§38.2.2)。因此，要计算命令行上提供的表达式，我们只需让我们的 Token_stream 从适当的 istream 读取即可：

```
Token_stream ts {cin};
int main(int argc, char * argv[]) {
switch (argc) {
case 1: // read from standard input break;
case 2: // read from argument string ts.set_input(new istringstream{argv[1]});
break;
default:
error("too many arguments");
return 1;
}
table["pi"] = 3.1415926535897932385; // insert predefined names table["e"] = 2.7182818284590452354;
calculate();
return no_of_errors;
}
```

要使用 **istringstream**，请包含 **<sstream>**。

很容易修改 **main()** 以接受多个命令行参数，但这似乎没有必要，尤其是可以作为单个参数传递多个表达式：

```
dc "rate=1.1934;150/rate;19.75/rate;217/rate"
```

我使用引号是因为 **;** 是我的 UNIX 系统上的命令分隔符。其他系统在程序启动时提供参数有不同的约定。

简单如它们是，**argc** 和 **argv** 仍然是轻微但令人讨厌的错误来源。为了避免这些错误，尤其是为了更轻松地传递程序参数，我倾向于使用一个简单的函数来创建 **vector<string>**：

```
vector<string> arguments(int argc, char * argv[])
{
vector<string> res;
for (int i = 0; i!=argc; ++i)
res.push_back(argv[i]);
return res;
}
```

更复杂的参数解析函数并不少见。

## 10.2.8 风格说明

对于不熟悉关联数组的程序员来说，将标准库 **map** 用作符号表似乎几乎像作弊。它不是。标准库和其他库就是为了被使用而设计的。通常，库在其设计和实现上投入的精力比程序员为仅在单个程序中使用的手工代码所能承受的要多。

查看计算器的代码，尤其是第一个版本，我们可以看到并没有太多传统的 C 风格、低级代码呈现。许多传统的棘手细节已被标准库类（如 **ostream**、**string** 和 **map** (§4.3.1, §4.2, §4.4.3, §31.4, 第 36 章, 第 38 章) 的使用所取代。

注意循环、算术和赋值的相对稀少。这是代码不直接操作硬件或实现低级抽象时应有的方式。

## 10.3 运算符摘要

本节介绍表达式的摘要和一些示例。每个运算符后面跟着一个或多个常用名称及其使用示例。在这些表中：

+   - *name* 是标识符（例如 **sum** 和 **map**）、运算符名称（例如 **operator int**、**operator+** 和 **operator”” km**）或模板特化的名称（例如 **sort<Record>** 和 **array<int,10>**），可能使用 **::** 限定（例如 **std::vector** 和 **vector<T>::operator[]**）。
+   - *class-name* 是类的名称（包括 **decltype(expr)**，其中 *expr* 表示一个类）。
+   - *member* 是成员名称（包括析构函数的名称或成员模板的名称）。
+   - *object* 是产生类对象的表达式。
+   - *pointer* 是产生指针的表达式（包括 **this** 和支持指针操作的该类型的对象）。
+   - *expr* 是表达式，包括字面量（例如 **17**、**“mouse”** 和 **true**）。
+   - *expr-list* 是（可能为空）的表达式列表。
+   - *lvalue* 是表示可修改对象的表达式 (§6.4.1)。
+   - *type* 只有在出现在括号中时才能是完全通用的类型名（带有 **∗**、**()** 等）；在其他地方，有限制 (§iso.A)。
+   - *lambda-declarator* 是（可能为空、以逗号分隔）的参数列表，可选后跟 **mutable** 说明符，可选后跟 **noexcept** 说明符，可选后跟返回类型 (§11.4)。
+   - *capture-list* 是指定上下文依赖的（可能为空）列表 (§11.4)。
+   - *stmt-list* 是（可能为空）的语句列表 (§2.2.4, 第 9 章)。

表达式的语法与操作数类型无关。此处介绍的含义适用于操作数为内置类型时 (§6.2.1)。此外，您可以为应用于用户定义类型的运算符定义含义 (§2.3, 第 18 章)。

表只能近似语法规则的细节。详情请参阅 §iso.5 和 §iso.A。

## 运算符摘要（继续） (§iso.5.1)

| Parenthesized expression | Lambda | Scope resolution | Scope resolution | Global |
|---|---|---|---|---|
| ( expr ) | [ capture-list ] lambda-declarator { stmt-list } §11.4 | class-name :: member §16.2.3 | namespace-name :: member §14.2.1 | :: name §14.2.1 |

每个方框包含具有相同优先级的运算符。较高方框中的运算符具有较高优先级。例如，**N::x.m** 表示 **(N::m).m** 而不是非法的 **N::(x.m)**。

## 运算符摘要（继续，继续）

- Member selection
- Member selection
- Subscribing
- Function call
- Value construction
- Function-style type conversion
- Post increment
- Post decrement
- Type identification
- Run-time type identification
- Run-time checked conversion
- Compile-time checked conversion
- Unchecked conversion
- **const** conversion
- Size of object
- Size of type
- Size of parameter pack
- Alignment of type
- Pre increment
- Pre decrement
- Complement
- Not
- Unary minus
- Unary plus
- Address of
- Dereference
- Create (allocate)
- Create (allocate and initialize)
- Create (allocate and initialize)
- Create (place)
- Create (place and initialize)
- Create (place and initialize)
- Destroy (deallocate)
- Destroy array
- Can expression throw?
- Cast (type conversion)
- Member selection
- Member selection

*object* · *member* §16.2.3  *pointer*-> *member* §16.2.3  *pointer* [ *expr* ] §7.3  *expr* ( *expr-list* ) §12.2  *type* { *expr-list* } §11.3.2  *type* ( *expr-list* ) §11.5.4  *lvalue* ++ §11.1.4  *lvalue*-- §11.1.4
typ​​eid ( *type* ) §22.5  **typeid** ( *expr* ) §22.5  **dynamic_cast** < *type* > ( *expr* ) §22.2.1  **static_cast** < *type* > ( *expr* ) §11.5.2  **reinterpret_cast** < *type* > ( *expr* ) §11.5.2  **const_cast** < *type* > ( *expr* ) §11.5.2  **sizeof** *expr* §6.2.8  **sizeof** ( *type* ) §6.2.8  **sizeof...** *name* §28.6.2
**alignof** ( *type* ) §6.2.9  ++ *lvalue* §11.1.4  -- *lvalue* §11.1.4  ~ *expr* §11.1.2  ! *expr* §11.1.1  - *expr* §2.2.2  + *expr* §2.2.2  & *lvalue* §7.2  * *expr* §7.2  **new** *type* §11.2  **new** *type* ( *expr-list* ) §11.2  **new** *type* { *expr-list* } §11.2  **new** ( *expr-list* ) *type* §11.2.4  **new** ( *expr-list* ) *type* (


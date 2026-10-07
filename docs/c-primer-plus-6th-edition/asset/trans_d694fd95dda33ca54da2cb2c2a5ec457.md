

# 第15章 友元、异常及其他

考虑清单 15.17 的核心：

```
Grand * pg;
Superb * ps;
for (int i = 0; i < 5; i++)
{
  pg = GetOne();
  pg->Speak();
  if (ps = dynamic_cast<Superb *>(pg))
    ps->Say();
}
```

通过使用 typeid 并忽略比原文更长的写法，它有严重缺陷，即显式命名每个类。假设你可以将此代码改写如下：

```
Grand * pg;
Superb * ps;
Magnificent * pm;
for (int i = 0; i < 5; i++)
{
  pg = GetOne();
  if (typeid(Magnificent) == typeid(pg))
  {
    pm = (Magnificent *) pg;
    pm->Speak();
    pm->Say();
  }
  else if (typeid(Superb) == typeid(pg))
  {
    ps = (Superb *) pg;
    ps->Speak();
    ps->Say();
  }
  else
    pg->Speak();
}
```

不仅这比原文更丑陋更长，而且它有严重缺陷，即显式命名每个类。假设，例如，你发现有必要从 Magnificent 类派生一个 Insufferable 类。并且假设新类重新定义了 Speak() 和 Say()。使用 typeid 显式测试每种类型的方法，你必须修改 for 循环代码，添加一个新的 else if 部分。然而，原版本完全不需要任何更改。以下语句适用于从 Grand 派生的所有类：

```
pg->Speak();
```

而以下语句适用于从 Superb 派生的所有类：

```
if(ps = dynamic_cast<Superb *>(pg))
  ps->Say();
```

## 类型转换运算符

### 提示

如果你发现自己在一段扩展的 if else 语句中使用 typeid，你应该检查是否应改用虚函数和 dynamic_cast。

### 类型转换运算符

在 Bjarne Stroustrup 看来，C 风格的类型转换运算符过于宽松。例如，考虑以下内容：

```
struct Data
{
    double data[200];
}
struct Junk
{
    int junk[100];
}
Data d = (2.5e33, 3.5e-19, 20.2e32);
char * pch = (char*) (&); // type cast #1 - convert to string
char ch = char (&); // type cast #2 - convert address to a char
Junk * pj = (Junk*) (&); // type cast #3 - convert to Junk pointer
```

首先，这三种类型转换中有哪一种有意义？除非诉诸于不切实际，否则它们都没有意义。其次，这三种类型转换中有哪三种是允许的？在 C 中，它们全部都是允许的。Stroustrup 对这种宽松性的回应是收紧一般类型转换的允许范围，并添加了四个类型转换运算符，以为转换过程提供更多纪律：

```
dynamic_cast
const_cast
static_cast
reinterpret_cast
```

而不是使用一般类型转换，你可以选择一个适合特定目的的运算符。这记录了类型转换的预期原因，并给编译器一个机会来检查你是否做了你认为你做的事情。

你已经见过 dynamic_cast 运算符。假设 High 和 Low 是两个类，ph 的类型为 *，pl 的类型为 *。那么以下语句仅在 Low 是 High 的可访问基类（直接或间接）时，才将 Low * 指针分配给 pl：

```
pl = dynamic_cast<Low *> ph;
```

否则，语句将空指针分配给 pl。通常，运算符具有以下语法：

```
dynamic_cast < type-name > (expression)
```

该运算符的目的是允许在类层次结构内进行上转型，这种类型转换因 is-a 关系而安全，并禁止其他转换。该运算符用于进行类型转换，其唯一目的是改变值是否为 const 或 volatile。它具有与 dynamic_cast 运算符相同的语法。

```
const_cast < type-name > (expression)
```

进行此类类型转换的结果如果更改了类型的任何其他部分，则为错误。即 type_name 和 expression 必须为同一类型，只是它们可能在 const 或 volatile 的存在上有所不同。同样，假设 High 和 Low 是两个类：

```
High bar;
const High * pbar = &bar;

High * pb = const_cast<High *>(pbar); // valid
Low * pl = const_cast<Low *>(pbar); // invalid
```

第一个类型转换 *pb 一个指针，可用于更改 bar 的值；它移除了 const 标签。第二个类型转换无效，因为它试图将类型从 const High * 更改为 Low *。

该运算符的原因是你偶尔可能需要一个大多数时间是常量但偶尔可以更改的值。在这种情况下，你可以将值声明为 const，并在需要更改值时使用 const_cast。这可以用一般类型转换来完成，但一般类型转换同时也会更改类型：

```
High bar;
const High * pbar = &bar;

High * pb = (High *) (pbar); // valid
Low * pl = (Low *) (pbar); // also valid
```

因为同时更改类型和常量的可能是一个无意的编程失误，使用 const_cast 运算符更安全。const_cast 并非功能强大。它可以更改对量的指针访问，但尝试更改声明为 const 的量的效果是未定义的。让我们用 15.19 中所示的简短示例来澄清这一陈述。

# 清单 15.19 constcast.cpp

```
// constcast.cpp -- using const_cast<
#include <iostream>
using std::cout;
using std::endl;
```

```
void change(const int * pt, int n);

int main()
{
    int pop1 = 38383;
    const int pop2 = 2000;

    cout << "pop1, " << pop1 << ", " << pop2 << endl;
    change(&pop1, -103);
    change(&pop2, -103);
    cout << "pop1, pop2: " << pop1 << ", " << pop2 << endl;
    return 0;
}
```

```
void change(const int * pt, int n)
{
    int * pc;

    pc = const_cast<int *>(pt);
    *pc += n;
}
```

const_cast 运算符可以从 const int * pt 中移除 const，从而允许编译器接受 change 中的以下语句：

```
*pc += n;
```

然而，因为 pop2 被声明为 const，编译器可能会保护它免于任何更改，如以下示例输出所示：
pop1, pop2: 38383, 2000
pop1, pop2: 38280, 2000

正如你所见，pop1 发生了更改但 pop2 没有。指针被声明为 const *，因此它不能更改指向的 int 的值。指针 pc 移除了 const，因此它可用于更改指向的值，但前提是该值本身不是 const。因此，pc 可用于更改 pop1 但不能更改 pop2。

static_cast 运算符与其他运算符具有相同的语法：
static_cast <type-name> (expression)

它仅在 type_name 可以隐式转换为 expression 所具有的相同类型，或反之亦然时才有效。类型转换是错误。假设 High 是 Low 的基类，Pond 是一个不相关的类。那么从 High 到 Low 以及从 Low 到 High 的转换是有效的，但从 Low 到 Pond 的转换是不允许的：

High bar;
Low blow...

# 第15章 友元、异常及其他

```
High * pb = static_cast<High *>(&blow); // valid upcast
Low * pl = static_cast<Low *>(&bar); // valid downcast
Pond * pmer = static_cast<Pond *>(&blow); // invalid, Pond unrelated
```

第一个转换是有效的，因为上转型可以是显式的。第二个转换，从基类指针到派生类指针，不能在没有显式转换的情况下进行。但因为在其他情况下可以不使用类型转换进行类型转换，所以使用 static_cast 进行下转型是有效的。

同样，枚举值可以不使用类型转换转换为整型值，整型值可以用 static_cast 转换为枚举值。你也可以使用 static_cast 将 double 转换为 int，将 float 转换为 long，并执行其他数值转换。

reinterpret_cast 运算符是固有风险的类型转换。它不允许你转换掉 const，但允许其他不安全的操作。有时程序员需要做实现相关、不安全的事情，而使用 reinterpret_cast 运算符使得跟踪此类行为变得不可能。它具有与另外三个运算符相同的语法：

```
reinterpret_cast <type-name> (expression)
```

这里有一个示例用法：

```
struct {long a; short b;};
long value = 0xA224B1B;
dat * pd = reinterpret_cast<dat *>(&value);
cout << hex << pd->da; // display first 2 bytes of value
```

通常，类型转换用于低级、实现相关的编程，并且不可移植。例如，一个系统可能以与另一个系统不同的顺序存储多字节值中的字节。

reinterpret_cast 运算符并不允许任何事情。例如，你可以将指针转换为足够大的整数类型以容纳指针表示，但你不能将指针转换为较小的整数或浮点类型。另一个限制是，你不能将函数指针转换为数据指针，反之亦然。

C++ 中的普通类型转换也被限制了。基本上，它可以做其他类型转换所能做的所有事情，一些组合，如 static_cast 或 reinterpret_cast 后跟 const_cast，但它不能做其他任何事情。因此，以下类型转换在 C 中是允许的，但在 C++ 实现中通常不允许，因为 char 太小而无法容纳指针实现：

```
char ch = char (&value); // type cast #2 - convert address to a char
```

这些限制是有意义的，但如果你发现这种强制的判断令人压抑，你仍然可以使用 C。


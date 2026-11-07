
```cpp
class Grand
{
private:
    int hold;
public:
    Grand(int h = 0) : hold(h) {}
    virtual void Speak() const { cout << "I am a grand class!\n"; }
    virtual int Value() const { return hold; }
};

class Superb : public Grand
{
public:
    Superb(int h = 0) : Grand(h) {}
    void Speak() const { cout << "I am a superb class!!\n"; }
    virtual void Say() const
        { cout << "I hold the superb value of " << Value() << "!\n"; }
};

class Magnificent : public Superb
{
private:
    char ch;
public:
    Magnificent(int h = 0, char cv = 'A') : Superb(h), ch(cv) {}
    void Speak() const { cout << "I am a magnificent class!!!\n"; }
    void Say() const { cout << "I hold the character " << ch <<
                " and the integer " << Value() << "!\n"; }
};

Grand * GetOne();
int main()
{
    srand(time(0));
    Grand * pg;
    Superb * ps;
    for (int i = 0; i < 5; i++)
    {
        pg = GetOne();
        cout << "Now processing type " << typeid(*pg).name() << ".\n";
        pg->Speak();
        if (ps = dynamic_cast<Superb *>(pg))
            ps->Say();
        if (typeid(Magnificent) == typeid(*pg))
            cout << "Yes, you're really magnificent.\n";
    }
    return 0;
}

Grand * GetOne()
{
    Grand * p;

    switch( rand() % 3)
    {
        case 0: p = new Grand(rand() % 100);
                break;
        case 1: p = new Superb(rand() % 100);
                break;
        case 2: p = new Magnificent(rand() % 100, 'A' + rand() % 26);
                break;
    }
    return p;
}
```

以下是程序清单 15.18 中程序的一次示例运行：

```text
Now processing type Magnificent.
I am a magnificent class!!!
I hold the character P and the integer 52!
Yes, you're really magnificent.
Now processing type Superb.
I am a superb class!!
I hold the superb value of 37!
Now processing type Grand.
I am a grand class!
Now processing type Superb.
I am a superb class!!
I hold the superb value of 18!
Now processing type Grand.
I am a grand class!
```

与前一个示例一样，确切的输出会因每次运行而异，因为程序使用 `rand()` 来选择类型。此外，某些编译器在调用 `name()` 时可能提供不同的输出，例如输出 `Grand` 而不是 `Grand`。

## 误用 RTTI

RTTI 在 C++ 社区中有许多直言不讳的批评者。他们认为 RTTI 是不必要的，是程序低效的潜在来源，也可能是不良编程实践的促成因素。我们不深入探讨关于 RTTI 的争论，而是看看你应该避免的那类编程方式。

请看程序清单 15.17 的核心部分：

```cpp
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

通过使用 typeid 并忽略 dynamic_cast 和虚函数，你可以将这段代码改写如下：

```cpp
Grand * pg;
Superb * ps;
Magnificent * pm;
for (int i = 0; i < 5; i++)
{
    pg = GetOne();
    if (typeid(Magnificent) == typeid(*pg))
    {
        pm = (Magnificent *) pg;
        pm->Speak();
        pm->Say();
    }
    else if (typeid(Superb) == typeid(*pg))
    {
        ps = (Superb *) pg;
        ps->Speak();
        ps->Say();
    }
    else
        pg->Speak();
}
```

这不仅比原版本更丑陋、更长，而且还有一个严重缺陷：显式命名每个类。例如，假设你发现有必要从 Magnificent 类派生出一个 Insufferable 类。并假设新类重新定义了 Speak() 和 Say()。对于使用 typeid 显式测试每种类型的版本，你将不得不修改 for 循环代码，添加一个新的 else if 分支。然而，原版本完全不需要修改。下面的语句适用于所有从 Grand 派生的类：

```cpp
pg->Speak();
```

而这条语句适用于所有从 Superb 派生的类：

```cpp
if (ps = dynamic_cast<Superb *>(pg))
    ps->Say();
```

**提示**

如果你发现自己在一长串 `if else` 语句中使用 `typeid`，你应该检查是否应改用虚函数和 `dynamic_cast`。

## 类型转换运算符

在 Bjarne Stroustrup 看来，C 风格的类型转换运算符过于宽松。例如，考虑以下代码：

```cpp
struct Data
{
    double data[200];
};

struct Junk
{
    int junk[100];
};
Data d = {2.5e33, 3.5e-19, 20.2e32};
char * pch = (char *) (&d);   // type cast #1 - convert to string
char ch = (char) (&d);        // type cast #2 - convert address to a char
Junk * pj = (Junk *) (&d);    // type cast #3 - convert to Junk pointer
```

首先，这三种类型转换中哪一种有意义？除非你诉诸难以置信的做法，否则它们都没有太大意义。其次，这三种类型转换中哪些是允许的？在 C 中，全部都是允许的。Stroustrup 对这种宽松性的回应是收紧通用类型转换的允许范围，并添加四个类型转换运算符，为转换过程提供更多约束：

```cpp
dynamic_cast
const_cast
static_cast
reinterpret_cast
```

你可以选择一个适合特定目的的运算符，而不是使用通用类型转换。这样可以记录类型转换的预期原因，并让编译器有机会检查你是否做了自己认为做过的事。

你已经见过 `dynamic_cast` 运算符。总结一下，假设 High 和 Low 是两个类，`ph` 的类型是 `High *`，`pl` 的类型是 `Low *`。那么，仅当 Low 是 High 的可访问基类（直接或间接）时，下面的语句才会将一个 `Low *` 指针赋给 `pl`：

```cpp
pl = dynamic_cast<Low *>(ph);
```

否则，该语句将空指针赋给 `pl`。一般来说，该运算符具有以下语法：

```cpp
dynamic_cast < type-name > (expression)
```

该运算符的目的是允许在类层次结构内进行向上转换（由于 is-a 关系，这种类型转换是安全的），并禁止其他转换。

const_cast 运算符用于进行类型转换，其唯一目的是改变某个值是否为 const 或 volatile。它的语法与 dynamic_cast 运算符相同：

```cpp
const_cast < type-name > (expression)
```

如果类型的任何其他方面被改变，则进行这种类型转换的结果就是错误。也就是说，type_name 和 expression 必须具有相同类型，只是它们在是否带有 const 或 volatile 方面可以不同。再次假设 High 和 Low 是两个类：

```cpp
High bar;
const High * pbar = &bar;
...
High * pb = const_cast<High *> (pbar);    // valid
const Low * pl = const_cast<const Low *> (pbar);    // invalid
```

第一个类型转换使 *pb 成为一个可用于修改 bar 对象值的指针；它移除了 const 标签。第二个类型转换无效，因为它试图将类型从 const High * 改为 const Low *。

这个运算符存在的原因是，有时你可能需要一个大多数时间保持不变但偶尔可以更改的值。在这种情况下，你可以将该值声明为 const，并在需要修改该值时使用 const_cast。这可以使用通用类型转换来完成，但通用类型转换也可能同时改变类型：

```cpp
High bar;
const High * pbar = &bar;
...
High * pb = (High *) (pbar);       // valid
Low * pl = (Low *) (pbar);         // also valid
```

由于同时改变类型和 const 属性可能是无意的编程失误，因此使用 const_cast 运算符更安全。

const_cast 并非无所不能。它可以改变对某个量的指针访问权限，但试图修改一个声明为 const 的量的效果是未定义的。让我们用程序清单 15.19 中所示的简短示例来阐明这一点。

### 程序清单 15.19  constcast.cpp

```cpp
// constcast.cpp -- using const_cast<>
#include <iostream>
using std::cout;
using std::endl;

void change(const int * pt, int n);

int main()
{
    int pop1 = 38383;
    const int pop2 = 2000;

    cout << "pop1, pop2: " << pop1 << ", " << pop2 << endl;
    change(&pop1, -103);
    change(&pop2, -103);
    cout << "pop1, pop2: " << pop1 << ", " << pop2 << endl;
    return 0;
}

void change(const int * pt, int n)
{
    int * pc;

    pc = const_cast<int *>(pt);
    *pc += n;
}
```

`const_cast` 运算符可以从 `const int * pt` 中移除 const，从而允许编译器接受 `change()` 中的以下语句：

```cpp
*pc += n;
```

然而，由于 `pop2` 被声明为 const，编译器可能会保护它免受任何更改，如下面的示例输出所示：

```text
pop1, pop2: 38383, 2000
pop1, pop2: 38280, 2000
```

如你所见，对 `change()` 的调用改变了 `pop1`，但没有改变 `pop2`。`change()` 中的指针被声明为 `const int *`，因此不能用它来改变所指向的 int 的值。指针 `pc` 已通过转换移除 const，因此可以用它来改变所指向的值，但前提是该值本身不是 const。因此，`pc` 可用于修改 `pop1`，但不能修改 `pop2`。

`static_cast` 运算符与其他运算符具有相同的语法：

```cpp
static_cast < type-name > (expression)
```

仅当 `type_name` 可以隐式转换为 `expression` 所具有的类型，或反之，它才有效。否则，该类型转换就是错误。假设 High 是 Low 的基类，而 Pond 是一个无关的类。那么从 High 到 Low 以及从 Low 到 High 的转换是有效的，但从 Low 到 Pond 的转换是不允许的：

```cpp
High bar;
Low blow;
...
```

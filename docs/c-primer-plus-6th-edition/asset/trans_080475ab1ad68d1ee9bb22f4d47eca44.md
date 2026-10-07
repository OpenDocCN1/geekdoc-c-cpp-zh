

# 第 15 章 朋友、异常及更多

```cpp
class Grand
...
virtual void Speak();
```

| class Superb |
| class Grand |
| ... virtual void Speak(); | void Speak(); <- 重定义 |
| virtual void Say(); <- 新 |

| class Magnificent |
| class Superb |
| class Grand |
| ... virtual void Speak(); | char ch(); void Speak(); <- 重定义
 virtual void Say(); <- 重定义 |

图 15.4 Grand 类族。

你不能直接使用这种方法（使用指向 `Grand` 的指针）来调用 `Say` 函数；因为它在 `Grand` 类中没有定义。但是，你可以使用 `dynamic_cast` 运算符来检查 `pg` 是否可以转换为指向 `Superb` 的指针。如果对象是 `Superb` 或 `Magnificent`，则结果为真。在任何情况下，你都可以安全地调用 `Say()` 函数：

```cpp
if (ps = dynamic_cast<Superb*>(pg))
ps->Speak();
```

记住，赋值表达式的值是其左侧的值。因此，`if` 条件的值是 `ps`。如果转换成功，`ps` 为非零（或真）。如果转换失败，且 `pg` 指向一个 `Grand` 对象，则 `ps` 为 0（或假）。列表 15.17 显示了完整的代码。（顺便说一下，某些编译器注意到程序员通常在 `if` 语句中使用 `=` 运算符，可能会对无意赋值发出警告。）

# 列表 15.17 rttil.cpp

```cpp
// 使用 RTTI 动态 dynamic_cast 运算符的 rttil.cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
```

```cpp
std::cout;
```

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
  void Speak() const { cout << "I am a superb class!\n"; }
  virtual void Say() const {
    cout << "I hold the superb value of " << Value() << "\n";
  }
};

class Magnificent : public Superb
{
private:
  char ch;
public:
  Magnificent(int h = 0, char c = 'A') : Superb(h), ch(c) {}
  void Speak() const { cout << "I am a magnificent class!\n"; }
  void Say() const {
    cout << "I hold the character " << ch << " and the integer " << Value() << "\n";
  }
};

Grand * GetOne();

int main() {
  std::srand(std::time(0));
  Grand * pg;
  Superb * ps;
  for (int i = 0; i < 5; i++) {
    pg = GetOne();
    pg->Speak();
    if (ps = dynamic_cast<Superb *>(pg))
      ps->Say();
  }
  return 0;
}
```

# 第 15 章 朋友、异常及更多

```cpp
Grand * GetOne() // 随机生成三种对象中的一种
{
    Grand * p;
    switch (std::rand() % 3) {
        case 0: p = new Grand(std::rand() % 100);
            break;
        case 1: p = new Superb(std::rand() % 100);
            break;
        case 2: p = new Magnificent(std::rand() % 100,
            'A' + std::rand() % 26);
            break;
    }
    return p;
}
```

> 注意
 即使你的编译器支持 RTTI，它也可能默认关闭该功能。如果该功能未激活，程序可能仍然编译但会产生运行时错误。如果你发现是这种情况，应该检查你的文档或探索菜单选项。

列表 15.17 中的程序说明了一个重要的点：你应该尽可能地使用虚函数，只有在必要时才使用 RTTI。以下是一些示例输出：

```
I am a superb class!!
I hold the superb value of 68!
I am a magnificent class!!
I hold the character R and the integer 68!
I am a magnificent class!!
I hold the character D and the integer 12!
I am a magnificent class!!
I hold the character V and the integer 59!
I am a grand class!
```

如你所见，`Say()` 方法被用于 `Superb` 和 `Magnificent` 类（输出每次运行都会不同，因为程序使用 `rand()` 来选择对象类型）。
你也可以对引用使用 `dynamic_cast`。用法略有不同；没有与空指针类型对应的引用值，因此没有特殊的引用值可以指示失败。相反，当受到不当请求引导时，`dynamic_cast` 会抛出 `bad_cast` 异常，该异常派自异常类并定义在 `typeinfo` 头文件中。因此，该运算符可以如下使用，其中 `rg` 是指向 `Grand` 的引用：

```cpp
#include <typeinfo> // 用于 bad_cast
try {
```

```cpp
Superb & rs = dynamic_cast<Superb>(rg);
...
catch(bad_cast &) {
...
};
```

# typeid 运算符和 type_info 类

`typeid` 运算符让你确定两个对象是否为相同类型。类似于 `sizeof`，它接受两种类型的参数：

- 类的名称
- 结果值为对象的表达式

`typeid` 运算符返回对 `type_info` 对象的引用，其中 `type_info` 是定义在 `typeinfo` 头文件（以前为 `typeinfo.h`）中的类。`type_info` 类重载了 `==` 和 `!=` 运算符，你可以使用这些运算符比较类型。例如，如果 `pg` 指向 `Magnificent`，则下面的表达式值为 `true`，否则为 `false`：

```cpp
typeid(Magnificent) == typeid(pg)
```

如果 `pg` 刚好是一个空指针，程序将抛出 `bad_type` 异常。此异常类型派自异常类并在 `typeinfo` 头文件中声明。

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;

```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 ` `()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

`type_info` 类的实现在厂商间有所不同，但它包含一个 `name()` 成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

```cpp
cout << typeid(pg).name() << endl;
```

# 列表 15.18 rttil.cpp

```cpp
int main() {
    rand(time(0));
    Grand * pg;
    Superb * ps;
    for (int i = 0; i < 5; i++) {
        pg = GetOne();
        cout << "Now processing type " << typeid(pg).name() << "\n";
        pg->Speak();
        if (ps = dynamic_cast<Superb *>(pg)) {
            ps->Say();
        }
        if (typeid(Magnificent) == typeid(*pg)) {
            cout << "Yes, you're really magnificent.\n";
        }
    }
    return 0;
}
```

这里是列表 15.18 程序的示例运行：

```
Now processing type Magnificent.
I am a magnificent class!!!
i hold the character P and the integer 52!
Yes, you're really magnificent.
Now processing type Super.
I am a superb class!!
I hold the superb value of 37!
Now processing type Grand.
I am a grand class!
Now processing type Super.
I am a superb class!!
I hold the superb value of 18!
Now processing type Grand.
I am a grand class!
```

与前面的示例一样，输出每次运行都会不同，因为程序使用 `rand()` 来选择类型。此外，某些编译器在调用 `name()` 时可能会提供不同的输出，例如 `5Grand` 而不是 `Grand`。

# 误用 RTTI

RTTI 在 C++ 社区中有许多公开的批评者。他们认为 RTTI 是不必要的、程序效率下降的潜在来源，也是糟糕编程实践的可能因素。在不深入探讨关于 RTTI 的争论之前，让我们来看看应该避免的编程方式。



`type_info`类的实现在厂商间有所不同，但它包含一个`name()`成员，返回一个取决于实现的字符串，该字符串通常是（但不一定为）类的名称。例如，下面的语句显示该类的字符串：

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

与前面的示例一样，输出每次运行都会不同，因为程序使用`rand()`来选择类型。此外，某些编译器在调用`name()`时可能会提供不同的输出，例如`5Grand`而不是`Grand`。

# 误用 RTTI

RTTI 在 C++ 社区中有许多公开的批评者。他们认为 RTTI 是不必要的、程序效率下降的潜在来源，也是糟糕编程实践的可能因素。在不深入探讨关于 RTTI 的争论之前，让我们来看看应该避免的编程方式。

# 第 15 章 朋友、异常及更多

考虑列表 15.17 的核心：

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

通过使用`typeid`并忽略比原始代码更长的类型，它有一个必须显式列出每个类的名的严重缺陷。假设你可以将此代码重写为如下：

```cpp
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

这不仅比原始代码更丑、更长，而且具有必须显式列出每个类的名的严重缺陷。例如，假设你发现必要从`Magnificent`类派生一个`Insufferable`类。假设新类重新定义了`Speak()`和`Say()`。在使用使用`typeid`显式测试每个类型的版本，你必须修改`for`循环代码，添加一个新的`else if`部分。然而，原始版本完全不需要任何更改。以下语句对于所有派自`Grand`的类都有效：

```cpp
pg->Speak();
```

此语句对于所有派自`Superb`的类都有效：

```cpp
if(ps = dynamic_cast<Superb *>(pg))
  ps->Say();
```

## 类型强制转换运算符

## 提示

如果你发现自己自己在一系列连续的`if else`语句中使用`typeid`，你应该检查是否应该改用虚函数和`dynamic_cast`。

### 类型强制转换运算符

在 Bjarne Stroustrup 看来，C 语言的类型强制转换运算符太松散了。例如，考虑以下内容：

```cpp
struct Data
{
    double data[200];
}
struct Junk
{
    int junk[100];
}
Data d = (2.5e33, 3.5e-19, 20.2e32);
char * pch = (char*) (&); // 强制转换 #1 - 转换为字符串
char ch = char (&); // 强制转换 #2 - 将地址转换为 char
Junk * pj = (Junk*) (&); // 强制转换 #3 - 转换为 Junk 指针
```

首先，这三种强制转换中哪一个是有意义的？除非采取不可手段，否则它们都没有意义。其次，这三种强制转换中哪些是允许的？在 C 语言中，都是允许的。Stroustrup 对这种松散性的反应是收紧通用强制转换的允许范围，并添加四个强制转换运算符，为转换过程提供更多纪律：

```
dynamic_cast
const_cast
static_cast
reinterpret_cast
```

与其使用通用强制转换，不如选择一个适用于特定目的的运算符。这记录了强制转换的意图，并给了编译器机会检查你是否执行了你想的操作。

你已经看到过`dynamic_cast`运算符。假设`High`和`Low`是两个类，`ph`是类型`*`，`pl`是类型`*`。那么以下语句仅当`Low`是`High`的可访问基类（直接或间接）时，将`Low *`指针赋给`pl`：

```cpp
pl = dynamic_cast<Low *> ph;
```

否则，该语句将空指针赋给`pl`。通常，该运算符具有此语法：

```cpp
dynamic_cast < type-name > (expression)
```

该运算符的目的是允许在类层次结构中向上转换，使得此类强制转换因为“是-a”关系而是安全的，并禁止其他转换。该运算符用于唯一目的是改变一个值是否为`const`或`volatile`的类型强制转换。它的语法与`dynamic_cast`运算符相同。

```cpp
const_cast < type-name > (expression)
```

如果修改了类型的任何其他部分，进行此类强制转换的结果将是错误。也就是说，`type_name`和`expression`必须类型相同，但在存在`const`或`volatile`时可以不同。再次假设`High`和`Low`是两个类：

```cpp
High bar;
const High * pbar = &bar;
High * pb = const_cast<High *>(pbar); // 有效
Low * pl = const_cast<Low *>(pbar); // 无效
```

第一个强制转换 *pb* 是一个可以修改`bar`值的指针；它移除了`const`标签。第二个强制转换是无效的，因为它尝试将类型从`const High *`改为`Low *`。

该运算符的原因是，你偶尔需要一个大部分时间是常量但偶尔可以更改的值。在这种情况下，你可以将值声明为`const`并在需要更改值时使用`const_cast`。这可以使用通用强制转换完成，但通用强制转换同时也改变了类型：

```cpp
High bar;
```

## 总结

友元（friend）允许你为类开发更灵活的接口。类可以拥有其他函数、其他类以及其他类的成员函数作为友元。在某些情况下，你可能需要使用前向声明，并仔细处理类声明和方法的顺序，以确保友元关系能够正确建立。

嵌套类是在其他类内部声明的类。嵌套类有助于设计辅助类，这些辅助类用于实现其他类的功能，但不需要是公共接口的一部分。

C++ 异常机制提供了一种灵活的方法来处理棘手的编程事件，例如不适当的值、I/O 操作失败等。抛出异常会终止直接或间接导致该异常的函数调用，异常必须在 try catch 块中进行处理。catch 块紧跟在 try 块之后，为了捕获异常，catch 块会执行其在 catch 块中的代码。这些代码可以尝试修复问题，也可以终止程序。类可以设计为嵌套类，当检测到特定于类的问题时可以抛出这些嵌套类。函数可以包含异常规范，用于标识在该函数中可能抛出的异常，尽管 C++11 弃用了该功能。未被捕获的异常（即没有 catch 块的异常）默认会终止程序。意外异常（不匹配异常规范的异常）也是如此。`dynamic_cast`运算符用于将派生类指针转换为转换为基类指针；其主要目的是确保调用虚拟函数是安全的。`typeid`返回一个`type_info`对象。可以通过比较两个`type_id`值来确定对象是否属于特定类型，返回的`type_info`对象可用于获取对象的信息。

`dynamic_cast`、`static_cast`、`const_cast`和`reinterpret_cast`运算符提供了比通用类型转换机制更安全、文档更良好的类型转换。

# 章节复习

- 1. 以下建立友元的尝试中有哪些错误？
    - a. class snap {
      friend clasp;
      };
      class clasp {
      };

    - b. class cuff {
      public:
      void snip(muff & &) { ... }
      };

```cpp
};
class muff {
  friend void cuff::snip(muff &);
  ...
};
```

```cpp
c. class muff {
  friend void cuff::snip(muff &);
  ...
};
class cuff {
  public:
  void snip(muff &) { ... }
  ...
};
```

- 2. 你已经见过如何创建类的相互友元。是否存在一种只有类 B 的某些成员是类 A 的友元，而类 A 的某些成员是 B 的友元的形式？请解释。

- 3. 以下嵌套类声明可能存在什么问题？
```cpp
class Ribs
{
private:
  class Sauce
  {
    int soy;
    int sugar;
  public:
    Sauce(int s1, int s2) : soy(s1), sugar(s2) { }
  ...
};
```

- 4. `throw`和`return`有什么区别？

- 5. 假设你有一个派生自基异常类的异常层次结构。你应该以什么顺序放置 catch 块？

- 6. 考虑本章定义的 Grand、Super 和 Magnificent 类。Super-pose `pg`是一个 Grand * 类型的指针，被分配了这三个类中一个对象的地址，`ps`是一个 Super * 类型的指针。这两个代码示例的行为有何不同？

```cpp
if (ps = dynamic_cast<Super *>(pg))
ps->say(); // 示例 #1
```

```cpp
if (typeid(*pg) == typeid(Superb))
  ((Superb *) pg)->say(); // 示例 #2
```


你必须了解关于拷贝构造函数的两点：它是何时被使用的以及它做了什么。

# 何时使用拷贝构造函数

每当创建一个新对象并初始化为相同类型的现有对象时，就会调用拷贝构造函数。这种情况发生在几种情况下。最明显的情况是你显式地将新对象初始化为现有对象。例如，假设 `motto` 是一个 `String` 对象，以下声明会调用拷贝构造函数：

```
String detto(motto);               // 调用 String(const String &)

String metodo = motto;            // 调用 String(const String &)

String bad also = String(motto); // 调用 String(const String &)

String * pStringBad = new StringBad(motto);// 调用 String(const String &)
```

取决于实现方式，这些声明可能使用拷贝构造函数来创建 `motto` 以及，或者它们可能使用拷贝构造函数生成临时对象，然后将这些的内容赋值给 `metodo` 和 `also`。最后一个示例将匿名对象初始化为 `motto`，并将新对象的地址赋值给 `pstring` 指针。

不那么明显的是，每当程序生成对象的副本时，编译器都会使用拷贝构造函数。特别是在函数按值传递对象时（如列表 12.3 中的 `callme2()` 所示）或函数返回一个对象时。记住，按值意味着创建原始变量的副本。编译器在生成临时对象时也会使用拷贝构造函数。例如，在相加三个 `Vector` 对象时，编译器可能会生成一个临时 `Vector` 对象来保存中间结果。编译器在生成临时对象方面各不相同，但在按值传递和返回对象时，都会调用拷贝构造函数。特别是，列表 12.3 中的这个函数使用了拷贝构造函数：

```
callme2(headline2);
```

程序使用拷贝构造函数来初始化 `sb`，它是 `callme2()` 函数的形式 `StringBad` 类型参数。

顺便说一下，按值传递对象涉及调用拷贝构造函数，这是改为按引用传递的好理由。这节省了调用构造函数的时间并

# 默认构造函数做了什么

默认构造函数执行成员级拷贝。也就是说，它将对象的每个成员的值拷贝到新对象中。这也称为浅拷贝。在列表 12.3 的情况下，效果是：

```
StringBad = sports;
```

这并没有拷贝字符串；它拷贝的是字符串的指针。也就是说，在 `sailor` 初始化为 `str` 后，你得到了指向同一个字符串的两个指针。图12.2 展示了成员拷贝的问题。默认析构函数释放了 `str` 指向的内存。因此销毁 `sailor` 的效果是：

```
delete [] sailor.str;
```

在这里，`sports.str` 指向已经被 `sailor` 析构函数释放的内存位置，这是未定义的、可能有害的行为。在列表 12.3 的情况下，程序产生了混乱的字符串，这通常是内存管理错误的象。另一个令人不安的症状是尝试删除同一块内存会导致程序中止。例如，Microsoft Visual C++ 2010（调试模式）显示错误窗口“Debug Assertion Failed!”，而 Linux 上的 `g++` 4.4.1 则报告“double free or corruption”。其他的提供不同的消息或没有消息，但同样的错误隐藏其中

# 通过定义显式拷贝构造函数解决问题

解决类设计中问题的方案是进行深拷贝。也就是说，而不是仅仅拷贝字符串的地址，拷贝构造函数应该复制字符串并将副本赋值给 `str` 成员。这样，每个对象都获得自己的字符串，而不是引用另一个对象的字符串。而且每个析构函数都释放不同的字符串，而不是尝试释放同一块内存。以下是你可以如何编写 `StringBad::StringBad(const String& str)`

```
{
    num_strings++; // 处理静态成员更新
    len = str.len; // 相同长度
    str = new char[len + 1]; // 分配空间
    std::strcpy(str, str.str); // 将字符串拷贝到新位置
}
```

## 动态内存与类 643

```cpp
cout << num_strings << " " << "\"" << str
		 << "\" object created\n"; // For Your Information
}
```

定义拷贝构造函数的必要性在于，某些类成员是指向新初始化的数据指针，而不是数据本身。图 12.3 释了深拷贝。

![](img/cd111a87c1db9aff4db4b18834327463_657_0.png)

图 12.3 深拷贝的内部视图。

## 第 12 章 类与动态内存分配

> 注意
> 如果一个类包含由 `new` 初始化的指针成员，那么你应该定义一个拷贝构造函数来拷贝指针所指向的数据，而不是拷贝指针本身。这被称为**深拷贝**。拷贝的另一种形式（成员级拷贝，或浅拷贝）仅仅复制指针值。浅拷贝顾如其名——只是为了拷贝而对指针信息进行浅层次的“剥离”，而不是为了拷贝指针所指的结构而进行更深层的“挖掘”。

## 更多 Stringbad 问题：赋值运算符

列表 12.3 中的所有问题不能都归咎于默认拷贝构造函数；你还需要查看默认赋值运算符。正如 ANSI 允许浅赋值一样，C++ 也允许类对象赋值。它是通过为类重载赋值运算符来实现此点的。该运算符具有以下原型原型：

```cpp
Class_name & Class_name::operator=(const Class_name &);
```

也就是说，它接收并返回该类对象的引用。例如，这里是 Stringbad 类的原型：

```cpp
Stringbad & Stringbad::operator=(const Stringbad &);
```

## 赋值运算符何时被使用以及它的作用

当你将一个对象赋值给另一个现有对象时，就会使用重载的赋值运算符：

```cpp
Stringbad headline("Celery Stacks at Midnight");
```

```
Stringbad knot;      // 调用赋值运算符
knot = headline;
```

在初始化对象时并不一定使用赋值运算符：

```cpp
Stringbad metoo = knot; // 使用拷贝构造函数，可能也使用赋值
```

在这里 `metoo` 是一个新创建的对象，被初始化为 `knot` 的值；然而，使用的是拷贝构造函数。但是，如前所述，实现上可以选择分两步处理此条语句：使用拷贝构造函数创建一个临时对象，然后使用赋值将值拷贝到新对象。初始化总是会调用拷贝构造函数，而使用 `=` 运算符也可能调用赋值运算符。

与拷贝构造函数一样，赋值运算符的隐式实现执行从成员到成员的拷贝。如果某个成员本身是某个类的对象，程序将使用该类定义的赋值运算符来完成该特定成员的拷贝。静态数据成员不受影响。

## Stringbag 赋值出错的地方

列表 12.3 将 `headline` 赋值给 `knot`：

```cpp
knot = headline;
```

当调用 `knot` 的析构函数时，它显示此消息：

"Celery Stalks at Midnight" object deleted, 2 left

当调用 `headline` 的析构函数时，它显示此消息：

-2 left

许多人遇到了与隐式构造函数相同的问题：数据损坏。再次，问题在于成员级拷贝，这导致 `headline.str` 和 `knot.str` 指向同一个地址。因此，当调用 `knot` 的析构函数时，它删除了字符串 "Celery Stalks at Midnight"，而当调用 `headline` 的析构函数时，它尝试删除之前已经删除的数据。如之前所述，尝试删除之前删除的数据的效果是未定义的，因此它可能会改变内存内容，并可能导致程序中止。需要指出的是，如果特定操作的效果是未定义的，你的编译器可以做任何它想做的事，包括显示《独立宣言》或从你的硬盘上释放难看的文件。或者，对于编译器编写者来说，花时间包含这种轻率或具有破坏性的行为难道不是件稀事吗。

## 修复赋值

解决由不恰默认赋值运算符产生的问题的方法是提供你自己的赋值运算符定义，使其进行深拷贝。实现与拷贝构造函数相似，但存在一些差异：

- 因为对象可能已经引用了之前分配的数据，函数应该使用 `delete []` 来释放之前的义务。
- 函数应该防止将对象赋值给自身；否则，上述的内存释放可能会在重新赋值之前擦除对象的内容。
- 函数返回对调用对象的引用。

通过返回一个对象，函数可以通过链式调用来模拟内置类型的普通赋值。也就是说，如果 `S0`、`S1` 和 `S2` 是 `StringBad` 对象，你可以写道：

```cpp
S0 = S1 = S2;
```

在函数表示法中，这变为：

```cpp
S0.operator=(S1.operator=(S2));
```

因此，`S1.operator=(S2)` 的返回值成为 `S0.operator=()` 函数的参数。因为返回值是一个 String 对象的引用，所以它是正确的参数类型。

以下是你如何为 `StringBad` 类编写赋值运算符：

```cpp
StringBad & StringBad::operator=(const StringBad &st)
{
    if (this == &st)            // 对象赋值给自身
        return *this;               // 完成
    delete [str];               // 释放旧字符串
    len = st.len;
    str = new char[len + 1];   // 为新字符串获取空间
    std::strcpy(str, st.str);   // 拷贝字符串
    return *this;               // 返回调用对象的引用
}
```

首先，代码检查是否自赋值。它通过查看赋值右侧的地址（`&st`）是否为接收对象的地址（`this`）来判断。如果是，程序返回 `*this` 并终止。你可能在第 10 章中记得，赋值运算符是可以被类成员函数重载的运算符之一。

否则，函数继续释放 `str` 指向的内存。此原因是因为稍后 `str` 将被赋予新字符串的地址。如果你不先应用 `delete` 运算符，之前的字符串将留在内存中。由于程序不再拥有指向旧字符串的指针，该内存将被浪费。

接下来，程序像拷贝构造函数一样，为新字符串分配足够的空间，然后将右侧对象拷贝到新位置。完成后，程序返回 `*this` 并终止。赋值不会创建新对象，所以你不需要调整静态成员 `num_strings`。

将之前讨论的拷贝构造函数和赋值运算符添加到 StringBad 中解决了所有问题。这里，是这些更改后的几行输出：

"Celery Stalks at Midnight" object deleted, 4 left
"Spinach Leaves for Dollars" object deleted, 3 left
"Spinach Leaves for Dollars" object deleted, 2 left
"Lettuce Prey" object deleted, 1 left
"Celery Stalks at Midnight" object deleted, 0 left

End of main()

对象计数现在是正确的，没有字符串泄漏。

## 修改后的默认构造函数

新的默认构造函数值得注意。它看起来如下：

```cpp
{
  len = 0;
  str = new char[1];
  str[0] = '\0';      // 默认字符串
}
```

你可能会疑惑为什么代码使用

```cpp
str = new char[1];
```

而不是这个：

```cpp
str = new char;
```

## 第 12 章 类与动态内存分配

两种形式分配的内存量相同。区别在于第一种形式与类的析构函数兼容，而第二种则不兼容。回析构函数包含此代码：

```
delete [] str;
```

使用 `delete []` 与使用 `new []` 初始指针以及空指针兼容。另一种可能性可能是将

```cpp
str = new char[1];
str[0] = '\0'; // 默认字符串
```

替换为：

```
str = 0; // 将 str 设置为空指针
```

对任何通过其他方式初始化的内存使用 `delete []`，其效果是未定义的：

- * words [15] = "坏主意"
- char p1 = words;
- char p2 = new char;
- char p3;
delete [] p1; // 未定义，所以不要这样做
delete [] p2; // 未定义，所以不要这样做
delete [] p3; // 未定义，所以不要这样做

## C++11 空指针

在 C++98 中，字面量 `0` 有两个含义——它可以是数字 `0`，也可以是空指针——这使得读者和编译器难以区分两者。某些程序员使用 `(void *)` 来标识指针版本。（空指针本身可能有一个非零表示）。其他程序员使用 `NULL`（一个 C 宏）来表示空指针。然而，这证明是一个不完整的解决方案。C++11 通过引入新关键字 `nullptr`（空指针）提供了一个更好的解决方案。你仍然像以前一样使用 `0`——否则大量现有代码将失效——但从现在起，建议使用 `nullptr`：

```cpp
str = nullptr; // C++11 空指针表示法
```

## 比较方法

String 类中的三种方法执行比较。`operator<` 函数如果第一个字符串按字母顺序排在第二个之前（或更准确地说，在匹配的排序序列中），则返回 `true`。实现字符串比较函数的简单方法是使用标准的 `strcmp` 函数，如果它的第一个参数在字母顺序上先于第二个，它返回负值；如果字符串相同，返回 0；如果第一个在字母顺序上后第二个，则返回正值。你可以这样使用 `strcmp()`：

```cpp
bool operator<(const String& s1, const String& s2)
{
  if (std::strcmp(str1.str, str2.str) < 0)
```

## 新的改进型 String 类

```cpp
return true;
else
  return false;
}
```

由于内置的 `<` 运算符已经返回 `bool` 类型值，你可以将代码进一步简化为：

```cpp
bool operator<(const String&st1, const String&st2)
{
  return (std::strcmp(st1.str, st2.str) < 0);
}
```

同样，你可以这样编写另外两个比较函数：

```cpp
bool operator>(const String&st1, const String&st2)
{
  return st2 < st1;
}
bool operator=(const String&st1, const String&st2)
{
  return (std::strcmp(st1.str, st2.str) == 0);
}
```

第一版在 `<` 运算符中表达 `>` 运算符，这作为内联函数是一个很好的选择。
将比较函数声明为 `friend`（友元）有助于 String 对象与普通 C 字符串之间的比较。例如，假设 `answer` 是一个 String 对象，并且你有如下代码：

```cpp
if ("love" == answer)
```

这被翻译为如下：
if (operator==("love", answer))
编译器使用其中一个构造函数来转换代码，实际上相当于：
if (operator==(String("love", answer))
这与原型相匹配。

## 使用括号表示法访问字符

对于 C 风格字符串，你可以使用括号访问单个字符：
```cpp
char city[40] = "Amsterdam";
cout << city[0] << endl; // 显示字母 A
```

在 C++ 中，两个括号符号构成单个运算符，即下标运算符，你可以通过名为 `operator[]()` 的方法来重载此运算符。通常，二元 C++ 运算符（具有两个操作数的运算符）将运算符放在两个操作数之间，如 `2 + 5`。但下标运算符将一个操作数放在第一个括号之前，另一个操作数放在两个括号之间。因此，在表达式 `city[0]` 中，`city` 是第一个操作数，`[]` 是运算符，`0` 是第二个操作数。

假设 `opera` 是一个 String 对象：

```cpp
String opera("The Magic Flight");
```

如果你使用表达式 `opera[4]`，C++ 会查找具有此名称和签名名的方法：

```cpp
String::operator[] (int i)
```

如果找到了匹配的原型，编译器会将表达式 `opera[4]` 替换为此函数调用：

```cpp
opera.operator[] (4)
```

`opera` 对象调用该方法，数组下标 4 变成函数参数。

这是一个简单的实现：

```cpp
char & String::operator[] (int i)
{
    return str[i];
}
```

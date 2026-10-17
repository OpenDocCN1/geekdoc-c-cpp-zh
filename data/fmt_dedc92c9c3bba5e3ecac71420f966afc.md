
```
Screen myScreen;
myScreen.move(Screen::HOME); // 调用 myScreen.home
myScreen.move(Screen::DOWN); // 调用 myScreen.down
```

该表可以如下初始化：

点击此处查看代码图片

```
Screen::Action Screen::Menu[] = {
    &Screen::home,
    &Screen::forward,
    &Screen::back,
    &Screen::up,
    &Screen::down
};
```

## 19.4.2 练习

练习 19.14：以下代码合法吗？如果，它做了什么？如果不是，为什么？

点击此处查看代码图片

```
auto pmf = &Screen::get_cursor;
pmf = &Screen::get;
```

练习 19.15：普通函数指针与成员函数指针的区别是什么？

练习 19.16：编写一个类型别名，作为指向 `Sales_data` 中 `avg_price` 成员的别名。

练习 19.17：为每种不同的 `Screen` 成员函数类型定义类型别名。

## 19.4.3. 将成员函数作为可调用对象

正如我们所见，为了通过成员函数指针进行调用，必须使用 `.*` 或 `->*` 运算符将指针绑定到特定对象。因此，与普通函数指针不同，成员指针不是可调用对象；这些指针

不支持函数调用运算符（§ 10.3.2, 388）。

由于指针不是可调用对象，因此我们不能直接将成员函数的指针传递给算法。例如，如果我们想在一个字符串 `vector<string>` 中查找第一个空字符串，显而易见的调用将不起：

点击此处查看代码图片

```
auto fp = &string::empty; // fp 指向 string empty 函数
// 错误：使用 .* 或 ->* 调用成员指针
find_if(svec.begin(), svec.end(), fp);
```

`find_if` 算法期望一个可调用对象，而我们提供的是 `fp`，它是一个指向成员函数的指针。这段代码无法编译，因为 `find_if` 内部的代码执行了类似如下的语句：

点击此处查看代码图片

```
// 检查应用于当前元素的谓词是否返回真
if (fp(*it)) // 错误：必须使用 ->* 通过成员指针进行调用
```

这会尝试调用它所接收的对象。

### 使用函数生成可调用对象

从成员函数指针获取可调用对象的一种方法是使用库函数（§ 14.8.3, p. 577）：

点击此处查看代码图片

```
function<bool(const string&)> fcn = &string::empty;
find_if(svec.begin(), svec.end(), fcn);
```

在这里我们告诉 `function`，`empty` 是一个可以用字符串调用并返回 `bool` 的函数。通常情况下，执行成员函数的对象会被传递给隐式参数。当我们想要使用 `function` 为成员函数生成可调用对象时，我们必须“翻译”代码以使隐式参数显式化。

当函数对象持有指向成员函数的指针时，函数类知道它必须使用适当的成员指针运算符来执行调用。也就是说，我们可以想象 `find_if` 拥有类似如下的代码：

点击此处查看代码图片

```
// 假设它是 find_if 内部的迭代器，因此 *it 是给定范围内的一个对象
if (fcn(*it)) // 假设 fcn 是 find_if 内部的可调用对象的名称
```

该函数将执行正确的成员指针运算符。本质上，函数类会将此调用转换为类似如下的内容：

点击此处查看代码图片

# C++ Primer, 第五版

```
// 假设它是 find_if 内部的迭代器，因此 *it 是给定范围内的一个对象
if ((*it).*p)()) // 假设 p 是 fcn 内部指向成员函数的指针
```

当我们定义一个函数对象时，必须指定函数类型，该类型是能够表示的可调用对象的签名。当可调用对象是成员函数时，签名的第一个参数必须代表（通常是隐式的）运行该成员函数的对象。我们传递给 `function` 的签名必须指定该对象是作为指针还是引用传递。

当我们定义 `fcn` 时，我们知道想在一组 `string` 对象上调用 `find_if`。因此，我们要求 `function` 生成一个接受 `string` 对象的可调用对象。我们的 `vector` 持有指向 `string` 的指针，我们会告诉 `function` 期望一个指针：

点击此处查看代码图片

```
vector<string*> pvec;
function<bool(const string*)> fp = &string::empty;
// // fp 接收 string 指针并使用 ->* 调用 empty
find_if(pvec.begin(), pvec.end(), fp);
```

# 使用 mem_fn 生成可调用对象

![](img/3a7e14b77396239ca7166fc2adb32975_1031_0.png)

要使用 `function`，我们必须提供想要调用的成员的调用签名。相反，我们可以通过另一个库设施 `mem_fn` 让编译器推导出成员的类型，`mem_fn` 与 `function` 一样定义在 `<functional>` 头文件中。与 `function` 一样，`mem_fn` 从成员指针生成可调用对象。与 `function` 不同的是，`mem_fn` 从成员指针的类型推导出可调用对象的类型：

点击此处查看代码图片

```
find_if(svec.begin(), svec.end(), mem_fn(&string::empty));
```

在这里我们使用 `mem_fn(&string::empty)` 生成一个接受 `string` 参数并返回 `bool` 的可调用对象。

`mem_fn` 生成的可调用对象可以是对象也可以是指针：

点击此处查看代码图片

```
auto f = mem_fn(&string::empty); // // f 接收 string 或 string*
f(*svec.begin()); // OK：传递了 string 对象；f 使用 .* 调用 empty
f(&svec[0]); // OK：传递了 string 指针；f 使用 -> 调用 empty
```

实际上，我们认为 `mem_fn` 就像是生成了一个带有一个重载函数调用运算符的可调用对象——其中一个接受 `string*`，另一个接受 `string&`。

# 使用 bind 生成可调用对象

为了完整性，我们还可以使用 `bind`（§ 10.3.4, p. 397）从成员函数生成可调用对象：

点击此处查看代码图片

```
// 将范围内的每个字符串绑定到 empty 的隐式第一个参数上
auto it = find_if(svec.begin(), svec.end(),
    bind(&svec::empty, _1));
```

与 `function` 一样，使用 `bind` 时，我们必须显式表示代表成员函数将操作对象的成员函数。与 `mem_fn` 一样，`bind` 生成的可调用对象的第一个参数可以是指向 `string` 的指针或引用：

点击此处查看代码图片

```
find_if(svec.begin(), svec.end(),
    bind```svec::empty, _1));
```

```
f(*svec.begin()); // OK：传递了 string 对象;f 使用 .* 调用 empty
f(&svec[0]); // OK：传递了 string 指针；f 使用 -> 调用 empty
```

## 19.5 嵌套类

类可以定义在另一个类内部。这种类是嵌套类，通常被称为内部类。

- 练习 19.4
  - 练习 19.18：编写一个函数，使用 `find_if` 统计多少个空字符串。
  - 练习 19.19：编写一个函数，接受 `vector<Sales_data>` 并找到平均价格大于给定值的元素。

嵌套类是独立的类，与其包含类无关。特别是，嵌套类型对象没有包含类的成员。同样，包含类的对象没有嵌套类的成员。

嵌套类的名称在包含类内部可见的，但在类外不可见。与其他任何其他名称一样，嵌套类的名称在另一个作用范围内不会发生冲突。

嵌套类可以定义在它的类中。正如任何类一样，嵌套类使用访问限定符来控制其成员。包含类对嵌套类的成员没有特殊访问权限，嵌套类对包含类的成员也没有特殊访问权限。

嵌套类在其包含类中定义一个类型。正如任何其他成员一样，包含类决定该类型的访问权限。在包含类公共部分的嵌套类定义了一个可以在地方使用的类型。在保护部分的嵌套类定义的类型仅由包含类、其友元和派生类访问。私有部分的嵌套类定义的类型仅由包含类的成员及其友元访问。

### 声明嵌套类

§12.3.2 (p. 487) 中的 `TextQuery` 类定义了一个名为 `QueryResult` 的辅助类。`QueryResult` 类与我们的 `TextQuery` 类紧密耦合。除了作为 `TextQuery` 对象的查询结果外，将 `QueryResult` 用于其他目的似乎意义不大。为了反映这种耦合，我们把 `QueryResult` 设置为 `TextQuery` 的成员。

点击此处查看代码图片

```
class TextQuery {
public:
    class QueryResult; // 稍后定义的嵌套类
    // 其他成员如 12.3.2 (p. 487) 所示
};
```

我们对原始 `TextQuery` 类只需要进行一处更改——声明将 `QueryResult` 定义为嵌套类。`QueryResult` 是一个类型成员（§7.4.1, p. 284），在使用它之前必须声明它。特别，在我们将其作为成员函数的返回类型之前，必须声明 `QueryResult`。我们原始类的其余成员保持不变。

我们在 `TextQuery` 内部声明了 `QueryResult` 但没有定义它。与成员函数一样，嵌套类必须在类内部声明，但可以在类内部或类外部定义。

当我们在类外部定义嵌套类时，必须通过包含类的名称来限定该嵌套类：

# C++ 教程 - 第五版

```cpp
// 我们正在定义 QueryResult 类，它是 TextQuery 类的一个成员类
class TextQuery::QueryResult {
    // 在类作用域内，我们不需要为 QueryResult 参数限定作用名
    friend std::ostream&
    print(std::ostream&, const QueryResult&);
public:
    // 不需要定义嵌套类的类名
    QueryResult(std::string, std::shared_ptr<std::set<std::line_no>>,
    std::shared_ptr<std::vector<std::string>>);
    // 嵌套类可以使用其他成员
    // 的成员，如 § 12.3.2 (p. 487) 所示
}
```

我们与原始类相比的唯一改变是我们不再在 QueryResult 中定义 `line_no` 成员。QueryResult 的成员可以直接从 TextQuery 访问该成员，因此没有必要再次定义它。

> **警告**
在看到定义在类体之外的嵌套类的实际定义之前，该类是一个不完整类型（§ 7.3.3, p. 278）。

### 定义嵌套类的成员

在这一版本中，我们没有在类体内定义 QueryResult 构造函数。为了定义构造函数，我们必须指定 QueryResult 嵌套在 TextQuery 的作用域内。我们通过用包含类的名称来限定嵌套类来实现这一点：

**点击此处查看代码图片**

```cpp
// 定义名为 QueryResult::QueryResult(string s,
// shared_ptr<vector<string>> p,
// sought(s), lines(p), file(f) { }
```

从右向左读该函数名，我们看到我们正在为类 QueryResult 定义构造函数，该类嵌套在类 TextQuery 的作用域内。该代码本身只是将给定的参数存储在数据成员中，没有进一步的工作需要做。

### 嵌套类的静态成员定义

如果 QueryResult 声明了一个静态成员，则它的定义将出现在 TextQuery 作用域之外。例如，假设 QueryResult 有一个静态成员，它的定义看起来像这样

点击此处查看代码图片

```cpp
// 定义 QueryResult 的一个 int 成员
// 该成员是嵌套在 TextQuery 内部的类
int TextQuery::QueryResult::static_mem = 1024;
```

### 嵌套类作用域中的名称查找

普通规则允许嵌套类内部的名称查找（§ 7.4.1, p. 283）。当然，因为嵌套类是一个嵌套类，嵌套类有额外的包含作用域需要搜索。这种作用域的嵌套解释了为什么我们没有在 QueryResult 的嵌套版本中定义 `line_no`。我们的原始 QueryResult 类定义了这个成员，以便其所有者可以避免编写 `TextQuery::line_no`。由于我们的类定义在 TextQuery 内部，我们不再需要 `typedef`。QueryResult 可以在不指定 `line_no` 定义在 TextQuery 中的情况下访问 `line_no`。包含类的成员也是可用的。

正如我们所见，嵌套类是一种可以像使用任何其他类型一样使用嵌套类名的类型。由于 QueryResult 嵌套在 TextQuery 内部，TextQuery 的 `query` 成员可以直接引用名称 `QueryResult`：

点击此处查看代码图片

```
// 返回类型必须指示 QueryResult 现在是一个嵌套类
TextQuery::QueryResult
TextQuery::query(const string &sought) const
{
    // 如果没有找到 sought，我们将返回此处的指针
    static shared_ptr<set<line_no>> nodata(new set<line_no>);
    // 使用 find 而不是下标向 wm 添加单词！
    auto loc = wm.find(sought);
    if (loc == wm.end())
        return QueryResult(sought, nodata, file); // 未找到
    else
        return QueryResult(sought, loc->second, file);
}
```

通常情况下，返回类型不在类的作用域内（§ 7.4, p. 282），因此我们首先注意到我们的函数返回一个 `TextQuery::QueryResult` 值。然而，在函数体内，我们可以直接引用 `QueryResult`，就像我们在返回语句中所做的那样。

### 嵌套类和包含类是独立的

尽管嵌套类定义在它的包含类的作用域内，但重要的是，包含类的对象与其嵌套类的对象之间没有连接。嵌套类型对象只包含定义在嵌套类型内部的成员。同样，包含类的对象只包含由包含类定义的成员。它不包含任何嵌套类的数据成员。

更具体地说，TextQuery::query 中的返回语句

点击此处查看代码图片

```cpp
return QueryResult( sought, loc->second, file);
```

使用了运行 query 的 TextQuery 对象的数据成员来初始化 QueryResult 对象。我们使用这些成员来构造我们返回的 QueryResult 对象，因为 QueryResult 对象不包含其包含类的成员。

| 练习 19.5 |
| :--- |
| 练习 19.20：将你的 QueryResult 类嵌套在 TextQuery 内部，并重新运行你为 § 12.3.2 (p. 490) 的 TextQuery 的程序。 |

# 19.6. union: 节省空间的类

union（联合体）是一种特殊的类。联合体可以有多个数据成员，但在任何时刻，只有一个成员可以有值。当一个值赋值给联合体中的一个成员时，所有其他成员都变成未定义状态。为联合体分配的存储空间至少等等于包含其最大数据成员所需的空间。像任何类一样，union 定义了一个新类型。

但是，并不是所有类特征都具有引用成员，但它可以拥有其他类型的成员，包括根据新标准，具有构造函数或析构函数的类类型。union 可以指定保护标签来使成员成为公共、私有或保护。默认情况下，像结构体一样，union 的成员是公有的。

union 可以定义成员函数，包括构造函数和析构函数。然而，union 不能继承自其他类，union 也不能作为基类。因此，union 不能有虚函数。

## 定义 union

union 提供了一种表示一组互斥不同值的方便方法。例如，我们可能有一个处理不同数值或字符数据的进程。该进程可能会定义一个 union 来持有这些值：

点击此处查看代码图片

```cpp
// 类型 Token 的对象可以是列出类型中的一种
union Token {
  // 成员默认是公有的
  char cval;
  int ival;
  double dval;
};
```

union 的定义以关键字 union 开始，后面是可选的 union 名称和一组封装在大括号内的成员声明。这段代码定义了一个名为 Token 的 union，它可以持有 char、int 或 double 类型的值。

## 使用 union 类型

union 的名称是一个类型名。与内置类型一样，默认 union 是未初始化的。我们可以像显式初始化聚合类 [7.5.5, p. 298] 一样，通过将初始化器封装在对括号中来显式初始化：

点击此处查看代码图片

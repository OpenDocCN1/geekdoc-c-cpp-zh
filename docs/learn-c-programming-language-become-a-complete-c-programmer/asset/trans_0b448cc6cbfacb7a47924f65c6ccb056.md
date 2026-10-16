
facet。对于没有名称的区域设置，name() 返回 “*”。

区域设置可以看作是对 map<id,facet*> 的一个接口，即一种允许我们使用 locale::id 找到从 locale::facet 派生的类的对应对象的机制。区域设置的实际实现是这一思想的高效变体。其布局大致如下：

collate<char>:
locale : compare() hash() ...
num punct<char> : decimal_point()
truename() ...

这里，collate<char> 和 numpunct<char> 是标准库的 facet（§39.4）。所有 facet 都派生自 locale::facet。

区域设置被设计为可以自由且低成本地复制。因此，区域设置几乎肯定实现为指向专门化 map<id,facet*> 的句柄，该 map 构成了其实现的主要部分。facet 必须在区域设置中能够快速访问。因此，专门化的 map<id,facet*> 将被优化以提供类似数组的快速访问。通过使用 use_facet<Facet>(loc) 表示法访问区域设置的 facet；参见 §39.3.1。

标准库提供了丰富的 facet 集合。为了帮助程序员在逻辑组中操作 facet，标准 facet 被分组为多个类别，如 numeric 和 collate（§39.4）：facet 类别（§iso.22.3.1）

- collate
- ctype
- numeric
- monetary
- time
- messages
- all
- none

例如，collate；§39.4.1
例如，ctype；§39.4.5
例如，num_put、num_get、numpunct；§39.4.2
money_put、money_get、moneypunct；§39.4.3
例如，time_put、time_get；§39.4.4
messages；§39.4.7
collate | ctype | monetary | numeric | time | messages

程序员无法为新创建的区域设置指定名称字符串。名称字符串要么在程序的执行环境中定义，要么由区域设置构造函数根据这些名称组合而成。

程序员可以替换现有类别中的 facet（§39.4、§39.4.2.1）。但是，程序员无法定义新的类别。“类别”的概念仅适用于标准库 facet，并且不可扩展。因此，一个 facet 不必属于任何类别，许多用户自定义的 facet 也确实不属于任何类别。

如果区域设置 x 没有名称字符串，则 locale::global(x) 是否会影响 C 全局区域设置是未定义的。这意味着 C++ 程序无法可靠且可移植地将 C 区域设置设置为从执行环境中获取之外的区域设置。C 程序没有标准方法设置 C++ 全局区域设置（除非调用 C++ 函数来实现）。在混合 C 和 C++ 程序中，让 C 全局区域设置与 global() 不同容易出错。

到目前为止，区域设置的主要用法是隐式地用于流 I/O。每个 istream 和 ostream 都有自己的区域设置。流的区域设置默认是流创建时的全局区域设置（§39.2.1）。可以通过 imbue() 操作设置流的区域设置，我们可以使用 getloc() 获取流的区域设置的副本（§38.4.5.1）。

设置全局区域设置不会影响现有的 I/O 流；这些流仍然使用在全局区域设置重置之前它们被注入的区域设置。

## 39.2.1 命名区域设置

区域设置是由另一个区域设置和 facet 构造的。最简单的方法是复制现有的区域设置。例如：

```
locale loc1;
locale loc2 {""};
// copy of the current global locale // copy of "the user’s preferred locale"
locale loc3 {"C"};
locale loc4 {locale::classic()};
// copy of the "C" locale // copy of the "C" locale

locale loc5 {"POSIX"};
locale loc6 {"Danish_Denmark.1252"}; locale loc7 {"en_US.UTF-8"};
// copy of the locale named "POSIX"
// copy of the locale named "Danish_Denmark.1252" // copy of the locale named "en_US.UTF-8"
```

locale{"C"} 的含义由标准定义为 “classic” C 区域设置；这是本书一直使用的区域设置。其他区域设置名称由实现定义。locale{""} 被视为 “用户的首选区域设置”。该区域设置通过程序执行环境中的语言外部手段设置。因此，要查看当前 “首选区域设置”，请编写：locale loc("");
cout << loc.name() << '\n';
在我的 Windows 笔记本电脑上，我得到：
English_United States.1252
在我的 Linux 机器上，我得到：
en_US.UTF-8

区域设置的名称并未为 C++ 标准化。相反，像 POSIX 和 Microsoft 这样的各种组织在不同的编程语言中维护各自不同的标准。例如：

## 第 39.2.1 节 命名区域设置 1115

GNU 区域设置名称示例（基于 POSIX）

- ja_JP
- da_DK
- en_DK
- de_CH
- de_DE
- en_GB
- en_US
- fr_CA
- de_DE
- de_DE@euro
- de_DE.utf8
- de_DE.utf8@euro

日语（日本）
丹麦语（丹麦）
英语（丹麦）
德语（瑞士）
德语（德国）
英语（英国）
英语（美国）
法语（加拿大）
德语（德国）
德语（德国，使用欧元符号€）
德语（德国，使用UTF-8）
德语（德国，使用UTF-8和欧元符号€）

POSIX 推荐一种格式：小写语言名称，可选地后跟大写国家/地区名称，可选地后跟编码说明符，例如 sv_FI@euro（瑞典语，用于芬兰，包括欧元符号）。

## Microsoft 区域设置名称示例

- Arabic_Qatar.1256
- Basque.Spain.1252
- Chinese_Singapore.936
- English_United Kingdom.1252
- English_United States.1252
- French_Canada.1252
- Greek_Greece.1253
- Hebrew_Israel.1255
- Hindi_India.1252
- Russian_Russia.1251

Microsoft 使用后跟国家/地区名称（可选后跟代码页编号）的语言名称。代码页是一种已命名（或编号）的字符编码。

大多数操作系统都有为程序设置默认区域设置的方法。通常，该

```
preferred locale": "" << locale("").name() << "\n"; cout << "name of my locale: " << my_loc.name() << "\n";
}
```

## 39.2.1.1 构造新的区域设置

新的区域设置是通过获取现有区域设置并添加或替换 facet 来创建的。通常，新区域设置是现有区域设置的一个小变体。例如：

```
void f(const locale& loc, const My_money_io *mio) // My_money_io defined in §39.4.3.1 {
locale loc1(locale{"POSIX"},loc,locale::monetary); // use monetaryfacets from loc
locale loc2 = locale(locale::classic(), mio); // classic plus mio // ...
}
```

## 第 39.2.1.1 节 构造新的区域设置 1117

这里，loc1 是修改后的 POSIX 区域设置的副本，使用 loc 的货币 facet（§39.4.3）。类似地，loc2 是修改后的 C 区域设置的副本，使用 My_money_io（§39.4.3.1）。生成的区域设置可以如下表示：

```
classic(): collate<char>:
compare() loc2: hash()
...

numpunct<char> :
decimal_point()

curr_symbol()
...
My_money_io:
decimal_point()
curr_symbol()
...
```

如果 Facet_* 参数（此处为 My_money_io）为 nullptr，则生成的区域设置只是 locale 参数的副本。

在构造 locale{loc,f} 中，f 参数必须标识特定的 facet 类型。普通的 facet_* 是不够的。例如：

```
void g(const locale::facet * mio1, const money_put<char>* mio2)
{
locale loc3 = locale(locale::classic(), mio1); // error :type of facet not known locale loc4 = locale(locale::classic(), mio2); // OK: type of facet known (moneyput<char>) // ...
}
```

区域设置使用 Facet_* 参数的类型在编译时确定 facet 的类型。具体来说，区域设置的实现使用 facet 的标识类型 facet::id（§39.3）在区域设置中找到该 facet（§39.3.1）。构造函数

```
template<class Facet> locale(const locale& x, Facet * f);
```

是语言提供的唯一允许程序员提供 facet 以通过 **区域设置** 使用的机制。其他 **区域设置** 由实现者作为命名区域设置提供（§39.2.1）。命名区域设置可以从程序的执行环境中获取。理解实现特定机制的程序员也许能够添加新的 **区域设置**。

**区域设置** 的构造函数集合被设计为使每个 **facet** 的类型要么通过类型推导（来自 **Facet** 模板参数）已知，要么因为来自另一个 **区域设置**（该设置知道其类型）。指定 **类别** 参数间接指定了 **facet** 的类型，因为 **区域设置** 知道这些类别中 **facet** 的类型。这意味着 **区域设置** 类可以（并且确实）跟踪 **facet** 的类型，以便以最小的开销操作它们。**区域设置** 使用 **locale::id** 成员类型来标识 **facet** 类型（§39.3）。

无法修改 **区域设置**。相反，**区域设置** 操作提供了从现有 **区域设置** 创建新 **区域设置** 的方法。**区域设置** 在创建后不可变这一事实对于运行时效率至关重要。这允许使用 **区域设置** 的人调用 **facet** 的虚函数并缓存返回的值。例如，**istream** 可以知道用于表示小数点的字符以及 **true** 是如何表示的，而无需在每次读取数字时调用 **decimal_point()** 以及每次读取到 **bool** 时调用 **truename()**（§39.4.2）。只有对流调用 **imbue()**（§38.4.5.1）才会导致这些调用返回不同的值。

## 39.2.2 比较 **字符串**

根据 **区域设置** 比较两个 **字符串** 可能是 **区域设置** 在 I/O 之外最常见的用法。因此，**区域设置** 直接提供此操作，用户不必从 **collate** facet 构建自己的比较函数（§39.4.1）。该 **字符串** 比较函数被定义为 **区域设置** 的 **operator()()**。例如：

```
void user(const string s1, const string s2, const locale& my_locale)
{
if (my_locale(s,s2)) { // is s<s2 according to my_locale?
// ...
}
}
```

将比较函数作为 **()** 运算符使其直接可用作谓词（§4.5.4）。例如：

```
void f(vector<string>& v, const locale& my_locale)
{
sort(v.begin(),v.end()); // sort using < to compare elements
// ...
sort(v.begin(),v.end(),my_locale); // sort according to the rules of my_locale
// ...
}
```

默认情况下，标准库 **sort()** 使用 **<** 来比较元素的数值


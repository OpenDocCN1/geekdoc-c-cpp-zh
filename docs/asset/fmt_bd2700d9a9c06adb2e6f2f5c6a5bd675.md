
Consider writing a program that needs to be used in several countries. Writing a program in a style that allows that is often called `internationalization` (emphasizing the use of a program in many countries) or `localization` (emphasizing the adaptation of a program to local conditions). Many of the entities that a program manipulates will conventionally be displayed differently in those countries. We can handle this by writing our I/O routines to take this into account. For example:

```
`void print_date(const Date& d) // printing the appropriate format`
```

```
{
switch(where_am_I) { // user-defined style indicator
case DK: // e.g., 7. marts 1999
cout << d.day() << "." << dk_month[d.month()] << " " << d.year();
break;
case ISO: // e.g., 1999-3-7
cout << d.year() << "-" << d.month() << "/" << d.day();
break;
case US: // e.g., 3/7/1999
cout << d.month() << "/" << d.day() << "/" << d.year();
break;
//...
}
}
```

This style of code does the job. However, such code is ugly and hard to maintain. In particular, we have to use this style consistently to ensure that all output is properly adjusted to local conventions. If we want to add a new way of writing a date, we must modify the application code. Worse yet, writing dates is only one of many examples of cultural differences.

Consequently, the standard library provides an extensible way of handling cultural conventions. The iostream library relies on this framework to handle both built-in and user-defined types (§38.1). For example, consider a simple loop copying (`Date`, `double`) pairs that might represent a series of measurements or a set of transactions:

```
void cpy(istream& is, ostream& os) // copy(Date,double) stream
{
Date d;
double volume;

while (is >> d >> volume)
os << d << ' ' << volume << '\n';
}
```

Naturally, a real program would do something with the records and ideally also be a bit more careful about error handling.

How would we make this program read a file that conformed to French conventions (where a comma is the character used to represent the decimal point in a floating-point number; for example,

### Section 39.1 Handling Cultural Differences 1111

12,5 means twelve and a half) and write it according to American conventions? We can define locales and I/O operations so that `cpy()` can be used to convert between conventions:

```
void f(istream& fin, ostream& fout, istream& fin2, ostream& fout2)
{
fin.imbue(locale{"en_US.UTF-8"}); // AmericanEnglish
fout.imbue(locale{"fr_FR.UTF-8"}); // French
```

```
cpy(fin,fout); // read American English, write French // ...
fin2.imbue(locale{"fr_FR.UTF-8"}); // French
fout2.imbue(locale{"en_US.UTF-8"}); // American English
cpy(fin2,fout2); // read French, write American English // ...
}
```

Given these streams:

```
Apr 12, 1999 1000.3
Apr 13, 1999 345.45
Apr 14, 1999 9688.321
...
3 juillet 1950 10,3
3 juillet 1951 134,45
3 juillet 1952 67,9
...
```

this program would produce:

```
12 avril 1999 1000,3
13 avril 1999 345,45
14 avril 1999 9688,321
...
July 3, 1950 10.3
July 3, 1951 134.45
July 3, 1952 67.9
...
```

Much of the rest of this chapter is devoted to describing the mechanisms that make this possible and explaining how to use them. However, most programmers will have little reason to deal with the details of locales and will never explicitly manipulate a locale. At most, they will simply retrieve a standard locale and imbue a stream with it (§38.4.5.1).

- The concept of localization (internationalization) is simple. However, practical constraints make the design and implementation of locale quite intricate:

- [1] A locale encapsulates cultural conventions, such as the appearance of a date. Such conventions vary in many subtle and unsystematic ways. These conventions have nothing to do with programming languages, so a programming language cannot standardize them.

- [2] The concept of a locale must be extensible, because it is not possible to enumerate every cultural convention that is important to every C++ user.

- [3] A locale is used in operations (e.g., I/O and sorting) from which people demand run-time efficiency.

- [4] A locale must be invisible to the majority of programmers who want to benefit from facilities “doing the right thing” without having to know exactly what “the right thing” is or how it is achieved.

- [5] A locale must be available to designers of facilities that deal with culture-sensitive information beyond the scope of the standard.

The mechanisms provided to compose those locales and to make them trivial to use constitute a little programming language of their own.

`facet`。对于没有名称的区域设置，`name()` 返回 “*”。

区域设置可以看作是对 `map<id,facet*>` 的一个接口，即一种允许我们使用 `locale::id` 找到从 `locale::facet` 派生的类的对应对象的机制。区域设置的实际实现是这一思想的高效变体。其布局大致如下：

`collate<char>`:

`locale` : `compare()` `hash()` ...

`num punct<char>` : `decimal_point()`

`truename()` ...

这里，`collate<char>` 和 `numpunct<char>` 是标准库的 `facet`（§39.4）。所有 `facet` 都派生自 `locale::facet`。

区域设置被设计为可以自由且低成本地复制。因此，区域设置几乎肯定实现为指向专门化 `map<id,facet*>` 的句柄，该 `map` 构成了其实现的主要部分。`facet` 必须在区域设置中能够快速访问。因此，专门化的 `map<id,facet*>` 将被优化以提供类似数组的快速访问。通过使用 `use_facet<Facet>(loc)` 表示法访问区域设置的 `facet`；参见 §39.3.1。

标准库提供了丰富的 `facet` 集合。为了帮助程序员在逻辑组中操作 `facet`，标准 `facet` 被分组为多个类别，如 `numeric` 和 `collate`（§39.4）：`facet` 类别（§iso.22.3.1）

- `collate`

- `ctype`

- `numeric`

- `monetary`

- `time`

- `messages`

- `all`

- `none`

例如，`collate`；§39.4.1

例如，`ctype`；§39.4.5

例如，`num_put`、`num_get`、`numpunct`；§39.4.2

`money_put`、`money_get`、`moneypunct`；§39.4.3

例如，`time_put`、`time_get`；§39.4.4

`messages`；§39.4.7

`collate` | `ctype` | `monetary` | `numeric` | `time` | `messages`

程序员无法为新创建的区域设置指定名称字符串。名称字符串要么在程序的执行环境中定义，要么由区域设置构造函数根据这些名称组合而成。

程序员可以替换现有类别中的 `facet`（§39.4、§39.4.2.1）。但是，程序员无法定义新的类别。“类别”的概念仅适用于标准库 `facet`，并且不可扩展。因此，一个 `facet` 不必属于任何类别，许多用户自定义的 `facet` 也确实不属于任何类别。

如果区域设置 `x` 没有名称字符串，则 `locale::global(x)` 是否会影响 C 全局区域设置是未定义的。这意味着 C++ 程序无法可靠且可移植地将 C 区域设置设置为从执行环境中获取之外的区域设置。C 程序没有标准方法设置 C++ 全局区域设置（除非调用 C++ 函数来实现）。在混合 C 和 C++ 程序中，让 C 全局区域设置与 `global()` 不同容易出错。

到目前为止，区域设置的主要用法是隐式地用于流 I/O。每个 `istream` 和 `ostream` 都有自己的区域设置。流的区域设置默认是流创建时的全局区域设置（§39.2.1）。可以通过 `imbue()` 操作设置流的区域设置，我们可以使用 `getloc()` 获取流的区域设置的副本（§38.4.5.1）。

设置全局区域设置不会影响现有的 I/O 流；这些流仍然使用在全局区域设置重置之前它们被注入的区域设置。

# 39.2.1 命名区域设置

区域设置是由另一个区域设置和 `facet` 构造的。最简单的方法是复制现有的区域设置。例如：

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

`locale{"C"}` 的含义由标准定义为 “classic” C 区域设置；这是本书一直使用的区域设置。其他区域设置名称由实现定义。`locale{""}` 被视为 “用户的首选区域设置”。该区域设置通过程序执行环境中的语言外部手段设置。因此，要查看当前 “首选区域设置”，请编写：`locale loc("")`;

`cout << loc.name() << '\n';`

在我的 Windows 笔记本电脑上，我得到：

`English_United States.1252`

在我的 Linux 机器上，我得到：

`en_US.UTF-8`

区域设置的名称并未为 C++ 标准化。相反，像 POSIX 和 Microsoft 这样的各种组织在不同的编程语言中维护各自不同的标准。例如：

### 第 39.2.1 节 命名区域设置 1115

GNU 区域设置名称示例（基于 POSIX）

- `ja_JP`

- `da_DK`

- `en_DK`

- `de_CH`

- `de_DE`

- `en_GB`

- `en_US`

- `fr_CA`

- `de_DE`

- `de_DE@euro`

- `de_DE.utf8`

- `de_DE.utf8@euro`

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

POSIX 推荐一种格式：小写语言名称，可选地后跟大写国家/地区名称，可选地后跟编码说明符，例如 `sv_FI@euro`（瑞典语，用于芬兰，包括欧元符号）。

# Microsoft 区域设置名称示例

- `Arabic_Qatar.1256`

- `Basque.Spain.1252`

- `Chinese_Singapore.936`

- `English_United Kingdom.1252`

- `English_United States.1252`

- `French_Canada.1252`

- `Greek_Greece.1253`

- `Hebrew_Israel.1255`

- `Hindi_India.1252`

- `Russian_Russia.1251`

Microsoft 使用后跟国家/地区名称（可选后跟代码页编号）的语言名称。代码页是一种已命名（或编号）的字符编码。

大多数操作系统都有为程序设置默认区域设置的方法。通常，该

```
preferred locale": "" << locale("").name() << "\n"; cout << "name of my locale: " << my_loc.name() << "\n";
}
```

# 39.2.1.1 构造新的区域设置

新的区域设置是通过获取现有区域设置并添加或替换 `facet` 来创建的。通常，新区域设置是现有区域设置的一个小变体。例如：

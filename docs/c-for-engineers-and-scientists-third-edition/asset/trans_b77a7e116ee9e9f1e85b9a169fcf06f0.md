

## 第 10 章

作为类的一个具体示例，请看以下名为 `Date` 的类的定义。这种类型的类在设备交付日期和计划取决于具体日期的应用程序中是非常重要的。为了完成这项任务，仍然需要向此类类中添加若干用于判断日期是否为周末或节日的函数。

```cpp
// class declaration section
class Date {
private:
    // 注意 private 单词后面的冒号
    int month;
    // 一个数据成员
    int day;
    // 一个数据成员
    int year;
    // 一个数据成员
public:
    // 再次，注意这里的冒号 // 成员函数
    Date(int month = 7, int day = 4, int year = 2005); // 构造函数
    void setState(int, int, int); // 成员函数
    void showDate(); // 成员函数
}; // 这是一个声明 - 不要忘记分号
// class implementation section
Date::Date(int mm, int dd, int yyyy) {
    month = mm;
    day = dd;
    year = yyyy;
}
void Date::setState(int mm, int dd, int yyyy) {
    month = mm; day = dd; year = yyyy;
    return;
}
void Date::showDate() {
    cout << "The date is ";
    cout << setfill('0')
    cout << setw(2) << month << "/";
    cout << setw(2) << day << "/";
    cout << setw(2) << year % 100; // 提取最后两位
    return;
}
```

由于这个定义看起来可能很复杂，首先请注意，它确实包含两个部分——声明部分和实现部分。声明部分以 `class` 关键字开头，后跟一个类名。类名之后是类的变量声明和函数原型，它们被括在以分号结尾的大括号对中。这种形式的一般结构如下：

```cpp
class Name
{
  private:
  一个变量声明列表
  public:
  一个函数原型列表
};
```

注意 `Date` 类遵循这种格式。为了方便起见，在不带内部注释的情况下再次列出：

```cpp
// class declaration section
class Date
{
  private:
  int month;
  int day;
  int year;
  public:
  Date(int = 7, int = 4, int = 2005);
  void setState(int, int, int);
  void showDate();
};
```

类名是 `Date`。虽然首字母并不强制大写，但按照惯例，它用于指定一个类。声明部分的体（在大括号内）由变量和函数声明组成。在这种情况下，数据成员 `month`、`day` 和 `year` 被声明为整数，而 `setState()` 和 `showDate()` 被声明为原型。`private` 和 `public` 访问修符定义了它们中的哪些成员（在本例中为 `month`、`day` 和 `year`）只能由类函数（或友元函数）访问，正如 10.2 节所述。`private` 标记旨在通过要求通过私有方法访问所有私有成员来确保数据安全。这种访问限制了用户查看数据实际上是如何存储的，被称为封装。

在 `Date` 类中，数据使用三个整数存储月份、日期和年份。年份也存储为四位整数。例如，年份 1998 存储为 1998，而不是 98。确保所有年份都带有世纪标识，消除了如果只存储最后两位时可能出现的许多问题。例如，2006 年到 1999 年之间的数字可以计算为 2006 - 1999 = 7，由于包含了世纪标识，避免了歧义。此外，如果年份是 2006，它指的是 2006 年，而不是 06。例如，数字 06 值可能指的是 1906 或 2006 年。

在私有成员之后，函数原型被声明为 `public`。这意味着这些函数可以被类的任何对象调用。通常情况下，所有类函数都应该是 `public` 的，以便提供操作类变量的能力。

- *其他形式也是可能的。但这种形式常用且易于理解。*
- *注意，类中的默认成员是私有的，这意味着可以省略。在本书中，私有标记被用于加强对类访问的限制。*

`Date` 类提供了三个名为 `Date()`、`setState()` 和 `showDate()` 的函数。注意这些函数中的一个与类名相同。该函数被称为构造函数，它具有特殊目的：用于初始化类成员。该函数的默认值使用的是 7、4 和 2005，你可以看到这些是默认月份、日期和年份值。注意年份的默认值表示为四位整数。构造函数没有返回类型，这是该特殊函数的要求。剩下的两个函数 `setState()` 和 `showDate()` 被声明为不返回值（`void`）。（在实现部分编写这三个成员函数是为了允许初始化、赋值和显示能力。）

实现部分是编写声明部分定义的成员函数的地方。此示例显示了实现部分中函数的通用形式。对于构造函数以外的所有所有函数，这种格式都是正确的：

```cpp
returnType className::functionName(parameter list)
    function body
}
```

作为示例，实现部分定义的成员函数与所有 C++ 函数格式相同，增加了类名和作用域运算符 `::`；这标识了函数是类的成员。现在再次查看 `Date` 类的实现部分，重复如下：

```cpp
// class implementation section
Date::Date(int month, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
void Date::setState(int month, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    return;
}
void Date::showDate()
{
    cout << "The date is ";
    cout << setw(2) << month << "/";
```

你也可以通过在声明部分将这些函数定义为内联函数。10.2 节包含了成员函数的示例。注意实现部分的第一个函数与类名相同，这使其成为一个构造函数。因此，它没有返回类型。函数头部的 `Date::` 标识该函数是 Date 类的成员。所有年份都存储为四位值以保留世纪信息，用户习惯于看到年份值为 59 的日期。要显示年份的最后两位，可以使用 `% 100` 表达式。如果年份是 1999，表达式 `1999 % 100` 产生值 99；如果年份是 2006，表达式 `2006 % 100` 产生值 6。

如果你将年份作为两位值（例如 09），那么你将更改存储的年份值以对应最后两位。由于你想要保留年份为四位数，你必须使用输出语句中的 `year % 100` 表达式仔细地操作显示的值。`setfill` 和 `setw` 修饰符用于确保显示值符合惯例。对于 2006 年 3 月 9 日，应该显示为 3/9/06 或 030906。`setw` 修饰符强制每个值显示在宽度为 2 的字段中。该修饰符仅对下次插入（即日期值之前）有效。`setfill` 保持有效直到整个字符被更改，它只需要包含一次。`setfill` 修饰符已用于将填充字符从空格改为字符 0。这确保了像 2006 年 12 月 9 日这样的日期显示为 12/09/06，而不是 12/9。


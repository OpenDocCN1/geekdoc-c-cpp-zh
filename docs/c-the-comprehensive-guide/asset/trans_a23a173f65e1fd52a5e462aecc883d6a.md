
尝试将不同时间单位的类型替换为 `int` 值，插入到 `Date` 的构造函数中：

```cpp
/* return Date{Year(y), Month{b%31}, Day{b%31 + 1}}; */
return Date{y, b/31, b%31 + 1};
```

哦，天哪，这样居然可行！`Date` 构造函数（在这个意义上类似于函数）能很好地处理三个 `int` 值——从逻辑上也是如此，因为三个日历类型都有以一个 `int` 作为参数的构造函数，现在允许编译器执行隐式转换：

```cpp
Year::Year(int v);
Month::Month(int v);
Day::Day(int v);
```

你已经看到，编译器进行的隐式转换有时可能有用。但在许多情况下，比如这里，它可能很危险。现在它剥夺了我们防止参数被交换的保护。因为甚至 `Date{b%31 + 1, b/31, y}` 也会被编译器接受，但这是错误的。

## 用“explicit”防止转换

解决方案是 `explicit` 关键字。如果将其添加到单参数构造函数的声明中，那么编译器将不再选择它进行隐式类型转换。在这种情况下，你*必须*通过编写 `Year{y}` 将 `int` 类型的 y 转换为 `Year`。

这些类型的其余代码行保持不变，但构造函数的声明现在如下面的清单所示。

```cpp
// only excerpts
class Year {
    explicit Year(int v) : value_{v} {}
};
class Month {
    explicit Month(int v) : value_{v} {}
};
class Day {
    explicit Day(int v) : value_{v} {}
};
class Date {
    explicit Date(int y) : year_{y} {}
};
```

清单 12.26 使用“explicit”，可以防止自动类型转换。

对于具有多个参数的构造函数，`explicit` 没有意义。毕竟，多个类型不能同时转换为另一种类型。

缺点是，现在在调用 `ostream` 时也必须放弃隐式转换，而改为显式转换。然而，这种额外的工作是值得的：

```cpp
Date date = easter(Year{number});
```

> **提示**
>
> 通常，你应该用 `explicit` 关键字标记恰好有一个参数的构造函数。

## 12.11.4 封装与解封装

Year、Month 和 Day 这三个类型本质上只是封装了一个值。通过封装实际的 int 值，你创建了一个隐藏内部值的独特类型。但当然，你需要以某种方式把真实值存入和取出。

我已经描述了存入的方式。它通过构造函数完成，之后 `value_` 不能再被更改。如果你想要一个新的 `value_`，那么你也需要创建一个新的外围封装——例如，`Year a{2023};`，然后 `a = Year{2024}`。

取出的方式在示例如下实现：

```cpp
int Year::value() { return value_; }
```

这可以看作一个缺点：每次你想获取 Year 的实际值时，都必须使用 `value()`。`print()` 方法大量使用了它：

```cpp
ostream& Date::print(ostream& os) {
    return os << format("{}-{:02}-{:02}",
        year_.value(), month_.value(), day_.value());
}
```

我想向你展示两种不同的实现方式——在某些情况下它们甚至更好。

### 解封装

如果你希望部分暴露内部值，可以随意使用类似 `int value()` 的访问函数。但是要注意，这要求类的用户对类原本隐藏的（因为它们是私有）细节有一定了解。使用如下方法，你在某种程度上放弃了封装：

```cpp
int Year::value() { return value_; }
```

你暴露了 int 类型，而它实际上是私有变量 `value_` 的类型。这并不总是必须成为设计上的排除标准；对于这些小类，你主要想为 `Date` 的构造函数实现类型安全。另一种直接使用三个 `int` 值的方案，如前所述，不是类型安全的。

因此，如果你接受类似 `int Year::value()` 的方法，你可能会烦恼于不能像操作 `int` 那样直接操作 `Year`。总是写 `year.value()` 比只写 `year` 更麻烦。由于借助单参数构造函数可以转换为自己的类型，因此可以推断，在 C++ 中也存在将你自己的类型转换为另一种类型的方法。

将你的类型转换为 `int` 的方式称为运算符 `int()`。这里可以看到完整的 `Year` 类：

```cpp
class Year {
    int value_;
public:
    explicit Year(int v) : value_{v} {}
    int value() { return value_; }
    operator int() { return value(); }
};
```

现在，你可以在原本允许使用 `int` 的地方使用 `Year` 变量：

```cpp
Year year{2024};
cout << year;             // output like an int
int number = year;      // assign like an int
Year future { year + 10 };  // year to int and back again
```

最后一行做的最多。在 `year + 10` 中，运算符 `+` 应用于 `Year` 和 `int` 类型的两个操作数。然而，没有可以直接组合 `Year` 和 `int` 的 `+`。但是，编译器发现通过 `Year::operator int()` 可以从 `Year` 转换为 `int`，因此存在将 `+` 应用于 `int` 和 `int` 的方法。因此，`year` 被转换为 `2024` 这个 `int`，并执行 `+10`。结果 `2034` 当然又是 `int`。然后，这成为 `Year future{2034}` 构造函数调用的参数。

### 谨慎使用转换方法

尽管用 `value()` 来节省输入工作可能很诱人，但通过添加新的转换运算符，你为编译器应用其自动机制打开了一条新路径；如果过度使用，很快就会变得令人困惑。有时你会奇怪编译器是如何找到这条转换路径的。如果你还有非 `explicit` 的构造函数，情况尤其如此。

你应该谨慎使用转换方法。如果确实要用，优先使用单参数构造函数。只有在这还不够时，才应允许转换，并且只应在一个小而紧密协作的类族内进行。你尤其应避免转换为 `int` 这类无处不在的类型。

### 完全封装

通常你应该走另一条路。如果你的数据类型不仅仅隐藏一个值，那么应尽可能少地暴露内部细节。因此，避免使用 `int Year::value()` 之类的方法。

不过，当然有些操作是你想要执行的。没有操作，类型就没有意义。到目前为止，你一直依赖 `int` 提供的操作来“作弊”：输入、输出、计算等等。

如果你现在不想暴露类的内部细节，就必须为你的数据类型提供必要的操作。这可能工作量很大，但它允许严格分离*接口*和*实现*。

以 Year 为例。到目前为止，当你想要用 Year 进行计算时，你一直使用 `int value()` 方法来使用实际封装的 `int` 值。因此，你把实际上为 `int` 设计的操作用在了 Year 上。在复活节示例中，Year 只涉及*输出*，通过 `operator<<` 实现。

对于其他目的，更改年份可能很有用。这个操作名为 advance，方法签名如下：

```cpp
Year& Year::advance(const Year& difference);
```

注意，这里要更改的是实例的当前值。这样就可以实现以下操作，例如：

```cpp
Year year{2024};
year.advance(Year{1});
cout << year; // Output: 2025
```

能够在 `if` 语句中检查两个年份是否相等也很有用。而如果你不能再通过 `value()` 依赖 `int` 值，那么就需要一个方法来完成这件事：

```cpp
bool Year::equals(const Year& other);
// allows:
Year year{2024};
if( year.equals( Year{2020}.advance(Year{4}) ) ) {
    //...
}
```

在这个例子中，你可以看到为什么需要为你自己的数据类型提供操作，而该数据类型的内部值已被你完全封装。对于提到的函数，Year 的写法将如下面的清单所示。

```cpp
// https://godbolt.org/z/EPZ4Kd6jP
class Year {
    int value_;

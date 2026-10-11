
不幸的是，那段代码仍然有点混乱。特别是，如果我们读取大量文件，重复终止符测试会很繁琐。我们可以编写一个函数来处理这个问题：

```cpp
// somewhere: make ist throw if it goes bad:
std.exceptions(std.exceptions() | ios_base::badbit);

void end_of_loop(istream& ist, char term, const string& message)
{
    if (ist.fail()) {            // use term as terminator and/or separator
        ist.clear();
        char ch;
        if (ist >> ch && ch == term) return;      // all is fine
        error(message);
    }
}
```

这将输入循环简化为

```cpp
for (My_type var; ist >> var; ) {                // read until end of file
    // maybe check that var is valid
    // ... do something with var ...
}
end_of_loop(ist, '|', "bad termination of file");    // test if we can continue
// carry on: we found end of file or a terminator
```

除非流处于 `fail()` 状态，否则 `end_of_loop()` 什么也不做。我们认为这足够简单，也足够通用，适用于许多用途。

## 10.11 读取结构化文件

让我们尝试将这个“标准循环”用于一个具体的例子。像往常一样，我们将使用这个例子来说明广泛适用的设计和编程技术。假设你有一个温度读数文件，其结构如下：

- 文件包含若干年（每月读数）。
    - 一年以 `{ year }` 开始，后跟表示年份的整数，例如 `1900`，并以 `}` 结束。
- 一年包含若干月（每日读数）。
    - 一个月以 `{ month` 开始，后跟三字母月份名称，例如 `jan`，并以 `}` 结束。
- 一个读数包含一个时间和一个温度。
    - 一个读数以 `(` 开始，后跟月份中的日期、一天中的小时数和温度，并以 `)` 结束。

例如：

```
{ year 1990 }
{year 1991 { month jun }}
{ year 1992 { month jan ( 1 0 61.5) } { month feb ( 1 1 64) (2 2 65.2) } }
{year 2000
    { month feb ( 1 1 68) (2 3 66.66) (1 0 67.2)}
    {month dec (15 15 −9.2) (15 14 −8.8) (14 0 −2) }
}
```

这种格式有点特别。文件格式通常如此。行业中有向更规则和层次结构化的文件（如 HTML 和 XML 文件）发展的趋势，但现实情况是，我们很少能控制我们需要读取的文件所提供的输入格式。文件就是那个样子，我们只能读取它们。如果格式太糟糕或文件包含太多错误，我们可以编写一个格式转换程序来生成更适合我们主程序的格式。另一方面，我们通常可以选择内存中数据的表示方式来满足我们的需求，并且经常可以选择适合需求和口味的输出格式。

因此，让我们假设我们被给予了上述温度读数格式，必须接受它。幸运的是，它包含自识别组件，例如年份和月份（有点像 HTML 或 XML）。另一方面，单个读数的格式不太有帮助。例如，如果有人将月份中的日期值与一天中的小时数互换，或者有人生成了一份摄氏度为温度单位的文件而程序期望的是华氏度（或反之），就没有信息可以帮助我们。我们只能应对。

### 10.11.1 内存表示

我们应该如何在内存中表示这些数据？显然的第一个选择是三个类，`Year`、`Month` 和 `Reading`，以完全匹配输入。`Year` 和 `Month` 在操纵数据时显然很有用；我们想要比较不同年份的温度，计算月度平均值，比较一年中不同的月份，比较不同年份的相同月份，将温度读数与日照记录和湿度读数匹配等。基本上，`Year` 和 `Month` 符合我们思考温度和天气的一般方式：`Month` 持有一个月的信息，`Year` 持有一年的信息。但是 `Reading` 呢？那是一个低层概念，匹配某块硬件（传感器）。`Reading` 的数据（月份中的日期、一天中的小时数、温度）是“奇怪的”，只有在 `Month` 内部才有意义。它也是非结构化的：我们没有任何保证，读数会按月份中的日期或一天中的小时数顺序排列。基本上，每当我们想对读数做有趣的事情时，我们都要对它们进行排序。

为了在内存中表示温度数据，我们做出以下假设：

- 如果我们某个月有任何读数，那么该月通常会有很多读数。
- 如果我们某一天有任何读数，那么该天通常会有很多读数。

在这种情况下，将一个 `Year` 表示为 12 个 `Month` 的 `vector`，将一个 `Month` 表示为大约 30 个 `Days` 的 `vector`，将一个 `Day` 表示为 24 个温度（每小时一个）是有意义的。这对于各种用途来说简单且易于操作。因此，`Day`、`Month` 和 `Year` 是简单数据结构，每个都有一个构造函数。由于我们计划在知道有哪些温度读数之前将 `Months` 和 `Days` 作为 `Year` 的一部分创建，因此我们需要为尚未读取数据的一天中的某个小时拥有“非读数”的概念。

```cpp
const int not_a_reading = -7777;    // less than absolute zero
```

同样，我们注意到经常有月份没有数据，因此我们引入了“非月份”的概念来直接表示这一点，而不是必须遍历所有天数以确保某处没有隐藏数据：

```cpp
const int not_a_month = -1;
```

那么三个关键类变成

```cpp
struct Day {
    vector<double> hour {vector<double>(24, not_a_reading)};
};
```

也就是说，一个 `Day` 有 24 个小时，每个都初始化为 `not_a_reading`。

```cpp
struct Month {                             // a month of temperature readings
    int month {not_a_month};               // [0:11] January is 0
    vector<Day> day {32};                 // [1:31] one vector of readings per day
};
```

我们“浪费” `day[0]` 以保持代码简单。

```cpp
struct Year {  // a year of temperature readings, organized by month
    int year; // positive == A.D.
    vector<Month> month {12}; // [0:11] January is 0
};
```

每个类基本上都是一个由“部分”组成的简单 `vector`，并且 `Month` 和 `Year` 分别具有标识成员 `month` 和 `year`。

这里有几个“魔法常量”（例如，`24`、`32` 和 `12`）。我们试图避免在代码中使用这种字面量常量。这些是相当基本的（一年中的月份数量很少变化），并且不会在代码的其余部分中使用。然而，我们主要将它们保留在代码中是为了提醒你“魔法常量”的问题；符号常量几乎总是更可取（§7.6.1）。使用 `32` 作为一个月中天的数量绝对需要解释；`32` 在这里显然是“魔法”的。

为什么我们没有写成

```cpp
struct Day {
    vector<double> hour {24, not_a_reading};
};
```

那会简单一些，但不幸的是，我们会得到一个包含两个元素（`24` 和 `–1`）的 `vector`。当我们要为 `vector` 指定元素数量，而该 `vector` 的整数可以转换为元素类型时，不幸的是我们必须使用 `()` 初始化器语法（§18.2）。

### 10.11.2 读取结构化值

`Reading` 类仅用于读取输入，而且更简单：

```cpp
struct Reading {
    int day;
    int hour;
    double temperature;
};

istream& operator>>(istream& is, Reading& r)
// read a temperature reading from is into r
// format: ( 3 4 9.7 )
// check format, but don’t bother with data validity
{
```

`char ch1;`

`if (is>>ch1 && ch1!='(') {              // 这可能是一个 Reading 吗？`

`    is.unget();`

`    is.clear(ios_base::failbit);`

`    return is;`

`}`

`char ch2;`

`int d;`

`int h;`

`double t;`

`is >> d >> h >> t >> ch2;`

`if (!is || ch2!=')') error("bad reading"); // 读取的数据格式错误`

`r.day = d;`

`r.hour = h;`

`r.temperature = t;`

`return is;`

`}`

基本上，我们会检查输入格式是否看起来合理，如果不合理，我们就将文件状态设置为 `fail()` 并返回。这允许我们尝试以其他方式读取信息。另一方面，如果在读取部分数据后发现格式错误，且实际上没有恢复的可能性，我们就使用 `error()` 退出。

`Month` 的输入操作基本相同，区别在于它必须读取任意数量的 `Readings`，而不是固定的一组值（就像 `Reading` 的 `>>` 那样）：

```cpp
istream& operator>>(istream& is, Month& m)
// read a month from is into m
// format: { month feb ... }
{
    char ch = 0;
    if (is >> ch && ch!='(') {
        is.unget();
        is.clear(ios_base::failbit);   // 读取 Month 失败
        return is;
    }

    string month_marker;
    string mm;
    is >> month_marker >> mm;
    if (!is || month_marker!="month") error("bad start of month");
    m.month = month_to_int(mm);

    int duplicates = 0;
    int invalids = 0;
    for (Reading r; is >> r;) {
        if (is_valid(r)) {
            if (m.day[r.day].hour[r.hour] != not_a_reading)
                ++duplicates;
            m.day[r.day].hour[r.hour] = r.temperature;
        }
        else
            ++invalids;
    }
    if (invalids) error("invalid readings in month",invalids);
    if (duplicates) error("duplicate readings in month", duplicates);
    end_of_loop(is, '}', "bad end of month");
    return is;
}
```

我们会稍后再讨论 `month_to_int()`；它将月份的符号表示（如 `jun`）转换为 `[0:11]` 范围内的数字。请注意使用 §10.10 中的 `end_of_loop()` 来检查终止符。我们统计了无效和重复的 `Readings`；这可能会引起某些人的兴趣。

`Month` 的 `>>` 在存储之前会对 `Reading` 进行快速检查，以确保其合理性：

```cpp
constexpr int implausible_min = -200;
constexpr int implausible_max = 200;

bool is_valid(const Reading& r)
// a rough test
{
    if (r.day<1 || 31<r.day) return false;
    if (r.hour<0 || 23<r.hour) return false;
    if (r.temperature<implausible_min|| implausible_max<r.temperature)
        return false;
    return true;
}
```

最后，我们可以读取年份。`Year` 的 `>>` 与 `Month` 的 `>>` 类似：

```cpp
istream& operator>>(istream& is, Year& y)
// read a year from is into y
// format: { year 1972 . . . }
{
    char ch;
    is >> ch;
    if (ch!='{') {
        is.unget();
        is.clear(ios::failbit);
        return is;
    }

    string year_marker;
    int yy;
    is >> year_marker >> yy;
    if (!is || year_marker!="year") error("bad start of year");
    y.year = yy;

    while(true) {
        Month m;         // 每次循环都获取一个干净的 m
        if(!(is >> m)) break;
        y.month[m.month] = m;
    }

    end_of_loop(is, '}', "bad end of year");
    return is;
}
```

我们更希望是“平淡无奇地相似”而非仅仅是“相似”，但存在一个显著差异。看看读取循环。你是否期待过类似下面的代码？

```cpp
for (Month m; is >> m; )
        y.month[m.month] = m;
```

你本来应该这样写的，因为这就是我们之前编写所有读取循环的方式。实际上，我们最初就是这样写的，但它是错误的。问题在于 `operator>>(istream& is, Month& m)` 不会给 `m` 赋一个全新的值；它只是将来自 `Readings` 的数据添加到 `m` 中。因此，反复执行 `is>>m` 会不断向唯一的一个 `m` 添加数据。糟糕！每读取一个新的月份，都会累积该年之前所有月份的读数。我们需要一个全新的、干净的 `Month` 对象，以便每次执行 `is>>m` 时都能从中读取。最简单的做法是将 `m` 的定义放在循环内部，以便它在每次迭代时都被初始化。替代方案是让 `operator>>(istream& is, Month& m)` 在读取前先给 `m` 赋一个空月份，或者让循环这样做：

```cpp
for (Month m; is >> m; ) {
    y.month[m.month] = m;
    m = Month{}; // "重新初始化" m
}
```

让我们来试用一下：

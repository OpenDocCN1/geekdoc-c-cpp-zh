
```cpp
// Create date from Gregorian year, month and day.
date myDate2(2011, May, 16); Print(myDate2);    // Print is author-defined.

// Copy constructor.
date myDate3(myDate2); Print(myDate3);

// Constructor at the 'extremes'.
try
{
    date myDate4(pos_infin); Print(myDate4, "Positive infinity");
}
catch (bad_year& e)
{
    cout << e.what() << endl;
}

try
{
    date myDate5(neg_infin); Print(myDate5, "Negative infinity");
}
catch (bad_year& e)
{
    cout << e.what() << endl;
}

try
{
    date myDate6(max_date_time); Print(myDate6, "Max Date Time");
}
catch (bad_year& e)
{
    cout << e.what() << endl;
}

try
{
    date myDate7(min_date_time); Print(myDate7, "Min Date Time");
}
catch (bad_year& e)
{
    cout << e.what() << endl;
}
```

# 以上代码的输出为：

```text
Date Information...
not-a-date-time
Year is out of valid range: 1400..10000

Date Information...
2011-May-16
```

Year: 2011, Month: May, Day: 16
Day of week: Mon, Day of year: 136
End of month: 2011-May-31
ISO 8601 week number: 20, Day of year: 2455698

Date Information...
2011-May-16
Year: 2011, Month: May, Day: 16
Day of week: Mon, Day of year: 136
End of month: 2011-May-31
ISO 8601 week number: 20, Day of year: 2455698

Date Information...Positive infinity
+infinity
Year is out of valid range: 1400..10000

Date Information...Negative infinity
-infinity
Year is out of valid range: 1400..10000

Date Information...Max Date Time
9999-Dec-31
Year: 9999, Month: Dec, Day: 31
Day of week: Fri, Day of year: 365
End of month: 9999-Dec-31
ISO 8601 week number: 52, Day of year: 5373484

Date Information...Min Date Time
1400-Jan-01
Year: 1400, Month: Jan, Day: 1
Day of week: Wed, Day of year: 1
End of month: 1400-Jan-31
ISO 8601 week number: 1, Day of year: 2232400

请注意，我们创建了一个打印日期的函数：

```
void Print(const date& myDate, const string& type = "")
{
    cout << "\nDate Information..." << type << endl;
    cout << myDate << endl;
    cout << "Year: " << myDate.year() << ", Month: " << myDate.month() << ", Day: " << myDate.day() << endl;
    // Extra stuff.
    cout << "Day of week: " << myDate.day_of_week() << ", Day of year: " << myDate.day_of_year() << endl;
    cout << "End of month: " << myDate.end_of_month() << endl;
    cout << "ISO 8601 week number: " << myDate.week_number() << ", Day of year: " << myDate.julian_day() << endl;
}
```

接下来，我们注意到可以从字符串以及基于硬件时钟的信息创建日期，如下例所示：

```
// Constructing dates from strings.
string s("2009/1/9");                                      // 9 January 2009.
date myDate8(from_simple_string(s));
Print(myDate8,"from simple string");

// ISO 8601 extended format CCYY-MM-DD.
string s2("2009-10-9");                                     // 9 October 2009.
date myDate9(from_simple_string(s2));
Print(myDate9,"from delimited string");

// Now convert to a string
string converted = to_simple_string(myDate9);
cout << "String: " << converted << endl;                    // OUTPUT is 2009-Oct-09.

string s3("2009109");                                       // 10 October 2009.
date myDate10(from_undelimited_string(s3));
Print(myDate10,"from UNdelimited string");

// Create dates from the clock.
date myDate11(day_clock::local_day());
Print(myDate11,"Local day based on time zone settings of computer");
date myDate12(day_clock::universal_day());
Print(myDate12,"Coordinated UniversalTime (UTC)");
```

这段代码的输出是（取决于当前时间）：

```
Date Information...from simple string
2009-Jan-09
Year: 2009, Month: Jan, Day: 9
Day of week: Fri, Day of year: 9
End of month: 2009-Jan-31
ISO 8601 week number: 2, Day of year: 2454841

Date Information...from delimited string
2009-Oct-09
Year: 2009, Month: Oct, Day: 9
Day of week: Fri, Day of year: 282
End of month: 2009-Oct-31
ISO 8601 week number: 41, Day of year: 2455114
String: 2009-Oct-09

Date Information...from UNdelimited string
2009-Oct-09
Year: 2009, Month: Oct, Day: 9
Day of week: Fri, Day of year: 282
End of month: 2009-Oct-31
ISO 8601 week number: 41, Day of year: 2455114
```

Date Information...Local day based on time zone settings of computer
2011-May-18
Year: 2011, Month: May, Day: 18
Day of week: Wed, Day of year: 138
End of month: 2011-May-31
ISO 8601 week number: 20, Day of year: 2455700

Date Information...Coordinated Universal Time (UTC)
2011-May-18
Year: 2011, Month: May, Day: 18
Day of week: Wed, Day of year: 138
End of month: 2011-May-31
ISO 8601 week number: 20, Day of year: 2455700

现在我们已经完成了对 date 类主要功能的讨论。

## 10.6 前向列表和编译期数组

在本节中，我们讨论 C++ 中两种较新的数据结构。

### 10.6.1 std::forward_list<

在 STL 中，容器类 `std::list<>` 通常实现为双向链表。这意味着链表中的每个元素都有两个指针，一个指向前驱元素，另一个指向后继元素。这允许我们在链表中向前和向后两个方向导航。然而，这种灵活性是有代价的：

- 增加内存消耗（我们需要存储指针）。
- 某些应用只需要向前导航。
- 在双向链表中删除和插入元素需要销毁和创建资源。
- 使用双向链表可能带来性能问题。

由于这些原因，我们可以考虑使用容器 `std::forward_list<>`，它将其元素作为单向链表管理。它支持在容器中的任意位置高效地插入和删除元素。不支持随机访问迭代器。简而言之，当不需要双向迭代时，前向列表提供了比 `std::list<>` 更节省空间的替代方案。

成员函数的类别包括（Josuttis, 2012）：

- 创建和销毁链表。
- 非修改操作。
- 赋值。
- 元素访问。
- 插入和移除元素。
- 拼接和合并链表。

其语法与 `std::list<>`（假设已了解）类似，这意味着学习曲线平缓。我们举一些简单的例子来说明，代码很容易理解。首先，我们创建一些链表：

```
using List = std::forward_list<double>;

void CreateForwardLists()
{
    // Default empty list
    List c;

    // List with a size and a value
    int sz = 5; double val = 3.14;
    List c2(sz, val);
    print(c2);        // 3.14, 3.14, 3.14, 3.14, 3.14

    // List with initialiser list (2 forms)
    List c3{ 1.0, -4.6, 8.9 };
    print(c3); //  1.0, -4.6, 8.9

    List c4 = { 10.0, -40.6, 80.9 };
    print(c4);      //  10.0, -40.6, 80.9
}
```

```
void print(const List& list)
{
    // Single list has no size(), so we calculate distance
    // between first and last elements of list
    std::cout << "\nList size: "
              << std::distance(list.begin(), list.end())
              << ", contents are: ";

    for(auto& elem: list)
    {
        std::cout << elem << ",";
    }
}
```

我们现在给出一些在链表中查找给定值的代码：

```
List::const_iterator Find(const List& list, double val)
{ // Find a value in a list

    for (auto pos = std::begin(list); pos != std::end(list); ++pos)
    {
        if (*pos == val)
        {
            return pos;  // value found
        }
    }

    return list.cend();
}
```

我们举一个例子来说明如何在链表中的特定位置插入值以及如何从链表中删除元素。我们注意到，在这方面前向链表与双向链表的行为不同，因为前者没有反向迭代器。

```
void ModifyForwardList()
{ // Do some things with lists

    List list;
    list.push_front(-1.0);

    // Insert
    list.insert_after(list.begin(), 2.71);
    print(list);      // -1, 2.71

    int count = 2;
    list.insert_after(list.begin(), count, 148.33);
    print(list);      // -1, 148.33, 148.33, 2.71

    list.insert_after(list.begin(), { 150.1, 262.9, 56.3 });
    print(list);      // -1, 150.1, 262.9, 56.3, 148.33, 148.33, 2.71

    // Erase, remove the element AFTER the value
    double val = 262.9;
    auto pos = Find(list, val);
    if (pos != list.cend())
    {
        list.erase_after(pos);
    }
    else
    {
        std::cout << "\nValue " << val << " not found \n";
    }

    print(list);      // -1, 150.1, 262.9, 148.33, 148.33, 2.71
    val = 56.3;
    pos = Find(list, val);
    if (pos != list.cend())
    {
        list.erase_after(pos);
    }
    else
    {
        std::cout << "\nValue " << val << " not found \n";
    }

    print(list);      // -1, 150.1, 262.9, 148.33, 148.33, 2.71
}
```

在某些情况下，前向链表可能是双向链表的一种可行替代方案。参见练习3。

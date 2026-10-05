

# 第6 章 结构与类

## 显示 6.4 带有私有成员的类（3 部分中的第2 部分）

> //后置条件：日期设置为给定月份的第一天。

```cpp
int getMonthNumber(); // 1 月返回 1，2 月返回 2，以此此类推。
int getDay();
private:
    int month; // 私有成员
    int day;
};
```

```cpp
int main() {
    DayOfYear today, bachBirthday;
    cout << "Today's date:\n";
    today.input();
    cout << "Today's date is ";
    today.output();
    cout << endl;

    bachBirthday.set(3, 21);
    cout << "J. S. Bach's birthday is \n";
    bachBirthday.output();
    cout << endl;
    if (today.getMonthNumber() == bachBirthday.getMonthNumber() &&
        today.getDay() == bachBirthday.getDay())
        cout << "Happy Birthday Johann Sebastian!\n";
    else
        cout << "Happy Birthday Johann Sebastian!\n";
    return 0;
}
```

```cpp
// 使用 iostream 和 cstdlib
void DayOfYear::set(int newMonth, int newDay) {
    if ((newMonth >= 1) && (newMonth <= 12))
        month = newMonth;
    else {
        cout << "Illegal month value! Program aborted.\n";
        exit(1);
    }
    if ((newDay >= 1) && (newDay <= 31))
        day = newDay;
    else {
        cout << "Illegal day value! Program aborted.\n";
        exit(1);
    }
}
```

> 注意函数名 set 是重载的。你可以像重载任何函数一样重载成员函数。

> 改变器函数 (Mutator function)

## 显示 6.4 带有私有成员的类（3 部分中的第3 部分）

```cpp
58  // 使用 iostream 和 cstdlib
59  void DayOfYear::set(int newMonth)
60  {
61      if ((newMonth >= 1) && (newMonth <= 12))
62          month = newMonth;
63      else
64          {
65              cout << "Illegal month value! Program aborted. \n"
66              exit(1);
67          }
68      day = 1;
69  }
70  
71  int DayOfYear::getMonthNumber()
72  {
73      return month;
74  }
75 
76  int DayOfYear::getDay()
77  {
78      return day;
79  }
80 
81  // 使用 iostream 和 cstdlib
82  void DayOfYear::input()
83  {
84      cout << "Enter the month as a number: \ ";
85      cin >> month;
86      cout << "Enter the day of the month: \ (but not elsewhere).\n"
87      cin >> day;
88      if ((month < 1) || (month > 12) || (day < 1) || (day > 31))
89          {
90              cout << "Illegal date! Program aborted. \n"
91              exit(1);
92          }
93}
```

```cpp
92  void DayOfYear::output()
93  <DayOfYear::output 的其余定义在显示 6.3 中给出。>
```

## 示例对话

```
Enter today's date:
Enter the month as a number: 3
Enter the day of the month: 21
Today's date is March 21
J. S. Bach's birthday is March 21
Happy Birthday Johann Sebastian
```

一旦你将成员变量设为私有成员变量，除非使用成员函数之一，否则没有办法更改它的值（或以任何其他方式引用成员变量）。这意味着编译器将强制隐藏 `DayOfYear` 类数据的实现细节。如果你仔细查看显示 6.4 中的程序，你会发现成员变量名 `month` 和 `day` 仅在成员函数的定义中使用过。在成员函数定义之外，没有对 `today.month`、`today.day`、`bachBirthday.month` 或 `bachBirthday.day` 的引用。

所有跟在 public 词（在本例中指成员函数）后面的项都被称为公共，这意味着它们可以在任何地方通过名称引用。对公共成员的使用没有限制。

任何成员变量可以是公共的也可以是私有的。任何成员函数可以是公共的也可以是私有的。然而，良好的编程实践要求所有成员变量必须是私有的，且通常大多数成员应该是函数。

在类定义中，你可以包含任意数量的 `public` 和 `private` 访问修饰符。每当你插入标签：

```cpp
public:
```

成员列表就会从私有变为公共。每当你插入标签：

```cpp
private:
```

成员列表就会变回为私有成员。你不需要只拥有一个公共和一个私有的成员组。不过，通常只有一个公共区域和一个私有区域。

关于应该先列出公共成员还是先列出私有成员，目前还没有通用的共识。大多数人似乎倾向于先列出公共成员。这便于查看程序员实际上可以使用的部分。你可以根据自己的想法决定先放置哪些内容，但书中的示例通常将公共成员列在私有成员之前。

从 C++ 的角度来看，似乎倾向于先列出私有成员。如果成员组既没有 `public` 也没有 `private` 修饰符，那么该成员将自动变为私有。你会在代码中看到这种默认行为，并应该熟悉它。

## 访问器函数 (Accessor Functions)

你应该始终将类中的成员变量设为私有。然而，你可能需要对类中的数据进行某些操作。成员函数允许你对数据进行许多操作，但迟晚你可能需要对那些没有成员函数的数据进行操作。你如何处理对象中的数据？答案是，只要你为类配备了访问器函数和改变器函数，就可以合理地进行任何操作。这些函数允许你以通用的方式访问并更改对象中的数据。访问器函数允许你读取对象中的数据。

## 改变器函数 (Mutator functions)

这些函数允许你以通用的方式更改对象中的数据。


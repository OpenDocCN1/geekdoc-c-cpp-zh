
```cpp
    cout << "Enter the month as a number: ";

    cin >> month;

    cout << "Enter the day of the month: ";

    cin >> day;

}

void DayOfYear::output() {

    cout << "month = " << month << ", day = " << day;

}

void DayOfYear::checkDate() {

    // 实现省略

}
```

# 显示 11.1 等等性函数（3 第三部分）

## 示例对话

```
Enter today's date:

Enter the month as a number: 3

Enter the day of the month: 21

Today's date is month = 3, day = 21

J. S. Bach's birthday is = 3, day = 21

Happy Birthday!
```

假设 `today` 和 `bachBirthday` 是两个具有代表某些日值的 `DayOfYear` 对象。你可以通过以下尔表达式测试它们是否代表同一日期：

```
equal(today, bachBirthday)
```

此 `equal` 函数调用在 `today` 和 `bachBirthday` 代表同一日期时返回 `true`。在显示 11.1 中，该布尔表达式用于控制 `if-else` 语句。

`equal` 函数的定义非常直接。如果两个日期代表相同的月份和日期，则它们相等。`equal` 的定义使用访问器函数 `getMonth` 和 `getDay` 来比较两个对象的月份和日期。

注意我们没有将 `equal` 函数实现为成员函数。可以将 `equal` 实现为 `DayOfYear` 类的成员函数，但 `equal` 的是两个 `DayOfYear` 对象。如果你将 `equal` 实现为成员函数，你必须决定调用对象应该是第一个日期还是第二个日期。与其随机选择两个日期中的一个作为调用对象，我们而是将 `equal` 实现为接收两个日期作为参数的普通（非成员）函数。

## 自测练习

- 编写一个名为 `before` 的函数，接收两个 `DayOfYear` 类型参数（定义在显示 11.1 中）。该函数返回一个 `bool` 值，如果第一个参数代表的日期在第二个参数代表的日期之前，则返回 `true`；否则，函数返回 `false`，例如，1 月 5 日在 2 月 2 日之前。

## 朋友函数

如果你的类拥有一套完整的访问器函数（accessor functions），你可以使用这些访问函数来定义相等性测试，或者执行任何其他依赖于私有成员变量的计算。然而，尽管这可能让你访问私有成员变量，但它可能并不能让你高效地访问它们。再次查看显示 11.1 中 `equal` 函数的定义。为了读取月份，它必须调用访问函数 `month()`。为了读取日期，它必须调用访问函数 `day()`。这行得通，但如果我们能直接访问成员变量，代码将会更简单、更高效。

显示 11.1 中给出的 `equal` 函数的一个更简单且高效的定义将：

```cpp
bool equal(DayOfYear date1, DayOfYear date2)
{
    return (date1.month == date2.month &&
            date1.day == date2.day);
}
```

这个定义只有一个问题：它是非法的！之所以非法是因为成员变量 `month` 和 `day` 是 `DayOfYear` 类的私有成员。通常，私有成员变量（以及私有成员函数）不能在类体中被引用，除非该函数是成员函数，而 `equal()` 不是 `DayOfYear` 类的成员函数。但有一种方法可以让非成员函数拥有与朋友（friend）相同的访问权限。如果我们把 `equal` 函数设为 `DayOfYear` 类的朋友，那么之前的 `equal` 定义就是合法的。

朋友类不是类的成员函数，但朋友函数拥有像成员函数一样访问类私有成员的权限。朋友函数可以直接读取成员变量的值，甚至可以直接修改成员变量的值，例如通过一个赋值操作符之一包含私有成员的赋值语句来实现。要使一个函数成为朋友，你必须在类定义中将其声明为朋友。例如，在显示 11.2 中，我们重写了 `DayOfYear` 类的定义，使得 `equal` 函数成为该类的朋友。你通过在类定义中列出朋友声明并在函数声明前加上 `friend` 关键字来使类类的朋友。

通过列出朋友声明，可以将朋友函数添加到类定义中，就像列出成员函数的声明一样，只不过要在函数声明之前加上 `friend` 关键字。然而，朋友不是成员函数；相反，它是一个对类数据成员具有特殊访问权限的普通函数。朋友函数的定义和调用方式完全一样。

## 显示 11.2 作为朋友的相等函数

```cpp
 // 演示 equal 函数。
// 在这个版本中，equal 是 DayOfYear 类的朋友。
#include <iostream>
using namespace std;
class DayOfYear {
public:
    friend bool equal(DayOfYear date1, DayOfYear date2);
    // 前提条件：date1 和 date2 有值。
    // 如果 date1 和 date2 代表同一日期，则返回 true
    // 否则，返回 false。
    DayOfYear(int month, int day);
    // 前提条件：月份和日期构成一个
    // 可能的日期。根据参数初始化日期。
    DayOfYear();
    // 将日期初始化为1 月 1 日。
    void input();
    void output();
    int getMonth();
    // 返回月份，1 月为 1，2 月为 2，以此此类推。
    int getDay();
    // 返回月份中的几。
private:
    void checkDate();
    int month;
    int day;
};
int main() {
    // ... 函数实现 ...
    bool equal(DayOfYear date1, DayOfYear date2) {
        return (date1.month == date2.month && date1.day == date2.day);
    }
}
```

> 注意，私有成员变量 `month` 和 `day` 可以通过名称访问。

程序的主部分与显示 11.1 相同。
该显示的其他部分（包括示例对话）与显示 11.1 相同。

## 第 11 章 / 类中的朋友、重载运算符和数组

特别地，显示 11.2 所示的 `equal` 函数定义没有在函数头中包含 `DayOfYear::` 限定符。此外，`equal` 函数不是通过点运算符（`.`）调用的。`equal` 函数将 `DayOfYear` 类型的对象作为参数，就像任何其他非成员函数接受任何类型的参数的方式一样。然而，朋友函数的定义可以通过名称访问类的私有成员变量和私有成员函数，因此它拥有与成员函数相同的访问权限。

## 编程提示：同时定义访问器函数和朋友函数

看起来似乎如果你把所有函数都设为类的朋友，那么就不需要在类中包含访问函数（accessor functions）或修改器函数（mutator functions）了。毕竟，朋友函数可以访问私有成员变量，不需要访问或修改器函数。这并不完全错误。确实，如果你把世界上所有的函数都设为类的朋友，你就不需要访问或修改器函数。然而，让所有函数变成朋友是不现实的。

为了了解为什么你仍然需要访问函数，请考虑显示 11.2 给出的 `DayOfYear` 类示例。你可能在另一个程序中使用此类，而另一个程序可能想对 `DayOfYear` 对象的月份部分做一些操作。例如，程序可能想计算一年还剩几个月。具体来说，程序的主部分可能包含以下内容：

```cpp
DayOfYear today;
cout << "enter today's date: ";
// ...
cout << "months remaining: " << 12 - today.getMonth();
```

朋友函数通过列出朋友声明，将朋友函数添加到类定义中，就像列出成员函数的声明一样，只不过要在函数声明之前加上 `friend` 关键字。然而，朋友不是成员函数；相反，它是一个对类数据成员具有特殊访问权限的普通函数。朋友函数的定义和调用方式完全一样。

## 朋友

```cpp
friend returnType name(arguments);
```

## 语法 (Syntax)

```cpp
class ClassName {
    ...
    friend returnType functionName(arguments);
    ...
};
```

## 示例 (Example)

```cpp
class ClassName {
    private:
    int data;
public:
    ...
    friend void functionName(ClassName &obj);
};
void functionName(ClassName &obj) {
    obj.data = 10; // 直接访问私有成员
}
```



# 嵌套 if 语句

Team LiB

上一页 下一页

# 逻辑运算符

C++ 拥有逻辑运算符，允许你在一个 `if` 或 `else` 语句中组合比较操作。表 6-1 列出了 C++ 支持的逻辑运算符并描述了它们的功能。

## 表 6-1: 逻辑运算符

| 运算符 | 名称 | 功能 |
| --- | --- | --- |
| && | 与 | 连接关系表达式。只有当两个表达式都为真时，整个表达式才才为真。 |
| || | 或 | 连接两个关系表达式。如果其中一个表达式为真，整个表达式就为真。 |
| ! | 非 | 反转表达式的“真值”，使真表达式变为假，使假表达式变为真。 |

## && 运算符

`&&` 运算符称为逻辑与运算符。它是一个二元运算符；它接受两个布尔表达式作为操作数。只有当两个表达式都为真时，它才返回真。如果其中一个表达式为假，整个表达式就为假。当然，如果两个表达式都为假，整个表达式也是假。表 6-2 阐释了这一点。

## 表 6-2: 逻辑与运算符

| 表达式 #1 | 表达式 #2 | 表达式 #1 && 表达式 #2 |
| --- | --- | --- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

下面的程序展示了如何使用逻辑与运算符判断用户是否有投票资格，标准是用户必须至少 18 岁且是公民。

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int age;
    char choice;
    bool citizen;
    cout << "Enter your age: ";
    cin >> age;
    cout << "Are you a citizen (Y/N): ";
    cin >> choice;

if (choice == 'Y')
    citizen = true;
else
    citizen = false;

if (age >= 18 && citizen == true)
    cout << "You are eligible to vote";
else
    cout << "You are not eligible to vote";
    return 0;
}
```

以下是几次示例运行，用 === 分隔：

Enter your age: 18
Are you a citizen (Y/N): Y
You are eligible to vote
===
Enter your age: 18
Are you a citizen (Y/N): N
You are not eligible to vote
===
Enter your age: 17
Are you a citizen (Y/N): Y
You are not eligible to vote
===
Enter your age: 17
Are you a citizen (Y/N): N
You are not eligible to vote

程序中使用逻辑与运算符的部分是：

```cpp
if (age >= 18 && citizen == true)
    cout << "You are eligible to vote";
else
    cout << "You are not eligible to vote";
```

比较表达式 `age >= 18` 被称为表达式的左部分，因为它在逻辑运算符的左侧。同样，比较表达式 `citizen == true` 被称为表达式的右部分，因为它在逻辑运算符的右侧。

如果用户的年龄至少为 18 岁，程序将进行第二次比较，即用户是否为公民。如果用户的年龄未满 18 岁，则在执行第一个表达式之前不会进行第二次比较。其目的是避免浪费 CPU 时间；如果左表达式为假，无论右表达式求值结果如何，整个表达式都为假。

因为只有在用户年龄至少为 18 岁时才会进行用户是否为公民的第二次比较，所以使用嵌套语句的程序图6-1 也适用于此使用逻辑运算符的程序。

## || 运算符

`||` 运算符称为逻辑或运算符。与逻辑运算符一样，逻辑或运算符也是一个二元运算符，接受两个布尔表达式作为操作数。如果任一个表达式为真，它返回真。如果两个表达式都为假，它返回假。当然，如果两个表达式都为真，整个表达式为真。表 6-3 阐释了这一点。

## 表 6-3: 逻辑运算符

| 表达式 #1 | 表达式 #2 | 表达式 #1 || 表达式 #2 |
|---|---|---|
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

下面的程序展示了如何使用逻辑运算符判断你是否可以免费看电影，标准是用户年龄必须不超过 12 岁或至少满 65 岁。

```cpp
#include <iostream>
using namespace std;
int main() {
    int age;
    cout << "Enter your age: ";
    cin >> age;
    if (age <= 12 || age >= 65)
        cout << "Admission is free";
    else
        cout << "You have to pay";
    return 0;
}
```

以下是几次示例运行：

```
Enter your age: 12
Admission is free
===
Enter your age: 18
You have to pay
===
Enter your age: 65
Admission is free
```
（注：OCR 原文中为 "Enterter" 和 "nEnter"，已修正为 "Enter"）

程序中使用逻辑运算符的部分是：

```cpp
if (age <= 12 || age >= 65)
    cout << "Admission is free";
    else
    cout << "You have to pay";
    return 0;
```

与与运算符一样，比较表达式 `<= 12` 被称为表达式的左部分，比较表达式 `age >= 65` 被称为表达式的右部分。

如果用户的年龄超过 12 岁，程序将进行第二次比较，即用户是否至少满 65 岁。如果用户不超过 12 岁，则在执行第一部分之前不会进行第二次比较。结果与逻辑与运算符一样，是为了避免浪费 CPU 时间；如果表达式为真，无论求值如何结果均为真。

因为只有在用户年龄至少为 18 岁时才会进行第二次比较，所以使用嵌套语句的程序图6-1 也适用于此使用逻辑运算符的程序。

## ! 运算符

`!` 运算符称为逻辑非运算符。它是一个一元运算符；它只接受一个布尔表达式作为操作数。它反转表达式的“真值”，使真表达式变为假，使假表达式变为真。

下面的程序展示了如何使用逻辑非运算符判断用户是否有折扣。

```cpp
#include <iostream>
using namespace std;
int main() {
    bool hasCoupon;
    cout << "Do you have a coupon (Y/N): ";
    cin >> hasCoupon;
    if (!hasCoupon)
        cout << "You get a discount";
    else
        cout << "You do not get a discount";
    return 0;
}
```

以下是几次示例运行，用 === 分隔：

Do you have a coupon (Y/N): Y
You do not get a discount
===
Do you have a coupon (Y/N): N
You get a discount

程序中使用逻辑非运算符的部分是：

```cpp
if (!hasCoupon)
    cout << "You get a discount";
else
    cout << "You do not get a discount";
```

`!` 运算符反转布尔表达式的值。如果表达式为真，`!expression` 为假。如果表达式为假，`!expression` 为真。这通常用于检查条件是否为假。

## 德摩根定律

德摩根定律提供了简化复杂逻辑表达式的方法。这两个律：

1. `!(A && B)` 等于 `!A || !B`
2. `!(A || B)` 等于 `!A && !B`

这些定律对于简化条件语句非常有用。例如，第一个律规定逻辑与（AND）的否定等同于逻辑或（OR）的否定的否定。第二个律规定逻辑或（OR）的否定等同于逻辑与（AND）的否定的否定。


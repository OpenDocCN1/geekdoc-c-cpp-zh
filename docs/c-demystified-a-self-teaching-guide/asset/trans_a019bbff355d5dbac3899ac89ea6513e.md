

# 测验

- 1. 关系表达式中有多少个操作数？
- 2. 流程图的作用是什么？
- 3. `if` 关键字后面表达式的数据类型是什么？
- 4. 在 `if /else if /else` 语句中，哪部分可以有多个但只能有一个？
- 5. 在 `if /else if /else` 语句中，哪部分可以有多个？
- 6. 在 `if /else if /else` 语句中，哪部分可以省略？
- 7. 在 `switch` 语句中，`switch` 关键字后面表达式的要求数据类型是什么？
- 8. 在 `switch` 语句中，可以跟一个字符数据类型的表达式吗？
- 9. 在 `switch` 语句中，`case` 关键字后面的表达式可以是变量吗？
- 10. `switch` 语句中的哪个关键字对应 `if /else` 语句中的 `else` 关键字？

## 第 6 章：嵌套 if 语句与逻辑运算符

## 概述

第 5 章从罗伯特·弗罗斯的著名诗句《未选择的路》的开头开始：“在黄色的树林里，有两条路在叉路，可惜我不能同时走向。”

我并不是要做一个诗歌评论家，但道路往往不止有两条。

在第 5 章中，我们每次只评估一个布尔表达式，并根据表达式的真假来选择我们的代码走哪条路。然而，有时需要评估两个（或多个）布尔表达式来确定代码将要走的路径。

例如，只有当你是公民且年龄至少满 18 岁时，你有权投票。除非两个条件都成立，否则你不能投票。在其他布尔表达式的情况下，你是在测试两个比较中的任意一个是否成立。例如，如果你是老人（65 岁及以上）或儿童（12 岁及以下），你可以免费进入电影院。因此，只要其中一个条件成立你就可以免费进入。

本章将介绍评估布尔表达式以确定应该执行哪些代码的方法。第一种方法是将 `if` 语句嵌套在另一个内部。第二种方法引入了另一种运算符：逻辑运算符。

# 嵌套 if 语句

一个 `if` 语句可以出现在另一个 `if` 语句内部。当这样做时，内部语句被称为“嵌套”在外部语句中。

你可以通过嵌套 `if` 语句来判断两个表达式是否都为真，或者判断其中一个表达式是否为真。

### 测试两个布尔表达式是否为真

以下程序展示了如何使用嵌套 `if` 语句来判断两个布尔表达式是否都为真。如果用户的输入是年龄至少 18 岁且是公民，程序将输出他们有权投票。否则，程序将输出他们无权投票。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int age;
    char choice;
    bool citizen;
    cout << "Enter your age: ";
    cin >> age;
    cout << "Are you a citizen (Y/N): ";
    cin >> choice;
    if (choice == 'Y') {
        citizen = true;
    } else {
        citizen = false;
    }
    if (age >= 18)
        if(citizen) cout << "You are eligible to vote";
        else cout << "You are not eligible to vote";
    else
        cout << "You are not eligible to vote";
    return 0;
}
```

以下是几个示例运行，用 === 分隔：

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
====

图 6-1 展示了该程序的流程图。

![](img/59a3417a6d5906fae6d8000d4c2cff76_112_0.png)

**图 6-1:** 投票程序的流程图

**图 6-1:** 投票程序的流程图

```cpp
if (age >= 18)
  if (citizen)
    cout << "You are eligible to vote";
  else
    cout << "You are not eligible to vote";
else
  cout << "You are not eligible to vote";
```

判断用户是否满 65 岁的内部 `if/else` 结构嵌套在判断用户是否至少满 12 岁的外部 `if/else` 结构中。通过这种嵌套，只有当用户年龄超过 12 岁时，才会进行是否至少满 65 岁的比较。

### 测试两个表达式是否为真

以下程序展示了如何使用嵌套 `if` 语句来判断两个布尔表达式是否都为真。如果用户的输入是年龄至少 18 岁且是公民，程序将输出结果。

```cpp
#include <iostream>
using namespace std;
int main(void) {
    int age;
    cout << "Enter your age: ";
    cin >> age;
    if (age > 12)
        if (age >= 65)
            cout << "Admission is free";
        else
            cout << "You have to pay";
    else
        cout << "Admission is free";
    return 0;
}
```

图 6-2 展示了该程序的流程图。

![](img/59a3417a6d5906fae6d8000d4c2cff76_114_0.png)

**图 6-2:** 电影程序的流程图


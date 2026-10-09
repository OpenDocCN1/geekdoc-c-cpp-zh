
```cpp
#include <iostream>    // 程序将使用键盘和屏幕

using namespace std;      // 将使用标准标识符 cin, cout, endl

int main()
{
    cout << "Type in a whole number..." << endl;

    int num;

    cin >> num;

    // 决定数字是负数、正数还是零

    if (num < 0)
        cout << "It was negative" << endl;
    else
        if (num > 0)
            cout << "It was positive" << endl;
        else
            cout << "It was exactly zero" << endl;

    return 0;
}
```

## 使用 `! NOT` 运算符寻找值或表达式的反面

你可以使用 `! NOT` 运算符来找到关系表达式或布尔表达式的反面。该运算符也被称为取反运算符。当你想要找到求值为 `true` 或 `false` 的表达式的反面时，就可以使用它。

使用 `!` 取反运算符最简单的方法是找到布尔变量值的反面。

```
isNight      = ! isDay
awake       = ! asleep
inCredit     = ! inDebt
```

它也可以用于找到某个表达式的反面。

例如，看下方的表达式：

```
temperature < 100
( today == "Sunday" ) or ( today == "Sunday" )
raining = true

( phoneCharged = true ) and ( credit > 0 )
myName.length() > 0
```

上述每个表达式都可以由计算机计算，并根据每个变量中存储的值给出一个 `true` 或 `false` 的答案。

你可以通过在每个表达式的前面加上 `!` 取反运算符来找到每个表达式的反面，如下述语句所示：

```
waterBoiling = ! ( temperature < 100 );
workingDay = ! ( today == "Sunday" ) or ( today == "Sunday" );
dryWeather = ! ( raining == true );
problem = ! ( phoneCharged = true ) and ( credit > 0 );
validSurname = ! ( myName.length() > 0 );
```

## 在表达式部分周围添加额外的 `()` 括号以确保正确结果

我们已经看到，可以将算术表达式的部分包含在 `()` 括号中，以改变某些特定操作执行的顺序。同样，你也可以将逻辑表达式的部分包含在 `()` 括号中，以强制逻辑操作在表达式的其他部分之前执行。

之前的示例都包含一个或多个运算符，在应用 `!` 运算符之前，为每个表达式加上 `()` 括号是重要的。如果你不这样做，`!` 运算符可能只影响表达式的一部分，并可能导致错误的结果。

在下面的示例中，我们需要在应用 `!` 运算符之前，在整个表达式周围使用一对额外的 `()` 括号：

```
bool goToWork = ! ( today == "Saturday" ) or ( today == "Sunday" );
```

这意味着，如果今天不是周六也不是周日，那么就是工作日；我是否需要上班取决于是否为周末（即周六或周日）的反面。

如果没有这对括号，该语句将给出错误的答案，因为它的含义将完全不同：

```
bool goToWork = ! ( today == "Saturday" ) or ( today == "Sunday" );
```

在上面的示例中，`!` 运算符只影响了表达式中加粗显示的部分。这意味着，如果不是周六，或者如果是周日，那么就是工作日。

### 使用 `and` 运算符结合 `not` 来检查密码是否有效

下一个程序使用逻辑运算符来检查字符串是否符合接受密码的规则：

```cpp
Example 6.12 - validate_password.cpp

#include <iostream> // 程序将使用键盘和屏幕

using namespace std; // 将使用标准标识符 string, cin, out, endl

int main()
{
    // 指示用户输入密码
    cout << "Please type new password between 8 and 12 characters long." << endl;
    cout << "It must contain at least one letter and at least one digit." << endl;
    cout << "It must not contain any spaces." << endl;

    // 让用户输入
    string password;
    cin >> password;

    // 找出他们输入了多少个字符
    unsigned int numChars = password.length();
```

```cpp
// 检查长度是否接受，应在 8 到 12 个字符之间
bool lengthOK = ( numChars >= 8 ) and ( numChars <= 12 );
```

```cpp
// 检查至少有一个数字和一个字母
char symbol;
bool foundDigit = false;
bool foundLetter = false;
```

```cpp
// 逐个检查输入的每个字符
for (unsigned int position = 0; position < numChars; position++)

    // 从字符串获取字符
    symbol = password.at(position);

    // 检查是否为数字
    if (symbol >= '0' && symbol <= '9')
        foundDigit = true;

    // 检查是否为小写字母
    if (symbol >= 'a' && symbol <= 'z')
        foundLetter = true;

    // 检查是否为大写字母
    if (symbol >= 'A' && symbol <= 'Z')
        foundLetter = true;
}

// 决定密码是否符合所有标准
if (lengthOK && foundDigit && foundLetter)
    cout << "Password is valid." << endl;
else
    cout << "Password is not valid." << endl;

return 0;
}
```

```cpp
// 在显示内容前等待 3 秒
sleep( 3 );
out << msg << endl;

} // 无限 while 循环结束

return 0;
}
```

当程序运行时，它会显示随机指令告诉你要做什么：

![](img/0c86cf81300257fe2415e40f8fb03508_202_0.png)

`switch` 语句在源代码文件中占据许多行文本。通过移除一些换行符，可以让代码变得更容易读，使语句占用的空间更小：

# 使用更少行数的重写的 `switch` 语句示例

```cpp
// 根据选出的随机数设置要显示的消息
switch ( choice )
{
case 0:    msg = "把你的手放在头上"; break;
case 1:    msg = "旋转三圈"; break;
case 2:    msg = "坐下"; break;
case 3:    msg = "站起来";
}
// switch 语句结束
```

到目前为止，我们的程序比真正的游戏要简单得多。传统上，只有当指令前面有“Simon 说（Simon says...）”时，你才执行该指令。

代码可以修改为随机欺骗玩家。它可以选择一个随机数，然后在告诉他们要做什么之前，决定是否显示“Simon 说...”。

程序需要一个新的整数变量：

```cpp
int bluff;
```

接下来，程序会有 1 分 4 的概率尝试欺骗玩家。

为了实现这一点，程序将在 0 到 3 之间选择另一个额外的随机数。这个值将用于一个简单的 `if` 决策，以决定是否显示“Simon 说...”。

额外的代码看起来像这样：

```cpp
// 选择一个 0 到 3 之间的随机数
bluff = random() % 4;

// 如果选中 1, 2 或 3，则显示消息“Simon says ” 
// 如果选中 0，则什么都不做——这是一个欺骗！
if (bluff > 0)
    cout << "Simon says...";
```

在原始程序中添加欺骗代码后，发生的情况如下：

```text
Simon says... 旋转三圈
Simon says... 站起来
Simon says... 把你的手放在头上
Simon says... 坐下
把你的手放在头上
Simon says... 坐下
旋转三圈
Simon says... 旋转三圈
Simon says... 旋转三圈
把你的手放在头上
Simon says... 旋转三圈
```

使用修改后代码程序的程序的版本所示：

示例 6.14 修改版 - `switch_simon_says.cpp`

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <unistd.h>

// 程序将在屏幕上显示一些文本
// 使用 random() 和 rand() 函数
// 使用 time() 函数作为随机种子
// 使用 sleep() 函数在执行期间进行暂停

using namespace std;

// 将使用标准标识符 string, cout 和 endl

int main() {
    // 为随机数生成器种子，使其不会总是选择相同的数字
    srand(time( 0));

    int choice;
    string msg;
    int bluff;

// 持续对要做什么进行随机选择的无限循环
while ( true ) {
  // 选择一个 0 到 3 之间的随机数
  bluff = random() % 4;

  // 如果选中 1, 2 或 3，则显示消息 "Simon says "
  // 如果选中 0，则什么都不做——这是一个欺骗！
  if (bluff > 0) {
    cout << "Simon says...";
```

一个 `switch` 语句可以包含一个 `default` 情况，当没有其他匹配项时触发。`switch` 语句匹配的变量必须是整数。

```cpp
switch ( choice ) {
    case 1: cout << "A"; break;
    default: cout << "Unknown";
} // switch 语句结束
```

使用 `?` 运算符来决策值

正如我们在本章早期阶段看到的，`?` 运算符是用于进行简单值决策的简写形式。它可以替代 `if-else` 语句。

考虑这个 `if-else` 语句：

```cpp
if ( waterTemp <= 0 )
    message = "冻结";
else
    message = "未冻结";
```

这意味着：

- 如果变量 `waterTemp` 的值小于等于零，

那么

将变量 `message` 的值设置为“冻结”，

否则

将变量 `message` 的值设置为“未冻结”。

相同的语句可以使用 C++ 中的 `?` 运算符重写为稍微更短的形式：

```cpp
message = ( waterTemp <= 0 ) ? "冻结" : "未冻结";
```

> `waterTemp <= 0` 是要执行的测试。

> "冻结" 是测试结果为真时返回的值。

> "未冻结" 是测试结果为假时返回的值。

同样，`?` 运算符可以返回一个 `int` 值作为其结果：

示例 6.17-条件运算符.cpp

```cpp
#include <iostream> // 程序将使用键盘和屏幕

using namespace std; // 将使用标准标识符 cin, cout, endl

int main() {
    cout << "天气糟糕吗？y 或 n:" << endl;
    char letter;
    cin >> letter;

    // 根据用户是否输入字母 y 决定使用种速度
    int speedLimit = (letter == 'y') ? 40 : 60;

    cout << "当前限速为 " << speedLimit << " mph" << endl;

    return 0;
}
```

下一个程序将检查一个整数并告诉你是奇数还是偶数。它通过获取该数字除以 2 的余数来实现这一点：

## 示例 6.18 - `conditional_odd_even.cpp`

```cpp
#include <iostream>    // 程序将使用键盘和屏幕

using namespace std;    // 将使用标准标识符 string, cin, cout, endl

int main()
{
    // 让用户输入数字
    cout << "Enter a whole number:" << endl;
    int numValue;
    cin >> numValue;

    // 找到数字除以 2 的余数
    int remainder = numValue % 2;

    // 使用余数来判断数字是奇数还是偶数
    string message = (remainder == 0) ? "even" : "odd";

    // 在屏幕上显示结果
    cout << "That number is ";
    cout << message << endl;

    cout << endl; // 显示空行

    return 0;
}
```

上面的示例为了易于理解，使用了比需要更多的语句。通常在使用 `?` 运算符时，我们可以将多个语句结合起来使代码更短，尽管如果你不小心，初看时可能会让人们更难理解。这里是合并语句且不使用不必要变量后的相同程序：

## 示例 6.19 - `simpler_odd_even.cpp`

```cpp
#include <iostream> // 程序将使用键盘和屏幕

using namespace std; // 将使用标准标识符 cin, cout, endl

int main() {
    cout << "Enter a whole number:" << endl;
    int numValue;
    cin >> numValue;

    cout << "That number is " << (numValue % 2 == 0 ? "even" : "odd");

    cout << endl; // 显示 2 行空行

    return 0;
}
```

最后是另一个使用 `?` 运算符的示例，根据几个持有真或假的布尔变量来决定显示哪些字面量值：

## 示例 6.20 - `conditional_rainbow.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本

using namespace std; // 将使用标准标识符 cout, endl

int main() {
    // 设置当前的天气
    bool isRaining = true;
    bool isSunny = true;

    // 根据下雨和阳光同时存在判断是否有彩虹
    bool makeRainbow = isRaining && isSunny;

    // 决定天气情况以及显示什么消息
    cout << (makeRainbow ? "Rainbow!" : "No rainbows.");

    cout << endl;

    return 0;
}
```

## 第 6 章总结：做出决策

以下是本章中涵盖的内容：

- 简单的 `if` 和 `if-else` 决策通过评估表达式为真或假来确定它们应该采取的操作。

- 表达式可以包含 `==`、`!=` 关系运算符。

- 多个 `if-else` 决策可以组合在一起形成涉及两个以上可能结果的嵌套决策。

- 决策可以使用 `&&` AND 运算符测试表达式的所有部分是否为真。

- 决策可以使用 `||` OR 运算符测试表达式的一个或多个部分是否为真。

- `!` 取反运算符可以用于找到表达式或值的相反值。

- 留字 `&&`、`!=` 或 `not` 可以代替 `||`、`!` 符号，使代码更易读。

- 留字 `!=` 可以代替运算符符号。

- `switch-case` 语句可以从许多不同的可能操作中做出决策。它是在代码中使用许多 `if` 语句的替代方案。

- `switch-case` 语句可以包含一个 `default` 情况，当对某个值没有其他匹配时将执行该情况。

- `?` 条件运算符评估表达式以选择返回两个可能值之一。它可以作为 `if-else` 语句的更短替代方案。

# 供你尝试的问题和练习

| | 任务 |
| :--- | :--- |
| 1 | 写一个程序要求你输入形状有多少边。让程序判断这种边数的形状是什么，然后显示形状的名称。例如：“你输入了 3 - 形状是三角形”。 |

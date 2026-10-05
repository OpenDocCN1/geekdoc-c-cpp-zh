

以下显示了列表 5.9 (binaryconversion.cpp) 的示例运行：

```cpp
Please enter an integer value in the range 0...1023: 805
1100100101
```

图 5.3 展示了当用户输入 805 时，列表 5.9 (binaryconversion.cpp) 的执行情况。

![](img/e326304bd50fbc4f7d5a64c1487eb635_100_0.png)

图 5.3：当用户提供 805 作为输入值时，二进制转换程序的过程。

列表 5.10 (simplebinaryconversion.cpp) 以一些额外的运算为代价简化了列表 5.9 (binaryconversion.cpp) 的逻辑。它只使用了一个 `if` 语句。

# 列表 5.10: simplebinaryconversion.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    int value;
    // 从用户处获取数字
    cout << "Please enter an integer value in the range 0...1023: ";
    cin >> value;
    // 整数必须小于 1024
```

## 5.7. 嵌套条件

```cpp
if (0 <= value && value < 1024) {
    cout << value/512;
    value %= 512;
    cout << value/256;
    value %= 256;
    cout << value/128;
    value %= 128;
    cout << value/64;
    value %= 64;
    cout << value/32;
    value %= 32;
    cout << value/16;
    value %= 16;
    cout << value/8;
    value %= 8;
    cout << value/4;
    value /= 4;
    cout << value/2;
    value %= 2;
    cout << value << endl;
}
```

列表 5.10 (simplebinaryconversion.cpp) 中唯一的 `if` 确保用户提供了正确范围内的整数。最初出现在列表 5.9 (binaryconversion.cpp) 中的其他 `if` 语句都消失了。一系列整数算运算取代了原始的条件逻辑。这两个程序——binaryconversion.cpp 和 simplebinaryconversion.cpp——行为完全相同，但 simplebinaryconversion 的逻辑更简单。

列表 5.11 (troubleshoot.cpp) 实现了一个非常简单的故障排除程序，一个（同样简单的）计算机可能会用它来设计一个运行有问题的编译器。

# 列表 5.11: troubleshoot.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Help! My computer doesn't work!" << endl;
    char choice;
    cout << "Does the computer make any sounds "
         << "(fans), or show any lights? (y/n)";
    cin >> choice;
    // 故障排除控制逻辑
    if (choice == 'n') // 电脑没有电
        cout << "Is it plugged in? (y/n)";
        cin >> choice;
        if (choice == 'n') // 没有插电源
            cout << "Plug it in. If the problem persists,"
                 cout << "Please run this program.";
    else // 已插电源
        cout << "Is the switch in \"on\" position? (y/n)";
        cin >> choice;
}
``````cpp
if (choice == 'n') { // 开关是关闭的，打开它！
    cout << "Turn it on. If the problem persists, "
         << "please run this program." << endl;
}
else { // 开关是开启的
    cout << "Does the computer have a fuse?" (y/n);
    cin >> choice;
    if (choice == 'n') { // 没有保险丝
        cout << "Is the outlet OK?" (y/n);
        if (choice == 'n') { // 修复插座
            cout << "Check the outlet's circuit "
                 << "breaker or fuse. Move to a "
                 << "new outlet, if necessary.";
                 << "If the problem persists, "
                 << "please run this program."
        }
    } else { // }}}
        cout << "Check the fuse. Replace if "
             << "necessary. If the problem "
             << "persists, then "
             << "please run this again."
    }
}
else { // 电脑有电
cout << "Please consult a service technician."
```这个简单的故障排除程序尝试诊断计算机无法工作的原因。改进空间是无限的，但版本只处理可以简单修复的电源问题。注意计算机是否有电源（风扇响或指示灯亮），程序引导用户查看其他地方！程序的逻辑决策树见图 5.4。执行的步骤如下：

1. 插电源了吗？这个简单的修复有时会被忽略。
2. 开关在开启位置吗？这是另一个简单的修复。
3. 如果适用，保险丝熔断了吗？（大多数电脑的电源可以承受浪涌且没有用户维护的保险丝。）也许插座的断路器或保险丝有问题。
4. 插座有电吗？程序引导用户先进行简单的修复。随着程序的进行，它逐步引入了更复杂的检查。根据你对运行良好的故障排除程序的经验，你可能对这个简单的程序提出许多改进。

## 5.7. 嵌套条件

![](img/e326304bd50fbc4f7d5a64c1487eb635_103_0.png)

注意列表 5.11 (troubleshoot.cpp) 在许多严格不需要的地方使用了大括号。它们在列表 5.11 (troubleshoot.cpp) 中的包含增加了程序的可读性并使逻辑更容易理解。即使你不遵循使用 `if/else` 体的哲学，在提高代码可读性的情况下使用它是很好的主意。

回想列表 4.11 (timeconv.cpp) 中的时间转换程序。如果用户输入 10000，程序运行：

```text
Please enter the number of seconds:10000
2 hours 46 minutes 40 seconds
```

如果用户输入 9961，程序输出：

```text
Please enter the number of seconds:9961
2 hours 46 minutes 1 second
```

假设我们希望通过不使用缩写来改进英语表达。如果我们写出小时、分钟和秒，当值为 1 时，我们必须小心使用单数形式 hour、minute 或 second。列表 5.12 (timeconvcond.cpp) 使用 `if/else` 语句用正确的数字表示时间单位。

# 列表 5.12: timeconvcond1.cpp

```cpp
// File timeconvcond1.cpp
#include <iostream>
using namespace std;
int main() {
    // 一些转换常量
    const int SECONDS_PER_MINUTE = 60;
    const int SECONDS_PER_HOUR = 60*SECONDS_PER_MINUTE; // 3600
    int hours, minutes, seconds;
    cout << "Please enter the number of seconds:";
    cin >> seconds;
    // 首先，计算给定秒数中的小时
    hours = seconds / SECONDS_PER_HOUR;
    // 计算剩余的秒数
    seconds = seconds % SECONDS_PER_HOUR;
    // 然后，计算剩余秒数中的分钟
    minutes = seconds / SECONDS_PER_MINUTE;
    // 计算考虑分钟后的剩余秒数
    seconds = seconds % SECONDS_PER_MINUTE;
    // 报告结果
    cout << hours;
    // 小小时的单数和复数
    if (hours == 1)
        cout << " hour";
    else
        cout << " hours";
    // 分钟的单数和复数
    if (minutes == 1)
        cout << " minute";
    else
        cout << " minutes";
    // 秒的单数和复数
    if (seconds == 1)
        cout << " second";
    else
        cout << " seconds";
}
```

列表 5.12 (timeconvcond1.cpp) 中的 `if/else` 语句负责为每个单位打印正确的版本——单数或复数。其中一个运行输出为：

```text
Please enter the number of seconds:10000
2 hours 46 minutes 40 seconds
```

所有的词都是复数。另一个运行输出为：

```text
Please enter the number of seconds:9961
2 hours 46 minutes 1 second
```

注意 *second* 是单数，正如应该是的样。

```text
Please enter the number of seconds:3601
1 hour 0 minutes 1 second
```

这里打印的词与它们代表的数字一致。

列表 5.12 (timeconvcond1.cpp) 的改进方法是在值为 0 时不打印数值及其关联的时间单位。列表 5.13 (timeconv2.cpp) 增加了这个功能。

# 列表 5.13: timeconv2.cpp

```cpp
// File timecond1.cpp
#include <iostream>

using namespace std;

int main() {
    // 一些实用的转换常量
    const int SECONDS_PER_MINUTE = 60,
           SECONDS_PER_HOUR = 60*SECONDS_PER_MINUTE; // 3600
    int hours, minutes, seconds;
    cout << "Please enter the number of seconds:";
    cin >> seconds;
    // 首先，计算给定秒数中的小时
    hours = seconds / SECONDS_PER_HOUR;
    // 计算剩余的秒数
    seconds = seconds % SECONDS_PER_HOUR;
    // 然后，计算剩余秒数中的分钟
    minutes = seconds / SECONDS_PER_MINUTE;
    // 计算考虑分钟后的剩余秒数
    seconds = seconds % SECONDS_PER_MINUTE;
    // 报告结果
    if (hours > 0) { // 打印小时？
        cout << hours;
        // 小小时的单数和复数
        if (hours == 1)
            cout << " hour";
        else
            cout << " hours";
    }
    if (minutes > 0) {
        cout << minutes;
        // 分钟的单数和复数
        if (minutes == 1)
            cout << " minute";
        else
            cout << " minutes";
    }
    if (seconds > 0) {
        cout << seconds;
        // 秒的单数和复数
        if (seconds == 1)
            cout << " second";
        else
            cout << " seconds";
    }
}
```
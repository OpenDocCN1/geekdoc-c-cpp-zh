

## 4.6. 错误 << 警告

```cpp
cout << n << endl;
)
```

尝试编译列表 4.8 (uninitialized.cpp) 时，Visual C++ 编译器输出了以下信息：

> warning C4700: 使用未初始本地变量 'n'

编译器发布了警告，但仍然生成了可执行文件。运行时，程序会产生随机结果，因为它打印了与变量关联的内存中的值，但程序并没有初始化该内存位置。

列表 4.9 (narrow.cpp) 将一个 `double` 类型的值赋给 `int` 变量，我们从第 4.1 节知道这会导致结果被截断。

列表 4.9: narrow.cpp
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    double d = 1.6;
    n = d;
    cout << n << endl;
}
```

编译时我们看到：

> warning C4244: '=': 从 'double' 转换到 'int', 可能会丢失数据

由于这是警告而非错误，编译器生成了可执行文件，但该警告应该提示我们停下来反思代码的正确性。增强的警告级别防止程序员忽视这种情况。

在 IDE 中编译时，Visual++ 的默认警告级别为 3，在命令行中为级别 1（这就是为什么我们在命令行中使用 `/W3` 选项）；最高警告级别为 4。你可以将警告级别降低到 1 或 2，但并不建议这样做。你可能想要降低等级的唯一理由是处理不符合 C++ 标准的旧 C++ 源代码。在开发新代码时，倾向于使用更高的警告级别以便在开发的各个阶段为程序员提供更多帮助。书中的示例在 Visual++ 级别 3 下可以良好编译。级别 3 有助于检测常见的逻辑错误。

我们可以通过在代码中添加一个简单的加法来避免大多数警告。第 4.2 节展示了我们如何使用 `static_cast` 将宽类型强制转换为窄类型。在 Visual 警告级别 3 下，如果不使用强制类型转换，编译器会发出警告。添加的这部分代码会让程序员停下来并反思该结构的正确性。增强的警告级别防止程序员忽视这种情况。

## 4.7. 算术示例

> 使用你的编译器可用的最高级别警告。将所有警告视为必须修正的问题。不要接受带有警告通过编译的程序视为已完成。

## 4.7 算术示例

在复杂表达式中执行的算术运算是根据运算符逐个决定的。例如，考虑列表 4.10 tempcomp.cpp，它尝试公式将华氏度温度转换为摄氏度：

$C = \frac{5}{9} \times (F - 32)$

列表 4.10: tempcomp.cpp
```cpp
// File tempcomp.cpp

#include <iostream>

using namespace std;

int main() {
    double degreesF, degreesC;
    // 提示需要转换的温度
    cout << "Enter the temperature in degrees F: ";
    // 读取用户输入
    cin >> degreesF;
    // 执行转换
    degreesC = 5/9 * (degreesF - 32);
    // 报告结果
    cout << degreesC << endl;
}
```

列表 4.10 (tempcomp.cpp) 包含了每一步代码目的的注释。初始测试看起来是有前景的：

```
Enter the temperature in degrees F: 32
Degrees C = 0
```

水在 32 华氏度和 0 摄氏度结冰，因此程序在该测试中的行为是正确的。其他尝试并不理想——考虑：

```
Enter the temperature in degrees F: 212
Degrees C = 0
```

水在 212 华氏度沸腾，即 100 摄氏度，所以这个答案是不正确的。

```
Enter the temperature in degrees F: -40
Degrees C = 0
```

值 –40 并不是华氏度和摄氏度曲线的交叉点，因此结果应该是 –40 而不是零。第一次测试仅仅是巧合正确。

遗憾的是，无论输入是什么，打印的结果总是相同的。问题在于语句中的 `5/9` 除法：

```cpp
degreeC = 5/9*(degreeF - 32);
```

除法和乘法的优先级相同，且它们都满足结合律：因此，先执行除法。如果两个操作数都是整数，则执行整数除法且商为零（5 除以 9 等于 0，余 5）。因此，零乘以任何数都是零。表达式中涉及浮点值（degreeF）以及最终结果赋值给浮点变量是无关的。关于执行精确操作类型的决定是基于运算符逐一的，而不是全局应用于整个表达式。由于除法先执行且它涉及两个整数，因此在其他浮点部分参与之前，使用的是整数除法。

一个简单的解决方案是在 9 上使用浮点字面量，或者像我们这样：

```cpp
degreeC = 5.0/9*(degreeF - 32);
```

这强制执行了双精度浮点除法（记得 5.0 是一个 double）。最终计算出了正确的结果（受舍入影响而非截断影响）。列表 4.11: timeconv.cpp 使用整数除法和模运算将秒数秒数拆分为小时、分钟。

列表 4.11: timeconv.cpp
```cpp
// File timeconv.cpp

#include <iostream>

using namespace std;

int main() {
    int hours, minutes, seconds;
    // 提示需要转换的温度
    cout << "Enter the temperature in degrees F: ";
    // 读取用户输入
    cin >> seconds;
    // 首先，计算给定秒数的小时
    hours = seconds / 3600;
    // 计算小时后的剩余秒数
    seconds = seconds % 3600;
    // 然后，计算剩余秒数中的分钟
    minutes = seconds / 60;
    // 报告结果
    cout << hours << " hr, " << minutes << " min, " << seconds << endl;
}
```

```
// 计算分钟后的剩余秒数
seconds = seconds % 60;
cout << hours << " hr, " << minutes << " min, " << seconds << endl;
```

如果用户输入 1000，程序输出 46 分钟。注意赋值运算符 (=) 的右侧先计算。秒除以 3600 的余数赋值回秒。如果当前值大于 3600，该语句会改变秒的值。

```
x = x + 1;
```

该语句增加 x 的值使其更大。程序中经常出现的类似语句进一步证明 C++ 赋值运算符并不意味着数学。在 C++ 中，此语句仅意味着“将 x 加一并将结果赋值回 x”。

4.11 (timeconv.cpp) 的变体。列表 4.12 (enhancedtimeconv.cpp) 执行了一些算术逻辑以产生略有不同的输出——与其将 11045 秒打印为 3 小 4 分 5 秒，列表 4.12 (enhancedtimeconv.cpp) 将其显示为 3:04:05。修改 4.11 (timeconv.cpp) 以打印 3:4:5 是必要的，列表 4.12 (enhancedtimeconv.cpp) 为单数字分钟和秒增加了前导零，正如数字钟显示所示。

# Listing 4.12: enhancedtimeconv.cpp
```cpp
// File enhancedtimeconv.cpp

#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int hours, minutes, seconds;
    cout << "enter the number of seconds:";
    cin >> seconds;
    // 首先，计算给定秒数的小时
    hours = seconds / 3600;
    // 计算小时后的剩余秒数
    seconds = seconds % 3600;
    // 然后，计算剩余秒数中的分钟
    minutes = seconds / 60;
    // 输出带有前导零的输出
    cout << hours << ":" << setfill('0') << setw(2) << minutes << ":" 
         << setfill('0') << setw(2) << seconds << endl;
}
```

©2024 Richard L. Halman

日期 date: January 26, 2014


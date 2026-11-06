

```cpp
int n = str.length();
for (int i = 0; i < n + 2; i++) { cout << "-"; }
cout << endl;
cout << "|" << str << "|" << endl;
for (int i = 0; i < n + 2; i++) { cout << "-"; }
cout << endl;
}
```

请注意，此函数不计算任何值。它执行一些操作，然后返回调用方。（请参阅示例程序 `ch05/box.cpp`。）

由于没有返回值，因此不能在表达式中使用 `box_string`。你可以调用

```cpp
box_string("Hello");
```

但不能这样调用：

```cpp
result = box_string("Hello"); // Error: box_string doesn't return a result.
```

如果希望在到达函数末尾之前从 `void` 函数返回，可以使用不带值的 `return` 语句。例如：

```cpp
void box_string(string str)
{
    int n = str.length();
    if (n == 0)
    {
        return; // Return immediately
    }
    ...
}
```

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_234_0.png)

- 13. 使用 `box_string` 函数，如何生成下面的输出？

```
------
!Hello!
------
```

- 14. 下面的语句有什么问题？

```cpp
cout << box_string("Hello");
```

- 15. 实现一个 `shout` 函数，打印由一个字符串后跟三个感叹号组成的一行。例如，`shout("Hello")` 应打印 `Hello!!!`。该函数不应返回值。

- 16. 应如何修改 `box_string` 函数，使字符串两侧各留一个空格，如下所示：

```
--------
! Hello !
--------
```

- 17. `box_string` 函数包含两次打印由 `-` 字符组成的行的代码。请将这段代码放入一个单独的函数 `print_line` 中，并使用该函数简化 `box_string`。这两个函数的代码是什么？

**练习** 现在可以尝试本章末尾的练习：R5.4、P5.24。

- 20. 考虑下面的函数。它计算初始余额为 10,000 美元、利率为 5% 的账户的复利：

```cpp
double balance(int years) { return 10000 * pow(1.05, years); }
```

- 21. 注释解释了下面循环的功能。请改用函数实现。

```cpp
// Counts the number of spaces
int spaces = 0;
for (int i = 0; i < input.length(); i++)
{
    if (input.substr(i, 1) == " ") { spaces++; }
}
```

- 22. 在自测题 21 中，要求你实现一个统计空格数量的函数。如何将其泛化，使它能够统计任意字符？为什么需要这样做？

**练习** 现在可以尝试本章末尾的练习：R5.7、P5.23。

## 5.7 问题求解：逐步细化

> 使用逐步细化的过程，将复杂任务分解为更简单的任务。

问题求解最强大的策略之一就是**逐步细化**。要解决一个困难的任务，先将它分解为更简单的任务。然后继续将这些简单任务分解为更简单的任务，直到剩下的都是你知道如何解决的任务。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_237_0.png)

下面是将这一过程应用于日常生活问题的一个例子。早上起床后，你只是必须**喝到咖啡**。如何喝到咖啡？你可以看看能否让别人，比如你的母亲或伴侣，给你带一杯。如果做不到，你就必须**冲咖啡**。如何冲咖啡？如果有速溶咖啡，可以**冲泡速溶咖啡**。如何冲泡速溶咖啡？只需**烧开水**，然后将开水与速溶咖啡混合即可。如何烧开水？如果有微波炉，就在杯子里装满水，把杯子放入微波炉中加热三分钟。否则，就在水壶里装满水，把水壶放在炉子上加热，直到水沸腾。另一方面，如果没有速溶咖啡，就必须**煮咖啡**。如何煮咖啡？向咖啡机中加水，放入滤纸，**研磨咖啡**，将咖啡放入滤纸，然后打开咖啡机。如何研磨咖啡？将咖啡豆放入咖啡研磨机，然后按下按钮 60 秒。

图 5 展示了制作咖啡解决方案的流程图视图。细化过程以展开的方框表示。在 C++ 中，可以将细化实现为函数。例如，函数 `brew_coffee` 会调用 `grind_coffee`，而它会由函数 `make_coffee` 调用。

让我们将逐步细化的过程应用于一个编程问题。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_238_0.png)

**图 5** 制作咖啡解决方案的流程图

填写支票时，通常会同时用数字（“274.15 美元”）和文字字符串（“两百七十四美元零 15 美分”）写出支票金额。这样可以减少收款人在金额前面添加几个数字的诱惑。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_238_1.png)

对于人类来说，这并不特别困难，但计算机如何完成这件事呢？没有内置函数可以将 274 转换为 “two hundred seventy four”。我们需要编写这个函数。下面是我们想要编写的函数的描述：

```c
/**
 * Turns a number into its English name.
 * @param number a positive integer < 1,000
 * @return the name of number (e.g., "two hundred seventy four")
 */
string int_name(int number)
```

如果（`part > 0`），则将 `digit_name(part)` 附加到 `name`。

与文字描述相比，这段伪代码有许多重要的改进。它展示了如何安排测试，从与较大数字的比较开始，并展示了之后如何在更多的 `if` 语句中继续处理较小的数字。

另一方面，这段伪代码对各部分的实际转换描述得比较模糊，只是提到了“几百的名称”等。此外，我们没有明确说明空格。按当前形式，代码会生成没有空格的字符串，例如 `twothousandseventyfour`。与主要问题的复杂性相比，人们希望空格只是一个小问题。最好不要让这些细节干扰伪代码。

现在将伪代码转换为实际代码。最后三种情况很简单，因为已经为它们开发好了辅助函数：

```cpp
if (part >= 20)
{
    name = name + " " + tens_name(part);
    part = part % 10;
}
else if (part >= 10)
{
    name = name + " " + teen_name(part);
    part = 0;
}

if (part > 0)
{
    name = name + " " + digit_name(part);
}
```

最后，让我们处理 100 到 999 之间的数字。由于 `part < 1000`，`part / 100` 是一个个位数，我们可以通过调用 `digit_name` 获取它的名称。然后添加 “hundred” 后缀：

```cpp
if (part >= 100)
{
    name = digit_name(part / 100) + " hundred";
    part = part % 100;
}
```

现在，你已经了解了 `int_name` 函数的所有重要构建模块。下面是完整的程序：

### ch05/intname.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;

/**
   Turns a digit into its English name.
   @param digit an integer between 1 and 9
   @return the name of digit ("one" ... "nine")
*/
string digit_name(int digit)
{
if (digit == 1) return "one";
if (digit == 2) return "two";
if (digit == 3) return "three";
if (digit == 4) return "four";
if (digit == 5) return "five";
if (digit == 6) return "six";
if (digit == 7) return "seven";
if (digit == 8) return "eight";
if (digit == 9) return "nine";
return "";
}

/**
 * Turns a number between 10 and 19 into its English name.
 * @param number an integer between 10 and 19
 * @return the name of the given number ("ten" ... "nineteen")
 */
string teen_name(int number)
{
   if (number == 10) return "ten";
   if (number == 11) return "eleven";
   if (number == 12) return "twelve";
   if (number == 13) return "thirteen";
   if (number == 14) return "fourteen";
   if (number == 15) return "fifteen";
   if (number == 16) return "sixteen";
   if (number == 17) return "seventeen";
   if (number == 18) return "eighteen";
   if (number == 19) return "nineteen";
   return "";
}

/**
 * Gives the name of the tens part of a number between 20 and 99.
 * @param number an integer between 20 and 99
 * @return the name of the tens part of the number ("twenty" ... "ninety")
 */
string tens_name(int number)
{
   if (number >= 90) return "ninety";
   if (number >= 80) return "eighty";
   if (number >= 70) return "seventy";
   if (number >= 60) return "sixty";
   if (number >= 50) return "fifty";
   if (number >= 40) return "forty";
   if (number >= 30) return "thirty";
   if (number >= 20) return "twenty";
   return "";
}

/**
 * Turns a number into its English name.
 * @param number a positive integer < 1,000
 * @return the name of the number (e.g. "two hundred seventy four")
 */
string int_name(int number)
{
   int part = number; // The part that still needs to be converted
   string name; // The return value
```



```java
****************************************************************
// BoxesPanel.java      作者: Lewis/Loftus
// 演示了使用条件判断和循环来引导绘制。
****************************************************************

import javax.swing.JPanel;
import java.awt.*;
import java.util.Random;
```

# 列表 6.8 续

```java
public class BoxesPanel extends JPanel {
    private final int NUM_BOXES = 50, THICKNESS = 5, MAX_SIDE = 50;
    private final int MAX_X = 350, MAX_Y = 250;
    private Random generator;

    //
    // 设置绘制面板。
    //
    public BoxesPanel() {
        generator = new Random();

        setBackground(Color.black);
        setPreferredSize(new Dimension(400, 300));
    }

    //
    // 在随机位置绘制随机宽度和高度的矩形。
    // 窄或短的矩形用填充颜色高亮。
    public void paintComponent(Graphics page) {
        super.paintComponent(page);

        int x, y, width, height;

        for (int count = 0; count < NUM_BOXES; count++) {
            x = generator.nextInt(MAX_X) + 1;
            y = generator.nextInt(MAX_Y) + 1;

            width = generator.nextInt(MAX_SIDE) + 1;
            height = generator.nextInt(MAX_SIDE) + 1;

            if (width <= THICKNESS) // 检查是否为窄矩形 {
                page.setColor(Color.yellow);
                page.fillRect(x, y, width, height);
            }
            if (height <= THICKNESS) // 检查是否为短矩形 {
                page.setColor(Color.green);
                page.fillRect(x, y, width, height);
            } else
            {
                page.setColor(Color.white);
                page.drawRect(x, y, width, height);
            }
        }
    }
}
```

## 6.6 对话框

# 列表 6.8 续

一个名为对话框的组件对于辅助 GUI 处理非常有帮助。对话框是一个弹出任何当前活动窗口之上的图形窗口，用户可以对其进行交互。对话框可以有多种用途，例如传递某些信息、确认操作，或让用户输入某些信息。通常，对话框只有一个目的，用户与其交互的时间是短暂的。

Java 类库的 Swing 包包含一个名为 `JOptionPane` 的类，它简化了对话框的创建和使用。6.3 列出了 `JOptionPane` 的一些方法。

> 核心概念
>
> 对话框是一个弹出窗口，允许简短、特定的用户交互以提供信息或验证操作。

```java
static String showInputDialog(Object msg)
显示一个包含指定消息和输入文本框的对话框。返回文本框的内容。
static int showConfirmDialog(Component parent, Object msg)
显示一个包含指定消息和 是/否 按钮选项的对话框。如果父组件为 null，则框将在屏幕上居中。
static void showMessageDialog(Component parent, Object msg)
显示一个包含指定消息的对话框。如果父组件为 null，则框将在屏幕上居中。
```

# 图 6.3' 类的一些方法

## 第 6 章 更多条件和循环

`JOptionPane` 对话框的基本格式分为三类。消息对话框仅显示一个输出字符串。输入对话框提供一个提示和一个单一输入文本框，用户可以在其中输入一个数据字符串。确认对话框向用户提出一个简单的“是”或“否”的问题。

让我们来看使用这些类型对话框的程序。列表 6.9 显示了一个程序，该程序首先向用户显示一个输入对话框，要求用户输入一个整数。在用户点击输入对话框上的 OK 按钮后，会出现第二个对话框（这次是消息对话框），告知用户输入的数字是偶数还是奇数。在用户关闭此框后，会出现第三个对话框，确定用户是否想测试另一个数字。如果用户点击标记为“是”的按钮，则系列对话框将重复。否则，程序终止。

# 列表 6.9

```java
********************************************************************
// EvenOdd.java         作者: Lewis/Loftus
// 演示了 JOptionPane 类的使用。
********************************************************************

import javax.swing.JOptionPane;

public class EvenOdd {
    
    // 确定输入的值是偶数还是奇数。
    // 使用多个对话框。

    public static void main(String[] args) {
        String numStr, result;
        int num, again;

        do {
            numStr = JOptionPane.showInputDialog("输入整数：");
            num = Integer.parseInt(numStr);

            result = "数字是" + (num % 2 == 0 ? "偶数" : "奇数");

            JOptionPane.showMessageDialog(null, result);
            again = JOptionPane.showConfirmDialog(null, "再次测试?");
        } while (again == JOptionPane.YES_OPTION);
    }
}
```

## 6.6 对话框

# 列表 6.9 续

```java
}
```

## 6.6 对话框

93

img/7f8e069c1898b741edc17dfeed34b0c1_316_0.png)

`JOptionPane` 对话框的基本格式分为三类。消息对话框仅显示一个输出字符串。输入对话框提供一个提示和一个单一输入文本框，用户可以在其中输入一个数据字符串。确认对话框向用户提出一个简单的“是”或“否”的问题。

`showInputDialog` 和 `showConfirmDialog` 方法允许创建许多对话框。`showMessageDialog` 方法可以让框在屏幕上居中。

## 概念总结

- `switch` 语句匹配字符或整数。
- `break` 语句通常用于末尾。
- 条件运算符求值为布尔值。
- `do` 语句至少执行一次。
- `for` 语句用于当你需要执行固定次数时。
- `for-each` 版本简化了对所有元素的处理。
- 循环语句功能上是等价的。
- 对话框是一个弹出窗口，允许简短、特定的用户交互以提供信息或验证操作。

## 练习

EX 6.1 以下代码的输出是什么？

```java
for (int num = 0; num < 20; num++)
    System.out.println(num);
```

EX 6.2 以下代码的输出是什么？

```java
for (int val = 20; val >= 0; val--)
    if (val % 4 == 0)
    System.out.println(val);
```

EX 6.3 将下面的 `while` 循环转换为等价的 `do` 循环。

```java
int num = 1;
while (num < 20)
{
    num++;
    System.out.println(num);
}
```

EX 6.4 将上一个练习中的 `while` 循环转换为等价的 `for` 循环。

EX 6.5 写一个 `do` 循环让用户输入整数值。

EX 6.6 写一个 `for` 循环打印从 1 到 99（包含边界）的奇数。

EX 6.7 写一个 `for` 循环打印从 30 到 3 的 3 的倍数。

EX 6.8 写一个代码片段从用户处读取 10 个整数并打印最大值。

EX 6.9 写一个代码片段定义并打印字符 'a' 在字符串对象 `name` 中出现的次数。

EX 6.10 写一个代码片段反向打印存储在 `str` 中的字符。

EX 6.11 写一个代码片段从第一个字符开始打印字符串对象 `word` 中的每一个字符。

EX 6.12 写一个名为 `powersTwo` 的方法，打印前 10 个 2 的幂（从 2 开始）。该方法不接受参数也不返回值。

EX 6.13 写一个名为 `alarm` 的方法，多行打印字符串 "Alarm!"。该方法接受一个整数参数，指定打印字符串的次数。如果参数小于 1，打印错误消息。

EX 6.14 写一个名为 `sum100` 的方法，返回从 1 到 100（包含）的整数和。

EX 6.15 写一个名为 `sumRange` 的方法，接受两个表示范围的整数。如果第二个参数小于第一个参数，发出错误消息并返回 0。否则，该方法返回该范围内整数的和（包含）。

EX 6.16 写一个名为 `countA` 的方法，接受一个字符串参数并返回字符串中字符 'A' 出现的次数。

## 编程项目

访问 `www.myprogramminglab.com` 在线完成许多编程项目并获取即时反馈。

- **PP 6.1** 设计并实现一个应用程序，读取一个整数值，并打印从 2 到输入值之间（包含边界）所有偶整数的和。如果输入值小于 2，则打印错误信息。进行相应的提示。
- **PP 6.2** 设计并实现一个应用程序，从用户处读取一个字符串，并每行打印一个字符。
- **PP 6.3** 设计并实现一个应用程序，生成一个乘法表，显示整数 1 到 12 与其自身相乘的结果。
- **PP 6.4** 设计并实现一个应用程序，打印旅行歌曲“百瓶啤酒”（One Hundred Bottles of Beer）的前几段。使用循环使每次迭代打印一段。从用户处读取要打印的歌段数，并对输入进行验证。以下是歌曲的前两段：

100 bottles of beer on the wall

100 bottles of beer

If of those bottles should happen to fall

99 bottles of beer on the wall

99 bottles of beer on the wall

99 bottles of beer

If of those bottles should happen to fall

98 bottles of beer on the wall
- **PP 6.5** 使用 PP 4.7 中的 `Pair` 类，设计并实现一个应用程序，掷一对骰子 1000 次，统计出现点数（两个六）的次数。
- **PP 6.6** 使用本章定义的 `Coin` 类，设计并实现一个驱动类 `CountFlips`，其 `main` 方法抛掷硬币 100 次，并统计每一面出现的次数。打印结果。
- **PP 6.7** 创建 Stars 程序的修改版本以打印以下模式。为每个模式创建一个独立的程序。*提示：*部分 b、c 和 d 需要多个循环，其中一些循环需要打印特定数量的空格。

![](img/7f8e069c1898b741edc17dfeed34b0c1_323_0.png)

![](img/7f8e069c1898b741edc17dfeed34b0c1_323_1.png)

VideoNote

开发 PP 6.2 的解决方案

a. ****** b. * c. ****** d. *

********** ****** ********** ****

********** ****** **********

********** ****** **********

********** ****** **********

*** ********** ****

*** *** ********** ****

**********

**********

** **

- **PP 6.8** 设计并实现一个应用程序，打印显示 Unicode 字符子及其数值的表格。每行打印五个数字/字符对，用制表符分隔。打印数值从 32（空格字符）到 126（~ 字符）的表格，这对应于 Unicode 字符集中可打印的 ASCII 子。将你的输出与附录 C 中的表格进行比较。表格中的数值随着行的移动增加。
- **PP 6.9** 设计并实现一个应用程序，从用户处读取一个字符串，然后确定整个字符串中每个小写元音（a, e, i, o 和 u）出现的次数。为每个元音设置单独的计数器。同时统计并打印非元音字符的数量。
- **PP 6.10** 设计并实现一个应用程序，打印歌曲“圣诞节十二天”（The Twelve Days of Christmas）的歌段，每段增加一行。你歌曲歌曲的前两段为：

- On the 1st day of Christmas my true love gave to me
- A Partridge in a pear tree.
- On the 2nd day of Christmas my true love gave to me
- Two turtle doves, and
- A Partridge in a pear tree.

在循环中使用 `switch` 语句来控制打印哪些行。提示：仔细安排 case 的顺序并避免使用 `break` 语句。使用单独的 `switch` 语句为日期数字添加适当的后缀（1st, 2nd, 3rd，等）。歌曲的最后一段涉及所有 12 天，如下：

On the 12th day of Christmas, my true love gave to me

Twelve drummers drumming,

Eleven pipers piping,

Ten lords a-leaping,

Nine ladies dancing,

Eight maids a-milking,

Seven swans a-swimming,

Six geese a-laying,

Five golden rings,

Four calling birds,

Three French hens,

Two turtle doves, and

A Partridge in a pear tree.
- **PP 6.11** 设计并实现一个绘制等间距平行线的程序。
- **PP 6.12** 设计并实现一个绘制侧视图的程序。
- **PP 6.13** 设计并实现一个绘制 100 个随机直径圆的程序。
- **PP 6.14** 设计并实现一个绘制随机图形的程序。
- **PP 6.15** 设计并实现一个绘制砖墙的程序。
- **PP 6.16** 设计并实现一个绘制网格的程序。
- **PP 6.17** 使用名为 `Pattern` 的独立类设计并实现一个被子。
- **PP 6.18** 设计并实现一个绘制简单围栏的程序。
- **PP 6.19** 设计并实现一个绘制彩虹的程序。
- **PP 6.20** 设计并实现一个在随机位置绘制 20,000 个点的程序。
- **PP 6.21** 设计并实现一个绘制 10 个随机半径圆的程序。
- **PP 6.22** 设计并实现一个使用对话框获取两个值的应用程序。
- **PP 6.23** 重新设计实现 `PalindromeTester` 的版本，使其使用对话框。
- **PP 6.24** 设计并实现一个名为 `Card` 的类，表示标准扑牌。创建一个分发五张随机牌的程序。

## 7.1 软件开发活动

创建软件不仅仅是编写代码。随着你所解决的问题变得越来越大，解决方案包含的类也越来越多，仔细思索软件的设计变得至关重要。任何适当的开发工作都由四项基本的开发活动组成：

- 建立需求
- 创建设计
- 实现设计
- 测试

如果这些活动能够按照这种顺序定义一种开发软件的步进式方法，那就太好了。然而，尽管它们可能是顺序的，但在现实中它们几乎从不是完全线性的。它们是重叠并相互作用的。让我们简要讨论每项开发活动。

软件需求规定了程序必须完成的内容。它们指示了程序应该执行的任务以及它执行这些任务的方式。通常，需求会在称为功能规格说明书的文档中表示。

我们在第1章中讨论过，基本前提其实是关于解决问题的；我们创建一个程序来解决特定问题。需求是对该问题的清晰表达。在我们真正知道正在试图解决什么问题之前，我们无法准确地解决它。

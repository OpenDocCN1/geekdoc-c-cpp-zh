
我从不花钱参加任何比赛。所有这些奖金都是白得的。当全国计算机科学教育者大会在内华达州雷诺市召开时，我的同事们说服我去试试老虎机。我输了23美元，然后又赢回了18美元。就在那时，我停止了游戏。我想在只落后5美元时就退出。

正因如此，我写一个关于老虎机的 Java 程序才显得如此奇怪。典型的老虎机有三个转轮，每个转轮大约有20个符号。但为了说明本节的思路，我不需要20个符号。相反，我使用四个符号——樱桃、柠檬、金桔和萝卜菜。

## 创建增强的 for 循环

当你玩我的简化版老虎机时，你可以旋转超过60种组合中的任意一种——樱桃+樱桃+金桔、萝卜菜+萝卜菜+萝卜菜，或其他任何组合。本章的目标是列出所有可能的组合。但首先，我向你展示另一种循环。清单15-5为老虎机的符号定义了一个枚举类型并显示符号列表。（有关枚举类型的介绍，请参阅第10章。）

## 清单 15-5：老虎机符号

```java
import static java.lang.System.out;

class ListSymbols {
    enum Symbol {
        cherry, lemon, kumquat, rutabaga
    }
    public static void main(String args[]) {
        for (Symbol leftReel : Symbol.values()) {
            out.println(leftReel);
        }
    }
}
```

清单15-5使用了Java的增强for循环。单词“enhanced”意为“与Java早期版本的循环相比有所增强”。增强for循环是在Java 5.0版本中引入的。如果你运行的是Java 1.4.2（或类似版本），就不能使用增强for循环。

以下是增强for循环的格式：

```java
for (TypeName variableName : RangeOfValues) {
    Statements
}
```

以下是清单15-5中的循环如何遵循该格式：

### 在清单15-5中，单词 Symbol 是一个类型的名称。

int 类型描述像 -1、0、1 和 2 这样的值。boolean 类型描述 true 和 false 值。而（由于清单15-5中的代码）Symbol 类型描述 cherry、lemon、kumquat 和 rutabaga 值。有关像 Symbol 这样的枚举类型的更多信息，请参阅第10章。

### 在清单15-5中，单词 leftReel 是一个变量的名称。

清单15-1中的循环将 count 定义为 int 变量。类似地，清单15-5中的循环将 leftReel 定义为 Symbol 变量。因此理论上，变量 leftReel 可以取四个 Symbol 值中的任意一个。

顺便说一下，我把这个变量称为 leftReel，因为代码列出了所有可能出现在老虎机三个转轮最左侧的符号。因为老虎机的三个转轮都有相同的符号，我也可能把这个变量命名为 middleReel 或 rightReel。但再想想，我会把 middleReel 和 rightReel 这两个名字留给后面的例子。

### 在清单15-5中，表达式 Symbol.values() 代表清单15-5中的四个值。

引用我前一条要点中的话，“理论上，变量 leftReel 可以取四个 Symbol 值中的任意一个。”好吧，for 语句的 RangeOfValues 部分将理论变成了实践。括号内的第三项说：“要有与 Symbol 值数量一样多的循环迭代，并在每次循环迭代期间让 leftReel 变量取一个不同的 Symbol 值。”

因此，清单15-5中的循环经历四次迭代——一次 leftReel 的值为 cherry，另一次 leftReel 的值为 lemon，第三次 leftReel 的值为 kumquat，第四次 leftReel 的值为 rutabaga。在每次迭代期间，程序打印 leftReel 变量的值。结果见图15-8。

图 15-8:
清单15-5中代码的输出。

![](img/bf4858233d2b2a32ff4e3991860526b3_317_0.png)

图 15-9:
清单15-6代码输出的几行

![](img/bf4858233d2b2a32ff4e3991860526b3_319_0.png)

与清单15-3中的代码类似，清单15-6中的程序包含一个循环套在另一个循环中。事实上，清单15-6有一个循环套在循环中再套在循环中。清单15-6的策略如下：

```
for (each of the 4 symbols that
    can appear on the left reel),
    for (each of the 4 symbols that
        can appear on the middle reel),
        for (each of the 4 symbols that
            can appear on the right reel),
            display the three reels' symbols.
```

你从樱桃符号开始外层循环。然后你进入中间循环，并以樱桃符号开始该循环。然后你进入内层循环并选择樱桃（双关语）。最后，在每个循环都调到樱桃设置时，你显示樱桃樱桃樱桃组合。（见图15-10。）

图 15-10:
首次进入清单15-6程序中的循环。

![](img/bf4858233d2b2a32ff4e3991860526b3_320_0.png)

显示樱桃樱桃樱桃之后，你继续使用最内层循环的其他值。也就是说，你将右转轮的值从樱桃改为柠檬。（见图15-11。）现在三个转轮的值为樱桃樱桃柠檬，所以你在屏幕上显示这些值。

图 15-11:
在最内层循环中从樱桃改为柠檬。

![](img/bf4858233d2b2a32ff4e3991860526b3_320_1.png)

在用尽最内层（右转轮）循环的四个值后，你跳出该最内层循环。但这次跳转会让你回到中间循环的顶部，在那里你将 middleReel 的值从樱桃改为柠檬。现在 leftReel 和 middleReel 的值分别为樱桃和柠檬。（见图15-12。）

## 图 15-14:
第二次遍历最内层循环。

```
for (each of the 4 symbols that
can appear on the left reel),
    cherry
    ↓
for (each of the 4 symbols that
can appear on the middle reel),
    cherry
    lemon
    ↓
for (each of the 4 symbols that
can appear on the right reel),
    cherry
    lemon

display the three reels' symbols.
```

循环一直进行下去，直到显示全部64种组合。呼！

## 在本部分……

- 同时处理多个项目
- 将工作分成可管理的部分
- 创建窗口和其他漂亮的东西

## 第16章

## 使用循环和数组

## 本章内容

- 充分使用 for 循环
- 在单个变量中存储多个值
- 处理一组值

本章有十幅插图。对于这些插图，Wiley Publishing 的人们坚持使用以下编号：Figure 16-1、Figure 16-2、Figure 16-3、Figure 16-4、Figure 16-5、Figure 16-6、Figure 16-7、Figure 16-8、Figure 16-9 和 Figure 16-10。但我喜欢另一种编号方式。我想把插图编号为 `figure[0]`、`figure[1]`、`figure[2]`、`figure[3]`、`figure[4]`、`figure[5]`、`figure[6]`、`figure[7]`、`figure[8]` 和 `figure[9]`。在本章中，你会明白为什么。

## 一些循环的实际应用

Java Motel 有十间舒适的房间，坐落在主干道旁的僻静之处。除了一个小而独立的办公室外，汽车旅馆只是一排长长的底层房间。每个房间都可从宽敞的前停车场轻松到达。

有趣的是，汽车旅馆的房间编号为0到9。我可以说这种编号是偶然的——与建筑师的原始设计方案有关。但事实是，从0开始使本章的示例更容易编写。

作为 Java Motel 的经理，你将入住数据存储在计算机硬盘上的一个文件中。该文件为汽车旅馆中的每个房间都有一个条目。例如，在图16-1中，房间0有一位客人，房间1有四位客人，房间2空着，等等。

![](img/bf4858233d2b2a32ff4e3991860526b3_328_0.png)

图 16-2
运行清单16-1中的代码。

![](img/bf4858233d2b2a32ff4e3991860526b3_328_1.png)

本示例的输入文件名为 occupancy——不是 occupancy.txt。如果你使用 Windows 记事本创建 occupancy 文件，必须在“另存为”对话框的文件名字段中使用引号。也就是说，你必须在文件名字段中输入“occupancy”（带引号）。如果不使用引号括住名称，记事本会为文件名添加默认扩展名（将 occupancy 变为 occupancy.txt）。类似的问题也适用于 Macintosh 的 TextEdit 程序。默认情况下，TextEdit 为每个新文件添加 .rtf 扩展名。要为特定文件覆盖 .rtf 默认设置，请选择格式→转换为纯文本。然后，在“另存为”对话框中，取消选中标记为“如果未提供扩展名，则使用‘.txt’”的复选框。（要为所有新创建的文件覆盖默认值，请选择 TextEdit→偏好设置。然后，在“偏好设置”对话框的“新建文档”选项卡的“格式”部分，选择纯文本。）

## 在运行时决定循环的限制

有时，你可能想要比图16-2中更简洁的报告。你说：“别给我列出一长串房间，只要告诉我房间3的客人数量。”要获得这样的报告，你需要一个稍微智能一点的程序。该程序在清单16-2中，程序的运行情况显示在图16-3中。

## 清单 16-2：仅报告一个房间，请

```java
import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;
import static java.lang.System.out;

public class ShowOneRoomOccupancy {
    public static void main(String args[])
        throws FileNotFoundException {
```

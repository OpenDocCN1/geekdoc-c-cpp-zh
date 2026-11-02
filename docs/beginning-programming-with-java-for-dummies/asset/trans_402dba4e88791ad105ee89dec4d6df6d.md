
我从不花钱参加任何比赛。所有这些奖金都是免费得来的。当全国计算机科学教育工作者大会在内华达州里诺召开时，同事们劝我去试试老虎机。我输了23美元，然后又赢回18美元。那时，我停手了。我只输了5美元，想趁早收手。

正因如此，我编写一个关于老虎机的Java程序就显得十分奇怪。典型的老虎机有三个转轮，每个转轮大约有20个符号。但为了说明本节的思想，我不需要20个符号。相反，我使用四种符号——樱桃、柠檬、金橘和芜菁甘蓝。

## 创建增强型 for 循环

当你玩我简化版的老虎机时，你可以旋转出超过60种组合中的任意一种——cherry•cherry•kumquat、rutabaga•rutabaga•rutabaga，或者别的什么。本章的目标是列出所有可能的组合。但首先，我要向你展示另一种循环。清单 15-5 为老虎机的符号定义了一个枚举类型，并显示了这些符号的列表。（关于枚举类型的介绍，请参见第 10 章。）

### 清单 15-5：老虎机符号

```
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

清单 15-5 使用了 Java 的增强型 for 循环。“增强”一词意为“与 Java 早期版本中的循环相比有所增强”。增强型 for 循环是在 Java 5.0 中引入的。如果你运行的是 Java 1.4.2（或类似版本），则无法使用增强型 for 循环。

以下是增强型 for 循环的格式：

```
for (TypeName variableName : RangeOfValues) {
    Statements
}
```

以下是清单 15-5 中的循环如何遵循该格式：

- **在清单 15-5 中，单词 `Symbol` 是一种类型的名称。**

  `int` 类型描述的是像 −1、0、1 和 2 这样的值。`boolean` 类型描述的是 `true` 和 `false` 这样的值。由于清单 15-5 中的代码，`Symbol` 类型描述的是 cherry、lemon、kumquat 和 rutabaga 这些值。有关像 `Symbol` 这样的枚举类型的更多信息，请参见第 10 章。

- **在清单 15-5 中，单词 `leftReel` 是一个变量的名称。**

  清单 15-1 中的循环将 `count` 定义为 `int` 变量。类似地，清单 15-5 中的循环将 `leftReel` 定义为 `Symbol` 变量。因此，理论上，变量 `leftReel` 可以取四个 `Symbol` 值中的任意一个。
  
  顺便说一下，我把这个变量叫做 `leftReel`，是因为代码列出了可能出现在老虎机三个转轮最左侧的所有符号。因为老虎机的三个转轮具有相同的符号，我也可以把这个变量命名为 `middleReel` 或 `rightReel`。但转念一想，我要把 `middleReel` 和 `rightReel` 这两个名字留到后面的例子中使用。

- **在清单 15-5 中，表达式 `Symbol.values()` 表示清单 15-5 中的四个值。**

  引用我在上一个列表项中所说的话：“理论上，变量 `leftReel` 可以取四个 `Symbol` 值中的任意一个。”嗯，`for` 语句中的 `RangeOfValues` 部分将理论变成了实践。括号中的这第三项表示：“循环迭代的次数与 `Symbol` 值的数量相同，并且在每次循环迭代期间，让 `leftReel` 变量取不同的 `Symbol` 值。”
  
  因此，清单 15-5 中的循环会经历四次迭代——一次迭代中 `leftReel` 的值为 cherry，另一次迭代中 `leftReel` 的值为 lemon，第三次迭代中 `leftReel` 的值为 kumquat，第四次迭代中 `leftReel` 的值为 rutabaga。在每次迭代期间，程序都会打印 `leftReel` 变量的值。结果如图 15-8 所示。

![](img/f938eba5f15e231d828a6255e7ec5523_317_0.png)

**图 15-8：** 清单 15-5 中代码的输出。

一般来说，someEnumTypeName.values() 表达式表示特定枚举类型的变量可以拥有的值集合。例如，在清单 10-7 中，你可以使用表达式 WhoWins.values() 来表示 home、visitor 和 neither 这些值。

![](img/f938eba5f15e231d828a6255e7ec5523_318_0.png)

类型名称（如 Symbol）与类型值（如 Symbol.values()）之间的区别非常微妙。幸运的是，你不必担心这个区别。作为初学者程序员，你只需在增强型 for 循环的 RangeOfValues 部分中使用 .values() 后缀即可。

## 嵌套增强型 for 循环

清单 15-5 以一种非常优雅的方式解决了一个简单问题。所以在读完清单 15-5 之后，你可能会问更复杂的问题：“我能列出老虎机四个符号的所有可能三转轮组合吗？”是的，你可以。清单 15-6 展示了如何做到这一点。

### 清单 15-6：列出组合

```java
import static java.lang.System.out;

class ListCombinations {
    enum Symbol {
        cherry, lemon, kumquat, rutabaga
    }

    public static void main(String args[]) {
        for (Symbol leftReel : Symbol.values()) {
            for (Symbol middleReel : Symbol.values()) {
                for (Symbol rightReel : Symbol.values()) {
                    out.print(leftReel);
                    out.print(" ");
                    out.print(middleReel);
                    out.print(" ");
                    out.println(rightReel);
                }
            }
        }
    }
}
```

当你运行清单 15-6 中的程序时，会得到 64 行输出。其中一些行（来自一次运行的中部）如图 15-9 所示。

### 图 15-10：首次进入清单 15-6 程序中的循环

![](img/f938eba5f15e231d828a6255e7ec5523_320_0.png)

在显示 cherry cherry cherry 之后，你继续使用最内层循环的其他值。也就是说，你把右转轮的值从 cherry 改为 lemon。（见图 15-11。）现在三个转轮的值是 cherry cherry lemon，于是你在屏幕上显示这些值。

### 图 15-11：在最内层循环中从 cherry 改为 lemon。

![](img/f938eba5f15e231d828a6255e7ec5523_320_1.png)

在穷尽了最内层（右转轮）循环的四个值之后，你跳出该最内层循环。但这次跳转会让你回到中间循环的顶部，在那里你把 middleReel 的值从 cherry 改为 lemon。现在 leftReel 和 middleReel 的值分别是 cherry 和 lemon。（见图 15-12。）

### 图 15-12：在中间循环中从 cherry 改为 lemon。

![](img/f938eba5f15e231d828a6255e7ec5523_321_0.png)

在中间循环改为 lemon 之后，你再次一头冲进最内层循环。就好像你从未见过这个内层循环一样，你把循环变量设置为 cherry。（见图 15-13。）

### 图 15-13：重新开始内层循环。

![](img/f938eba5f15e231d828a6255e7ec5523_321_1.png)

在显示了美味的 cherry lemon cherry 组合之后，你开始改变最内层循环的值。（见图 15-14。）

### 图 15-14：第二次遍历最内层循环。

![](img/f938eba5f15e231d828a6255e7ec5523_322_0.png)

循环一直进行，直到显示全部 64 种组合。呼！

## 第四部分

## 使用程序单元

![](img/f938eba5f15e231d828a6255e7ec5523_324_0.png)

## 本部分内容 . . .

- 同时处理多个项目
- 将你的工作划分为可管理的部分
- 创建窗口和其他漂亮的东西

![](img/f938eba5f15e231d828a6255e7ec5523_328_0.png)

图 16-2：
运行清单 16-1 中的代码

![](img/f938eba5f15e231d828a6255e7ec5523_328_1.png)

这个示例的输入文件名为 occupancy —— 而不是 occupancy.txt。如果你使用 Windows 记事本创建 occupancy 文件，你必须在“另存为”对话框的“文件名”字段中使用引号。也就是说，你必须在“文件名”字段中输入“occupancy”（带引号）。如果你不用引号括住文件名，记事本会为该文件名添加一个默认扩展名（将 occupancy 变成 occupancy.txt）。类似的问题也适用于 Macintosh 的 TextEdit 程序。默认情况下，TextEdit 会为每个新文件添加 .rtf 扩展名。要为特定文件覆盖 .rtf 默认设置，请选择 格式→制作纯文本。然后，在“另存为”对话框中，取消选中标记为“如果没有提供扩展名，则使用 .txt”的复选框。（要覆盖所有新建文件的默认设置，请选择 TextEdit→偏好设置。然后，在“偏好设置”对话框的“新建文档”选项卡的“格式”部分，选择“纯文本”。）

## 在运行时决定循环的限制

有时，你可能想要比图 16-2 更简洁的报告。“别给我一份长长的房间列表，”你会说，“只告诉我 3 号房间的客人数量。”要得到这样的报告，你需要一个稍微聪明一点的程序。该程序位于清单 16-2 中，程序的运行情况如图 16-3 所示。

### 清单 16-2：请只报告一个房间

```
import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;
import static java.lang.System.out;

public class ShowOneRoomOccupancy {
    public static void main(String args[])
        throws FileNotFoundException {
```


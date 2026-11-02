
## 图 16-4 房间号 10 很糟糕，得不到响应。

![](img/6d9dcff12e52b997f3ad31445b712549_332_0.png)

![](img/6d9dcff12e52b997f3ad31445b712549_332_1.png)

在清单 16-3 中，我想知道入住文件是否还包含更多数据（即我尚未读取的任何数据）。因此我调用 Scanner 类的 hasNext 方法。hasNext 方法会向前查看，判断是否可以读取任何类型的数据——一个 int 值、一个 double 值、一个单词、一个布尔值，或其他任何东西。对于本节的示例来说这没问题，但在某些情况下，你需要对输入数据更挑剔一些。例如，你可能想知道是否可以调用 nextInt（而不是 nextDouble 或 nextLine）。幸运的是，Java 提供了满足你最挑剔输入需求的方法。像 diskScanner.hasNextInt() 这样的方法会测试是否可以从磁盘文件读取一个 int 值。Java 还有像 hasNextLine、hasNextDouble 等方法。要了解有关普通 hasNext 方法的更多信息，请参阅第 14 章。

清单 16-3 有一个又大又胖的条件来保持 for 循环运行：

```java
for (int roomNum = 0;
    roomNum < whichRoom && diskScanner.hasNext();
    roomNum++) {
```

许多 for 循环条件都是简单的“小于”测试，但并没有规定所有 for 循环条件都必须如此简单。事实上，只要表达式的值为 true 或 false，任何表达式都可以作为 for 循环的条件。清单 16-3 中的条件将“小于”与对 Scanner 类的 hasNext 方法的调用结合在了一起。

## 读者，认识数组；数组，认识读者

疲惫的旅客走上 Java Motel 的前台。“我想要一个房间，”旅客说。于是前台服务员运行了一份像图 16-2 那样的报告。注意到名单上第一个空房，服务员建议房间 2。“我要了，”旅客说。

现在要得到好的服务实在太难了。你有多少次告诉过服务员先填满号码较高的房间？号码较低的房间更老旧，急需维修。例如，房间 3 有一个室内泳池。（管道漏水，所以地毯湿透了。）房间 2 没有暖气（至少在冬季不是）。房间 1 有严重的电气问题（因此对于那个房间，你总是要求预先付款）。此外，房间 8 是空的，而且你对号码较高的房间收取更高的费用。

这正是细微的展示变化可以带来巨大差异的地方。你需要一个程序以逆序列出空房。这样，房间 8 就能在房间 2 之前引起服务员的注意。

思考一下用于逆序显示数据的程序策略。输入来自图 16-1，程序的输出应如下图 16-5 所示的显示。

![](img/6d9dcff12e52b997f3ad31445b712549_333_0.png)

这是一个编程策略的第一个（糟糕的）想法：

```text
Get the last value in the occupancy file.
If the value is 0, print the room number.

Get the next-to-last value in the occupancy file.
If the value is 0, print the room number.

...And so on.
```

使用一些花哨的输入/输出程序，这个策略可能可行。但无论你使用什么输入/输出程序，直接跳到文件末尾或中间都是一件很痛苦的事。如果你计划反复跳转，那就更糟了。所以回到起跑线，重新思考一个更好的方案。

这里有一个想法！读取入住文件中的所有值，并将每个值存储在其自己的变量中。然后你以逆序遍历这些变量，在适当的时候显示房间号。

这个想法可行，但代码丑得我拒绝称之为“清单”。不，这只是“请看下面的代码”之类的东西。所以请看下面的丑陋代码：

```java
/*
 * Ugh! I can't stand this ugly code!
 */
guestsIn0 = diskScanner.nextInt();
guestsIn1 = diskScanner.nextInt();
guestsIn2 = diskScanner.nextInt();
guestsIn3 = diskScanner.nextInt();
guestsIn4 = diskScanner.nextInt();
guestsIn5 = diskScanner.nextInt();
guestsIn6 = diskScanner.nextInt();
guestsIn7 = diskScanner.nextInt();
guestsIn8 = diskScanner.nextInt();
guestsIn9 = diskScanner.nextInt();

if (guestsIn9 == 0) {
    System.out.println(9);
}
if (guestsIn8 == 0) {
    System.out.println(8);
}
if (guestsIn7 == 0) {
    System.out.println(7);
}
if (guestsIn6 == 0) {
// ... And so on.
```

你缺少的是统一命名十个变量的方法。也就是说，最好能写成

```java
/*
 * Nice idea, but this is not real Java code:
 */

//Read forwards
for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsInroomNum = diskScanner.nextInt();
}

//Write backwards
for (int roomNum = 9; roomNum >= 0; roomNum--) {
    if (guestsInroomNum == 0) {
        System.out.println(roomNum);
    }
}
```

好吧，你可以写这种循环。你只需要一些方括号。当你在前面代码所示的想法中加上方括号时，你就得到了所谓的 *数组*。一个 *数组* 是一行值，就像一层楼汽车旅馆中的房间排一样。要想象数组，只要想象 Java Motel 即可：

- 首先，想象房间并排排列。
- 接下来，想象这些房间的前墙被移除。每个房间内，你可以看到一定数量的客人。
- 如果可以的话，忘记房间 9 里的两位客人正在把一堆钞票放进大公文包里。忽略房间 5 的客人已经有一天半没离开电视机了的事实。不要关注这些细节，只看数字。每个房间，都看到一个代表该房间客人数量的数字。（如果你在自由想象方面不是强项，请看图 16-6。）

![](img/6d9dcff12e52b997f3ad31445b712549_335_0.png)

在 Java 编程的术语中，整排房间被称为 *数组*。数组中的每个房间称为数组的 *组件*（也称为 *数组元素*）。每个组件都关联着两个数字。

- **索引：** 在 Java Motel 数组的情况下，索引是房间号（0 到 9 之间的数字）。
- **值：** 在 Java Motel 数组中，值是给定房间的客人数量（存储在组件中的一个数字）。

使用数组可以免去你声明十个独立变量的麻烦：guestsIn0、guestsIn1、guestsIn2，等等。要声明一个包含十个值的数组，你可以写两行相当简短的代码：

```java
int guestsIn[];
guestsIn = new int[10];
```

你甚至可以将这两行压缩成一行更长的代码：

```java
int guestsIn[] = new int[10];
```

在这两个代码片段中，注意到数字 10 的使用。这个数字告诉计算机让 guestsIn 数组拥有十个组件。数组的每个组件都有自己的名称。起始组件名为 guestsIn[0]，下一个名为 guestsIn[1]，依此类推。十个组件中的最后一个名为 guestsIn[9]。

![](img/6d9dcff12e52b997f3ad31445b712549_336_0.png)

在创建数组时，你总是指定组件的数量。数组的索引总是从 0 开始，以比组件总数少一的数字结束。例如，如果你的数组有十个组件（并且你用 new int[10] 声明数组），数组的索引从 0 到 9。

### 在数组中存储值

创建数组后，你可以将值放入数组的组件中。例如，房间 6 的客人对你放在床上的那些薄荷糖已经厌倦了。所以他们退房，房间 6 变为空房。你应该将值 0 放入第 6 个组件。你可以用这个赋值语句做到：

```java
guestsIn[6] = 0;
```

某一天的生意很糟糕。没有人住在汽车旅馆。但随后你迎来了一个好运气。一辆大巴开到汽车旅馆前。巴士侧面有一个标语写着“Loners' Convention”。巴士上下来 25 个人，每个人都走向汽车旅馆的小办公室，没有人注意巴士上的其他人。每个人都想要一个私人房间。只有 10 个人可以住在 Java Motel，但这没关系，因为你可以把另外 15 个独行者送到路边的老 C-Side Resort and Motor Lodge。

无论如何，要将十个独行者登记入住 Java Motel，你在每个房间放一个客人。既然创建了数组，你就可以利用数组的索引写一个 for 循环，像这样：

```java
for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsIn[roomNum] = 1;
}
```

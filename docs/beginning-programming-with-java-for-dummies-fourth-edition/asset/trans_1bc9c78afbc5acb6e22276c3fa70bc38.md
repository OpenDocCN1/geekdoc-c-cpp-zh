
## 这所有 findWithinHorizon 乱七八糟的东西背后是什么？

不陷入太多细节，这里就是 `findWithinHorizon(".", 0).charAt(0)` 技术的工作原理：

Java 的 `findWithinHorizon` 方法会在输入中查找内容。方法找到的内容取决于你在括号中放入的内容。例如，对 `findWithinHorizon("\\d\\d\\d", 0)` 的调用会查找由三位数字组成的一组。以下代码行
```java
System.out.println(keyboard.findWithinHorizon("\\d\\d\\d", 0));
```

我可以输入

```
Testing 123 Testing Testing
```

计算机的响应是显示

```
123
```

在调用 `findWithinHorizon("\\d\\d\\d", 0)` 中，每个 `\\d` 代表一位数字。这种 `\\d` 的用法是特殊代码中称为 *正则表达式* 的众多缩写之一。

现在这里有个奇怪的事情。在正则表达式的世界里，点号代表任何字符，不一定是“点”。因此 `findWithinHorizon(".", 0)` 告诉计算机查找用户在键盘上输入的下一个任何类型的字符。当你尝试输入单个字符时，`findWithinHorizon(".", 0)` 非常有用。

在调用 `findWithinHorizon("\\d\\d\\d", 0)` 中，`0` 告诉 `findWithinHorizon` 一直搜索到输入的末尾。这个值 `0` 是一个特殊情况，因为除 `0` 之外的任何值都会将搜索限制为一定数量的字符。（这就是为什么方法名中包含单词 *horizon*。*horizon* 就是方法所能看到的最远距离。）以下是几个例子：

- 使用相同的输入 Testing 123 Testing Testing，调用 `findWithinHorizon("\\d\\d\\d", 9)` 返回 null。它返回 null 是因为输入的前九个字符（字符 Testing 1 —— 七个字母、一个空格和一个数字）不包含三位连续数字。这九个字符与模式 `\\d\\d\\d` 不匹配。
- 使用相同的输入，调用 `findWithinHorizon("\\d\\d\\d", 10)` 也返回 null。它返回 null 是因为输入的前十个字符（字符 Testing 12）不包含三位连续数字。
- 使用相同的输入，调用 `findWithinHorizon("\\d\\d\\d", 11)` 返回 123。它返回 123 是因为输入的前 11 个字符（字符 Testing 123）包含这 3 位连续数字。
- 输入为 A57B442123 Testing 时，调用 `findWithinHorizon("\\d\\d\\d", 12)` 返回 442。它返回 442 是因为在输入的前 12 个字符（字符 A57B442123 Test）中，由 3 位连续数字组成的最早序列是序列 442。

等等！要从键盘抓取单个字符，我调用 findWithinHorizon(".", 0). charAt(0)。charAt(0) 在读取单个字符时起什么作用？不幸的是，任何 findWithinHorizon 调用都表现得像是在查找一堆字符，而不仅仅是单个字符。即使你调用 findWithinHorizon(".", 0)，并且计算机从键盘获取一个字母，Java 程序也会将该字母视为可能存在的多个输入字符之一。

对 charAt(0) 的调用解决了多字符问题。这个 charAt(0) 调用告诉 Java 从 findWithinHorizon 获取的任何字符中挑选初始字符。

是的，这很复杂。是的，我不喜欢必须解释它。但不，你不必理解这个侧边栏中的任何细节。如果你想读就读细节，如果你不在乎就跳过细节。

我希望我能给你 12 条简单规则来帮助你决定何时以及何时不重用变量。问题是，我做不到。这完全取决于你想要完成什么。那么你如何自己判断何时重用变量、何时不重用变量呢？就像那个人对问如何到达卡内基音乐厅的人说的那样，“Practice, practice, practice.”

## 读取字符

创建 Java Scanner 类的人没有创建用于读取单个字符的 next 方法。因此，要输入单个字符，我将两个 Java API 方法粘合在一起。我使用 findWithinHorizon 和 charAt 方法。

第 5 章中的表 5-1 介绍了这种用于读取单个输入字符的 findWithinHorizon(".", 0). charAt(0) 技术，而清单 8-3 使用该技术一次读取一个字符。（事实上，清单 8-3 使用该技术四次来读取四个单独的字符。）

注意图 8-5 中输入的格式。要输入单词 pots 中的字符，我一次输入四个字母，字母之间没有空格，也没有引号。findWithinHorizon(".", 0).charAt(0) 技术就是这样工作的，但不要责怪我或我的技术。其他开发人员的字符读取方法也以相同的方式工作。不管你使用谁的方法，读取字符与读取数字是不同的。方法如下：

> 使用像 nextDouble 和 nextInt 这样的方法，你在数字之间输入空格。

如果我输入 80 6，那么两次对 nextInt 的调用会读取数字 80，然后是数字 6。如果我输入 806，那么一次对 nextInt 的调用会读取数字 806（八百零六），如图 8-8 所示。

使用 findWithinHorizon(".", 0).charAt(0) 时，你在字符之间不输入空格。

如果我输入 po，那么两次连续的 findWithinHorizon(".", 0).charAt(0) 调用会读取字母 p，然后是字母 o。如果我输入 p o，那么两次 findWithinHorizon(".", 0).charAt(0) 调用会读取字母 p，然后是一个空格字符。（是的，空格是一个字符！）再次参见图 8-8。

## 图 8-8：
读取
数字
和
字符。

![](img/6d9dcff12e52b997f3ad31445b712549_178_0.png)

![](img/6d9dcff12e52b997f3ad31445b712549_178_1.png)

要在计算机程序的文本中表示单个字符，你用单引号将字符括起来。但是，当你作为程序输入的一部分输入一个字符时，你不会用引号将字符括起来。

![](img/6d9dcff12e52b997f3ad31445b712549_178_2.png)

假设你的程序调用 nextInt 然后调用 findWithinHorizon(".", 0).charAt(0)。如果你在键盘上输入 80x，你会收到一条错误消息。（消息说 InputMismatchException。nextInt 方法期望你在每个 int 值后输入一个空格。）现在如果不是输入 80x，而是在键盘上输入 80 x 会怎样？那么程序会得到 80 作为 int 值，然后是空格作为字符值。为了让程序得到 x，程序必须再调用一次 findWithinHorizon(".", 0).charAt(0)。这看起来很浪费，但从长远来看是有意义的。

## 布尔类型

我遇到大麻烦了。我有 140 颗棒棒糖，15 个孩子在我客厅里跑来跑去大喊大叫。他们大喊大叫是因为每个孩子想要 10 颗棒棒糖，他们跑来跑去是因为孩子们在拥挤的客厅里就是这样做的。我需要一个程序来告诉我是否可以给每个孩子 10 颗棒棒糖。

我需要一个 boolean 类型的变量。布尔变量存储 2 个值之一 —— true 或 false（true，我可以给每个孩子 10 颗棒棒糖；或 false，我不能给每个孩子 10 颗棒棒糖）。无论如何，孩子们快疯了，所以我写了一个简短的程序并放在清单 8-4 中。程序的输出显示在图 8-9 中。

## 清单 8-4：使用布尔类型

```
class CanIKeepKidsQuiet {
    public static void main(String args[]) {
        int gumballs;
        int kids;
        int gumballsPerKid;
        boolean eachKidGetsTen;
        gumballs = 140;
        kids = 15;
        gumballsPerKid = gumballs / kids;
        System.out.print("True or false? ");
        System.out.println("Each kid gets 10 gumballs.");
        eachKidGetsTen = gumballsPerKid >= 10;
        System.out.println(eachKidGetsTen);
    }
}
```

![](img/6d9dcff12e52b997f3ad31445b712549_179_0.png)

在清单 8-4 中，变量 eachKidGetsTen 的类型为 boolean。因此存储在 eachKidGetsTen 变量中的值可以是 true 或 false。（我不能在 eachKidGetsTen 变量中存储数字或字符。）

要为变量 eachKidGetsTen 找到一个值，程序会检查 gumballsPerKid 是否大于或等于十。（符号 >= 代表“大于或等于”。多么遗憾！没有 ≥ 键在

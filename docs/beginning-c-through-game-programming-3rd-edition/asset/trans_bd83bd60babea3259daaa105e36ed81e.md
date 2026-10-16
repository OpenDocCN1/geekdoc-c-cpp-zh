

在接下来的几行中，我使用 MAX_ITEMS 来保护自己，避免向英雄的库存中添加另一个物品：

```
if (numItems < MAX_ITEMS)
{
    inventory[numItems++] = "healing potion";
}
else
{
    cout << "You have too many items and can't carry another.";
}
```

在上述代码中，我首先检查 numItems 是否小于 MAX_ITEMS。如果是，那么我可以安全地将 numItems 用作索引，并将一个新的字符串对象赋值给数组。在这种情况下，numItems 为 3，所以我把字符串 "healing potion" 赋给数组位置 3。如果不是这种情况，那么我就会显示消息：“You have too many items and can’t carry another.”

那么，如果你确实尝试访问数组边界之外的元素会发生什么？这取决于情况，因为你将访问计算机内存中某个未知的部分。最糟糕的是，如果你试图向数组边界之外的元素赋值，可能会导致程序做出不可预测的事情，甚至可能崩溃。

在使用索引之前，先测试以确保索引号是有效的数组位置，这被称为**边界检查**。当你想要使用的索引可能无效时，执行边界检查至关重要。

## 理解 C 风格字符串

在字符串对象出现之前，C++ 程序员使用以空字符结尾的字符数组来表示字符串。这些字符数组现在被称为 **C 风格字符串**，因为这种做法始于 C 程序。你可以像声明和初始化任何其他数组一样声明和初始化 C 风格字符串：

```
char phrase[] = "Game Over!!!";
```

C 风格字符串以称为空字符的字符结尾，以表示其结束。你可以将空字符写为 '\0'。在前面的代码中，我不需要使用空字符，因为它会自动存储在字符串的末尾。所以从技术上讲，phrase 有 13 个元素。（然而，处理 C 风格字符串的函数会说 phrase 的长度为 12，这很合理，并且与字符串对象的工作方式一致。）

与任何其他类型的数组一样，你可以在定义时指定数组大小。因此，另一种声明和初始化 C 风格字符串的方式是：

```
char phrase[81] = "Game Over!!!";
```

上面的代码创建了一个可以容纳 80 个可打印字符（加上其终止空字符）的 C 风格字符串。

C 风格字符串没有成员函数。但标准库中的 cstring 文件包含各种用于处理 C 风格字符串的函数。

字符串对象的一个优点是它们被设计为与 C 风格字符串无缝协作。例如，以下所有将 C 风格字符串与字符串对象一起使用的用法都是完全有效的：

```
string word1 = "Game";
char word2[] = "Over";
string phrase = word1 + word2;

if (word1 != word2)
{
	cout << "word1 and word2 are not equal.\n";
}

if (phrase.find(word2) != string::npos)
{
	cout << "word2 is contained in phrase.\n";
}
```

你可以连接字符串对象和 C 风格字符串，但结果始终是一个字符串对象（因此代码 char phrase[] = word1 + word2; 会产生错误）。你可以使用关系运算符比较字符串对象和 C 风格字符串。你甚至可以在字符串对象成员函数中使用 C 风格字符串作为参数。

C 风格字符串具有与数组相同的缺点。其中最大的缺点之一是它们的长度是固定的。因此，结论是：尽可能使用字符串对象，但如有必要，也要准备好处理 C 风格字符串。

## 使用多维数组

如你所见，序列非常适合游戏。你可以以字符串的形式使用它们来存储玩家姓名，也可以以数组的形式使用它们来存储 RPG 中的物品列表。但有时游戏的某部分需要的不仅仅是线性的列表。有时游戏的某部分确实需要更多维度。例如，虽然你可以用 64 个元素的数组来表示棋盘，但将其作为 8 × 8 元素的二维实体来处理确实更直观。幸运的是，你可以创建二维、三维（甚至更多维）的数组，以最好地满足游戏的需求。

### 介绍井字棋棋盘程序

井字棋棋盘程序显示一个井字棋棋盘。该程序显示棋盘并宣布 X 获胜。虽然该程序本可以使用一维数组编写，但它使用二维数组来表示棋盘。图 3.5 展示了该程序。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。该程序位于第 3 章文件夹中；文件名为 `tic-tac-toe_board.cpp`。

![](img/34f09be0ed6217c465debc4490197d4f_125_0.png)

**图 3.5**  
井字棋棋盘由二维数组表示。

```
for (int j = 0; j < COLUMNS; ++j)
{
    cout << board[i][j];
}

cout << endl;
}
```

通过使用一对嵌套的 for 循环，我遍历二维数组并逐个显示字符元素，从而形成一个井字棋棋盘。

## 介绍单词乱序

单词乱序是一款益智游戏，计算机生成一个单词的乱序版本，其中字母顺序随机。玩家必须猜出这个单词才能赢得游戏。如果玩家卡住了，可以请求提示。图 3.6 展示了该游戏。

![](img/34f09be0ed6217c465debc4490197d4f_128_0.png)

图 3.6
嗯……这个词看起来“乱序了”。

## 现实世界

尽管益智游戏通常不会进入游戏前十名榜单，但大公司仍然年复一年地发布它们。为什么？原因很简单：它们有利可图。益智游戏虽然通常不是热门大作，但仍然可以卖得很好。有很多玩家（休闲和硬核）会被设计精良的益智游戏所吸引。而且益智游戏的生产成本远低于那些需要大型制作团队和多年开发时间的高知名度游戏。

## 设置程序

像往常一样，我从一些注释和包含所需文件开始。你可以从 Course Technology 网站（www.coursetech.com/downloads）下载此程序的代码。该程序位于第 3 章文件夹中；文件名为 word_jumble.cpp。

```
// Word Jumble
// The classic word jumble game where the player can ask for a hint

#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;
```

## 选择要乱序的单词

我的下一个任务是选择一个要乱序的单词——即玩家将尝试猜测的单词。首先，我创建一个单词和提示的列表：

```
int main()
{
    enum fields {WORD, HINT, NUM_FIELDS};
    const int NUM_WORDS = 5;
    const string WORDS[NUM_WORDS][NUM_FIELDS] =
    {
        {"wall", "Do you feel you're banging your head against something?"},
        {"glasses", "These might help you see the answer."},
        {"labored", "Going slowly, is it?"},
        {"persistent", "Keep at it."},
        {"jumble", "It's what the game is all about."}
    };
};
```

```
cin >> guess;
}
```

循环不断询问玩家猜测，直到玩家猜出单词或要求退出。

## 告别

当循环结束时，玩家要么赢了，要么退出了，所以是时候说再见了。

```
if (guess == theWord)
{
    cout << "\nThat's it! You guessed it!\n";
}

cout << "\nThanks for playing.\n";

return 0;
}
```

如果玩家猜出了单词，我会祝贺他或她。最后，我感谢玩家的参与。

## 总结

在本章中，你学习了以下概念：

- for 循环允许你重复一段代码。在 for 循环中，你可以提供初始化语句、要测试的表达式以及每次循环迭代后要执行的操作。
- for 循环通常用于计数或遍历序列。
- 对象是封装的、内聚的实体，它结合了数据（称为数据成员）和函数（称为成员函数）。
- string 对象（通常简称为字符串）定义在标准库的 string 文件中。string 对象允许你存储字符序列，并且还具有成员函数。
- string 对象的定义使其能够直观地使用熟悉的运算符，例如连接运算符和关系运算符。



**图 6**
Web 应用程序设计的故事板

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_182_0.png)

如果数量不止一个怎么办？用户可能有一整张以厘米为单位的数值表，需要转换为英寸。

如果用户输入的單位我们的程序不知道如何处理怎么办，例如埃？

如果用户要求不可能的转换怎么办，例如英寸转换为加仑？

让我们从故事板面板开始。用不同颜色写出用户输入是个好主意。（如果手边没有彩色笔，就在它们下面画线。）

```
~~~
Converting a Sequence of Values

What unit do you want to convert from? cm
What unit do you want to convert to? in
Enter values, terminated by zero
30  ← Allows conversion of multiple values
30 cm = 11.81 in  ← Format makes clear what got converted
100
100 cm = 39.37 in
0
What unit do you want to convert from?
~~~
```

故事板展示了我们如何处理一种潜在的混淆。一个想知道 30 厘米是多少英寸的用户可能没有仔细阅读第一个提示，而指定了英寸。但随后输出是“30 in = 76.2 cm”，提醒用户存在问题。

故事板还提出了一个问题。用户应该怎样知道“cm”和“in”是有效单位？“centimeter”和“inches”也可以吗？会发生什么

27. Google 有一个简单的单位转换界面。你只需输入问题，就能得到答案。

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_184_0.png)

为一个 C++ 程序中的等效界面制作故事板。展示一切顺利的“happy day”场景，并展示对两类错误的处理。

28. 考虑对自测 26 中的程序进行修改。在计算平均值之前去掉最低分。为用户只提供一个分数的情况提供故事板。

29. 在 C++ 中实现以下故事板有什么问题？

```
~~~
Computing Multiple Averages
Enter scores: 90 80 90 100 80
The average is 88
Enter scores: 100 70 70 100 80
The average is 88
Enter scores: -1            -1 is used as a sentinel to exit the program
[Program exits!]
~~~
```

30. 为一个程序制作故事板，该程序比较一笔 $10,000 的投资在给定年数内在两种利率下的增长情况。

**实践练习** 现在你可以尝试本章末尾的这些练习：R4.17、R4.18、R4.19。

## 4.7 常见循环算法

在以下各节中，我们讨论一些最常见的以循环实现的算法。你可以将它们用作循环设计的起点。

### 4.7.1 求和与平均值

计算若干输入的总和是一项非常常见的任务。维护一个*累计总和*：一个变量，将每个输入值加到它上面。当然，总和应初始化为 0。

```cpp
double total = 0;
double input;
while (cin >> input)
{
    total = total + input;
}
```

要计算平均值，请维护所有值的总和与计数。

要计算平均值，请统计你有多少个值，然后除以计数。务必检查计数不为零。

```cpp
double total = 0;
int count = 0;
double input;
while (cin >> input)
{
    total = total + input;
    count++;
}
double average = 0;
if (count > 0) { average = total / count; }
```

### 4.7.2 计数匹配项

要统计满足条件的值，请检查所有值，并为每个匹配项递增计数器。

你常常想知道有多少个值满足特定条件。例如，你可能想统计一个字符串中有多少个空格。维护一个计数器，即一个初始化为 0 的变量，每当有匹配项时就递增。

```cpp
int spaces = 0;
for (int i = 0; i < str.length(); i++)
{
    string ch = str.substr(i, 1);
    if (ch == " ")
    {
        spaces++;
    }
}
```

例如，如果 str 是字符串 "My Fair Lady"，则 spaces 会递增两次（当 i 为 2 和 7 时）。

注意，spaces 变量声明在循环之外。我们希望循环更新单个变量。ch 变量声明在循环内部。每次迭代都会创建一个单独的变量，并在每次循环迭代结束时将其移除。

这个循环也可用于扫描输入。以下循环一次读取一个单词的文本，并统计字母数至多为三个的单词数量：

```cpp
int short_words = 0;
string input;
while (cin >> input)
{
    if (input.length() <= 3)
    {
        short_words++;
    }
}
```

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_185_0.png)

在统计匹配项的循环中，每当找到匹配项时，计数器就递增。

### 4.7.3 查找第一个匹配项

> > 如果你的目标是找到匹配项，那么在找到匹配项时就退出循环。

当你统计满足条件的值时，你需要查看所有值。然而，如果你的任务是找到匹配项，那么一旦条件满足就可以停止。

下面是一个查找字符串中第一个空格的循环。由于我们不会访问字符串中的所有元素，因此 while 循环比 for 循环更合适：

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_186_0.png)

```cpp
bool found = false;
int position = 0;
while (!found && position < str.length())
{
   string ch = str.substr(position, 1);
   if (ch == " ") { found = true; }
   else { position++; }
}
```

如果找到了匹配项，则 found 为 true，position 是第一个匹配项的索引。如果循环没有找到匹配项，那么循环结束后 found 仍为 false。

在前面的示例中，我们在字符串中搜索满足条件的字符。你可以将相同的过程应用于用户输入。假设你要求用户输入一个小于 100 的正值。持续询问，直到用户提供正确的输入：

```cpp
bool valid = false;
double input;
while (!valid)
{
   cout << "Please enter a positive value < 100: ";
   cin >> input;
   if (0 < input && input < 100) { valid = true; }
   else { cout << "Invalid input." << endl; }
}
```

注意，变量 input 声明在 while 循环之外，因为你希望在循环结束后使用该输入。如果它声明在循环体内部，你就无法在循环外使用它。

### 4.7.4 最大值与最小值

> > 要找到最大值，每当你看到更大的值时，就更新目前为止看到的最大值。

要计算序列中的最大值，请维护一个变量来存储你已遇到的最大元素，并在找到更大值时更新它：

```cpp
double largest;
cin >> largest;
double input;
while (cin >> input)
{
   if (input > largest)
   {
      largest = input;
   }
}
```

该算法要求至少有一个输入。

*要找到最高的公交车乘客的身高，请记住目前为止的最大值，并在看到更高的人时更新它。*

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_187_0.png)

要计算最小值，只需反转比较：

    double smallest;
    cin >> smallest;
    double input;
    while (cin >> input)
    {
        if (input < smallest)
        {
            smallest = input;
        }
    }

### 4.7.5 比较相邻值

在循环中处理一系列值时，你有时需要将一个值与它前面的值进行比较。例如，假设你想检查一系列输入是否包含相邻重复项，例如 1 7 2 9 9 4 9。

现在你面临一个挑战。考虑用于读取一个值的典型循环：

    double input;
    while (cin >> input)
    {
        // Now input contains the current input
        ...
    }

要比较相邻输入，请将前一个输入存储在变量中。

你如何将当前输入与前一个输入进行比较？在任何时候，input 都包含当前输入，并覆盖前一个输入。

答案是存储前一个输入，如下所示：

    double input;
    double previous;
    while (cin >> input)
    {
        if (input == previous) { cout << "Duplicate input" << endl; }
        previous = input;
    }


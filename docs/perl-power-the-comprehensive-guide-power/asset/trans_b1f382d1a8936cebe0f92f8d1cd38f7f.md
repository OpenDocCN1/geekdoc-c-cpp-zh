

## 类中的一系列

从另一个角度来看，你可以指定一系列字符类。在以下示例中，你搜索可能用于组成单词 yes 的任何大小写字母组合。

```
print "Match of yEs found $NL"
if ("yES" =~ m/[yY][eE][sS]/);
```

以下是 Listing15_06 中示例 2 的输出：

```
Match of yEs found
```

## 多个句点的使用

你使用句点来表示一个字母。你可以使用两个或多个句点来表示多个字母。这些字符允许任何类型的字符。在 Listing15_06 的示例 3 中，你在 p 后面使用句点。这样，你允许任何两个任意类型的字符。

```
$TestString = "Colorado is complemented by its capitol".
              "building and Denver, a capital city much complimented.";
if ($TestString =~ m/([a-z]p..ol)/){
    print "\nFound: $1";
}
```

以下是 Listing15_06 中示例 3 的输出：

```
Found: capitol
```

## 克服大小写问题

你可以在匹配后使用小写的“i”来指示匹配不考虑字母的大小写。Listing15_06 的示例 4 即使搜索词是小写而被搜索词是大写，也会返回 true；

```
print "5 Match YES found\n"
if ("YES" =~ m/yes/i);
```

以下是 Listing15_06 中示例 4 的输出：

```
Yes okay.
```

## 搜索数字

你可以使用范围来搜索术语中的数字。创建范围时，你使用两个数字来指定范围。你在它们之间放置一个短划线来表示你正在建立一个范围。在 Listing15_06 的示例 5 中，你创建一个表达式来建立从 0 到 9 的范围。

```
print "Topic0 matched $NL"if ("topic0" =~ m/[0-9]/);
print "Topic7 matched $NL"if ("topic7" =~ m/[0-9]/);
print "Topic8 matched $NL"if ("topic8" =~ m/[0-9]/);
print "Topic08 matched $NL"if ("topic08" =~ m/0[1-9]/);
```

在最后一个示例中，0 在括号之前，因此只有当搜索的数字前面有一个 0 时，搜索结果才为 true。以下是 Listing15_06 中示例 5 的输出：

```
Topic0 matched
Topic7 matched
Topic8 matched
Topic08 matched
```

## 使用插入符号进行否定

类范围中的插入符号 (^) 运算符具有特殊含义。它用于否定紧随其后的字母。例如，^c 表示“不是 c”。Listing15_06 的示例 6 遍历一个数组并搜索任何不以 c 开头的单词。

```
@ThreeLetters = qw(mat cat bet sat rat fat net);
foreach $Word (@ThreeLetters){
print "Matched $Word \n"if ($Word =~ m/[^c]at/);
}
```

该表达式匹配所有以 at 结尾的术语，但 cat 除外。以下是 Listing15_06 中示例 6 的输出：

```
Matched mat
Matched sat
Matched rat
Matched fat
```

## 排除一系列字符

作为示例 6 的变体，假设搜索涉及排除一系列 *字符*。插入符号可用于完成此操作。在 Listing15_06 的示例 7 中，匹配遍历一个数组并排除包含 2 到 4 范围内数字的项。

```
@NumWords = qw(rat1 rat2 rat3 rat4 rat5);
foreach $Word (@NumWords){
print "Match $Word found\n" if ($Word =~ m/rat[^2-4]/);
}
```

以下是 Listing15_06 中示例 7 的输出：

```
Match rat1 found
Match rat4 found
Match rat5 found
```

## 特殊字符和其他操作

你可以使用许多特殊字符来增强正则表达式的功能。表 15.2 列出了其中几个字符。以下各节提供了它们使用的一些示例。

**表 15.2  特殊字符**

| 字符 | 讨论 |
|---|---|
| `\d` | 这匹配任何数字。 |
| `\D` | 这匹配任何不是数字的字符。 |
| `\w` | 这匹配单词字符。 |
| `\W` | 这匹配任何非单词字符。 |
| `\s` | 任何空白字符 – `\t` `\n` `\f` `\r`（空格、制表符、回车、换页、回车）。 |
| `\S` | 任何非空白字符。 |
| `.` | 句点匹配除换行符 (`\n`) 之外的任何字符。 |
| `\n` | 一个换行符字符。 |
| `\t` | 一个制表符字符。 |
| `\z` | 匹配字符串末尾。 |

## 匹配数字

你可以使用特殊字符 `\d` 来匹配数字。在以下示例中，对于包含任何数字的任何字符串都会发生匹配。换句话说，匹配涉及对字符串中所有字符的评估。

```
$TestString = "This is 3 shades of gray.";
if ($TestString =~ /\d/) {
    print "$NL String has a number.";
}
```

为了进一步讨论，还要考虑使用 `\d` 相当于另一个更复杂的表达式：`[0-9]+`。换句话说，你正在检查给定范围内的任何数字。以下是 Listing15_07 中示例 1 的输出：

String has a number.

## 匹配非数字

你可以使用 `\D` 排除数字。被排除的数字是 0–9。在以下示例中，表达式从字符串中筛选出不是数字的字符。如果正在验证数值输入，这可能会很有用：

```
$TestString = "345678";
if ($TestString =~ /\D/) {
    #won't be true
    print "$NL String is okay.";
} else {
    #so
    print "$NL String should not be a number.";
}
```

以下是 Listing15_07 中示例 2 的输出：

String should not be a number.

## 使用分组 ()

分组括号 `()` 允许你建立可用于匹配的替代模式。创建的语句类似于 OR 语句：

```
$TestString = "This is with shades of gray.";
if ($TestString =~ m/(alive|with) shades/) {
    print "$NL Match of (alive | with) shades";
}
```

以下是 Listing15_07 中示例 3 的输出：

Match of (alive | with) shades

## 包含特定术语的句子

可以搜索字符串数组，查找包含给定单词的句子。此代码示例打印两个句子：

```
$TestArray[0] = "The earth is alive with care.";
$TestArray[1] = "The earth is teeming with care.";
$TestArray[2] = "The earth is pulsating with care.";

for($iv = 0; $iv < 3; $iv++) {
    if($TestArray[$iv] =~ m/(alive|pulsating)/) {
        print "$NL Found $TestArray[$iv] $NL";
    }
}
```

以下是 Listing15_07 中示例 4 的输出：
Found The earth is alive with care.
Found The earth is pulsating with care.

请注意，使用分组时，一旦出现第一个匹配项，匹配就会返回。在以下示例中，匹配的是 c，而不是整个单词：
$Word = "cats";
print "$NL $Word (cat) found." if($Word =~ m/(c|ca|cat|cats)/);

以下是 Listing15_07 中示例 5 的输出：
cats (cat) found.

## 结论

本章提供了应被视为正则表达式入门的内容。由于每个操作系统和许多编程语言（例如 Java、JavaScript 和 C#）都提供某种形式的正则表达式功能，因此无论你作为程序员朝哪个方向发展，你对 Perl 正则表达式的工作都将证明是有用的。同样，正则表达式对于使用 Unix/Linux 系统来说也是必不可少的。

一般来说，本章强调了匹配和替换的基础知识，这些知识可能应用于标准编程活动，仅限于做出选择语句或控制重复语句。你可以轻松地将此入门知识扩展到许多方向，包括创建帮助你处理文件 IO 的文件。

本页故意留空

TEAM LinG

# 索引

+   A
+   abs() 函数，102
+   抽象，函数，297–300
+   累加器，170–173
+   ActivePerl 解释器，4
+   ActiveState，6–7, 11–14
+   Alcott, Amos，235
+   匿名数组，352–355
+   匿名哈希，356–358
+   Apache Server，3, 6–7
+   Apache 软件基金会，6
+   应用程序，控制结构，255–296
+   块，282–285
+   continue 运算符，257, 285–288
+   控制值，257
+   do ... until 语句，256, 277–280
+   do ... while 语句，256, 273–275
+   for 语句，257–260
+   foreach 语句，280–282
+   处理程序，269
+   增量表达式，257
+   无限循环，262–270
+   last 运算符，257, 260–261, 282–288
+   限制，257
+   循环控制，257, 262–270
+   next 语句，257, 285–288
+   redo 运算符，257, 282–285
+   重复，255–260
+   system() 函数，268
+   until 语句，256, 275–277
+   while 语句，256, 270–273, 285–296
+   参数数组，309–313
+   参数，函数，301
+   接受，309–313
+   无，303–306
+   算术运算符，101
+   数组，8–9, 127–178
+   添加元素，128–131
+   访问元素，138–139
+   匿名，352–355
+   串联，135–137
+   数据容器，153–178
+   累加器，170–173
+   添加元素，166–168
+   动态数组，168–169
+   提取元素，160–162
+   插入元素，162–164
+   连接元素，159–160

+   数字，排序，157
+   队列，174–178
+   删除元素，164–166
+   反转元素，153–154
+   穿梭，169–170
+   排序元素，155–156
+   分割字符串，158–159
+   栈，169–173
+   隐式赋值，140
+   初始化问题，132–135
+   迭代，135–137
+   返回，324–328
+   传递，313–316, 347–349
+   填充，143–144
+   qw() 函数，143–144
+   切片，141–142
+   拼接，144–152
+   基本，144–146
+   末尾元素，删除，149–150
+   插入，150–152
+   范围，146–148
+   范围，删除，148–149
+   选定集，146–148
+   交换，142–143
+   值，赋值，129–130
+   值，打印，130–131
+   值，检索，131
+   ASCII 转换，119–121
+   ASCII 文本，5
+   ASCII 字符，408
+   赋值运算符，40, 102
+   关联容器，179
+   结合性，100–101
+   星号 (*)，410–411
+   at (@) 符号，8
+   atan2() 函数，102
+   Auden, W. H.，93
+   增量运算符，102
+   B
+   基础，1–9
+   社区，4–5
+   复杂性，5
+   派生，5–6
+   标识符，8–9
+   功率，2–4


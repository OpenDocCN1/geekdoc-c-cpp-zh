

# 隐藏字符和字符串

```perl
if($CoupletAlineA eq $CoupletBlineA)
{
    #Does not print since equal operator returns false
    print "\nLines are the same."
}

if($CoupletAlineA ne $CoupletBlineA)
{
    #Does since the not equal operator returns true
    print "\nLines are not the same."
}
```

Listing04_06 与 Listing04_05 相同，不同之处在于包含 `chomp()` 函数的两行。与注释 #1 相关的行中出现了对该函数的调用。图 4.8 显示了输出的变化。现在，解释器不再发现两组行不相等，而是发现它们相等。行的长度现在相同。它们在可见和不可见方面都相等。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_89_0.png)

**Figure 4.8**
解释器现在发现行相等。

除了删除隐藏字符外，`chomp()` 函数还会返回值。如果 `chomp()` 函数发现你提供的字符串包含隐藏的换行符，则返回值为 1。如果 `chomp()` 函数发现你作为参数提供的字符串不包含隐藏的换行符，则返回值为 0。在与注释 #1 相关的行中，Listing04_07 向你展示了 `chomp()` 函数的返回值。

```perl
#Listing04_07

#1 Set up lines with and without hidden end of line characters
$CoupletAlineA= "Sighs for folly said and done\n";
$CoupletAlineB= "Twist our narrow days\n";
```

chomp() function to a string after you have used it to delete a newline character, it does not truncate the string.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_91_0.png)

> **Figure 4.9**  
> `chomp()` 函数的返回值确认是否存在换行符。

## 使用 chop() 函数

chop() 函数允许你从字符串末尾删除一个字符。每次调用它时，它都会继续从字符串中删除字符。在这方面，它与 chomp() 函数不同，chomp() 函数仅删除换行符。Listing04_08 提供了一个示例，说明其工作原理：

```perl
#Listing04_08

#1 Set up a few lines from Hart Crane's
#"For the Marriage of Faustus and Helen"
# Simultaneously print the lines to show the lines
print (<<HCRANE);
        The mind has shown itself at times
        Too much the baked and labeled dough
        Divided by accepted multitudes.
HCRANE
#2 Assign the last line to a separate string
#Add a newline character
$LastLine = "Divided by accepted multitudes.\n";

#3 Employ the chop() function to show the string being truncated
print "\n 0 No action taken: $LastLine";
print "\nLength before actions: " . length($LastLine);
$ChopReport = chop($LastLine);
#show no return value
print "\n No return value:" . $ChopReport;
print "\n 1 EOL removed: $LastLine";
```

```perl
print "\nLength after the first action: " . length($LastLine);
chop($LastLine);
print "\n Now the characters....:\n";
print "\n 2 $LastLine";
chop($LastLine);
print "\n 3 $LastLine";
chop($LastLine);
print "\n 4 $LastLine";
```

Listing04_08 中的注释 #1 介绍了 Hart Crane 诗歌中的一段文字。在注释 #2 之后的行中，你将段落的最后一行赋值给标量 $LastLine。请注意，你在字符串末尾附加了一个换行符。在注释 #3 处，涉及 `chop()` 函数的截断操作开始。你调用 `print()` 函数来显示 `chop()` 函数不提供返回值。同时，它删除隐藏字符。然后，在随后对 `chop()` 的调用中，你继续截断字符串。图 4.10 显示了 Listing04_08 生成的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_92_0.png)

**Figure 4.10**  
每次调用 `chop()` 函数时，它都会删除一个字符。

## 命令行交互

虽然你使用 Perl 编写的许多程序不太可能涉及命令行交互，但了解如何使用命令行仍然很有价值，以便你可以测试程序。Listing04_09 提供了一个支持用户交互的程序的基本示例。

```perl
#Listing04_09
#Respond to a command prompt
print "Type your name and press Return: ";
```

```perl
#1 Prompt for information from the user
$NameTyped = <STDIN>;
print "\nYour name: " . $NameTyped;
```

你可以编写在命令行运行的程序，而不需要包含 Listing04_09 的前两行，但包含它们也无妨，以符合规范。在与注释 #1 相关的行中，你输入一行包含句柄 (<STDIN>) 的内容。句柄允许你输入信息。在此示例中，你输入的信息存储在标量 ($NameTyped) 中。然后，你使用 print() 函数显示该信息。

句柄将在后续章节中更详细地介绍，但目前请注意，表达式 <STDIN> 代表一种惯例。如果程序行仅包含小于号 (<) 和大于号 (>) 符号，而没有句柄标识符 (STDIN)，解释器不会发现程序有任何问题，你仍然可以按照提示输入内容。

要运行程序，你可以像运行任何其他 Perl 程序一样在 DOS 提示符下输入并执行它。如果你从 DzSoft Perl Editor 运行程序，请选择 Run > Run in command prompt 或按 Shift + F9。然后，按照提示在提示符处输入你的名字并按 Return。程序会显示你的名字。如果你再次按 Return，程序将退出。图 4.11 说明了程序的执行过程。（有关设置具有浅色背景和深色字体的会话，请参见侧边栏。）

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_93_0.png)

**Figure 4.11**  
程序提示你输入姓名，然后回显你的输入。

## 设置 DzSoft DOS 窗口

如果你从 DzSoft Perl Editor 执行命令提示符程序，可以更改窗口，使其永久显示白色背景和深色字体。如果你在 DzSoft Perl Editor 中按 Shift + F9（或从 DOS 提示符或 Windows 资源管理器执行程序），你会看到图 4.12 顶部所示的 DOS 窗口。

要更改背景，以便在浅色背景上看到深色字体，请右键单击命令提示符窗口上的控制图标并选择 Properties。然后，你会看到图 4.12 中间所示的对话框。单击 Colors 选项卡。然后单击 Screen Background 的单选按钮。单击调色板上的白色框以设置背景颜色。然后单击 Screen Text 的单选按钮。单击调色板上的黑色框以设置文本颜色。单击 OK 关闭对话框。当打开确认更改的对话框时，单击 Save Properties for Future Windows with the Same Title 按钮。

## 字符索引

`index()` 函数返回字符串在字符串中的起始位置。`index()` 函数的名称源自 _数组_ 的 _索引_。如图 4.13 所示，数组类似于抽屉柜。你可以通过编号来识别抽屉。字符串是字符数组，因此你可以通过其索引号来识别每个字符。数组索引从 0 开始。

要使用 `index()` 函数，你需要向其提供三个参数。第一个参数是你要搜索的字符串。这可以是标量或字符串字面量。第二个参数是目标字符串——你要搜索的字符串。最后一个参数是 _偏移量_。偏移量指示你希望作为搜索起始点的目标字符串中的位置。你使用一个标识目标字符串中索引的整数来标识此位置。The

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_94_0.png)

## Figure 4.13

数组有索引，就像抽屉柜有抽屉一样。

offset 标识相对于字符串起始索引的位置，而字符串的起始索引始终是零 (0) 索引。如图 4.14 所示，`index()` 函数默认从目标字符串的开头 (0 索引) 开始搜索。当 `index()` 函数找到它要查找的字符串时，它会返回目标字符串中标记你要查找的字符串开头的位置。

## Figure 4.14

`index()` 函数从你指示的起始索引开始搜索，并找到你提供的搜索字符串的第一个出现位置。

## 搜索算法

你向 `index()` 函数提供的参数反映了你可以用于搜索大量文本以查找给定字符串重复出现的算法的逻辑。当你在文本中搜索给定字符串的出现时，你从文本的开头开始。你在文本中移动，直到找到你要查找的字符串。如前所述，当你找到你要查找的字符串时，你会报告文本中你要查找的字符串开始的索引。

假设文本中存在多个搜索字符串实例。解决此问题的方法涉及使用新的起始 (offset) 位置继续搜索。要继续搜索，你使用已找到字符串的报告起始位置并加一。然后，你将这个新的起始位置传递给另一个对 `index()` 函数的调用。图 4.15 说明了其工作原理。

| Bureau   | Array   |
|----------|---------|
| drawer 0 | index 0 |
| drawer 1 | index 1 |
| drawer 2 | index 2 |
| drawer 3 | index 3 |
| drawer 4 | index 4 |

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 |
|-------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|       | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| $Str  | s | i | g | h | s |   | f | o | r |   | f | o | l | l | y |   | s | a | i | d |   | a | n | d |   | d | o | n | e |
|       |   |   |   |   |   |   | f | o |   |   | f | o | l | l | y |   |   |   |   |   |   |   |   |   |   |   |   |   |   |


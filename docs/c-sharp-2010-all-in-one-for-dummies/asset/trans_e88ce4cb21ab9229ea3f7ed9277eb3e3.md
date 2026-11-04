
```
compare(string s1, string s2)
{
    // Loop through each character of the strings until
    // a character in one string is greater than the
    // corresponding character in the other string.
    foreach character in the shorter string
        // quit if (s1's character > s2's character when treated as a number)
        return 1
        if (s2's character < s1's character)
            return -1
    // Okay, every letter matches, but if the string s1 is longer,
    // then it's greater.
    if s1 has more characters left
        return 1
    // If s2 is longer, it's greater.
    if s2 has more characters left
        return -1
    // If every character matches and the two strings are the same
    // length, then they are "equal."
    return 0
}
```

因此，“abcd”大于“abbd”，而“abcde”大于“abcd”。更常见的是，你并不关心一个字符串是否大于另一个字符串，而只关心这两个字符串是否相等。

你在执行排序时确实需要知道哪个字符串更大。

Compare() 操作在两个字符串 identical 时返回 0。下面的测试程序使用 Compare() 的相等特性，在程序遇到特定字符串或字符串时执行特定操作。

BuildASentence 提示用户输入文本行。每一行都会与前一行连接起来构建一个句子。如果用户输入单词 EXIT、exit、QUIT 或 quit，则此程序退出。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_74_0.png)

```
// BuildASentence -- The following program constructs sentences
// by concatenating user input until the user enters one of the
// termination characters. This program shows when you need to look for
// string equality.
using System;
namespace BuildASentence
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Each line you enter will be "
                + "added to a sentence until you "
                + "enter EXIT or QUIT");
            // Ask the user for input; continue concatenating
            // the phrases input until the user enters exit or
            // quit (start with an empty sentence).
            string sentence = "";
            for ( ; ; )
            {
```

~~~csharp
// Get the next line.
Console.WriteLine("Enter a string ");
string line = Console.ReadLine();
// Exit the loop if line is a terminator.
string[] terms = { "EXIT", "exit", "QUIT", "quit" };
// Compare the string entered to each of the
// legal exit commands.
bool quitting = false;
foreach (string term in terms)
{
    // Break out of the for loop if you have a match.
    if (String.Compare(line, term) == 0)
    {
        quitting = true;
    }
}
if (quitting == true)
{
    break;
}
// Otherwise, add it to the sentence.
sentence = String.Concat(sentence, line);
// Let the user know how she's doing.
Console.WriteLine("\nYou've entered: " + sentence);
}
Console.WriteLine("\n\nTotal sentence:\n" + sentence);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
~~~

在提示用户输入程序期望的内容后，程序创建一个名为 sentence 的空初始句子字符串。从那里开始，程序进入无限循环。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_75_0.png)

控制 while(true) 和 for(;;) 会无限循环，或者至少循环足够长的时间以便某个内部 break 或 return 将你中断。两个循环是等价的，实际上你会看到它们两者。（循环在本书第 5 章中介绍。）

BuildASentence 提示用户输入一行文本，程序使用 ReadLine() 方法读取该行。读取该行后，程序使用前例中加粗的行检查它是否为终止符。

程序的终止部分定义了一个名为 terms 的字符串数组和一个 bool 变量 quitting，初始化为 false。terms 数组的每个成员都是你要查找的字符串中的一个。任何这些字符串都会导致程序比被迫编写 COBOL 的程序员更快地退出。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_75_1.png)

程序必须同时包含 "EXIT" 和 "exit"，因为 Compare() 默认将这两个字符串视为不同。（按程序的写法，这只是 exit 的两种拼写方式。诸如 "Exit" 和 "eXit" 这样的字符串不会被识别为终止符。）你也可以使用其他字符串操作来检查 exit 的各种拼写。我将在下一节中向你展示这一点。

终止部分遍历目标字符串数组中的每个字符串。如果 Compare() 报告与任何终止短语匹配，则 quitting 设置为 true。如果在终止部分之后 quitting 仍然为 false 且 line 不是终止符字符串之一，则它会使用 String.Concat() 方法连接到句子的末尾。程序输出即时结果，只是为了让用户可以看到正在发生的事情。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_76_0.png)

TIP 通过数组迭代是查找各种可能值中的一个的经典方法。（我将在下一节中向你展示另一种方法，并在第二册中展示一种更酷的方法。）

以下是 BuildASentence 程序的示例运行：

```
Each line you enter will be added to a
sentence until you enter EXIT or QUIT
Enter a string
Programming with

You've entered: Programming with
Enter a string
C# is fun

You've entered: Programming with C# is fun
Enter a string
(more or less)

You've entered: Programming with C# is fun (more or less)
Enter a string
EXIT

Total sentence:
Programming with C# is fun (more or less)
Press Enter to terminate...
```

我已将我的输入标记为粗体以便于阅读输出。

## 你想要区分大小写的比较还是不区分大小写的比较？

上一示例中使用的 Compare() 方法将 "EXIT" 和 "exit" 视为不同的字符串。然而，Compare() 方法有一个第二个版本，其中包含第三个参数。该参数指示比较是否应忽略字母大小写。true 表示“忽略”。

BuildASentence 示例中冗长的终止部分的以下版本无论传递的字符串是大写、小写还是两者组合，都会将 quitting 设置为 true：

```
    // Indicate true if passed either exit or quit,
    // irrespective of case.
    if (String.Compare("exit", source, true) == 0) ||
        (String.Compare("quit", source, true) == 0)
    {
        quitting = true;
    }
```

这个版本比之前的循环版本更简单。此代码无需担心大小写，并且可以使用单个条件表达式，因为现在它只需要考虑两个选项而不是更长的列表：QUIT 或 EXIT 的任何拼写变体。

## 如果我想切换大小写呢？

你可能对字符串中的所有字符（或仅一个）是大写字符还是小写字符感兴趣。而且你可能需要从一种转换为另一种。

### 区分全大写和全小写字符串

我几乎不愿意提起，但你可以使用 switch 命令（参见本书第 5 章）来查找特定字符串。通常，你使用 switch 命令将计数数字与一组可能值进行比较；然而，switch 也适用于字符串对象。此版本的 BuildASentence 中的终止部分使用 switch 构造：

```
    switch(line)
    {
        case "EXIT":
        case "exit":
        case "QUIT":
        case "quit":
            return true;
    }
    return false;
```

这种方法之所以有效，是因为你只比较有限数量的字符串。for 循环为搜索字符串值提供了更灵活的方法。使用上一节中的不区分大小写的 Compare() 使程序在理解用户方面具有更大的灵活性。

### 将字符串转换为大写或小写

假设你有一个小写字符串并且需要将其转换为大写。你可以使用 ToUpper() 方法：

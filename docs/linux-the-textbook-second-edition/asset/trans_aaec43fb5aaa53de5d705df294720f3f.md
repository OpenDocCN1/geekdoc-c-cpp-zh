

```
then
    echo "Good input!"
exit 0
./debug_demo: 9: debug_demo: Syntax error: end of file unexpected (expecting "fi")
$ sh -xv debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
+ echo -e Enter a digit: \c
+ echo -e Enter a digit: read var1
+ read var1
4
if [ "$var1" -ge 1 -a "$var1" -le 9 ]
then
    echo "Good input!"
fi
+ [ 4 -ge 1 -a 4 -le 9 ]
./debug_demo: 5: debug_demo: [4: not found
exit 0
+ exit 0
$ ./debug_demo
Enter a digit: 4
Good input!
$
```

你也可以使用 Bash 调试器项目 bashdb 来调试 Bash 脚本。就像用于 C/C++ 程序的 GNU 调试器 gdb 一样，bashdb 允许你逐行单步执行 Bash 脚本、设置断点、执行回溯、检查变量值、列出程序语句等。它并非随所有 Linux 发行版一起打包。如果你的系统上未预装，请让系统管理员为你安装。

下面的章节练习旨在增强你对中断处理和 Bash 调试功能的理解。

## 练习 13.14

在你的 Linux 系统上测试 trap_demo 和 canleave 文件中的脚本。它们按预期工作吗？确保你理解它们。如果你的版本不能正常工作，请使用 sh -xv 命令来调试它们。

## 总结

Bash 没有内置的用于算术、逻辑和移位操作的数值整数数据处理能力。要对整数数据执行算术和逻辑操作，可以使用 let 或 expr 命令。可以使用 shell 展开 $((expression)) 来执行数值表达式求值。你也可以使用 bc 工具来求值任意精度的数学表达式。它允许交互式求值以及使用它支持的语言编写脚本，其特性和构造与 C 语言非常相似。

Bash 支持一维数组。它允许你使用 declare -a、local -a 和 readonly -a 命令，或 array_name[subscript]=value 语法来声明局部和全局数组。你可以使用语法 name=(value1 ... valueN) 来初始化一个数组，其中 value1 的形式为 [subscript]=string，例如 Fibonacci=(0 1 1 2 3 5 8 13 21) 或 names=("Xi Jinping" "Tom Nelson" "Muhammad Yousaf" "Ravi Shankar" "Zach Goldberg" "Akihito")。你可以使用 ${name[subscript]} 语法来索引数组。

Bash 的 here document 功能允许脚本中命令的标准输入附加到脚本中的数据。使用此功能可使程序更高效，因为无需额外的文件相关操作，如文件打开和读取，因为数据在脚本文件内，并且在脚本加载时应已加载到主内存中。

Bash 还允许用户编写忽略信号（如键盘中断 <Ctrl+C>）的程序。此有用的功能可用于在程序中间更新文件时禁用程序终止等。trap 命令可用于调用此功能。

Bash 允许使用函数，包括参数传递和访问函数的返回值。局部变量和全局变量的作用域规则定义明确。

Bash 具有强大的 I/O 功能，允许显式处理文件。exec 命令可用于打开文件以供读取或写入，并为其关联一个称为文件描述符的小整数。命令 exec n< file 打开文件以供读取并分配文件描述符 n。命令行 exec n> file 打开文件以供写入并分配文件描述符 n。此功能允许编写处理文件的脚本。命令行 exec n<&- 可用于关闭描述符为 n 的文件。exec 命令提供各种其他文件相关功能，包括打开 here document 并为其分配文件描述符，这允许在脚本中的任何位置使用 here document。

Bash 程序可以使用 sh 命令的 -x 和 -v 选项进行调试。此技术允许在变量替换后但在执行前查看用户脚本中的命令。你也可以使用 bashdb 调试 Bash 脚本，其功能与第 14 章中讨论的用于 C/C++ 的 GNU 调试器 gdb 相似。

## 问题与练习

- 1. 为什么需要 expr 命令？
- 2. 修改 num_array_demo 脚本以显示给定 Fibonacci 数字的平方和。
- 3. 编写一个 Bash 脚本 Fibonacci_series，它将整数 N 作为唯一命令行参数并显示前 N 个 Fibonacci 数。
- 4. 什么是 here document？为什么它有用？
- 5. 编写一个 Bash 脚本 cv，它将立方体的边长作为命令行参数并显示立方体的体积。
- 6. 修改第 13.2 节中的 countup 脚本，使其接受两个整数命令行参数。脚本在第一个数字小于第二个数字时按升序显示两个整数之间的数字（包括两个数字），如果第一个数字大于第二个数字则按降序显示。命名脚本为 count_up_down。
- 7. 给出两个 Bash 命令分别在不使用精度和精度达到五位小数的情况下求值以下表达式。显示命令及其输出。
  a. 97.03*57.71/23.97
  b. 23.4+93.17-61.721/13.97*13
- 8. 使用 bc 执行以下任务。在 Bash 下显示命令及其输出。
  a. 将二进制 10111011 转换为等价的十进制和十六进制数
  b. 将十进制 10111011 转换为等价的二进制、八进制和十六进制数
  c. 将二十进制 10111011 转换为等价的十进制、二进制、八进制和十六进制数
- 9. 以下命令的输出是什么？解释每个输出。
  a. echo "var=25;++var" | bc
  b. echo "var=25;var++" | bc
  c. echo "var=700;var%=9;var" | bc
  d. echo "var=25;var^=3;var" | bc
  e. echo "5 &&& 50" | bc
  f. echo "5 || 50" | bc
  g. echo "0 || 0" | bc
  h. echo "1 || 1" | bc
  i. echo "! 0" | bc
  j. echo "obase=2;15" | bc -l
  k. echo "ibase=2;1111" | bc -l
  l. echo "ibase=2;obase=8;1110" | bc -l

10. 编写一个 Bash 脚本，提示你输入用户 ID 并显示你的登录名、你的姓名和你的主目录。

11. 编写一个 Bash 脚本，它将整数列表作为命令行参数并显示它们的平方列表以及平方数列表的总和。

12. 编写一个 Bash 脚本，它将机器名作为参数并显示一条消息告知你主机是否在本地网络上。

13. Linux 中的信号是什么？Bash 脚本中可以拦截哪些类型的信号？

14. 编写一个 Bash 脚本，它将文件名和目录名作为命令行参数，如果在给定目录下找到该文件并且是普通文件，则删除该文件。如果文件（第一个参数）是目录，则删除它（包括其下的所有文件和子目录）。

15. 编写一个 Bash 脚本，它将目录作为参数并删除其下所有具有 .o、.ps 和 .jpg 扩展名的普通文件。如果未指定参数，则使用当前目录。

16. 增强第 13.6 节中的 diff2 脚本，使其显示两个文件不同的行号。

17. 增强问题 11 中的 diff2 脚本，以便如果仅向其传递一个文件作为参数，则使用标准输入作为第二个文件。

18. 为第 12 章问题 16 编写一个 Bash 脚本，但使用函数来实现各种选项的服务代码。

19. 假设函数 f 首先被定义，然后 f 被定义为变量。在提供第二个定义后，f 会引用函数还是变量？为什么？展示一个 shell 会话来支持你的答案。

20. Bash 中如何将参数传递给函数？

21. 编写一个 Bash 脚本实现以下菜单选项：
a. 显示你的系统使用的 CPU
b. 显示你的计算机使用的操作系统的名称
c. 在屏幕上用垂直制表符分隔显示 a 和 b
d. 显示已在你的系统上执行的命令的完整路径名
e. 显示进程可打开的最大文件数
f. 显示用户在系统上可同时拥有的最大进程数
你的程序不应在信号 1、2、3、15 和 18 上终止。利用函数来显示程序菜单。
提示：查看以下命令的手册页：hash、ulimit、uname。

## 高级问题与练习

22. 给出第 13.2.2 节中用于显示前十个十进制数字的 for 循环的 while 循环等价形式，每行一个。



# 常用的选项/功能：

算术、关系和逻辑运算是最常用的：

- |  按位或
- &  按位与
- ^  按位异或（XOR）
- =, >, >=, <, <=, !=  整数比较运算符：等于、大于、大于等于、小于、小于等于、不等于
- +, -, *, /, %  整数算术运算符：加、减、乘、整数除法（返回商）、取余

## 其他有用的运算符有

- **arg1 : arg2**
  在“arg1”中搜索模式“arg2”（一个正则表达式）。如果“arg2”被 \( 和 \) 包围，则返回“arg1”中匹配的部分；否则，返回匹配的字符数。默认情况下，搜索从“arg1”的第一个字符开始。在字符串开头加上 .* 以匹配字符串的其他部分。

- **substr string start length**
  搜索并返回“string”中从“start”开始、长度为“length”个字符的一部分。如果“start”或“length”不是数字或为负数，则返回 null。

- **index string character-list**
  在“string”中搜索“character-list”中第一个可能的字符，并返回其位置（字符串中的第一个字符位于位置 1）。如果未找到任何字符，则返回 0。

- **length string**
  返回“string”的长度（即其中的字符数）。

诸如 * 之类的 Shell 元字符必须在表达式中进行转义，以便按字面意义处理，而不是作为 Shell 元字符。在以下会话中，第一个 expr 命令将 Shell 变量 var1 的值增加 1。第二个 expr 命令计算 var1 的平方。最后两个 echo 命令展示了使用 expr 命令对 var1 执行整数除法和整数取余运算。

```
$ var1=10
$ var1=`expr $var1 + 1`
$ echo $var1
11
$ var1=`expr $var1 \* $var1`
$ echo $var1
121
$ echo `expr $var1 / 10`
12
$ echo `expr $var1 % 10`
1
$
```

以下示例演示了 expr 命令在字符串处理中的用法。第一个命令显示字符串“Hello, World.”中字符“r”的位置索引（值 10）。第二个命令显示 0，表示在给定的字符集（“i”和“p”）中没有在字符串中找到任何字符。第三个命令用于显示字符串的长度，第四个命令用于显示字符串“Hello, World.”的子字符串，从位置 8 的字符开始，长度为 5。第五和第六个 expr 命令表明，字符串变量可以代替实际字符串使用。变量展开必须按所示用双引号括起来；否则会引发异常。

```
$ expr index "Hello, World." arp
10
$ expr index "Hello, World." ip
0
$ expr length "Hello, World."
13
$ expr substr "Hello, World." 8 5
World
$ greeting="Hello, World."
$ expr length "$greeting"
13
$ expr substr "$greeting" 8 5
World
$
```

我们现在讨论几个使用 expr 命令进行算术表达式求值的脚本。下面的 countup 脚本将一个整数作为命令行参数，并以升序在一行中显示从 1 到给定数字的数字范围。在脚本中，我们使用一个简单的 while 循环来显示当前数字（从 1 开始），然后计算下一个数字，直到当前数字大于作为命令行参数传入的数字。

```
$ cat countup
#!/bin/sh
if [ $# != 1 ]
then
    echo "Usage: $0 integer-argument"
    exit 1
fi
target="$1"    # Set target to the number passed at the command line
current=1       # The first number to be displayed
# Loop here until the current number becomes greater than the target
while [ $current -le $target ]
do
    echo -n "$current "
    current=`expr $current + 1`
done
echo    # Move cursor to the next line
exit 0
$ ./countup 5
1 2 3 4 5
$
```

下面的脚本 addall 将整数列表作为命令行参数，并显示它们的总和。while 循环将参数列表中的下一个数字加到运行总和（初始化为 0）上，更新已添加数字的计数，并将命令行参数向左移动一个位置。然后循环重复，直到命令行参数中的所有数字都被添加。代码之后的示例运行将前八个完全平方数的列表作为参数，并返回它们的总和。

```
$ cat addall
#!/bin/bash

# File Name:    ~/linux2e/chapter13/bash/addall
# Author:       Syed Mansoor Sarwar
# Written:      August 18, 2004
# Modified:     August 18, 2004; July 28, 2014; July 9, 2017
# Purpose:      To demonstrate use of the expr command in processing
#               numeric data
# Brief Description:
#               Maintain the running sum of numbers in a numeric
#               variable called sum, initialized to 0. Read the next
#               integer and add it to sum. When all the integers
#               specified as command line arguments have been read,
#               display the answer, and terminate the program. If
#       the program is run with no arguments, inform the
#       user of the command syntax.
if [ $# = 0 ]
then
        echo "Usage: $0 number-list"
        exit 1
fi
sum=0              # Running sum initialized to 0
count=0            # Count the count of numbers passed as arguments
while [ $# != 0 ]
do
        sum=`expr $sum + $1`       # Add the next number to the running sum
        count=`expr $count + 1`    # Update count of numbers added so far
        shift                       # Shift the counted number out
done
# Display final sum
echo "The sum of the given $count numbers is $sum."
exit 0
$ ./addall
Usage: ./addall number-list
$ ./addall 1 4 9 16 25 36 49 64
The sum of the given 8 numbers is 204.
$
```

尽管这个例子清晰地解释了数值数据处理，但它不过是一个整数加法机器。我们现在介绍一个更有用的例子，它使用了 Linux 文件系统。**fs**（代表文件大小）文件包含一个脚本，该脚本将目录作为可选参数，并返回其中所有非目录文件的大小（以字节为单位）。在某些 Linux 系统上，运行 fs 命令会调用 xfs。如果您的系统出现这种情况，请将此脚本的名称改为 **files**，或您喜欢使用的任何名称。

当您不带命令行参数运行该程序时，脚本会将当前目录作为参数。如果您使用多个命令行参数运行它，脚本会显示命令语法并终止。当您仅使用一个非目录参数执行它时，程序同样会显示命令语法并退出。如果程序使用不存在的文件作为参数运行，它会显示错误消息并终止。

此脚本的关键在于，当脚本以目录作为命令行参数运行时，会执行以下代码。

```
ls $directory | more |
while read file
do
    ...
done
```

此代码使用 ls 命令生成 *目录* 中的文件列表，使用 more 命令将该列表转换为每行一个文件名的列表，并使用 read 命令逐一读取列表中的每个文件名，直到列表中不再有文件。read 命令在读取一行时返回 true，在读取文件结束标记（eof）时返回 false。循环体——即 do 和 done 之间的代码——在文件是普通文件时将该文件大小加到运行总和。当目录列表中没有剩余名称时，程序会显示目录中所有非目录文件占用的总字节空间，然后终止。

如果 file 变量的值不是现有文件，`[ ! -e "$file" ]` 表达式将返回 false，并显示错误消息 Usage: fs [directory name]，如示例运行中所示，其中 **linux2e** 是一个不存在的目录。在某些系统上，消息可能显示 ./fs 而不是 fs，就像我们的会话中那样。`file="$directory"/"$file"` 语句用于构造相对于指定为命令行参数的目录的文件相对路径名。如果没有该语句，`set -- "ls -l "$file"` 命令只有在目录包含当前目录名称时才会成功。


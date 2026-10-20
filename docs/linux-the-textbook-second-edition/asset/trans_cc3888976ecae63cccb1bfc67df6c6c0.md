

![](img/2a18e06cd9c6395e451f26126ecba1fd_411_0.png)

图 13.4 在登录 shell 下执行 csh 和 exec < sample 命令。

```bash
$ exec > data
$ date
$ echo "Hello, world!"
$ uname -sm
$ exec > /dev/tty
$ date
Sun Jul  9 13:06:51 PKT 2017
$ more data
Sun Jul  9 13:06:25 PKT 2017
Hello, world!
Linux Mint18 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64
x86_64 x86_64 GNU/Linux
$
```

同样地，你可以使用以下命令重定向一段 shell 脚本的标准输出和标准错误：

```bash
exec > outfile 2> errorfile
```

在这种情况下，此行之后 shell 脚本的输出和错误信息分别被定向到 outfile 和 errorfile。 （显然，文件描述符 1 可以与 > 一起使用来重定向输出。）如果需要将输出重新连接到终端，可以使用

```bash
exec > /dev/tty
```

一旦此命令执行完毕，所有后续输出都将发送到监视器屏幕。同样地，你可以使用 exec 2> /dev/tty 命令将输出发送回显示屏幕。

考虑以下 shell 会话。当 exec.demo1 被执行时，file1 得到包含 Hello, world! 的行，file3 得到 file2 的内容，而 file4 得到行 This is great!。在命令 exec < file2 和 exec < /dev/tty 之间的 shell 脚本从 file2 读取输入。因此，命令 cat > file3 实际上是 cat < file2 > file3。cat > file4 命令在 exec < /dev/tty 命令执行后才执行，该命令将脚本的 stdin 重新连接到键盘，因此它从键盘读取输入。图 13.5 说明了 shell 脚本中三个 cat 命令的语义。

```bash
$ more exec.demo1
cat > file1
exec < file2
cat > file3
exec < /dev/tty
cat > file4
$ ./exec.demo1
Hello, world!
<Ctrl+D>
This is great!
<Ctrl+D>
$ more file1
Hello, world!
$ more file2
Contents of file2.
$ more file3
Contents of file2.
$ more file4
This is great!
$
```

![](img/2a18e06cd9c6395e451f26126ecba1fd_412_0.png)

**图 13.5** 在 shell 脚本内部 **stdin** 和 **stdout** 的分离与重新连接。

现在，我们开发一个 shell 脚本 diff2，它使用 Bash 的文件输入/输出 I/O 功能。它将两个文件作为命令行参数接收并逐行比较它们。如果文件相同，它会显示一条相应的信息并终止程序。如果一个文件比另一个小，它会显示一条告知你的信息并退出。一旦程序找到两个文件不同的行，它就会显示一条错误信息，告知你来自两个文件的不同行并终止。以下是脚本和一些示例运行：

```bash
$ cat diff2
#!/bin/bash
# File Name: ~/linux2e/chap13/bash/diff2
# Author:     Syed Mansoor Sarwar
# Written:    August 28, 2004
# Modified:   July 29, 2014; April 9, 2017
# Purpose:    To see if the two files passed as command line arguments
#            are same or different

# Brief Description:
#     Read a line from each file and compare them. If
#     the lines are the same, continue. If they are
#     different, display the two lines and exit. If one
#     of the files finishes before the other, display a
#     message and exit. Otherwise, the files are the
#     same; display an appropriate message and exit

if [ $# != 2 ]
then
        echo "Usage: $0 file1 file2"
        exit 1
elif [ ! -f "$1" ]
then
        echo "$1 is not an ordinary file"
        exit 1
elif [ ! -f "$2" ]
then
        echo "$2 is not an ordinary file"
        exit 1
else
        :
fi
file1="$1"
file2="$2"

# Open files for reading and assign them file descriptors 3 and 4

exec 3< "$file1"
exec 4< "$file2"

# Read a line each from both files and compare. If both reach EOF, then files
# are the same. Otherwise, they are different. 0<&3 is used to attach standard
# input of the read line1 command to file descriptor 3. 0<&4 is used to attach
# standard input of the read line2 command to file descriptor 4.

while read line1 0<&3
do
        if read line2 0<&4
        then
                # if lines are different, the two files are not the same
                if [ "$line1" != "$line2" ]
                then
                        echo "$1 and $2 are different."
                        echo " $1: $line1"
                        echo " $2: $line2"
                        exit 1
                fi
        else
                # if EOF for file2 reached, file1 is bigger than file2
                echo "$1 and $2 are different and $1 is bigger than $2."
                exit 1
        fi
done
# if EOF for file1 reached, file2 is bigger than file1. Otherwise, the two
# files are the same. 0<&4 is used to attach standard input of read to file
# descriptor 4
if read line2 0<&4
then
        echo "$1 and $2 are different and $2 is bigger than $1."
        exit 1
else
        echo "$1 and $2 are the same!"
        exit 0
fi

# Close files corresponding to descriptors 3 and 4
exec 3<&-
exec 4<&-
$ cat test1
Hello, world!
Not the same!
Another line.
$ cat test2
Hello, world!
$ cat test3
Hello, world!
Not the same!
$ cat test4
This is different file.
Hello, world!
$ ./diff2
Usage: ./diff2 file1 file2
$ ./diff2 test1 test2 test3
Usage: ./diff2 file1 file2
$ ./diff2 test1 test1
test1 and test1 are the same!
$ ./diff2 test1 test3
test1 and test3 are different and test1 is bigger than test3.
$ ./diff2 test1 test2
test1 and test2 are different and test1 is bigger than test2.
$ ./diff2 test2 test3
test2 and test3 are different and test3 is bigger than test2.
$ ./diff2 test1 test4
test1 and test4 are different.
    test1: Hello, world!
    test4: This is different file.
$
```

exec 命令用于打开和关闭文件。exec 3< "$file1" 和 exec 4< "$file2" 命令打开作为命令行参数传递的文件以供读取，并将它们分配文件描述符 3 和 4。从这一点开始，你可以使用这些描述符读取两个文件。命令 read line1 0<&3 和 read line2 0<&4 分别从文件描述符为 3 的 file1 和文件描述符为 4 的 file2 读取下一行。命令 exec 3<&- 和 exec 4<&- 关闭两个文件。第一个 if 语句 else 部分中的冒号符号 (:) 是一个空语句，只是简单地返回 true。你也可以为此目的使用 Bash 命令 true。顺便说一下，false 命令，如预期一样，返回 false。

在以下章节练习中，你将使用 exec 命令将你的 shell 的 I/O 重定向到普通文件。脚本内部的 I/O 重定向概念以及使用文件描述符的文件 I/O 也得到了加强。

## 练习 13.11

编写一个命令，将你的 shell 的 **stdin** 更改为名为 **data** 的文件，将 **stdout** 更改为名为 **out** 的文件，两者都在你当前的工作目录中。如果 data 文件包含以下行，执行命令后会发生什么？

```sh
echo -n "The time now is: "
date
echo -n "The users presently logged on are: "
who
```

## 练习 13.12

完成练习 13.11 中的步骤后，当你在 shell 提示符下输入命令时会发生什么？结果对你有意义吗？编写将你的环境恢复正常的命令。

## 练习 13.13

创建一个包含 diff2 脚本的文件并尝试使用不同的输入。

## 13.8 调试 Shell 脚本

你可以使用 sh 命令的 -x（echo）选项来调试 Bash 脚本。此选项在变量替换后但在执行之前显示脚本的每一行。你可以将 -x 选项与 -v（verbose）选项结合使用，以在执行前按脚本文件中出现的样子显示脚本的每一行。你也可以从命令行调用 sh 命令来运行脚本，或者可以将其作为脚本的一部分，如 #!/bin/sh -xv。在后一种情况下，在调试完成后删除 -xv 选项。

```bash
cat debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
read var1
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0
```

在以下会话中，我们展示了如何调试 shell 脚本。debug_demo 文件中的脚本提示你输入一个数字。如果输入的值在 1 到 9 之间，它会显示 Good input! 并退出。如果输入其他值，它就简单地退出。当脚本被执行并且你输入 4 时，它会显示消息 ./debug_demo: line 9: syntax error: unexpected end of file。此消息通常意味着你没有完全关闭某个控制结构，例如 if 语句中缺少 fi 或 while 语句中缺少 done。

```bash
$ cat debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
read var1
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0

$ ./debug_demo
Enter a digit: 4
./debug_demo: line 9: syntax error: unexpected end of file
$
```

我们使用 sh -xv debug_demo 命令调试程序。错误信息清楚地说明 if 语句中缺少 fi。我们在合适的位置插入 fi 并重新运行程序。我们现在得到错误信息 ./debug_demo: 5: debug_demo: [4: not found。运行跟踪的阴影部分显示了问题区域。在这种情况下，错误是由于 if 语句的条件问题而产生的。对阴影区域的更仔细检查显示 [ 与 4 之间缺少空格是问题所在。换句话说，[4 与 1 之间的比较是问题所在；它应该是 4 与 1 之间的比较。在我们通过将 ["$var1" 改为 [ "$var1" 解决此问题后，脚本正常工作。

```bash
$ sh -xv debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
+ echo -e "Enter a digit: \c"
read var1
+ read var1
4
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0
```


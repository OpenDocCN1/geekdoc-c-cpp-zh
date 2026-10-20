

Information about john
    John Doe        555.232.0000    johnd@somedomain.com

$ ./dext jim
Information about jim
    Jim Davis       777.000.9999    davis@great.adviser.edu

$ ./dext pohm masood carr
Information about pohm
    Art Pohm        333.000.8888    art.pohm@great.professor.edu

Information about masood
    Masood Shah     666.010.9820    shah@Garments.com.pk

Information about carr
    David Carr      777.999.2222    dcarr@net.net.gov
    Don Carr        555.111.3333    dcarr@old.hoggie.edu

$

## 13.6.5 函数中的参数传递

参数传递给函数的方式与命令行参数传递给 Bash 脚本的方式相同，即参数指定在函数名之后。在脚本内部，这些参数通过 `$1`、`$2` 等访问。函数可以返回一个值，该值可通过脚本中的 `$?` 访问。

在下面的示例中，

```
```bash
$ cat function_parameters
#!/bin/bash
#Passing parameters to functions

display_params () {
    if [ $# = 0 ]
    then
        exit 1
    fi

    while [ $# != 0 ]
    do
        echo $1
        shift
    done
}
# Function call
display_params "New York" London Paris
exit 0
$ function_parameters
New York
London
Paris
$
```
```

在 Bash 脚本中，变量默认是全局的。如果您想在函数中使用局部变量，可以在函数内部使用关键字 local 在变量名前声明它，如 `local var1` 或 `local var1=5`。局部变量在声明它的函数之外不可见。如果局部变量和全局变量同名，则在函数内部将访问局部变量。

在 variable_scope 脚本中，我们通过示例解释了变量作用域的概念。全局变量 *var1* 和 *var2* 分别初始化为 100 和 200。change_vars 函数中的局部变量 *var1* 初始化为 10。因此，在 change_vars 内部，var1 引用局部 var1，而 var2 引用全局 var2。调用 change_vars 后，局部 var1 消失，全局 var1 再次变得可见。由于 var2 是全局的，对它的任何更改在函数内部和外部都是可见的。以下会话中 variable_scope 的执行表明，在 change_vars 内部对 var1 所做的任何更改在函数外部不可见，但对 var2 所做的更改在函数内部和外部都是可见的。因此，全局 var1 的初始值在调用 change_vars 之前和之后仍然为 100，但 change_vars 内部将全局 var2 的值从 200 改为 300 的更改在函数调用返回后是可见的。

```
$ cat variable_scope
#!/bin/bash
#All variables are global unless they are explicitly specified as
#local with the keyword local, as in local var1 or local var1=5

var1=100
var2=200

change_vars () {
    local var1=10

    echo "Inside function: var1 is $var1 and var2 is $var2"
    var1=50
    var2=300
    echo "Inside function: var1 is $var1 and var2 is $var2"
}
echo "Before call to change_vars: var1 is $var1 and  var2 is $var2"
change_vars
echo "After call to change_vars: var1 is $var1 and var2 is $var2"
$ variable_scope
Before call to change_vars: var1 is 100 and  var2 is 200
Inside function: var1 is 10 and var2 is 200
Inside function: var1 is 50 and var2 is 300
After call to change_vars: var1 is 100 and var2 is 300
$
```

在下面的章节练习中，您将编写一个简单的函数和一个使用它的 Bash 脚本。

### Exercise 13.9

在您的系统上重现关于参数传递和变量作用域的先前 Bash 会话。它们是否重现了此处显示的结果？

### Exercise 13.10

编写一个名为 menu 的函数，显示以下菜单。然后编写一个使用此函数的 shell 脚本。

```
Select an item from the following menu:
d. to display today's date and current time,
f. to start an ftp session,
t. to start a telnet session, and
q. to quit.
```

## 13.7 exec 命令和文件 I/O

exec 命令是 Linux 加载器的命令级版本。通常，exec 命令用于用新进程替换当前进程。因此，在 shell 下执行时，exec cmd 会用 cmd 覆盖当前 shell。exec 命令也可用于打开和关闭文件描述符。

![](img/2a18e06cd9c6395e451f26126ecba1fd_409_0.png)

FIGURE 13.3 Execution of the exec date command under a subshell of the login shell.

```
% exec date
Sun Mar 19 18:04:24 PKT 2017
$ ps
PID TTY TIME CMD
6990 pts/2 00:00:00 bash
7163 pts/2 00:00:00 ps
$
```

### 13.7.2 通过 exec 命令进行文件输入/输出

不同的 shell 允许同时使用不同数量的文件描述符。如第 7 章所述，其中三个描述符保留用于标准输入 (0)、标准输出 (1) 和标准错误 (2)。使用 exec 命令的重定向运算符可以使用所有这些描述符进行 I/O。表 13.2 描述了 exec 命令用于文件 I/O 的语法。

# TABLE 13.2

Syntax of the exec Command for File I/O

| Syntax | Meaning |
|---|---|
| exec < file | Opens file for reading and attaches standard input of the process to file |
| exec > file | Opens file for writing and attaches standard output of the process to file |
| exec >> file | Opens file for writing, attaches standard output of the process to file, and appends standard output to file |
| exec n< file | Opens file for reading and assigns it the file descriptor n |
| exec n> file | Opens file for writing and assigns it the file descriptor n |
| exec n<< tag ... tag | Opens a here document (data between << tag and tag) for reading; the opened file is assigned a descriptor n |
| exec n>> file | Opens file for writing, assigns it file descriptor n, and appends data to the end of file |
| exec n>&m | Duplicates m into n; whatever goes into file with file descriptor n will also go into file with file descriptor m |
| exec <&- | Closes standard input |
| exec >&- | Closes standard output |
| exec n<&- | Closes file with descriptor n attached to stdin |
| exec n >&- | Closes file with descriptor n attached to stdout |

当从命令行执行时，exec < sample 命令会导致 sample 文件中的每一行都被视为命令并由当前 shell 执行。这是因为 shell 进程，其唯一目的是从 stdin 读取命令并执行它们，执行 exec 命令；由于 sample 文件附加到 stdin，shell 从此文件读取其命令。shell 在执行 sample 中的最后一行后终止。当从 shell 脚本内部执行此命令时，它会导致脚本其余部分的 stdin 附加到 sample。以下会话说明了当在命令行执行此命令时的语义。如图所示，sample 文件包含两个命令：date 和 echo。Bash 在登录 shell 下运行，后者是 C shell，通过 /bin/sh 命令。当执行 exec < sample 命令时，sample 文件中的命令将被执行，Bash（登录 C shell 的子进程）在完成 sample 中最后一个命令的执行后终止（exec < sample 命令完成后，第三个 ps 命令的输出显示只有登录 shell 在运行），并且控制返回到登录 shell。

```
% cat sample
date
echo "Hello, world!"
% ps
PID TTY        TIME CMD
874 pts/0    00:00:00 bash
933 pts/0    00:00:00 ps
% /bin/sh
% ps
PID TTY        TIME CMD
874 pts/0    00:00:00 bash
942 pts/0    00:00:00 sh
949 pts/0    00:00:00 ps
% exec < sample
$ Sun Apr  9 19:23:37 PKT 2017
$ Hello, world!
$
% ps
PID TTY        TIME CMD
874 pts/0    00:00:00 bash
979 pts/0    00:00:00 ps
%
```

因此，从命令行执行 exec < sample 命令时，它有效地将当前 shell 的 stdin 附加到 sample 文件。当此命令从 shell 脚本执行时，它将 shell 脚本的 stdin 附加到 sample 文件。在任何一种情况下，都必须执行 exec < /dev/tty 命令来重新将 stdin 附加到终端。这里，/dev/tty 是表示 shell 执行的终端的伪终端。以下会话说明了从命令行使用此命令的情况。这些步骤的语义如图所示 Figure 13.4。

同样，当从命令行执行 exec > data 命令时，它会将当前 shell 的 stdout 附加到 data 文件。因此，它会导致 shell 下执行的后续所有命令的输出都进入 data 文件。因此，您看不到任何命令的输出在屏幕上。为了再次在屏幕上看到输出，您需要执行 exec > /dev/tty 命令。执行此操作后，您可以查看 data 文件的内容，以查看在此命令之前执行的所有命令的输出。当从 shell 脚本执行 exec > data 命令时，它会导致后续所有命令的输出都进入 data 文件，直到从 shell 脚本内部执行 exec > /dev/tty 命令为止。

以下会话说明了从命令行使用此命令的情况。请注意，在 exec > data 命令完成执行后，后续所有命令（date、echo 和 more）的输出都进入 data 文件。为了将命令的输出重定向到屏幕，必须执行 exec > /dev/tty 命令，如以下会话所示。请注意，我们的系统具有 Intel x86（或兼容）64 位 CPU，并且如预期运行的是 Linux Mint18。




```
echo -n "Enter your code word again: "
read same
if [ $secretcode != $same ]
then
    clear
    echo "Work on your short-term memory before using this code!"
    echo "Goodbye!"
    exit 1
fi

# Keyboard locked. Hit <Enter> to continue.
clear
echo -n "Keyboard locked. Hit <Enter> to continue."
read ignore
clear

# Get user guess to unlock the terminal
clear
echo -n "Enter the code word: "
read yourguess
echo ""

# As long as the user input is not the original code word, loop here: display
# a message and take user input again. When the user input matches the secret
# code word, terminate the loop and execute the following echo command.
while [ "$secretcode" != "$yourguess" ]
do
    clear
    echo "Wrong code. Try again."
    echo -n "Enter the code word: "
    read yourguess
done
# Set terminal to echo mode clear
clear
echo "Back again!"
stty echo
exit 0
$
```

你可以使用此脚本在短时间离开终端前锁定它——例如，去取打印件或拿一罐汽水；因此得名 canleave（可以离开）。使用它可以节省原本用于注销和登录程序所需的时间。

以下本章练习旨在强化你对 Bash 信号处理功能的理解。

## Exercise 13.8

在你的 Linux 系统上测试 trap_demo 和 canleave 文件中的脚本。它们按预期工作吗？确保你理解它们。

## 13.6 Functions in Bash

Bash 允许你编写函数。函数由一系列命令组成，称为函数体，并被赋予一个名称。你可以通过使用函数名来调用函数体中的命令。

### 13.6.1 Reasons for Using Functions

函数通常在脚本的多个位置重复使用某段代码时使用。通过将此代码制作成函数，你可以节省输入时间。因此，如果脚本中某段代码在九个不同位置使用，你可以将其创建为函数，并在需要插入的位置通过使用函数名来调用它。函数的另一个优点是，任何对代码的更改，原本需要在九个地方进行，现在只需在一个地方进行——即在函数体中。权衡之处在于，将控制权转移到函数代码并返回到调用代码的机制需要时间，这会略微增加脚本的运行时间。

节省输入时间的另一种方法是为代码块创建另一个脚本文件，并通过将脚本作为命令调用来调用此代码。使用此技术的一个缺点是，由于脚本文件位于二级存储设备（如硬盘）上，调用脚本需要在定义后将其从磁盘加载到主内存中，这是一个昂贵的操作。无论它们位于 ~/.profile 中、交互式地在 shell 中定义，还是在脚本中定义，函数定义始终位于主内存中。因此，调用函数比调用位于磁盘上的 shell 脚本快数倍。

### 13.6.2 Function Definition

在使用函数之前，你必须先定义它。对于经常使用的函数，你应该将其定义放在 ~/.profile 文件中。这样，shell 在你登录时会将其记录在其环境中，并在你使用系统时允许你调用它们。特定于脚本的函数的定义通常放在包含脚本的文件中。你必须在其中定义函数后使用 .（点）命令执行 ~/.profile 文件，然后再使用它，除非你想注销然后重新登录。你也可以在交互式使用 shell 时定义函数。这些定义在你定义这些函数时所在的会话期间有效。

函数定义的语法如下：

```
name () command
```

其中 name 是函数的名字（也称为标签），command 是函数的函数体。对于函数体中包含多个命令的函数，命令列表用大括号 { 和 } 括起来。这允许你以以下方式格式化函数定义：

```
function_name () command
```

```
function_name () { command-list; }
```

```
function_name () {
    command-list
}
```

```
function_name ()
{
    command-list
}
```

function_name 是你选择的函数名称，command-list 中的命令构成了函数体。以下会话显示了对应于四种函数定义方式的示例函数定义以及前三种函数的示例运行。函数 function4 和 function5 的输出与 function3 相同。

```
$ function1 () { date; }
$ function2 () { uname -s; }
$ function3 () { date; echo "Hello, world!"; ps; }
$ function4 () {
> date
> echo "Hello, world!"
> ps
> }
$ function5 ()
```
```
> {
> date
> echo "Hello, world!"
> ps
> }
> {
> function1
> Sun Apr 9 19:43:18 PKT 2017
> function2
> function3
> Sun Apr 9 19:47:57 PKT 2017
> Hello, world!
> PID TTY TIME CMD
> 874 pts/0 00:00:00 bash
> 1497 pts/0 00:00:00 ps
> }
$ 
```

请注意没有用于函数的 export 命令。因此，函数定义仅对定义它们的 shell 可见。

### 13.6.3 Function Invocation/Call

函数体中的命令在函数被调用——即被调用——之前不会执行。你可以通过使用其名称作为命令来调用函数。当你调用一个函数时，其函数体被执行，控制权返回到函数调用之后的命令。如果你从命令行调用函数，控制权在函数执行完毕后返回到 shell。

在函数内声明的变量在函数外部可见并且可以相应地访问。要使变量对函数局部，可以使用关键字 local，如以下示例中的函数 f1。局部变量继承了在周围作用域中定义的同名变量的值和已导出及只读标志。如果周围作用域中没有此类变量，则局部变量初始化为空。Bash 使用动态作用域。这意味着在调用函数中定义的局部变量可供被调用函数访问。这也在以下会话中得到演示，其中变量 x 在 f1（调用函数）中定义为 local，并且可供 f2（被调用函数）访问。然而，x 在 f1 外部不可访问。另一方面，变量 y 未定义为 local，并且在 f1 外部可访问。echo $x、echo $y 和 f2 命令的输出验证了这些作用域规则。

```
```bash
$ f1 () { local x=10; y=20; f2; }
$ f2 () { echo "x is $x"; echo "y is $y"; }
$ f1
x is 10
y is 20
$ echo $x
20
$ echo $y
y is 20
$
```
```

### 13.6.4 A Few More Examples of Functions

以下名为 machines 的函数的执行将返回你本地网络上所有计算机的名称。

```
```bash
$ machines ()
> {
> date
> }
$ 
```
```
>   echo "These are the machines on the network: "
>   uptime | cut -f1 -d' ' | more
> }
$ ./machines
Thu Jul 31 20:23:28 PKT 2014
These are the machines on the network: upibm0
...
upsun1
...
upsun29
$
```

我们现在增强第 13.3 节中描述的 dext 脚本，使其能够在命令行上接受多个名称。增强版本还使用函数 OutputData 来显示每个作为命令行参数传递的名称的一个或多个输出记录（即目录中的行）。对于名称的多个行，此函数按排序顺序显示它们。脚本后的几条示例运行如下所示。

```
$ cat dext
#!/bin/bash
# File Name:    ~/linux2e/chaper13/bash/dext
# Author:       Syed Mansoor Sarwar
# Written:      August 1999
# Modified:     August 28, 2004; July 29, 2014; April 9, 2017

if [ $# = 0 ]
    then
        echo "Usage: $0 name"
        exit 1
fi
OutputData()
{
    echo "Infomation about $user_input"
    (grep -i "$user_input"| sort) << DIRECTORY

    John Doe      555.232.0000    johnd@somedomain.com
    Jenny Great   444.6565.11111  jg@new.somecollege.edu
    David Nice    999.111.3333    david_nice@xyz.org
    Don Carr      555.111.3333    dcarr@old.hoggie.edu
    Masood Shah   666.010.9820    shah@Garments.com.pk
    Jim Davis     777.000.9999    davis@great.adviser.edu
    Art Pohm      333.000.8888    art.pohm@great.professor.edu
    David Carr    777.999.2222    dcarr@net.net.gov

DIRECTORY
    echo      # A blank line between two records
}

# As long as there is at least one command line argument (name), take the
# first name, call the OutputData function to search the DIRECTORY and
# display the line(s) containing the name, shift this name left by one
# position, and repeat the process.

while [ $# != 0 ]
do
    user_input="$1"    # Get the next command line argument (name)
    OutputData          # Display info about the next name
    shift               # Get the following name
done
exit 0
$ ./dext john
```


## 12.3.2 Variable Declaration

Bash does not require you to declare variables and initialize them, but you can use the declare and typeset commands to declare variables, initialize them, and set their attributes. The attributes of a variable dictate the type of values that can be assigned to it and its scope (i.e., where it is accessible). A Bash variable is a string variable by default, but you can define a variable to be of integer type. You can also declare functions and arrays (see Chapter 13) by using these commands. You can mark a variable read only and make a variable’s value available to a child process. The following is a brief description of these commands:

```
Syntax:
    declare    [options] [name=value]
    typeset    [options] [name=value]
Purpose:  Declare variables, initialize them, and set their attributes. Inside functions, new copies of the variables are created. Using + instead of – turns attributes off
Output:   Without name and options, display names of all shell variables and their values in the environment of the current shell. With options, display names of variables with the given attributes and their values
Commonly used options/features:
    -a each "name" is an array
    -f each "name" is a function
    -i "name" is an integer
    -r mark each "name" read-only (cannot be turned off by using +x)
    -x mark each "name" exported
```

An undeclared and uninitialized variable has an initial value of a null string. Bash also does not require you to specify a variable’s attributes at the time of its declaration. You can initialize a variable and set its attributes at a later time by using the declare or typeset command, or by using other commands for setting specific attributes. Declaring an existing variable does not change its current value/attributes. In the following session, we demonstrate the use of the declare command; you can replace it with the typeset command if you so desire.

```
$ declare age=58
$ declare -rx OS=Linux
$ echo $age
58
$ echo $OS
Linux
$ declare OS
$ declare age
$ echo $OS
Linux
$ echo $age
58
$
```

When you use the declare and typeset commands without arguments, they display the names of all the shell variables in your environment and their values. You can use these commands to view the values of variables with particular attributes. The following session shows some examples. We have shown partial outputs for some commands to save space. Note that the declare -ir command displays all integer and read-only variables in your environment.

```
$ declare -i
declare -ir BASHPID
declare -ir EUID="1004"
declare -i HISTCMD
declare -i LINENO
declare -i MAILCHECK="60"
declare -i OPTIND="1"
declare -ir PPID="13147"
declare -i RANDOM
declare -ir UID="1004"
$ declare -x
declare -x HOME="/home/sarwar"
... [output truncated] ...
declare -x MAIL="/var/mail/sarwar"
declare -x OLDPWD="/home/sarwar"
declare -x PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"
declare -x PWD="/home/sarwar/linux2e/ch12"
declare -x SHELL="/bin/bash"
declare -x SHLVL="1"
declare -x SSH_CLIENT="103.255.5.92 6489 22"
declare -x SSH_CONNECTION="103.255.5.92 6489 202.147.169.195 22"
declare -x SSH_TTY="/dev/pts/1"
declare -x TERM="xterm-color"
declare -x USER="sarwar"
... [output truncated] ...
$ declare -ir
declare -ir BASHOPTS="checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote:force_fignore:histappend:interactive_comments:login_shell:progcomp:promptvars:sourcepath"
declare -ir BASHPID
declare -r BASH_COMPLETION_COMPAT_DIR="/etc/bash_completion.d"
declare -ar BASH_VERSINFO='([0]="4" [1]="3" [2]="42" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")'
declare -ir EUID="1004"
... [output truncated] ...
declare -ir UID="1004"
$ declare
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote:force_fignore:histappend:interactive_comments:login_shell:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_COMPLETION_COMPAT_DIR=/etc/bash_completion.d
BASH_LINENO=()
BASH_SOURCE=()
BASH_VERSINFO=([0]="4" [1]="3" [2]="42" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
BASH_VERSION='4.3.42(1)-release'
COLUMNS=80
DIRSTACK=()
EUID=1004
...
$
```

You can change the value of a variable by using the name=value syntax, discussed in detail in Section 12.2.3. You can use this syntax to declare generic variables that can be assigned a string value. An integer variable cannot be assigned a noninteger value; doing so results in the variable getting a value of zero. Noninteger variables can be assigned any value because every value is stored as a string. The following:

```
$ name=John*
$ echo $name
John.Bates.letter John.Johnsen.memo John.email
$ echo "$name"
John*
$ name=John*
Sat Jun 10 23:19:49 PKT 2017
$ echo $name
John.Bates John.email John.Johnsen
$ echo "The name $name sounds familiar!"
The name John* sounds familiar!
$ echo \$name
$name
$ echo '$name'
$name
$
```

If the right-hand side of an assignment statement is not enclosed in quotes and includes spaces, the shell assumes that the second and remaining words in the right-hand side form a command, and tries to execute it. The shell displays an error message if the assumed command does not correspond to a valid command, as shown in the statements name=Jimmy Doe. On the other hand, for the name=David date command, the output of the date command is displayed. Similarly, for name=James more ~/.profile | grep PATH the shell displays the output of the more ~/.profile | grep PATH command. In all these cases, regardless of whether the second and subsequent words form a valid command or not, the first command does not execute. Thus, the value of the name variable remains initialized with the previous value, John, as assigned at the beginning of the session.

After the name=John* statement has been executed and $name is not quoted in the echo command, the shell lists the file names in your present working directory that match John*, with * considered as the shell metacharacter. However, if there is no file in your current directory that starts with the string John, the echo command displays John*. However, if your current directory does not contain any file that starts with the string John, the echo John* command displays John*. The variable $name must be enclosed in quotes to refer to John*, as in echo "$name."

## 12.3.4 Command Substitution

Command substitution allows you to replace a command with its output. The following is a brief description of command substitution. Note the use of back quotes (also known as grave accents) in the first form of the syntax. In our example, shell sessions and scripts throughout the book, we will use the first syntax.

```
Syntax:
`command`
$(command)
Purpose: Execute command and substitute `command` (or $(command), if you use this syntax) with the output of the command
```

The following session illustrates this concept with a few examples. In the first assignment statement, the variable command is assigned a value pwd. In the second and third assignment statements, the output of the pwd command is assigned to the command variable.

```
$ command=pwd
$ echo "The value of command is: $command."
The value of command is: pwd.
$ command=`pwd`
$ echo "The value of command is: $command."
The value of command is: /home/sarwar/linux2e/ch12.
$ command=$(pwd)
$ echo "The value of command is: $command."
The value of command is: /home/sarwar/linux2e/ch12.
$
```

Command substitution can be specified in any command. For example, in the following session, the output of the date command is substituted for `date` before the echo command is executed.

```
$ echo "The date and time are `date`."
The date and time are Sat Jun 10 23:32:58 PKT 2017.
$
```

We demonstrate the real-world use of command substitution in various ways throughout this chapter and Chapter 13.

The following in-chapter exercises are designed to reinforce the creation and use of shell variables and the concept of command substitution.

### Exercise 12.3

Assign your full name to a shell variable called myname and echo its value. How did you accomplish the task? Show your work.

### Exercise 12.4

Assign the output of the echo "Hello, world!" command to the myname variable and then display the value of myname. List the commands that you executed to complete your work.

## 12.3.5 Exporting Environment

When a variable is created in a shell, subsequent shells do not have automatic access to it. The export, declare -x, or typeset -x command passes the value of a variable to subsequent shells. Thus, when a shell script is called and executed in another shell script, it does not get automatic access to the variables defined in the original (i.e., caller) script unless they are explicitly made available to it. These commands can be used to pass the value of one or more shell variables to any subsequent script. All read/write shell environment variables are available to every command, script, and subshell, so they are exported at the time they are initialized. The following is a brief description of the three commands:

```
Syntax:
  declare -x [name-list]
  typeset -x [name-list]
  export [name-list]
Purpose: Export the names and copies of the current values in name-list to every command executed from this point on
```

The following session presents a simple use of the declare -x command. The place variable is initialized to notre dame and is exported to subsequent commands executed under the current shell and any subshells that run under the current shell.

```
$ declare -x place="notre dame"
$ export place
$
```

We now illustrate the concept of exporting shell variables via some simple shell scripts. However, it is important to know that unless your search path (i.e., PATH variable) is set to include your current directory (.), you would have to explicitly place ./ before the name of a script file on the command line or inside a script file. If you do not do so, the shell will display the following error message.

```
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

# Exercise 12.3

Assign your full name to a shell variable called myname and echo its value. How did you accomplish the task? Show your work.

# Exercise 12.4

Assign the output of the echo "Hello, world!" command to the myname variable and then display the value of myname. List the commands that you executed to complete your work.

# 12.3.5 Exporting Environment

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
+   - ~
+   - [ ]

The ?.txt string can be used for all the files that have a single character before .txt, such as a.txt, G.txt, @.txt, and 7.txt. The [0-9].c string can be used for all the files in a directory that have a single digit before .c, such as 3.c and 8.c. The lab1\/c string stands for lab1/c. Note the use of backslash (\ ) to quote (escape) the slash character (/).

The following command prints the names of all the files in your current directory that have two-character file names and an .htm1 extension, with the first character being a digit and the second being an uppercase or lowercase letter. The printer on which these files are printed is spr.

```
$ lpr -Pspr [0-9][a-zA-Z].htm
$
```

Note that [0-9] means any digits from 0 to 9 and [a-zA-Z] means any lowercase or uppercase letter. The following command displays the names of all six-character-long files with .c extension in your current directory, with the first three characters being lab, the fourth being a digit, and the remaining being any two characters.

```
$ ls lab[0-9]???.c
lab11a.c lab1a1.c lab123.c lab4ab.c
$
```

# 2.10 The sudo and su Commands

The sudo command allows a permitted user to execute a command as the superuser, or to assume the role of another user, as specified by security policy. The su command allows an ordinary user to switch user roles or to also simulate being the superuser on the system. The superuser has file permission and access privileges to everything on the system.

In many of the operations shown in the following chapters, particularly in Chapter 17 on system administration, it will be necessary to execute the sudo or su command to accomplish the tasks shown. In order to use this command, it is necessary to know the root or superuser password.

We give a more complete explanation of the sudo command in Chapter W26, Section 9.2.1, at the book website.

An example of using the su command is as follows:

```
$ su
Password: www
/home/bob#
```

# Summary

The Linux operating system is most famous for its text-based command execution, but in the 21st century it has a competitively developed GUI environment as well. This chapter serves to familiarize you with the basic structure of a CUI Linux command. It also shows you how to log in via three popular and typical login methods and how to gracefully log off.

A beginner must be able to do basic file maintenance, and a core set of CUI file maintenance commands and their options are introduced in this chapter. These commands will be useful throughout the rest of this book. Finally, we illustrate and give examples of some basic utility commands—most importantly, the commands and their options that allow you to print files and the alias command.

When you log on to a Linux computer, the system runs a program called a shell that gives you a prompt and waits for you to type commands, either as single commands or as multiple commands connected by redirection or piping operators. The shell program, coded in C, is an interpreter, and
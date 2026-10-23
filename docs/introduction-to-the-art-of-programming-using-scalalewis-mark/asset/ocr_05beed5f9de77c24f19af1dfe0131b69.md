Not only does tab completion save you from typing a lot of extra characters, it never misspells a file or directory name. Use tab often and it will save you a lot of key strokes and a lot of little mistakes.

It is not uncommon to want to enter the same command or a very similar command more than once. The easiest way to do this, if it is a command you entered recently, is to use the up and down arrow keys to navigate backward and forward through the command history. When you get to a command, you can edit it if you want to make changes.

Using the arrow keys is not all that convenient if the command was something you entered a long time ago. The simplest way to repeat an old command exactly is to start the line with an exclamation point (often read “bang”) and follow it by some of the command. This will go back through the history and find the most recent command that started with those characters. That command will be executed without the chance to edit it. The limitation that you can not edit it or see exactly what the command is you will execute before you execute it means that ! is most useful for commands that start in a rather unique way.

You can also press Ctrl-r to get the ability to search through history. After pressing Ctrl-r, start typing in characters that occur consecutively in the command you want. It will bring up the most recent command that includes what you have typed in and you can edit it.

Another command that is very useful in general is the man command. This is short for manual and basically functions as help pages for commands or installed programs on the systems. The most basic usage is to type in man followed by the command that you want information on. You can also put in a -k option to do a search for something in the man pages.

# 2.1.1.4 Permissions

All modern operating systems have permissions that control who can get access to different types of files. What files you can access depends on who you are and what permissions you have. The act of logging into a machine determines who you are. You can use the command whoami to see who you are logged onto the machine as.

```
mlewis@mlewis-laptop:~$ whoami
mlewis
```

In this case the prompt also displays the user name, but that will not always be the case. Each user can also be a member of various groups. You can use the groups command to see what groups you are a member of.

```
mlewis@mlewis-laptop:~$ groups
mlewis adm dialout cdrom floppy audio dip video plugdev fuse lpadmin admin
```

The combination of who you are and the groups that you are in will determine what you have access to on a machine.

On Unix and Linux every file has read, write, and execute permissions for their owner, their group, and others. Those, along with the owner and the group of a file are displayed by ls when you use the -l option. Let us go back to the Desktop directory and look at the long listing of the files again.

```
mlewis@mlewis-laptop:~/Desktop$ ls -l
total 8
-rw-rwxrwx 1 root root 1261 2008-11-28 12:21 AdobeReader.desktop
-rw-r--r-- 1 mlewis mlewis 250 2009-12-22 11:03 QtCreator.desktop
```
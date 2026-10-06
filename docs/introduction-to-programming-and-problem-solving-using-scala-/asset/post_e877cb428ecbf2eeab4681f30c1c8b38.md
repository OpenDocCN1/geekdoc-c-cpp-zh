
# Getting to Know the Tools

By default, rm does not remove directories. To remove a directory command. Like mkdir, you follow it with the name of one or more directories you want to remove. rmdir will only remove a directory if it is empty. So you would need to remove the contents to the directory first before you can remove it.

## A.1.1.2 Aside

If you really want to delete an entire directory and all of its contents, including potentially other directories, there is an option for rm that will do that. The -r option allows rm or cp to recursively run into a directory and either remove or copy all of its contents. It is very helpful if you want to copy a directory. Remember to tread carefully. Using rm with the -r flag has the possibility to wipe out a lot of files that you wanted to keep. The command below uses -r with a copy over an entire directory and all of its contents to the current directory.

```
mlewis@mlewis:~/Desktop$ cp -r ../Music/
```

The last thing you want to do with your files is actually look at what is in them. There are many ways to do this. The commands we will consider here work best plain text files. We are dealing with all of these in this book. The most basic way to look at such a file is with the cat command which simply prints the contents of one or more files to standard output. Another step is that the more command will display one screen at a time and let you move around one line by hitting enter or a whole screen by hitting space. You can also search for things by typing what you want to search after /. Another step is the less command allows you to move around freely using arrow keys or page-up and page-down as well as you could with more.

## A.1.1.3 Helpful Tips

Many who are not familiar with the command line are initially turned off a bit by the amount of time they have to do. People who use command line do not necessarily type more, they know more tricks to do with things with the keyboard that do not require a lot of time. A couple of tricks will help you use the command line more efficiently include tab completion and viewing your command environment.

Typing in complete file names can be tedious and weary often prone to error. If you mistake something it will not work and you have to enter the whole thing again. Worse, it might work or you do something you did not want to do. Because of this, tab completion is probably the most helpful feature you will find in command line environment. If you type in the first few letters of a file or directory hit tab, the shell will give you the whole file. If there is only one file that starts with y, it will give you the whole file. If there is more than one, it will fill in as much as it can until it gets to a point where you have to make a choice. Double it will print out the different options that fit.

You should try this by going back to your home directory (remember you can do this any time by typing in cd and hitting enter without giving it a directory) and then typing De and hitting tab. Odds are good that the word Desktop will be completed for you

> Like those discussed in this section vary depending on the exact command shell you are using. A command shell is a separate software program that provides direct communication between the user and the operating system. This book describes features of the bash shell, which is standard for many Linux systems.

![](img/06d4e84f27a8884ea40ba6182ec7c778_559_0.png)

# Introduction to Programming and Problem-Solving Using Scala

with / at the end because it is a directory. Use ls if there are two files/directories that start with the same few letters. Type in cat followed by the first two letters and hit tab. The shell will complete as much as it can then stop. Hit tab quickly and it will show you the different options. It might look something like this.

```
mlewis@mlewis-laptop:~$ cd
```
Documents/ Downloads/

Not only tab completion save you from typing a lot of extra characters, it never misspells a file or directory name. Tab often and it will save you a lot of key strokes and a lot of little mistakes.

It is uncommon to want to enter the same command or a very similar command more than once. The easiest way to do this, if it is a command entered, is to use the up and arrow keys to navigate backward and forward through the command history. When you get to a command, you can edit it if necessary to make changes.

Using the arrow keys is not as convenient if the command was something you entered a long time ago. The simplest way to repeat an old command exactly is to start the line with an exclamation mark (!) and follow it by some of the command. This will go back through the history and find the most recent command that you started. The limitation that you cannot edit it or see exactly what the command is you will execute before you execute it means that ! is most useful for commands that start in a rather unique way.

You can also press Ctrl-r to get the ability to search through history. After pressing Ctrl-r, start typing in characters that occur in the command you want. It will bring up the most recent command that contains what you have typed and you can edit it.

Another command that is very useful in general is the man command. This is for manual and basically functions as help pages for commands or installed programs on the systems. The most basic usage is to use man followed by the command that you want information on. You can also put in a -k option to do a search for something in the pages.

## A.1.1.4 Permissions

All operating systems have permissions that control who can get access to different types of files. What files you access depends on who you are and what permissions you have. The act of logging into a machine determines who you are. You can use the command who to see who you are logged onto the machine.

```
mlewis@mlewis-laptop:~$ whoami
```

In this case the prompt displays the user name, but will not always be the case. Each user can be a member of various groups. You can use the groups command to see what groups you are a member of.

```
mlewis@mlewis-laptop:~$ groups
```

```
mlewis adam dialout cdrom floppy audio dip video plugdev fuse admin
```

The combination of who you are and the groups you are in will determine what you have access to a machine.

On Unix and Linux every file has read, write, execute permissions for their owner, their group, and others. Those, along with the group of a file are displayed by ls when you use the -l option. Let us go back to the Desktop directory and look at the long listing of the files again.

# Getting to the Knows 537

```
mlewis@mlewis-laptop:~/Desktop$ ls -l
total 8
-rw-rw-rw 1 root root 1261 2008-11-28 12:21 AdobeReader.desktop
drwxr-xr-x 2 mlewis mlewis 4096 2010-08-11 19:59 NewDir
-rw-r--r 1 mlewis mlewis 250 2009-12-22 11:03 QtCreator.desktop
```

This new directory is also owned by part of group mlewis. Note the letter 'd' first telling us is a directory. The owner, mlewis, has full read, write, and execute permissions. Anyone in group but others do not. Now that you know how to tell permissions on a file, the next question is how you change them. The chmod command is used to change permissions on a file. There are a few different ways to use chmod. We will introduce one of them here. After chmod you want to change or set permissions, give a list of the files you want to make the changes to. The simplest way to change permissions is to use character codes for which of users and the permissions involved and separate them with a '+', '-', or '=' to say if you want to add, remove, or set them. The permission sets are specified by 'u' for the user, 'g' for group, 'o' for others and 'a' for all. The rights are specified by the letters 'r', 'w', and 'x' as we have already seen.

Let us say that we are going to put things in this new directory we do not want anyone but the user to have the ability to see. In case we would want to remove the read and execute permissions from the group and others. We can see how this is done and the result of it

```
mlewis@mlewis-laptop:~/Desktop$ chmod go-rx NewDir/
mlewis@mlewis-laptop:~/Desktop$ ls -l
total 12
-rw-rw-rw 1 root root 1261 2008-11-28 12:21 AdobeReader.desktop
drwxr-x-- 2 mlewis mlewis 4096 2010-08-11 19:59 NewDir
-rw-r--r 1 mlewis mlewis 250 2009-12-22 11:03 QtCreator.desktop
```

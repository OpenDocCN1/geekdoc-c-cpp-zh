
tells rm or cp to recursively³ run down into a directory and either remove or copy all of its contents. This is very helpful if you want to copy a directory that has a lot of things in it. It can also be of great help if you want to remove such a directory. Remember to tread carefully though. Using rm with the -r flag has the possibility to wipe out a lot of files that you might have wanted to keep around. The command below uses -r with a copy to copy over an entire directory and all of its contents into the current directory.

```
mlewis@Mlewis-laptop:~/Desktop$ cp -r ../Music/ .
```

The last thing you might want to do with your files is actually look at what is in them. There are many ways to do this. Indeed, a big part of most of the programs you have on your computer is the ability to let you view the contents of specific types of files. The commands we will consider here work best with plain text files. We will be dealing with a lot of those in this book. The most basic way to look at such a file is with the cat command, which simply prints the contents of one or more files to standard output. A step above that is the more command which will display one screen at a time and let you move down one line by hitting enter or a whole screen by hitting space. You can also search for things by typing what you want to search for after pressing /. Yet another step up is the less command, which allows you to move around freely using arrow keys or page-up and page-down as well as search as you could with more.

## 2.1.1.3 Helpful Tips

Many people who are not familiar with the command-line are initially turned off a bit by the amount of typing they have to do. People who use command-line all the time do not necessarily like typing more, they know more tricks to do things with the keyboard that do not require a lot of typing. Here are some handy tricks to help you use the command-line more efficiently.⁴

Typing in complete file names can be tedious and worse, is often error prone. If you mistype something it will not work and you have to enter the whole thing again. Worse, it might work and do something you did not really want to do. Because of this, tab completion is probably the most helpful feature you find in your command-line environment. If you type in the first few letters of a file or directory then hit Tab, the shell will fill in as many characters as it can. If there is only one file that starts that way, it will give you the whole file. If there is more than one, it will fill in as much as it can until it gets to a point where you have to make a choice. If you double tab it will print out the different options that fit.

You should try this by going back to your home directory (remember you can do this at any time by typing in cd and hitting enter without giving it a directory) and then typing cd Desktop and hitting Tab. Odds are good that the word Desktop will be completed for you with a / at the end because it is a directory. Use ls to see if there are two files/directories that start with the same first few letters. Type in cat followed by the first two letters and hit Tab. The shell will complete as much as it can then stop. Hit Tab twice quickly and it will show you the different options. It might look something like this.

```
mlewis@mlewis-laptop:~$ cd Do
Documents/ Downloads/
```

> ³Recursion is a topic that you probably are not familiar with yet, but which we will hit on several times during this book.

> ⁴Tricks like those discussed in this section vary depending on the exact command shell you are using. This describes features of the bash shell, which is standard for many Linux installs.

Not only does tab completion save you from typing a lot of extra characters, it never misspells a file or directory name. Use tab often and it will save you a lot of key strokes and a lot of little mistakes.

It is not uncommon to want to enter the same command or a very similar command more than once. The easiest way to do this, if it is a command you entered recently, is to use the up and down arrow keys to navigate backward and forward through the command history. When you get to a command, you can edit it if you want to make changes.

Using the arrow keys is not all that convenient if the command was something you entered a long time ago. The simplest way to repeat an old command exactly is to start the line with an exclamation point (often read “bang”) and follow it by some of the command. This will go back through the history and find the most recent command that started with those characters. That command will be executed without the chance to edit it. The limitation that you can not edit it or see exactly what the command is you will execute before you execute it means that ! is most useful for commands that start in a rather unique way.

You can also press Ctrl-r to get the ability to search through history. After pressing Ctrl-r, start typing in characters that occur consecutively in the command you want. It will bring up the most recent command that includes what you have typed in and you can edit it.

Another command that is very useful in general is the man command. This is short for manual and basically functions as help pages for commands or installed programs on the systems. The most basic usage is to type in man followed by the command that you want information on. You can also put in a -k option to do a search for something in the man pages.

## 2.1.1.4 Permissions

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

scenario for this is if you want to change the group to a shared group so that a select set of users can have access to something. If the group were called **project** then you would type in “**chown** : **project files** ”.

> **Aside**
> 
> As with the **cp** and **rm** commands, there are times when you will want to change the permissions of a large number of files in an entire directory. Both **chmod** and **chown** accept the **-R** option so that they will do this.

## 2.1.1.5 Compression/Archiving

If you spend much time on a system, you will likely need to interact with compressed or archived files at some point. Both of these play the role of taking many separate files and turning them into one large file. If it is compressed, that large file should be smaller than the sum of the files that went into it. Many programs that you might want to put on your computer come in the form of compressed files. If you have assignments or projects that span multiple files, your instructor might want you to combine them into a single file to turn them in. There are many different compression and archiving utilities. We’ll just talk about the main ones here.

- * **tar** – Archive files to a single tarball.
- * **gzip/gunzip** – Compress one or more individual files to the gzip format.
- * **zip/unzip** – compress multiple files to a single zip file. The zip format is used extensively on many operating systems.

The first two are used in the Unix/Linux world. They do archiving and compression separately, but are often used together to do both. The archiving program is called **tar**. It was originally created for archiving files from disk to tape. It simply collects multiple files together into a single file called a tarball. It can also extract files from a tarball. As with our other programs, **tar** is controlled by passing it arguments. You can use the **man** pages to see the many different options for **tar**. We will only discuss the basic ones.

The three main ways you will interact with a tarball are to create one, view the contents of one, or extract files from one. These different options are given with the characters c, v, and x. Most of the time you will want to interact with a file, and for that you will give the **f** option. The next thing after the **f** option should be the file name of the tarball you are creating, viewing, or extracting. Tarball files should typically end with the extension **.tar**. If you are creating a tarball, that will be followed by the file and directory names of the things you want to put into the tarball. Here are some sample invocations.

```
tar cf assign1.tar header.txt Assign1/
tar tf assign1.tar
tar xf assign1.tar
```

The first command is what you might execute to create a tarball called **assign1.tar**, which contains a header file and all the contents of the directory **Assign1**. The second command might be used to verify that everything you want is in the file or to check what is there before it is extracted. The last command would extract the contents.

The counterpart to **tar** is **gzip**. This command will compress one or more files. Simply follow the **gzip** command with a set of file names to compress. That will create a new set

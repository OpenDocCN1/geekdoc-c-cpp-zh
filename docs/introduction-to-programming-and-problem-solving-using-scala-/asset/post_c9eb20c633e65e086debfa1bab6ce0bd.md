
# Getting to Know the Tools

541

has a machine name with a colon the file will go to that remote location. As with cp, the -r option can be used to copy an entire directory structure.

sftp command is a secure version of the classic ftp program, ftp stands for File Transfer Protocol. It allows you to locate and remote directory structures, where files are on the remote machine, and then move them. The full usage of sftp is beyond the scope of what we want to cover here, but you should be aware it exists in case you need to move files around and not certain what to move or where it should be moved or.

## A.1.1.7 Other Commands

There are many other commands that are available to you the Unix/Linux command line. You do not have to be familiar with all of them to get things done with the command line. In fact, this appendix should have enough to get through the tasks that you will need for this book. There are just a few more commands you might find helpful that we will list:

- clear - Clears the terminal so you get a fresh screen. This is only cosmic, but it can be helpful at times.
- df - Stands for disk free. This will list all of the different volumes on the current disk system and show you information on their usage.
- du - Stands for disk usage. This will give you a rundown of how much disk space is being used in the current directory and its sub-directories.
- echo - Prints whatever follows the command to the terminal.
- find - Finds files that have different properties specified on the command line.
- grep - Searches for text inside of the specified files.
- head - Print the first lines of a file.
- ps - Show information about processes running on the machine.
- tail - print the last lines of a file.
- touch - Updates the edit time on the specified file to the current time.
- top - Lists the resource consuming programs currently running on the machine.
- w - Tells you who is logged into your machine, where they are coming from, and what they are running.
- wget - You give this command a URL and it will download the file at that URL to the current directory.
- which - This command should be followed by the name of an executable. It will tell you the full path to that executable if it is in the current path.

As a final tip, you can follow any command with & to make it run in the background.

542 Introduction to Programming and Problem-Solving Using Scala

## A.1.2 I/O Redirection

So we have been talking about the different commands we can run from command line. We have typed input into the console when it was needed, and the commands output to the terminal screen so we could see it. The Unix/Linux command line gains a significant amount of power from the fact that you redirect input and output. The simple forms of redirection have the output of a program to go to a file or the input from a file. These will be of use to you in many of the projects in later chapters even if you do not see the benefit right now.

To send the output of a program to a file you are greater than, followed by a file name after the command. The output will go into that file. Here is an example:

```
mervis@laptop:~/Desktop ls -l > list.txt
mervis@laptop:~$ ls -l
total 16
-rw-r--r 1 root 2021-11-28 12:21 AdobeReader.desktop
-rw-r--r 1 mlevis 259 2010-08-12 22:32 list.txt
d-----
-rw-r--r 1 mlevis 406 2010-08-11 19:59 NewDir
-rw-r--r 1 mlevis 250 2009-12-22 11:03 QtCreator.desktop
d-----
-rw-r--r 1 root 621 2020-11-28 12:21 AdobeReader.desktop
-rw-r--r 1 mlevis 0 2010-08-12 12:32 list.txt
d-----
-rw-r--r 1 mlevis 406 2010-08-11 19:59 NewDir
-rw-r--r 1 mlevis 250 2009-12-22 11:03 QtCreator.desktop
```

The first call is not print to screen. It sends it to the file list.txt because of the greater followed by that file name. We can then do other ls and let it print to verify the file is there. Then we have a new file that is 259 bytes in length. We can also use cat to view the contents of the file, and you see the output as parts of ls. There is one interesting aspect to it. The file we are outputting to is, but it has a size of zero. Because the file is created as soon as we execute the command, it does not get any output big that they have to be moved from a buffer to the file.

Using > redirecting output will create a new file if there is none and will wipe out any existing file if there is. If you want a command to add onto an existing file, use >>. This will redirect the output so that it appends to an existing file.

We can also tell a command to import it <, symbol. The name of commands we import <, symbol.

# Getting to Know the Tools

567 Introduction to the Tools

## Getting to Know the vi

567 Introduction to the vi

## A.1.3 Text Editors (vi/vim)

Most programming languages have programs that are written in plain text. You can use any simple text editor to edit them. Word processors, such as Microsoft Word® or Open Office® are not text editors.
```

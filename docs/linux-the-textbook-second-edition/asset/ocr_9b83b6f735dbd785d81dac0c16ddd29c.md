```
142      640     4448 /usr/include/x86_64-linux-gnu/sys/epoll.h
1         2       19 /usr/include/x86_64-linux-gnu/sys/errno.h
44      208     1399 /usr/include/x86_64-linux-gnu/sys/eventfd.h
38      187     1291 /usr/include/x86_64-linux-gnu/sys/fanotify.h
1         2       19 /usr/include/x86_64-linux-gnu/sys/fcntl.h
56      281     1721 /usr/include/x86_64-linux-gnu/sys/file.h
... 
175     934     6223 /usr/include/x86_64-linux-gnu/sys/wait.h
105     674     4274 /usr/include/x86_64-linux-gnu/sys/xattr.h
8165   38513  267732 total
$
```

# Exercise 6.9

Repeat the ls and wc commands discussed in this section on your system. Create the requisite files and directories in order to replicate the Bash sessions on your system. Did the command executions result as expected?

# 6.4 Appending to Files

Appending to a file means putting new data at the end of the contents of the file. If the file does not exist, it is created to contain new data. The append operation is useful when an application or a user needs to augment a file by adding data to it. The following command syntax is used to append one or more files, or keyboard input, at the end of a file.

```
Syntax:
  cat [file-list] >> destination-file
Purpose: Append the contents of the files in file-list, in the order specified in the command line, at the end of destination-file
```

The >> operator is the Linux append operator. We discuss the >>, <, and > operators in detail in Chapter 9. That chapter describes how the input of your commands can be read as input from a file instead of the keyboard, and how the output and error messages of your commands can be redirected from the terminal (or console widow) to files. In this chapter, we use these operators only to describe how you can append new data at the end of the current contents of a file and how you can combine the contents of multiple files and put them in one file using the cat command.

The following session illustrates how the append operation works. The cat sample >> temp command appends the contents of the sample file at the end of the temp file. The cat commands before and after this command show the contents of the files involved. The command syntax can be used to append multiple files to a file, as shown in the command cat memo1 memo2 memo3 >> memos.record. This command appends the contents of the memo1, memo2, and memo3 files at the end of the memos.record file.

```
$ cat temp
This is a simple file used to illustrate the working of append operation. The new data will be appended right below this line.
$ cat sample
These are the new data that will be appended at the end of the test file.
$ cat sample >> temp
$ cat temp
This is a simple file used to illustrate the working of append operation. The new data will be appended right below this line.
These are the new data that will be appended at the end of the test file.
$ cat memo1 memo2 memo3 >> memos.record
$
```
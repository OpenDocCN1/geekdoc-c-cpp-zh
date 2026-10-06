inDirectory: @"birdImages";

The method returns an array of path names. If your JPEG's are not stored in a subdirectory in your application, you can specify `""` as the value of the `inDirectory` parameter.

There are more methods in the NSBundle class that you'll want to learn about. Check your documentation for details.

# Exercises

+   1. Modify the copy program developed in Program 16.6 so that it can accept more than one source file to be copied into a directory, like the standard UNIX `cp` command. So, the command

```
$ copy1.m file1.m file2.m progs
```

should copy the three files `copy1.m`, `file1.m`, and `file2.m` into the directory progs. Be sure that when more than one source file is specified, the last argument is, in fact, an existing directory.

+   2. Write a command-line tool called `findfind that takes two arguments. The first is a starting directory to begin the search, and the second is a filename to locate. So, the command

```
$ myfind /Users proposal.doc
/Users/stevekochan/MyDocuments/proposals/proposals/al.doc
$
```

begins searching the file system from `/Users` to locate the file `proposal.doc`. Print either a full path to the file if it's found (as shown) or an appropriate message if it's not.
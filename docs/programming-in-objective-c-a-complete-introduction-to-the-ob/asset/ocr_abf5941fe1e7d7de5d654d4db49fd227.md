# Chapter 16.6 Working with Files

# Program 16.6 Output

```
$ ls -l
see what files we have
total 96
-rwxr-xr-x 1 stevevec staff 19956 Jul 24 14:33 copy
-rw-r--r- 1 stevevec staff 14884 Jul 24 14:32.m
-rw-r--r- 1 stevevec staff 14003 Jul 24 14:00 file.m
drwxr-xr-x 2 stevevec staff 68 Jul 24 14:40 newdir
-rw-r--r- 1 stevevec staff 1567 Jul 24 14:21 path1.m
-rw-r--r- 1 stevevec staff 84 Jul 24 13:22 testfile
$ copy try with no args
Usage: copy src dest
$ copy foo2 backup
Can't read foo
$ copy.m backup.m
Copy of copy.backup.m succeeded!
$ diff copy.m newdir compare the files
$ copy.m newdir try copy into directory
Copy of copy.m to newdir/copy.m succeeded!
$ ls -d newdir
total 8
-rw-r--r- 1 stevevec staff 14884 Jul 24 14:44 copy.m
$
```

# Note

The output will differ on your system based on the files you have stored in your directory when you run this program.

ProcessInfo's arguments method returns an array of string objects. The first element is the name of the process, and the remaining elements contain the arguments on the command line.

You first check to ensure that two arguments were typed on the command line. This is done by testing the size of the args array that is returned from the arguments method. If this succeeds, the program then extracts the source and destination filenames from the args array, assigning their values to source and dest, respectively.

The program next checks to ensure the source file can be read, issuing an error message if it can't.

The statement

```
[if fileExistsPath: dest isDirectory: &is];
```

checks the file specified by dest to see whether it is a directory. As you've seen previously, the answer—YES or NO—is stored in the variable isDir.

If dest is a directory, you want to append the last path component of the source filename to the end of the directory's name. You use the path utility method stringAppendingPathComponent to do this. So, if the value of source is the string chil/copy1.m and the value of dest is /Users/stevekochan/progs and the latter is a directory, you change the value of dest to /Users/stevekochan/progs/copy1.m.

The copyPath:pathTo:handler method doesn't allow files to be overwritten. Thus, to avoid an error, the program tries to remove the destination file by using the
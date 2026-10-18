In this section, we will show how to build an application by typing a few commands in the Linux OS.4 Not surprisingly, actions to perform are also summarized in the form of an algorithm, as follows.

+   Open a terminal window (in Linux, use the Ctrl+Alt+T shortcut)

+   Run the ls -l command to list files and directories. The following is some example output:

```
boxy@PARSEC:~$ ls -l
total 0
drwxrwxrwx 1 boxy boxy 512 Aug 16 18:32 Desktop
drwxr-xr-x 1 boxy boxy 512 Aug 16 18:32 Videos
```

+   With the mkdir command, create a new directory, such as Projects, and list its contents:

```
boxy@PARSEC:~$ mkdir Projects
boxy@PARSEC:~$ ls -l
total 0
drwxrwxrwx 1 boxy boxy 512 Aug 16 18:32 Desktop
drwxrwxrwx 1 boxy boxy 512 Aug 30 19:51 Projects
drwxr-xr-x 1 boxy boxy 512 Aug 16 18:32 Videos
```

+   Go into Projects by calling cd Pro* (to save typing, the special grep character * is used, which substitutes for zero or more characters):

```
boxy@PARSEC:~$ cd Pro*
boxy@PARSEC:~/Projects$ ls -l
total 0
```

+   Now type, or copy-paste, the code from Listing 2.1. To do so, we can call one of the installed text editors, such as GNU nano or emacs. However, to create a sq.cpp file, a simple cat command can be used. Just after typing cat > sq.cpp, paste the code from the clipboard (or type it), as follows

```
boxy@PARSEC:~/Projects$ cat > sq.cpp
// This is a C++ comment in the program to compute the square root of a
value
```
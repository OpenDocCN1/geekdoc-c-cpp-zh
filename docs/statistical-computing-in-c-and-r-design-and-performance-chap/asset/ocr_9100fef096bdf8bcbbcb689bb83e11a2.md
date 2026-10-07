# 480 AN INTRODUCTION TO UNIX

Starting from our original login location we would like to go various places and accomplish various things. Commands for such purposes will be discussed in subsequent sections. The presentation is organized by groupings of commands with similar or related purposes.

# A.1 Getting around and finding things

The main tool for moving from point A to point B in Unix is the change directory command cd. For example, by entering

```
cd pathToDirectory/directoryName
```

you will move from your current location along the path specified by pathToDirectory and end up at directoryName on the Unix tree. There are various shortcut ways to specify a path. But, what works is a list, separated by '/' starts at the root directory and details every stop along the way from the root to the location of interest. In general, this is what we refer to as a path throughout the text. For example, the command cd /usr/local/share will take you from your current location in the directory tree to the share subdirectory by going from the root / to the subdirectory usr and then to its sublocal directory.

A very useful shortcut is the ~ symbol which can always be used in place of the name for your home directory. Some related shortcut commands that come in handy are:

```
cd .. moves you one level lower to the root and
cd without an argument, which always returns you to your home directory.
```

# A.2 Seeing what’s there

So, now you have arrived at a location (or know of location of interest) and would like to find out what is there. The list command, ls, can be used for this purpose. Specifically:

```
ls pathToDirectory/directoryName
```

will provide a list of all the files in the directoryName reached by pathToDirectory. More generally,

```
ls -l pathToDirectory/directoryName
```

gives a complete listing that, from left to right, the following information for each file in the directory:

+   - read, write and execute permissions (that will be discussed in more detail below),
- the number of hard links (i.e., the number of directory entries that reference the file or directory),
- the owning user,
- the owning group,
- the size of the file or directory in bytes,
- creation date and
- the file or directory name.

It turns out that neither ls nor ls -l tell the whole story. Many times there are files in your directory that begin with a . such as .bashrc and emacs. To see these you have to use ls -a. Using ls without a path specification returns the result of applying it to the current directory.
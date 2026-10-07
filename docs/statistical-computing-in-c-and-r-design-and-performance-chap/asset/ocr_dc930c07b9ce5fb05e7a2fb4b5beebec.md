# CREATING AND DESTROYING THINGS

The find command gives us what we need to determine the contents of a directory. For big directories (as well as for other reasons), it is sometimes preferable to automate the search for things of interest inside a directory. This can be accomplished with the find command.
For example,

```
find pathToDirectory/directoryName -name filename
```

will locate any file with the name filename directoryName. Often, instead of seeking a particular file, what is really needed is a list of all files with similar names as those having the same file extension. This can be accomplished by combining wildcards, thereby allowing find (as well as other commands) to match some portion of a file's name. Perhaps the most common wildcards are * that matches all characters in any quantity and ? will match any single character. Using wildcard one can create commands like

```
find pathToDirectory/directoryName -name *.cpp
```

will produce a list of every file in directoryName with a .cpp extension. Similarly,

```
find pathToDirectory/directoryName -name ex?.cpp
```

would give a list of files with names such as ex1.cpp, ex2.cpp, exe.cpp, etc., but not, e.g., ex.cpp or ex12.cpp. The latter would be returned if ex*.cpp was used as the search argument.
To see the actual contents of a file you can edit it as will be discussed below. But, if you just want a peek at a few lines of a fileName, either the head or tail commands can be used in

```
head -n fileName
```

to list the first n lines of the file and

```
tail -n fileName
```

to see its n lines. The entire contents of fileName will be written to the screen with
The commands more and less will allow you to scroll through a file. The space bar will advance the one line "page" when q returns to the shell prompt. You can obtain information about a file without looking at it we the wc command. Entering

```
wc fileName
```

will return the number of lines, words and bytes in fileName.

# A.3 Creating and destroying things

So far our interaction with Unix has been relatively static. But, things become much more interesting once you can create and populate directories of your own. There are a multitude of ways to go about this and we will consider a few of the standards ones here.
The simplest way to create a file is through the touch command which creates an empty text file fileName upon entering

```
touch fileName
```

To delete fileName, employ the remove command, rm, like

```
rm fileName
```
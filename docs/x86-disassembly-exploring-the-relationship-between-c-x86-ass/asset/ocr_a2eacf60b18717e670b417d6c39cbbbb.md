Dumps out information about an executable including symbols and assembly. It comes standard. It can be made to support non-native binary formats.

```
objdump -p displays a list of functions imported from
other libraries, exported to and miscellaneous file header
information
```

It's useful to check dll dependencies from command line

# readelf

Like objdump but more specialized for ELF executables.

# size

Lists the sizes of the segments.

# nm

Lists the symbols in an ELF file.

# strings

Prints the strings from a file.

# file

Tells you what type of file it is.

# fold

Folds the results of strings into something pageable.

# kill

Can be used to halt a program with the sig_stop signal.

# strace

Trace system calls and signals.

# 3.5 Other Tools for Linux

# oprofile

Can be used the find out what functions and data segments are used

# subterfuge

A tool for playing odd tricks on an executable as it runs. The tool is scriptable in python. The user can write scripts to take action on events that occur, such as changing the arguments to system calls.

```
http://subterfuge.org/
```

# lizard

Lets you run a program backwards.
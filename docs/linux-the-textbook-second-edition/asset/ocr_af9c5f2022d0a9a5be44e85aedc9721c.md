```
$ gcc -w file_sharing.c -o fileshare
$ fileshare foo 32
BASH(1) Gene
CHILD: position of the file pointer after I/O is 32
ral Commands Manual
PARENT: position of the file pointer after I/O is 64
```

```
$ fileshare foo 64
BASH(1) General Commands Manual
CHILD: position of the file pointer after I/O is 64
BASH(1)
NAME
bash - GNU Bourne-Again SHell
SYNOP
PARENT: position of the file pointer after I/O is 128
```

```
$ fileshare foo 256
BASH(1) General Commands Manual BASH(1)
NAME
bash - GNU Bourne-Again SHell
SYNOPSIS
bash [options] [command_string | file]
COPYRIGHT
Bash is Copyright (C) 1989-2013 by the Free Software Foundat
CHILD: position of the file pointer after I/O is 256
ion, Inc.
DESCRIPTION
Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file. Bash also incorporates useful features from the Korn and C shells (ksh and csh).
PARENT: position of the file pointer after I/O is 512
$
```

# Exercise 16.12

Replicate the preceding session on your system. Does the file_sharing.c program work as expected?

# Exercise 16.13

Modify the file_sharing.c program so that it takes the number of bytes to be read as the first command line argument and the filename as the second argument. Compile and run the program with different files and bytes-to-read as command line arguments.
that it knows where to stop reading. Therefore, C input functions come equipped with a built-in, end-of-file detector. Because keyboard input is treated like a file, you should be able to use that end-of-file detector to terminate keyboard input, too. Let’s see how this is done, beginning with files.

# The End of File

A computer operating system needs some way to tell where each file begins and ends. One method to detect the end of a file is to place a special character in the file to mark the end. This is the method once used, for example, in CP/M, IBM-DOS, and MS-DOS text files. Today, these operating systems may use an embedded Ctrl+Z character to mark the ends of files. At one time, this was the sole means these operating systems used, but there are other options now, such as keeping track of the file size. So a modern text file may or may not have an embedded Ctrl+Z, but if it does, the operating system will treat it as an end-of-file marker. Figure 8.2 illustrates this approach.

prose:
Ishpbat the robot
slid open the hatch
and shouted his challenge.

prose in a file:

```
Ishpbat the robot\n slid open the hatch\n and shouted his challenge.\n^Z
```

Figure 8.2 A file with an end-of-file marker.

A second approach is for the operating system to store information on the size of the file. If a file has 3000 bytes and a program has read 3000 bytes, the program has reached the end. MS-DOS and its relatives use this approach for binary files because this method allows the files to hold all characters, including Ctrl+Z. Newer versions of DOS also use this approach for text files. Unix uses this approach for all files.

C handles this variety of methods by having the getchar() function return a special value when the end of a file is reached, regardless of how the operating system actually detects the end of file. The name given to this value is EOF (end of file). Therefore, the return value for getchar() when it detects an end of file is EOF. The scanf() function also returns EOF on detecting the end of a file. Typically, EOF is defined in the stdio.h file as follows:

```
#define EOF (-1)
```

Why -1? Normally, getchar() returns a value in the range 0 through 127, because those are values corresponding to the standard character set, but it might return values from 0 through 255 if the system recognizes an extended character set. In either case, the value -1 does not correspond to any character, so it can be used to signal the end of a file.
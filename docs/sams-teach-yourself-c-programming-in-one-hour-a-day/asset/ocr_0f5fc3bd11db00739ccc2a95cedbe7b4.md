# 452 LESSON 17 Using Disk Files

```
char tempename[80];
*tmpfile;
tmpnam(tempename);
tmpfile = fopen(tempename, "w"); /* Use appropriate mode */
close(tmpfile);
remove(tempename);
```

| DO | DON'T |
|---|---|
| DO remember to remove temporary files that you create. They aren't deleted automatically. | DON'T remove a file that you might need again. |

# Summary

In this lesson, you learned C programs use disk files. C treats a disk file like a stream (sequence of characters), just like the predefined streams you learned about Lesson 14. A stream associated with a disk file must be opened before it can be used, and it must be closed after use. A disk file stream can be opened in either text or binary mode.

After a disk file has been opened, you can read data from the file into your program, write data from the program to the file, or both. There are three general types of file I/O: formatted, character, and direct. Each type of I/O is best used for certain types of data storage and retrieval tasks.

Each disk file has a position indicator associated with it. This indicator specifies the position in the file, measured as the number of bytes from the start of the file, where subsequent read and write operations occur. With some types of file access, the position indicator is updated automatically, and you don't have to be concerned with it. For random file access, the C standard provides functions for manipulating the position indicator.

Finally, C provides some rudimentary file management functions, enabling you to delete and rename disk files. In this lesson, you developed your own function for copying disk files.

# Q&A

+   Can I use directories and paths with filenames when using remove(), rename(), fopen(), and the other file functions?

+   You can use a full filename with a path and a drive or just the filename by itself. If you use the filename by itself, the function looks for the file in the
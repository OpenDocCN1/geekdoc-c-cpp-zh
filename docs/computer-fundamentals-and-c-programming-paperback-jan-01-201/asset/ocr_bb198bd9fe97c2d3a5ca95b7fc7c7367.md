```
```c
fp = fopen("foo", "r");        /* Opens foo for reading */
fgets(buf2, 79, fp);              /* Reads a line from foo */
fputs(buf2, stdout);               /* Writes line to display */
fclose(fp);

exit(0);
}
```
```

PROGRAM 15.1: **fopen_fclose.c**

Enter a line of text:
**Characters, words, lines and structures**
Characters, words, lines and structures

PROGRAM OUTPUT: **fopen_fclose.c**

# 15.4 THE FILE POINTER AND FILE BUFFER

Opening a file with **fopen** has two important consequences—creation of a file pointer and file buffer. The file pointer (like fp in previous programs) is a variable that points to a structure typedef’d to FILE. This structure, which is instantiated when a file is opened, contains the following information related to the opened file:

+   - The mode of opening.
+   - The location of the file buffer.
+   - The file position indicator.
+   - Whether EOF or any errors have been encountered on reading or writing.

The *file position indicator*, also called *file offset pointer*, has an important role to play in input/output operations. For instance, a read operation updates this field in the FILE structure with the position of the buffer up to which all data have been read. The next read operation (by the same or another function) looks up this field to determine the position from where to resume reading. The same logic applies to write operations.

File opening also sets up a buffer which acts as a go-between between the program and the file. When a file is read with, say, **fgetc**, the data is first sent from disk to the buffer from where it is sent to the program. So, even if **fgetc** reads one character from the buffer in each call, the buffer itself is populated in one disk-read operation. This speeds up the eventual data transfer rate from disk to the program.

A similar buffer is set up when a file is opened for writing. In this case, all write operations are made to the buffer, which itself is flushed (i.e., written) to disk when full. A file used for read/write access thus needs two buffers. Figure 15.1 replicates Figure 9.1 which demonstrated the role of these buffers in terminal I/O.

> **Takeaway:** All read/write operations on files actually take place through their buffers. A buffer is connected to a disk file by the file pointer which is generated when a file is opened with **fopen**.
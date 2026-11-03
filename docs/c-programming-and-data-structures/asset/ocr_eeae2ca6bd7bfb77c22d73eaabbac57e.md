# UNIT 8
File Handling

# 8.1 INTRODUCTION

Until now we have been using the functions such as scanf and printf to read and write data. These are console oriented I/O functions, which always use the terminal (keyboard and screen) as the target place. This works fine as long as the data is small. However, many real-life problems involve large volumes of data and in such situations, the console oriented I/O operations pose two major problems.

+   1. It becomes cumbersome and time consuming to handle large volumes of data through terminals.
+   2. The entire data is lost when either the program is terminated or the computer is turned off.

It is therefore necessary to have a more flexible approach where data can be stored on the disks and read whenever necessary, without destroying the data. This method employs the concept of files to store data. A file is a place on the disk where a group of related data is stored. Like most other languages, C supports a number of functions that have the ability to perform basic file operations, which include:

+   - naming a file,
+   - opening a file,
+   - reading data from a file,
+   - writing data to a file, and
+   - closing a file.

There are two distinct ways to perform file operations in C. The first one is known as the low-level I/O and uses UNIX system calls. The second method is referred to as the high-level I/O operation and uses functions in C's standard I/O library. We shall discuss in this chapter, the important file handling functions that are available in the C library. They are listed in Table 8.1.

# Table 8.1 High Level I/O Functions

| Function name | Operation |
|---|---|
| fopen() | * Creates a new file for use.
* Opens an existing file for use. |
| fclose() | * Closes a file which has been opened for use. |
| getc() | * Reads a character from a file. |
| putc() | * Writes a character to a file. |
| fprintf() | * Writes a set of data values to a file. |
| fscanf() | * Reads a set of data values from a file. |
| getw() | * Reads an integer from a file. |
| putw() | * Writes an integer to a file. |
+   - Appending data to a file (adding contents at the end of the file)
- Updating contents of a file
- Closing a file

C language supports number of predefined functions to assist the programmer to perform various file operations. File functions can be broadly classified into the following two types:

+   - High-level file I/O functions
- Low-level file I/O functions

High-level file I/O functions are basically standard library functions and can be easily used by a programmer. Low-level file I/O functions use system calls of the underlying operating system to perform lower-level I/O operations. They are relatively more complex in nature when compared to high-level file I/O functions. However, these functions are more efficient. In this chapter, we shall deal with high-level file I/O functions only. The file functions that will be discussed in this chapter are listed in Table 1:

Table 1: C Library Functions for Performing File Operations
| Function name | Purpose |
| :--- | :--- |
| fopen( ) | To open a file |
| ferror( ) | To check whether any error is encountered while opening a file |
| fgetc( ) | To get character from a file |
| fputc( ) | To put character to a file |
| getw( ) | To get an integer from a file |
| putw( ) | To put an integer to a file |
| fscanf( ) | To read formatted set of data values from a file |
| fprintf( ) | To write formatted set of data values to a file |
| ftell( ) | To retrieve the current position of associated file pointer in a file |
| fseek( ) | To set the associated file pointer to a desired point in a file |
| rewind( ) | Sets the position of associated file pointer to the beginning of a file |
| fread( ) | To read records stored in binary file |
| fwrite( ) | To write records in a binary file |
| feof( ) | To detect end-of-file marker |

# 13.4 Opening and Closing a File

Before performing any operations such as reading contents of a file and writing contents to a file, the file should be first opened. To open a file, function fopen is available in C library. The function fopen accepts two parameters. The syntax of its usage is as follows:

```
file_pointer = fopen("filename", "mode of opening");
```

The first parameter is the name of the file to be opened. By default, function fopen attempts to locate file from the folder that contains C program. If a programmer wishes to open a file located in a different file, he/she can specify full path, including the file name
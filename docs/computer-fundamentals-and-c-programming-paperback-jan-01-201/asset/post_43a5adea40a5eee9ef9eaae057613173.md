
## 15 File Handling

**WHAT TO LEARN**

- Significance of the *file pointer* and *buffer* in file-I/O operations.
- Opening a file in read, write and append modes (**fopen**).
- Handling I/O errors (**perror**) and detecting EOF (**feof**).
- How functions use the *file position indicator* in I/O operations.
- Handling data in units of characters (**fgetc/fputc**) and lines (**fgets/fputs**).
- Formatting data with **fscanf** and **fprintf**.
- Using command-line arguments to specify filenames.
- Read/write operations on arrays and structures (**fread/fwrite**).
- Random file access using the file position indicator (**fseek/ftell**).
- Deleting and renaming files (**remove** and **rename**).

### 15.1 A PROGRAMMER’S VIEW OF THE FILE

So far, our programs used data that was either provided in the program itself or input from the keyboard. The output always appeared on the terminal. Unsaved input and output are totally unsuitable for handling voluminous data that we often encounter in real life. You can’t obviously key in the details of every employee for preparing the payroll, and you certainly can’t do it every month. The most convenient mechanism for handling bulk data is to store them in files and use programs to read from and write to these files.

A file is a *named* container of information that is stored in multiple *blocks* in a file system. This file system typically resides in the hard disk but a CD-ROM, DVD-ROM or flash drive also support a file system. All files are administered by the operating system which allocates and deallocates disk blocks as and when needed. The OS also controls the transfer of data between programs and the files they access. Thus, a file-oriented program has to make a call to the OS for a service that it can’t handle on its own.

When we invoked **a.out < foo1 > foo2** from the shell (9.6), the OS opened the two files, gathered their scattered blocks and connected their data to the **a.out** program. This mechanism has some drawbacks. First, a program can use more than two files. Second, read/write operations don’t always start from the beginning of the file. Finally, the same file could be both read and written. These situations can only be handled by the I/O functions offered by the standard library.

A file comprises a set of byte-sized characters, where each character can have any value between 0 and 255. If we needed to have only a character view of a file, only one read and one write function would have been adequate for read/write operations. However, programs need to know whether a group of characters represents a string or a number, so multiple functions are needed for making this distinction. Partly for this reason, we often classify files as *binary* or *text*, even though this distinction has never been fully convincing.

> **Note:** The file-I/O functions have no knowledge of the organization of a file’s data on disk. Neither are they aware of the mechanism employed by the OS to transfer data between the program and a file.

### 15.2 FILE-HANDLING BASICS

A file has to be *opened* before data can be read from or written to it. Typically, data is read from a file and then manipulated by program logic. The output is often written to another file. Because different functions can read the same file, a common *buffer* and a *file position indicator* are maintained in memory for a function to know how much of the file has already been read. C also supports functions that handle issues like EOF and file-related errors.

Only the **fopen** function needs to know the name and location of a file. **fopen** returns information on the opened file in the form of a *file pointer* which points to a structure of type FILE. The other functions use this file pointer to access the information stored in the structure. This information includes the file position indicator and the location of the buffer that are associated with each opened file.

The buffer is used as temporary storage by the I/O-bound functions like **fgetc** and **fputc**. Even though **fgetc** reads one character at a time, it would be inefficient to access the disk every time a character is read. The OS reduces this overhead by reading a block of data into the buffer from where **fgetc** fetches a character at a time. A similar buffer is set up when a file is opened for writing. This buffer is written to disk when it is full or when specifically instructed to do so.

Even though files simply contain characters, it is often necessary to group these characters into words, lines, arrays and structures. The **fgets** function fetches a line while **fread** reads a structure or even an array of them in one call. Text files contain only printable characters while *binary* files may contain any character. It is sometimes necessary for a function to know the type of file it is dealing with, so the type has to be specified as text or binary when the file is opened.

C was born in a UNIX environment which uses the LF character (ASCII value: 10) as newline. However, MSDOS/Windows uses CR-LF (two characters) as newline, while Mac uses only CR. For this reason, some of the library functions have to carry out the necessary replacement when newline is read or written on these systems.

> **Note:** All file-handling functions discussed in this chapter use the file `stdio.h`, which must be included in every program containing one of these functions.

### 15.3 OPENING AND CLOSING FILES

File handling begins with the opening of a file and ends with its closing. A file can be opened in several modes, and we must know the exact significance of each mode. Opening a file in the wrong mode can lead to errors—or even disaster. File closing is not mandatory for most situations, even though it is a good idea to explicitly close a file when you no longer need it.

When a file is opened, the OS associates a *stream* with the file. Because C treats all devices as files and device characteristics vary, it is logical that read/write operations are performed on the stream rather than to the device directly. The OS connects one end of the stream to the physical file and the other end to the program. This means that any read/write operation on the stream actually accesses the file on disk. The stream is disconnected when the file is closed.

#### 15.3.1 fopen: Opening a File

| | |
|---|---|
| Prototype: | `FILE *fopen(pathname, mode);` |
| Return value: | A pointer to FILE, or NULL on error. |

The **fopen** function needs two strings as arguments—the pathname of the file and its mode of opening. The *pathname* can be an absolute one (like `"/data/foo.txt"`) or a simple one (`"foo.txt"`). The *mode* is usually `"r"`, `"w"` or `"a"` for simple read, write and append operations, but we’ll also learn to use the `+` suffix for read/write operations. The following code shows the simplest way of using **fopen**:

```
FILE *fp;
fp = fopen("foo.txt", "r");
```

> Defines file pointer  
> Only reading permitted

If the call is successful, **fopen** returns a pointer to a structure typedef’d to FILE, so the pointer needs to be defined first. The file is opened for reading (`"r"`); you can’t write to this file. The pointer variable, fp, assigned by **fopen** now acts as a file handle which will be used subsequently by all functions that access the file. Once a file has been opened, its pathname is not required any longer.

#### 15.3.2 File Opening Modes

We opened the file `foo.txt` for reading, but **fopen** supports a number of options to represent the mode. These options enable you to write, append and also update a file (Table 15.1). For the time being, you need to keep in mind the following modes:

- `r` Reading a file.
- `w` Writing a file.
- `a` Appending to the end of an existing file.

**fopen** used with `"r"` as the mode expects the file to exist, but when used with `"w"`, it overwrites an existing file or creates one if the file doesn’t exist. When used with `"a"`, **fopen** also creates a file if

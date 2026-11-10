
```
gets(newname);

/* Rename the file */
if(rename(oldname, newname) == 0)
    printf("Renamed %s to %s.\n", oldname, newname);
else
    perror("rename");
    return 0;
}
```

- **Note**
  - The copy and delete operations are also associated with file management.
  - In case of `remove()` function, the only precondition is that the specified file must not be open.
  - The only restriction in `rename()` function is that both names must refer to the same disk drive; a file cannot be renamed on a different disk drive.

### 15.9 LOW-LEVEL I/O

This form of I/O is unbuffered. This means that, each read or write request results in accessing the disk (or device) directly to fetch/put a specific number of bytes. There are no formatting facilities. Instead of file pointers, we use low-level file handles or file descriptors, which give a unique integer number to identify each file.

To open a file the following function is used.

`int open(char *filename, int flag, int perms);`

The above function returns a file descriptor or -1 for a failure. The flag controls the file access and has the following predefined in `fcntl.h`: `O_APPEND`, `O_CREAT`, `O_EXCL`, `O_RDONLY`, `O_RDWR`, `O_WRONLY`, and others. `perms` is best set to 0 for most of our applications.

The function `creat(char *filename, int perms);` can also be used to create a file.

`int close(int handle);` can be used to close a file.

The following functions are used to read/write a specific number of bytes from a file stored or to be put in the memory location specified by buffer.

```
int read(int handle, char *buffer, unsigned length);
int write(int handle, char *buffer, unsigned length);
```

The `sizeof()` function is commonly used to specify the length. The `read()` and `write()` functions return the number of bytes read/written or -1 if they fail.

- **Note**
  - Low-level I/O has no formatting facilities.
  - Instead of file pointers, low-level file handles or file descriptors, which give a unique integer number to identify each file, are used.

## SUMMARY

Data can also be stored in disk files. C treats a disk file like a stream (a sequence of characters), just like the predefined streams stdin, stdout, and stderr. A stream associated with a disk file must be opened using the fopen() library function before it can be used, and it must be closed after use through the fclose() function. A disk file stream can be opened either in text or in binary mode.

After a disk file has been opened, data can be read from the file, written into the file, or both. Data can be accessed either in a sequential manner or in a random manner. Each open disk file has an associated file position indicator. This indicator specifies the position in the file, measured as the number of bytes from the start of the file, where subsequent read and write operations occur. In some cases, the position indicator is updated automatically by the system, and programmers do not have to be bothered with it. For random file access, the C standard library provides functions such as fseek(), ftell(), and rewind() for manipulating the position indicator.

Finally, C provides some rudimentary file management functions, allowing deletion and renaming of disk files. Low-level file handling functions that do not use formatting and file position indicators are also available.

## KEY TERMS

- **Binary file** It is a collection of bytes or a character stream. The data that is written into and read from binary file remains unchanged, with no separation between lines and no use of end-of-line characters and the interpretation of the file is left to the programmer.
- **Buffer** It is a block of memory used for temporary storage of data being written to and read from the file. It serves as an interface between the stream (which is character-oriented) and the disk hardware (which is block-oriented).
- **File management** It refers to all operations related to creating, renaming, deleting, merging, reading, writing, etc. of any type of files.
- **Path** It specifies the drive and/or directory (or folder) where the file is located. On PCs, the backslash character is used to separate directory names in a path. Some systems like UNIX use the forward slash (/) as the directory separator.
- **Random file access** It means reading from or writing to any position in a file without reading or writing all the preceding data by controlling the position indicator.
- **Record** It consists of a collection of data fields that conforms to a previously defined structure that can be stored on or retrieved from a file.

- 7. What is a stream? Describe two different methods of creating a stream-oriented data file.
- 8. What are the three general methods of file access?
- 9. What is EOF? When is it used?
- 10. Describe the different methods for reading from and writing into a data file.
- 11. What is the difference between a binary file and a text file in C?
- 12. Compare `fscanf()` and `fread()` functions.
- 13. What is the purpose of the `feof()` function?
- 14. How do you detect the end of a file in text and binary modes? Write a code to close all file streams.
- 15. Indicate two different ways to reset the file position pointer to the beginning of the file.
- 16. Is anything wrong with the following program?

```
FILE *fp;
int c;
if ((fp = fopen(oldname, "rb")) == NULL)
    return -1;
while ((c = fgetc(fp)) != EOF)
    fprintf(stdout, "%c", c);
fclose(fp);
```

- 17. Write a program to copy one existing file into another named file.
- 18. Write a complete C program that can be used as a simple line-oriented text editor. The program must have the following capabilities:
  - (i) Enter several lines of text and store them in a data file
  - (ii) List the data file
  - (iii) Retrieve and display a particular line
- 18. (continued)
  - (iv) Insert n lines
  - (v) Delete n lines
  - (vi) Save the new text and exit
  Carry out these tasks using different functions.
- 19. Write a program that opens a file and counts the number of characters. The program should print the number of characters when finished.
- 20. Write a program to compare two files and print out the lines where they differ.
- 21. Write an interactive C program that will maintain a list of roll, name, and total marks of students. Consider the information associated with each roll to be a separate record. Represent each record as a structure. Include a menu that will allow the user to select any of the following:
  - (i) Add a new record
  - (ii) Delete a record
  - (iii) Modify a record
  - (iv) Retrieve and display an entire record for a given roll or name
  - (v) Display all records
  - (vi) End of computation
- 22. Write a program that opens an existing text file and copies it to a new text file with all lowercase letters changed to capital letters and all other characters unchanged.
- 23. Write a function that opens a new temporary file with a specified mode. All temporary files created by this function should automatically be closed and deleted when the program terminates.
- 24. Write a C code that will read a line of characters (terminated by a `\n`) from a text file into a character array called buffer. NULL terminates the buffer upon reading a `\n`.

## Project Questions

- 1. Write a C program that takes the name of a file as a command-line argument, opens the file, reads through it to determine the number of words in each sentence, displays the total number of words and sentences, and computes the average number of words per sentence. The results should be printed in a table (as standard output), such as shown below:

  This program counts the words and sentences in file “comp.text”.

  ```
  Sentence: 1   Words: 29
  Sentence: 2   Words: 41
  Sentence: 3   Words: 16
  Sentence: 4   Words: 22
  Sentence: 5   Words: 44
  Sentence: 6   Words: 44
  Sentence: 7   Words: 32
  ```

  File “comp.text” contains 198 words in 7 sentences for an average of 28.3 words per sentence.

  In this program, you should count a word as any contiguous sequence of letters, and apostrophes should be ignored. Thus, “O’Henry”, “government’s”, and “friend’s” should each be considered as one word.

  Also in the program, you should think of a sentence as any sequence of words that ends with a period, exclamation point, or question mark. A period after a single capital letter (e.g., an initial) or embedded within digits (e.g., a real number) should not be counted as being the end of a sentence. White space, digits, and other punctuation should be ignored.
- 2. Write a C program that removes all comment lines from a C source code.

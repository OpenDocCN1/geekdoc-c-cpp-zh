```
```c
}
fclose(fp);
}
```
```

**Output**

```
```
Input file name
INVENTORY
Input inventory data
```
```

| Item name | Number | Price | Quantity |
| --- | --- | --- | --- |
| AAA-1 | 111 | 17.50 | 115 |
| B8B-2 | 125 | 36.00 | 75 |
| C-3 | 247 | 31.75 | 104 |

| Item name | Number | Price | Quantity | Value |
| --- | --- | --- | --- | --- |
| AAA-1 | 111 | 17.50 | 115 | 2012.50 |
| B8B-2 | 125 | 36.00 | 75 | 2700.00 |
| C-3 | 247 | 31.75 | 104 | 3302.00 |

**Fig. 14.3**   *Operations on mixed data types*

# ## 14.5 ERROR HANDLING DURING I/O OPERATIONS    LO 14.3

It is possible that an error may occur during I/O operations on a file. Typical error situations include the following:

+   1. Trying to read beyond the end-of-file mark.
+   2. Device overflow.
+   3. Trying to use a file that has not been opened.
+   4. Trying to perform an operation on a file, when the file is opened for another type of operation.
+   5. Opening a file with an invalid filename.
+   6. Attempting to write to a write-protected file.

If we fail to check such read and write errors, a program may behave abnormally when an error occurs. An unchecked error may result in a premature termination of the program or incorrect output. Fortunately, we have two status-inquiry library functions: **feof** and **ferror** that can help us detect I/O errors in the files.

The **feof** function can be used to test for an end of file condition. It takes a **FILE** pointer as its only argument and returns a nonzero integer value if all of the data from the specified file has been read, and returns zero otherwise. If **fp** is a pointer to file that has just been opened for reading, then the statement

```
```c
if(feof(fp))
    printf("End of data.\n");
```
```

would display the message “End of data.” on reaching the end of file condition.

The **ferror** function reports the status of the file indicated. It also takes a **FILE** pointer as its argument and returns a nonzero integer if an error has been detected up to that point, during processing. It returns zero otherwise. The statement
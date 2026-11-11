# 14.6 RANDOM ACCESS TO FILES

LO 14.4

So far we have discussed file functions that are useful for reading and writing data sequentially. There are occasions, however, when we are interested in accessing only a particular part of a file and not in reading the other parts. This can be achieved with the help of the functions **fseek**, **ftell**, and **rewind** available in the I/O library.

**ftell** takes a file pointer and return a number of type **long**, that corresponds to the current position. This function is useful in saving the current position of a file, which can be used later in the program. It takes the following form:

```
```c
n = ftell(fp);
```
```

**n** would give the relative offset (in bytes) of the current position. This means that n bytes have already been read (or written).

**rewind** takes a file pointer and resets the position to the start of the file. For example, the statement

```
```c
rewind(fp);
n = ftell(fp);
```
```

would assign **0** to **n** because the file position has been set to the start of the file by **rewind**. Remember, the first byte in the file is numbered as 0, second as 1, and so on. This function helps us in reading a file more than once, without having to close and open the file. Remember that whenever a file is opened for reading or writing, a **rewind** is done implicitly.

**fseek** function is used to move the file position to a desired location within the file. It takes the following form:

```
```c
fseek(file_ptr, offset, position);
```
```

**file_ptr** is a pointer to the file concerned, **offset** is a number or variable of type long, and **position** is an integer number. The **offset** specifies the number of positions (bytes) to be moved from the location specified by **position**. The **position** can take one of the following three values:

| Value | Meaning |
| --- | --- |
| 0 | Beginning of file |
| 1 | Current position |
| 2 | End of file |

The offset may be positive, meaning move forwards, or negative, meaning move backwards.

Examples in Table 14.2 illustrate the operations of the **fseek** function:

**Table 14.2** Operations of fseek Function

| Statement | Meaning |
| --- | --- |
| fseek(fp,0L,0); | Go to the beginning. (Similar to rewind) |
| fseek(fp,0L,1); | Stay at the current position. (Rarely used) |
| fseek(fp,0L,2); | Go to the end of the file, past the last character of the file. |
| fseek(fp,m,0); | Move to (m+1)th byte in the file. |
| fseek(fp,m,1); | Go forward by m bytes. |
| fseek(fp,m-1); | Go backward by m bytes from the current position. |
| fseek(fp,-m,2); | Go backward by m bytes from the end. (Positions the file to the mth character from the end.) |
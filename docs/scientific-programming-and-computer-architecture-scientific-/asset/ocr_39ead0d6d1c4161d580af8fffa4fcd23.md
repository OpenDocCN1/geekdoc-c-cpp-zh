# 6.3. MPI examples

which marks the beginning of the file view of the calling process, as already explained.
The third argument is the elementary type, and the fourth argument is the file type for accessing the file. The elementary and file types are used to specify file views of mind-bending complexity. Lines 13 and 14 give both arguments as MPI_BYTE, thus specifying the process's view of the file as a sequence of bytes keeps things simple for the programmer, the MPI implementation, the file system, and the fifth argument of type char * and not const * is given as datapare (line 15). The variable datapare holds the character string "native" (lines 9 and 10). Presumably, a byte is a byte in the native representation. The final info argument is given as null on line 16.

The MPI_File_write_at() call spanning lines 21 through 26 gets down to the business of writing to the file. There is a problem. The count (line 24) of the number of bytes to be written is an int and not a long. The process will not be to write all the data in

```
data[0], ..., data[len-1]
```

if len, is of type long, is greater than $2^{31}-1$. However, the offset relative to the beginning of the file view can be of type long (line 22). The variable maxcount, which is the maximum number of bytes the process will write with a single function call, is initialized to $2 	imes 10^9$ (which is less than $2^{31}-1$) on line 18. The while-loop spanning lines 19 through 30 writes to the file in stages. The variable len is the number of bytes to be written at the top of the loop, and line 20 calculates the count of bytes to be written in the current iteration. Once the data is written, the variable offset, which is the offset relative to the beginning of the file, and data, points to the first entry in the array that is yet to be written, are incremented by count (lines 27 and 28). The variable len is decremented by count (line 29) because the number of bytes to be written is fewer by count.

The library function MPI_File_write_at() is not collective, but MPI provides a collective version (obtained by appending all to the function name). The collective version would deadlock if the while-loop spanning lines 11 through 30 did not have exactly the same iteration over every MPI process. Therefore, we have used the noncollective version. The collective version can be slightly faster, however.

The MPI_File_close() is collective, like the calls for opening a file and setting its view. Calls to a collective MPI function made by different processes must match. As long as we restrict ourselves to the MPI_BYTE data type, the matching
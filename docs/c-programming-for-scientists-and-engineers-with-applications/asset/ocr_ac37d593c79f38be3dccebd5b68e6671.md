indicates that fptr is a pointer variable. This declaration declares fptr as a file pointer. The program only uses the file pointer fptr, and not the external file name. The file pointer declared in the program space is connected to the external data file by using a file open statement. The file open statement will be discussed in detail in Section 3.2.2.

If several file pointers are needed they can be declared in one statement as follows:

```
FILE *inptr, *outptr;
```

The two pointer variables inptr and outptr are declared in the same declaration statement. The file pointer inptr would be used to reference the input file and file pointer outptr, to reference the output file.

> Warning: Do not use an external file name in any place other than the open statement. Once the external file is opened all references to the file must be made through the file pointer.

# 3.2.2 open and close Statements

Data files normally stored on the disk have a file name with the dat extension. Files with this extension are external to any program. The internal file pointer declared within the program, and the external files on the disk, are connected logically and physically by using an open statement. Once the external file and the internal file pointer are connected, the connection will remain in effect until either the file is closed or the program is terminated. After the file is opened for input or output, the program can communicate with the file on the disk through the file pointer. Note that if the file is already open and the program attempts to open it again the file open statement, when executed, will return a null value. The file can be closed explicitly by using an fclose statement. Once the file is closed it is disconnected from the program. If it has been disconnected, it can beconnected and opened again.

open Statement For a program to communicate with an external file through the internal file pointer, the internal file pointer must be connected to the external file by means of an fopen statement. The general form of the fopen statement to is
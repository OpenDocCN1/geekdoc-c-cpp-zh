
indicates that fptr is a pointer variable. This declaration declares fptr as a file pointer. The program only uses the file pointer fptr, and not the external file name. The file pointer declared in the program space is connected to the external data file by using a file open statement. The file open statement will be discussed in detail in Section 3.2.2.

If several file pointers are needed they can be declared in one statement as follows:

```
FILE *inptr, *outptr;
```

The two pointer variables inptr and outptr are declared in the same declaration statement. The file pointer inptr would be used to reference the input file and file pointer outptr, to reference the output file.

> Warning: Do not use an external file name in any place other than the open statement. Once the external file is opened all references to the file must be made through the file pointer.

## 3.2.2 open and close Statements

Data files normally stored on the disk have a file name with the dat extension. Files with this extension are external to any program. The internal file pointer declared within the program, and the external files on the disk, are connected logically and physically by using an open statement. Once the external file and the internal file pointer are connected, the connection will remain in effect until either the file is closed or the program is terminated. After the file is opened for input or output, the program can communicate with the file on the disk through the file pointer. Note that if the file is already open and the program attempts to open it again the file open statement, when executed, will return a null value. The file can be closed explicitly by using an fclose statement. Once the file is closed it is disconnected from the program. If it has been disconnected, it can be connected and opened again.

open Statement

For a program to communicate with an external file through the internal file pointer, the internal file pointer must be connected to the external file by means of an fopen statement. The general form of the fopen statement is to connect the external data file name, for example "myfile.dat", on the disk to the internal file pointer fptr declared within the program is as follows:

```
FILE *fptr;
```

```
fptr = fopen("myfile.dat", mode);
```

Where fopen is a function call that returns a link to the external file, fptr is the declared file pointer, and mode is simply the way the file is to be used. There are three common modes of operation, they are: read (r), write (w), and append (a). In read mode the file is opened for data, in write mode the file is opened to receive output, and in append mode the file is opened for adding data to the end of the file. Opening the file for modes r or w positions the file at the beginning. Opening the file for mode a positions the file at the end.

An fopen() function using read mode must reference an existing file. If the file does not exist or the file is already opened the function will return a null pointer rather than a pointer to the file. The program must then check whether the file has been opened successfully.

In write mode, if the file already exists, its contents will be erased and over-written from the beginning of the file. If the file does not exist it will be created and written from the beginning of the file. If the file is already open, the function will return a null value rather than a pointer to the file and the file will be unavailable.

In append mode, if the file exists the new data will be added to the end of the existing data. If the file does not exist the file will be created and the data will be written starting at the beginning of the file. If the file is already open, the function will return a null pointer rather than a pointer to the file.

The open statements for different modes of input and output operations are as follows:

```
fptr = fopen("myfile.dat", "r");
```
Reads if the file exists, error if the file does not exist.

```
fptr = fopen("myfile.dat", "w");
```
Writes to the file from beginning if the file exists. Creates a new file and writes to the file from the beginning if the file does not exist.

```
fptr = fopen("myfile.dat", "a");    # Appends to the end of the file if the file exists. Creates and writes to the new if the file does not exist.
```

```
fptr = fopen("myfile.dat", "r+");    # Opens file for reading and writing if the file exists, error if the file does not exist.
```

```
fptr = fopen("myfile.dat", "w+");    # Opens a new file for reading and writing if the file exists. Creates a new file if the file does not exist.
```

```
fptr = fopen("myfile.dat", "a+");    # Opens the file for reading and writing at the end of the file if the file exists. Creates a new file if the file does not exist.
```

```
fptr = fopen("myfile.dat", "wb");    # Opens the binary file for writing.
```

```
fptr = fopen("myfile.dat", "r+b"); # Opens the binary file for reading and writing.
```

The fopen function requires two arguments: a character string, which is the external name of the data file, and a character string, which indicates the use of the file.

Once the file is opened in any of these modes the program can communicate with the data file on the disk through the pointer. Once the file is closed it is disconnected from the program.

close Statement

The fclose statement disconnects the file from the program. The general form of the fclose statement is:

```
fclose(fptr);
```

## 3.2 File Input and Output

### 3.2.3 Input from a Data File

The input from a data file is obtained by calling the fscanf function. The general form is:

```
fscanf(fptr, "format", &var1, &var2, ...);
```

The first argument is the file pointer, the second argument is the format string that specifies the data to be read. The remaining arguments are the addresses of the variables. If there is not enough data in the file the fscanf function returns a special EOF (end-of-file) flag.

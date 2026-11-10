![](bbox=[0.04, 0.06, 0.42, 0.14])

However, if the filename is entered by the user through the keyboard, a single backslash has to be entered. Not all systems use the backslash as the directory separator. For example,

UNIX uses the forward slash (/).

# ### File modes—What sort of open

Before a file can be used for reading or writing, it must be opened. This is done through the fopen() function. fopen() takes two string arguments. The first of these is the filename; the second is an option that conveys to C what processing is to be done with the file: read it, write to it, append to it, etc. Table 15.1 lists the options available with fopen().

**Table 15.1 File opening modes**

| Mode | Meaning |
|---|---|
| r | Open a text file for reading |
| w | Create a text file for writing |
| a | Append to a text file |
| rb | Open a binary file for reading |
| wb | Open a binary file for writing |
| ab | Append to a binary file |
| r+ | Open a text file for read/write |
| w+ | Create a text file for read/write |
| a+ | Append or create a text file for read/write |
| r+b | Open a binary file for read/write |
| w+b | Create a binary file for read/write |
| a+b | Append a binary file for read/write |

The following statements are used to create a text file with the name `data.dat` under current directory. It is opened in `w` mode as data is to be written into the file `data.dat`.

```
````c
FILE *fp;
fp = fopen("data.dat","w");
````
```

fopen() requires two parameters—both are character strings. Either parameter could be a string variable. The following is an example where a file pointer *fp is declared, the file name, which is declared to contain a maximum of 80 characters, is obtained from the keyboard and then the file is opened in the “write” mode.

```
````c
char filename[80];
FILE *fp;
printf("Enter the filename to be opened");
gets(filename);
fp = fopen(filename,"w");
````
```

# ### Checking the result of fopen()

The fopen() function returns a FILE *, which is a pointer to structure FILE, that can then be used to access the file. When the file cannot be opened due to reasons described below, fopen() will return NULL. The reasons include the following.

+   - Use of an invalid filename
+   - Attempt to open a file on a disk that is not ready; for example, the drive door is not closed or the disk is not formatted
+   - Attempt to open a file in a non-existent directory or on a non-existent disk drive
+   - Attempt to open a non-existent file in mode r

One may check to see whether fopen() succeeds or fails by writing the following set of statements.

```
````c
fp = fopen("data.dat","r");

if(fp == NULL)
{
    printf("Can not open data.dat\\n");
    exit(1);
}
````
```

![](bbox=[0.72, 0.32, 0.89, 0.38])

Alternatively, the above segment of code can be written as follows.

```
````c
FILE *fp;
if((fp = fopen("data.dat", "r")) ==NULL)
{
    printf("Can not open data.dat\\n");
    exit(1);
}
````
```

Whenever fopen() is used in a program, it is recommended to test for the result of an fopen() and check whether it is NULL or not. There is no way to find exactly which error has occurred, but one can display an error message to the user and try to open the file again, or end the program.

# ### 15.2.3 Closing and Flushing Files

After completing the processing on the file, the file must be closed using the fclose() function. Its prototype is

```
int fclose(FILE *fp);
```

The argument fp is the FILE pointer associated with the stream; fclose() returns 0 on success or -1 on error. When a program terminates (either by reaching the end of main() or by executing the exit() function), all streams are automatically flushed and closed. Generally, in a simple program, it is not necessary to close the file because the system closes all open files before returning to the operating system. It would be a good programming practice to close all files.
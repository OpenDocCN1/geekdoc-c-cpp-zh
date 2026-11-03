```
programmer and the operating system takes care of all these things.
typedef struct{
..........
..........
}FILE;
```

A file pointer is a pointer to a structure of type FILE. Whenever a file is opened, a structure of ty FILE is associated with it, and a file pointer that points to this structure identifies this file. The functi fopen() is used to open a file.

# Declaration:

```
FILE *fopen( const char *filename, const char *mode);
```

fopen() function takes two strings as arguments, the first one is the name of the file to be open and the second one is the mode that decides which operations( read, write, append etc) are to performed on the file. On success, fopen() returns a pointer of type FILE and on error it returns NUL The return value of fopen( ) is assigned to a FILE pointer declared previously. For example-

```
FILE *fp1, *fp2;
fp1 = fopen ( "myfile.txt", "w" );
fp2 = fopen ( "yourfile.dat", "r" );
```

The name of a file is limited to FILENAME_MAX characters. After opening the file with fopen( ), name of file is not used in the program for any operation on it. Whenever we have to perform a operation on the file, we'll use the file pointer returned by fopen( ) function. So the name of file sometimes known as external name, while the file pointer associated with it is known as its inter name. The second argument represents the mode in which the file is to be opened. The possible val of mode are-

+   1. "w" ( write )
+   If the file doesn't exist then this mode creates a new file for writing, and if the file already exists th the previous data is erased and the new data entered is written to the file.
+   
+   2. "a" ( append )
+   If the file doesn't exist then this mode creates a new file, and if the file already exists then the n data entered is appended at the end of existing data. In this mode, the data existing in the file is erased as in "w" mode.
+   
+   3. "r" ( read )
+   This mode is used for opening an existing file for reading purpose only. The file to be opened m exist and the previous data of file is not erased.
+   
+   4. "w+" ( write+read )
+   This mode is same as "w" mode but in this mode we can also read and modify the data. If the doesn't exist then a new file is created and if the file exists then previous data is erased.
+   
+   5. "r+" ( read+write )
+   This mode is same as "r" mode but in this mode we can also write and modify existing data. The to be opened must exist and the previous data of file is not erased. Since we can add new data modify existing data so this mode is also called update mode.
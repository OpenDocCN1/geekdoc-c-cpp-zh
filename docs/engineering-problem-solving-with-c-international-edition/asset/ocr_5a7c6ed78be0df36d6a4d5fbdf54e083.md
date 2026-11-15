When debugging programs read information from data files, echo (or print) the information read from the file to be sure that the data are being read properly. If the data values are all zero, or are unusual numbers, it may be possible that the program cannot find the file because it is in a directory that the program cannot access. The solution is either to move the file to a directory that the program can access or to change some of the operating system parameters so that the program can find the file.

![](bbox=[0.13, 0.08, 0.2, 0.18])

In the examples that follow, we use data files containing sensor data. For this discussion, we assume that the sensor is a seismometer. Seismometers are usually buried near the surface of the earth and record earth motion. These sensors are very sensitive and can record tidal motion, even though they may be located hundreds of miles from the ocean. Seismometer data are collected from sensors all over the earth, and are sent by satellite to central locations for collection and analysis. By studying this motion, scientists and engineers may someday be able to predict earthquakes from seismometer data.

# I/O Statements

Each data file used in a program must have a file pointer associated with it. If a program uses two files, then each file requires a different file pointer. A file pointer is defined with a FILE declaration, as in

```
FILE *sensor1;
```

The FILE data type is defined in the header file stdio.h, and thus the word FILE is capitalized to match the definition in the header file. The asterisk before the identifier specifies that the identifier is a pointer. Later chapters include more information on pointers; in this section, we present only the statements needed to work with file pointers.

After a file pointer is defined, it must then be associated with a specific file. The fopen function obtains the information needed to assign a file pointer to a specific file. The two arguments for this function are the file name and a character that indicates the file status, which is also called the file open mode; both the file name and the character need to be enclosed in double quotes. If we are going to read information from a file with a program, the file open mode is r for read. If we are going to write information to a file with a program, the file open mode is w for write. Thus, the following statement specifies that the file pointer sensor is going to be used with a file named sensor1.txt, from which we will read information:

```
sensor = fopen("sensor1.txt","r");
```

If a data file cannot be opened, fopen returns a value of NULL. (NULL is a symbolic constant defined in <stdio.h> and has the value of a character zero.) A common reason that a program might not be able to open a data file is because the file cannot be found by the program.

![](bbox=[0.13, 0.72, 0.2, 0.76])

Therefore, to be sure that our programs find their data files, it is good practice to check the value returned by fopen to ensure that the file was successfully opened. The following statements open a file referenced by file1; if the file is not successfully found, an error message is printed and the rest of the if statement is skipped:

```
file1 = fopen(FILENAME,"r");
if (file1 == NULL)
    printf("Error opening input file \n");
else
{
    ...
}
```

```c
char tempName[20];

fp = fopen("D:\\studentRecords.dat", "wb+");

if(!fp)
{
    printf("\n Cannot Open File ");
    exit(0);
}

do
{
    printf("\n 1. Add Records to a file ");
    printf("\n 2. Display Records ");
    printf("\n 3. Modify Record ");
    printf("\n 4. Delete Record ");
    printf("\n 5. Exit");
    printf("\n Enter your choice -> ");
    scanf("%d", &choice);

    switch(choice)
    {
        case 1:
            fflush(stdin);
            fseek(fp, 0, SEEK_END);
            printf("\n Enter Name Class Age ->");
            scanf("%s %d %d", &stu.name, &stu.class, &stu.age);
            fwrite(&stu, sizeof(stu), 1, fp);
            break;
        case 2:
            rewind(fp);
            while(fread(&stu, sizeof(stu), 1, fp))
            {
                printf("\n %s %d %d ", stu.name, stu.class, stu.age);
            }
            break;
        case 3:
            fflush(stdin);
            rewind(fp);
            printf("\n Enter Name of the Student -> ");
            gets(tempName);
            while(fread(&stu, sizeof(stu), 1, fp))
            {
                if(!strcmp(stu.name, tempName))
                {
                    fflush(stdin);
                    printf("\n Enter New Name Age Class ->");
                    scanf("%s %d %d", &stu.name, &stu.class, &stu.age);
                    fseek(fp, -sizeof(stu), SEEK_CUR);
                    fwrite(&stu, sizeof(stu), 1, fp);
                    break;
                }
            }
            break;
        case 4:
            fflush(stdin);
            rewind(fp);
            fd = fopen("D:\\temp.dat","wb");
            printf("\n Enter Student Name for Deletion -> ");
            gets(tempName);
            while(fread(&stu, sizeof(stu), 1, fp))
            {
                if(strcmp(tempName,stu.name))
                {
                    fwrite(&stu, sizeof(stu), 1, fd);
                }
            }
            fclose(fp);
            fclose(fd);
            remove("D:\\studentRecords.dat");
            rename("D:\\temp.dat","D:\\studentRecords.dat");
            fp = fopen("D:\\studentRecords.dat","rb+");
            break;
        default:
            break;
    }
} while(choice != 5);

fclose(fp);
getch();
return 0;
}
```

Output of the preceding program is as follows:

```text
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->BRIAN 1 5

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->CRISTINA 2 6

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
CRISTINA 2 6
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->RONALD 3 9

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 4

Enter Student Name for Deletion -> CRISTINA

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
RONALD 3 9
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->EMMIE 5 11

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
RONALD 3 9
EMMIE 5 11
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 3

Enter Name of the Student -> BRIAN

Enter New Name Age Class->VICKY 5 10

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

VICKY 5 10
RONALD 3 9
EMMIE 5 11
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 5
```

In Listing 5.26, a file is created in the binary mode and a file pointer is set up, which points to the first record of the file. The file pointer moves to the beginning of the next record on using the fread() and fwrite() functions; however, the file pointer gets deactivated on the closing of file. The movement of the file pointer is crucial in this program, as it controls the position from where fread() will read the next record and fwrite() will write the next record. The rewind() function places the file pointer to the beginning of the file. The fseek() function helps in moving the file pointer from one record to another. If we want to move to the previous record, then we can use the following syntax:

```c
fseek(fp, -(sizeof(stu)), SEEK_CUR);
```

Similarly, the following syntax moves the file pointer to the last record in the file:

```c
fseek(fp, 0, SEEK_END);
```

Now, let's discuss file management functions in C.

## File Management Functions

C provides several file management functions that can be used for performing various file related tasks. All the file management functions are defined in the <stdio.h> header file. Following are some file management functions in C:

- fclose()
- feof()
- ferror()
- fgetpos()
- freopen()
- ftell()

Let's learn about these functions, in detail.

### fclose()

The fclose() function closes the file associated with the stream and flushes its buffer. The signature of fclose() is given as follows:

```c
int fclose(FILE*stream);
```

After a call is made to fclose(), the stream no longer remains connected with the file and the allocated buffer automatically gets deallocated. On success, fclose() returns 0; else, it returns EOF.

### feof()

The feof() function determines whether the end of file associated with the stream has been reached. The signature of feof() is given as follows:

```c
int feof(FILE *stream);
```

If the file pointer is at the end of file, then a non-zero value is returned; else, 0 is returned. Listing 5.27 shows the working of feof():

Listing 5.27: Showing the Working of feof()

```c
#include<stdio.h>
int main()
{
    char *end_char;
    char sentence[100];
    FILE *fp;

    fp = fopen("D:\\readme.txt","r");

    if(!fp)
    {
        printf("\n Failed to open the file");
        return 0;
    }
    while(!feof(fp))
    {
        end_char = fgets(sentence, 100, fp);
        printf("%s \n",sentence);
    }

    fclose(fp); /* For closing the file pointer */
    getch();

    return 0;
}
```

In Listing 5.27, we have opened an already existing file in the read-only mode and fetched information from that file. The feof() function is used to signify whether the end of file has been reached or not. Fetching information from the file will continue until the end of file is reached.

### ferror()

The ferror() function checks for a file error on the given stream. The signature of ferror() is given as follows:

```c
int ferror(FILE *stream);
```

A return value of 0 indicates that no error has occurred, while a non-zero value means an error. Listing 5.28 shows the working of ferror():

Listing 5.28: Working with ferror()

```c
#include<stdio.h>
int main()
{
    char *end_char;
    char sentence[100];
    FILE *fp;

    fp = fopen("D:\\readme.txt","r");

    if(!fp)
    {
        printf("\n Failed to open the file");
        return 0;
    }
    while(!feof(fp))
    {
        end_char = fgets(sentence, 100, fp);
        if(ferror(fp)) {
            printf("\n Error Occurred while reading ");
        }
        printf("%s \n",sentence);
    }

    fclose(fp); /* for closing the file pointer */
    getch();

    return 0;
}
```

In Listing 5.28, we are reading information from a file, which is opened in the read-only mode. While reading from the file, if we encounter any error, the error will be notified by the ferror() function and appropriate measures can be taken against it.

### fgetpos()

The signature of fgetpos() is given as follows:

```c
int fgetpos(FILE *stream, fpos_t *position);
```

The fgetpos() function stores the current value of the file pointer in the object pointed to by position. The object pointed to by position must be of type fpos_t. If an error occurs, then fgetpos() returns a non-zero value; else, it returns 0.

### freopen()

The freopen() function associates an existing stream with a different file. The end of file and error flags are cleared in the process. The signature of freopen() function is given as follows:

```c
FILE *freopen(const char *fname, const char *mode, FILE *stream);
```

The new file's name is pointed to by fname, the access mode is pointed to by mode, and the stream to be reassigned is pointed to by stream.

### ftell()

The ftell() function returns the current value of the file pointer for the specified stream. The signature of ftell() function is given as follows:

```c
long int ftell(FILE *stream);
```

For binary streams, the value is in number of bytes. For text streams, the return value may not be meaningful because of possible character translations, such as carriage return/linefeeds being substituted for newlines, which affect the apparent size of the file.

Next, let's discuss bitwise operators in C.

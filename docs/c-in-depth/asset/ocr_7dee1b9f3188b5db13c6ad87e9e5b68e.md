```
```c
/* P11.9 Program to understand the use of fscanf() */
#include<stdio.h>
struct student
{
    char name[20];
    float marks;
};
stu;
main()
{
    FILE *fopen(),*fp;
    fp=fopen("students.dat","r");
    printf("NAME\tMARKS\n");
    while(fscanf(fp,"%s%f",stu.name,&stu.marks)!=EOF)
        printf("%s\t%f\n",stu.name,stu.marks);
    fclose(fp);
}
```
```

We had mentioned earlier that the file pointers stdout and stdin are automatically opened. If we use these file pointers in the functions fprintf() and fscanf(), then these function calls become equivalent to printf() and scanf().

If we replace the file pointer fp by stdout then-
 fprintf( stdout, "My age is %d", age); is equivalent to printf("My age is %d", age);

If we replace the file pointer fp by stdin then-
 fscanf(stdin,"%s%d", name, &age); is equivalent to scanf("%s%d", name, &age);

# 11.12 Block Read / Write

It is useful to store blocks of data into file rather than individual elements. Each block has some fixed size, it may be a structure or an array. It is easy to read the entire block from file or write the entire block to the file. There are two useful functions for this purpose- fread() and fwrite(). Although we can read or write any type of data varying from a single character to arrays and structures through these functions, these are mainly used to read and write structures and arrays.

For using these functions, the file is generally opened in binary mode( e.g. "wb", "rb" ).

# 11.12.1 fwrite()

This function is used for writing an entire block to a given file.
Declaration: size_t fwrite( const void *ptr, size_t size, size_t n, FILE *fptr );
size_t is defined in stdio.h as-
typedef unsigned int size_t;
ptr is a pointer which points to the block of memory that contains the information to be written to the file, size denotes the length of each item in bytes, n is the number of items to be written to the file, and fptr is a FILE pointer which points to the file to which the data is written.
If successful, fwrite( ) will write n items or total ( n * size ) bytes to the file and will return n. On error or end of file it will return a number less than n.
To write a single float value contained in variable fval to the file
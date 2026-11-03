# 14.11.11 fopen( )

Declaration: FILE *fopen(const char *filename, const char *mode, FILE *fptr);

This function is used to associate a new file with a file pointer. The file associated with fptr is closed as by fclose(), after that the filename that is specified in the first argument is opened in the specified mode as by fopen(), and this fptr is now associated with this file. On success fopen() returns fptr, and on error it returns NULL.

This function is generally used to change the files associated with file pointers stdin, stdout and stderr. For example the file pointer stderr is associated with the screen, if we want to store the error messages in a file instead of displaying them on the screen, then we can use fopen() as- fopen("errorfile", "a", stderr);

# 11.15 Command Line Arguments

The function main() can accept two parameters. The definition of main() when it accepts parameters can be written as-

```
main(int argc,char *argv[ ])
```

The first parameter is of type int and the second one is an array of pointers to strings. These parameters are conventionally named argc(argument counter) and argv(argument vector), and are used to access the arguments supplied at the command prompt. Let us see how this is done.

The program is compiled and executable file is created. In DOS, name of the executable file is same as the name of the program and it has a .exe extension. In UNIX, the executable file is named as a.out. We can give any other name to the executable file in UNIX using -o option as- cc -o myprog myprog.c

Now the program is executed at the command prompt, and arguments are supplied to it. The first argument is always the name of executable file. The parameters argc and argv can be used to access the command line arguments. The parameter argc represents the number of arguments on command line. All the arguments supplied at the command line are stored internally as strings and their addresses are stored in the array of pointers named argv.

```
/*11.27 Program to understand command line arguments*/
#include<stdio.h>
main(int argc,char *argv[ ])
{
int i;
printf("argc=%d\n",argc);
for(i=0;i<argc;i++)
printf("argv[%d]=%s\n",i,argv[i]);
}
```

Suppose the name of the program is myprog.c and it is executed on the command prompt as- myprog you r 2 good

The variable argc will have value 5, since total five arguments are supplied at the command prompt. The first argument is the name of the program, so argv[0] points to the base address of string "myprog"
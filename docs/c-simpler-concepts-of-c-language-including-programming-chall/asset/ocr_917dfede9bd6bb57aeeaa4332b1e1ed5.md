# # 13
CHAPTER

# # C Programming
UNIX/LINUX

# ## 13.1. INTRODUCTION – GETTING STARTED WITH C PROGRAMMING IN LINUX

Writing a small C code in Linux with C programming will help the reader to understand the concept in a great way. The following simple code will just print welcome to the C programming world. GNU tool kit in Linux helps compile and execute C programs with GCC compilers. GCC is expanded as Gnu Compiler.

Here is the program presented along execution steps.
// Name the file as prog1.c and save it.

```
include <stdio.h>
int main ()
{
    printf("\n welcome to the C programming world");return 0;
}
```

Now to compile the program, written steps need to be followed. Before that it would be better to know the internal happenings when a file is compiled. When compilation is, firstly there is no compilation or syntax errors the object file will be formed and will be created with the extension .o. Then the object file will be made as an executable one process of linking with the library files. The executable file can then be run to get the above statement mentioned in C code printed.

All these in a sequence and are the commands presented for the same.
$ gcc -c prog1.c

In the above command, gcc is the compiler being used, expanded as GNU Compiler which will compile the code and get the object file. Object file will be generated with the same name as file name, here it is prog1.o “.o” is to just say it is an object file.

After the process is over, one should get an executable file for the above generated object file. It is again a simple process and can be carried out with the following command.
$ gcc -o executable prog1.o

Above command will convert the object file to an executable file after linking the file with necessary library files. To complete the execution step has to be followed.
$ ./executable
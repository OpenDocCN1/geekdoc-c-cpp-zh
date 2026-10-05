# C PROGRAMMING IN UNIX/LINUX

From the picture one can understand 0 is fd for standard input (key board), 1 is for standard output (monitor) and 2 is the number allotted for standard error message. Since 0,1 and 2 are allotted already newly created file will get number 2. For an instance if a file is created it will get 3 as the file descriptor and next file will created 4. Theoretically discussing would not be sufficient.

Writing a small C in Linux with C programming will help the reader to understand the concept in a great way. The following C code aims in creating 2 files. After creation one can manually check the file descriptor table easily and check if the files have been allotted with numbers as expected. GNU tool kit in Linux helps to compile and execute C programs with GCC compilers. GCC is expanded as Gnu Compiler. The following C file prog1.c simply creates 2 files txt1.txt and txt2.txt.

```
// prog1.c - C code for creating 2 files.
// create is the system call used to create new files through code.
// While loop in code will execute the code continuously so that user can check
// /proc file system.

#include <stdio.h>
int main ( {
    int fd1, fd2;
    printf("/n THIS WILL CREATE 2 FILES NOW");
    fd1 = create("txt1.txt", 0777);
    // create txt1.txt file through this system call, also file permissions
    // mentioned. Since every function in C will have a return value, this will also
    // have the same and here once the file is created, it will return an integer
    // which is being referred as file descriptor.
    fd2 = create("txt2.txt", 0777);
    while(1) {
    }
}
```

# 13.2.1. Execution procedure

User has to store the file with .c extension and once done the following command can be issued from prompt.

$ gcc -o prog1 prog1.c

Where

+   - Gcc is Compiler
- Prog1 - Executable file name
- Prog1.c - File name.
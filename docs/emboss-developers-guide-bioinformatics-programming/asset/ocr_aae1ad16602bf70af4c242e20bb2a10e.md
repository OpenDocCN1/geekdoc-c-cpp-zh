# Your first EMBOSS application

Most programming books begin with a program to write a simple phrase to the screen, and that phrase is invariably “Hello World!”. This section will lead you through the process of writing helloworld under EMBOSS. You’ll cover the basic elements common to every EMBOSS program and introduce the steps used to create applications.

Some of the examples below use myemboss (Section 3.2, ‘Integration and compilation’), so you must first install and configure this package. myemboss is a special EMBASSY package and is found in the normal EMBASSY application directory, e.g.

```
/home/auser/emboss/emboss/embassy/myemboss
```

# 2.1 helloworld in C

Here is the source code of a C program that prints “Hello World!” to the screen:

```
#include <stdio.h>
int main(void)
{
  printf("Hello World!\n");
  return 0;
}
```

The first line is a preprocessor directive telling the compiler to include the header file stdio.h. The angle brackets around the name of the file to be included tell the preprocessor to look in the default location for stdio.h. On a Linux system this default location is typically the directory /usr/include.

The program consists of a single function (main) which has no parameters and an integer return type, in this case it returns 0 to the operating system after printing “Hello World!” to the screen.

If you save the source code to a file called helloworld.c, then to get an executable (runnable) version of the program, you have to compile the source by typing one of the following commands.

Using gcc, an ANSI C compiler:
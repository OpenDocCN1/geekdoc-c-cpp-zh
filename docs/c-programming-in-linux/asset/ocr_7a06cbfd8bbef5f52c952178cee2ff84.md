Let's rewrite the program to see what all this means before we start to panic.

```
~~~c
/*
C Programming in Linux (c) David Haskins 2008
chapter1_2.c
*/
#include <stdio.h>

int main(int argc, char *argv[])
{
    int i=0;
    printf("Hello, you are learning C!!\n");
    printf("Number of arguments to the main function:%d\n", argc);
    for(i=0; i<argc; i++)
    {
        printf("argument number %d is %s\n", i, argv[i]);
    }
    return 0;
}
~~~
```

Save the text as **chapter1_2.c** in the same folder.

Open a terminal window and type:  
**gcc -o hello2 chapter1_2.c** to compile the program into a form that can be executed.

Now type **ls -l** to list the details of all the files in this directory. You should see that chapter1_2.c is there and a file called **hello2** which is the compiled C program you have just written.

Now type **./hello2** to execute, or run the program and it should return the text:

*Hello, you are still learning C!!*  
*Number of arguments to the main function:1*  
*argument number 0 is ./hello2*

We can see that the name of the program itself is counted as a command line argument and that the counting of things in the list or array of arguments starts at zero not at one.

Now type **./hello2 my name is David** to execute the program and it should return the text:

*Hello, you are still learning C!!*  
*Number of arguments to the main function:5*  
*argument number 0 is ./hello2*  
*argument number 1 is my*  
*argument number 2 is name*
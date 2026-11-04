```
int main ()
{
    FILE *fp;
    fpos_t position;

    fp = fopen("file.txt","w+");
    fgetpos(fp, &position);
    fputs("Hello, World!", fp);

    fsetpos(fp, &position);
    fputs("This is going to override previous content", fp);
    fclose(fp);

    return(0);
}
```

Let us compile and run the above program to create a file **file.txt** which will have the following content. First of all we get the initial position of the file using **fgetpos()** function and then we write *Hello, World!* in the file, but later we have used **fsetpos()** function to reset the write pointer at the beginning of the file and then over-write the file with the following content:

This is going to override previous content

Now let us see the content of the above file using the following program:

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    int n = 0;

    fp = fopen("file.txt","r");
    while(1)
    {
```
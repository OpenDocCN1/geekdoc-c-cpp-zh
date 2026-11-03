In Line 16, the base address of the highscore array is passed to fread() as the first argument. Next comes the size of each element to be read, the size of an int variable. Then comes the immediate value 5, effectively ordering fread() to scan in five values. The final argument is the file handle variable, confusingly named handle.

**Exercise 22-9:** Type the source code from Listing 22-6 into your editor. Build and run to see the five int values that were previously saved to the scores.dat file.

Because fread() can read any file's data, you can use it to create a file-dumper type of program, as shown in Listing 22-7.

# LISTING 22-7: A File Dumper

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char filename[255];
    FILE *dumpme;
    int x,c;

    printf("File to dump: ");
    scanf("%s",filename);
    dumpme=fopen(filename,"r");
    if(!dumpme)
    {
        printf("Unable to open '%s'\n",filename);
        exit(1);
    }
    x=0;
    while( (c=fgetc(dumpme)) != EOF)
    {
        printf("%02X ",c);
        x++;
        if(!(x%16))
            putchar('\n');
    }
    putchar('\n');
    fclose(dumpme);
    return(0);
}
```
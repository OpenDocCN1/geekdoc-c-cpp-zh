```
```c
fp = fopen("D:\\_readme.txt", "r");

if(!fp)
{
        printf("\n failed to open the file");
        return 0;
}
do
{
        character = fgetc(fp);
        printf("%c",character);
}while(character != EOF);
printf("\n EOF  {%d}",EOF);
fclose(fp); /* for closing the file pointer */
getch();

return 0;
}
```
```

While reading information from a file, if an unsigned char is used instead of a char, then the code will turn out into an infinite loop. However, some of the advanced compilers recognize this problem and provide warnings during compilation, such as:

> > [warning] comparison is always true due to limited range of data type

Now, let’s learn how to read words from a file.

# Reading Words from a File

Similar to characters, we can also read the words from a text file. Instead of using the fgetc() or getc() function, we have to use the fscanf() function, which is capable of reading one word from a file at a time. Listing 5.18 shows how to read words from a text file:

# Listing 5.18: Reading Words from a File

```
```c
#include<stdio.h>

int main()
{
    char end_char;
    char word[20];
    FILE *fp;

    fp = fopen("D:\\_readme.txt", "r");

    if(!fp)
    {
            printf("\n failed to open the file");
            return 0;
    }
    do
    {
            end_char = fscanf(fp, "%s", word);
            printf("%s \n",word);
    }while(end_char != EOF);

    fclose(fp); /* for closing the file pointer */
    getch();
    return 0;
}
```
```
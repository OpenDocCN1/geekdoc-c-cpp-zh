Most of the code in Listing 22-8 should be familiar to you if you’ve worked through earlier exercises in this chapter.

Exercise 22-12: Copy the code from Listing 22-8 into your editor. Build and run the program to create the bond.db file, and write one structure to that file.

Exercise 22-13: Modify the code from Listing 22-8 so that a new program is created. Have that program write two more records to the bond.db file. They must be appended to any existing data, not overwriting the original file. Use this data:

> Roger Moore, 1973, Live and Let Die
> Pierce Brosnan, 1995, GoldenEye

Good information in a file doesn’t do you any good unless you create code to read the data. Listing 22-9 reads in the three records written to the bond.db file, assuming that you’ve run program solutions to both Exercises 22-12 and 22-13.



```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    struct agent {
        char actor[32];
        int year;
        char title[32];
    };
    struct agent bond;
    FILE *jdbdb;
    int r;
    jdbdb = fopen("bond.db", "r");
    if(!jdbdb)
    {
        puts("SPECTRE wins!");
        exit(1);
    }
    while( !feof(jdbdb) )
    {
        r = fread(&bond,sizeof(struct agent),1,jdbdb);
        if( r!=0 )
            break;
    }
```
```
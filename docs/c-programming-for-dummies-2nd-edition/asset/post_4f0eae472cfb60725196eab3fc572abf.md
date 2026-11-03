
```
printf("%s",buffer);
}
fclose(fh);
return(0);
}
```

The fgets() function at Line 20 reads in a line of text (terminated by a newline) or 64 characters, whichever comes first. The function returns a pointer to the string read unless an error occurs, in which case NULL is returned. This value is saved in char pointer variable s, which is tested at Line 21.

**Exercise 22-4:** Type the source code from Listing 22-3 into your editor. Build and run.

## Appending text to a file

When you're using the fopen() function in the "a" mode, text is appended to an already existing file. Or when the file doesn't exist, the fopen() command creates a new file. At Line 9 in Listing 22-4, the "a" mode opens an existing file, hello.txt, for appending. If the file doesn't exist, it's created.

### LISTING 22-4: Add More Text

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE *fh;

    /* "a" == append */
    fh=fopen("hello.txt","a");
    if(fh==NULL)
    {
        puts("Can't open that file!");
        exit(1);
    }
    fprintf(fh,"This text was added later\n");
    puts("Text appended");
    fclose(fh);
    return(0);
}
```

The standard file-writing functions are used to spew text to the open file, as shown in Line 15.

Exercise 22-5: Create a new project by using the source code shown in Listing 22-4. Build and run to append text to the hello.txt file. Use the program from Exercise 22-4 to view the file’s contents. Then run the program (from Exercise 22-5) again to append the text to the file a second time. View the result.

When you're done, the hello.txt file contains the following text:

```
Look what I made!
My C program wrote this file.
This text was added later
This text was added later
```

## Writing binary data

The demo programs shown so far in this chapter deal with plain text files. Not every file is text, however. Most files contain binary data, unreadable by humans. You can use the C language to work with these files as well. Start by studying Listing 22-5.

### LISTING 22-5: Writing Binary Data

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE *handle;
    int highscore;

    handle = fopen("scores.dat", "w");
    if(!handle)
    {
        puts("File error!");
        exit(1);
    }
    printf("What is your high score? ");
    scanf("%d",&highscore);
    fprintf(handle,"%d",highscore);
    fclose(handle);
    puts("Score saved");
    return(0);
}
```

Exercise 22-6: Type the source code from Listing 22-5 into a new project. Build and run.

Most everything that goes on in Listing 22-5 is familiar to you. The problem? Binary data wasn't written. Instead, the fprintf() function at Line 17 writes the int value to the file as a text string. To prove it, examine the contents of the scores.dat file and you see that the value is stored as plain text.

## Exercise 22-7

Replace Line 17 from the code for your solution to Exercise 22-6 with this statement:

```
fwrite(&highscore, sizeof(int), 1, handle);
```

Save the change. Build and run. When you try to examine the contents of the scores.dat file now, it isn’t plain text. That’s because binary information was written, thanks to the fwrite() function.

Here’s the format for fwrite():

```
fwrite(variable_ptr, sizeof(type), count, handle);
```

The fwrite() function is concerned with writing chunks of information to a file. Unlike the fprintf() and fputs() functions, it doesn’t always write text.

Arrays and strings need not be prefixed with the & operator when specified in the fwrite() function.

sizeof(type) is the variable's storage size based on the type of variable — int, char, and float, for example.

count is the number of items to write. If you were writing an array of ten int values, you specify 10 as the size.

handle is the file handle address, returned from an fopen() function.

## Exercise 22-8

Using the source code from Listing 22-5 as a start, write a program that saves an array of five high-score values to the file scores.dat. (It's okay if the program overwrites the original scores.dat file.)

The next section covers how to read binary data from a file.

![](img/dcc0cd79d4a45cfce24fa49d85442884_363_0.png)

In earlier versions of the C standard, it was common to add a b to the fopen() function's mode string when reading or writing binary data. This requirement is no longer the case. A modern compiler ignores the "b" in a mode string if used in the fopen() function.

## Reading binary data

The fread() function reports for duty when it comes time to read binary information from a file. Like the fwrite() function, fread() takes in raw data and stuffs it into a C language variable for further examination. Listing 22-6 provides a demonstration. The scores.dat file in the listing is created in the preceding section's Exercise 22-8.

### LISTING 22-6: Check Those High Scores

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE *handle;
    int highscore[5];
    int x;

    handle = fopen("scores.dat","r");
    if(!handle)
    {
        puts("File error!");
        exit(1);
    }
    fread(highscore,sizeof(int),5,handle);
    fclose(handle);
    for(x=0;x<5;x++)
        printf("High score %d: %d\n",x+1,highscore[x]);
    return(0);
}
```

In Line 16, the base address of the highscore array is passed to fread() as the first argument. Next comes the size of each element to be read, the size of an int variable. Then comes the immediate value 5, effectively ordering fread() to scan in five values. The final argument is the file handle variable, confusingly named handle.

**Exercise 22-9:** Type the source code from Listing 22-6 into your editor. Build and run to see the five int values that were previously saved to the scores.dat file.

Because fread() can read any file's data, you can use it to create a file-dumper type of program, as shown in Listing 22-7.

### LISTING 22-7: A File Dumper

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

The source code from Listing 22-7 displays each byte in a file. It uses a 2-digit hexadecimal format, %02X, to represent each byte in the printf() statement at Line 24.

The fgetc() function reads the file one byte at a time in Line 21. To prevent the code from reading beyond the end of the file, this byte is compared with the EOF, or end-of-file, marker at Line 22.

The if decision at Line 26 uses the modulus operator to determine when 16 bytes have been displayed. When true, a newline is output, keeping the display neat and tidy.

Unlike other programs presented in this chapter, Listing 22-7 prompts the user for a filename at Line 10. Therefore, a good possibility exists that you'll see the error message displayed when an improper filename is typed.

Exercise 22-10: Type the source code from Listing 22-7 into your editor. Build the project. Run it using the scores.dat file you created earlier in this chapter, or use the file's own source code listing as the file to view.

Exercise 22-11: Rewrite the source code from Listing 22-7 so that the filename can also be typed at the command prompt as the program's first argument.

![](img/dcc0cd79d4a45cfce24fa49d85442884_365_0.png)

- Dump is an old programming term. It's an inelegant way to refer to a transfer of data from one place to another without any manipulation. For example, a core dump is a copy of the operating system's kernel (or another basic component) transferred from memory into a file.
- The information saved by the fwrite() and read by the fread() functions is binary — effectively, the same information that's stored in memory when you assign a value to an int or a float or another C variable type.
- As long as you get the order correct, you can use fwrite() and fread() to save any data to a file, including full arrays, structures, and what-have-you. But if you read the information out of sequence, it turns into garbage.

## Random File Access

Random file access has nothing to do with random numbers. Rather, the file can be accessed at any point hither, thither, and even yon. It's like watching streaming video as opposed to broadcast TV: You can start reading the file at any point, fetching or putting whatever information wherever you need it.

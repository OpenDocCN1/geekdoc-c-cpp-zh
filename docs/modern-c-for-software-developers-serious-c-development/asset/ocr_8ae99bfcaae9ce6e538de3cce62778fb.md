```
fp = fopen("hello.txt", "r");

// Read a single character
char c = fgetc(fp);

// Print the character to stdout
printf("%c\n", c);

// Close the file when done
close(fp);
}
```

# EOF: End Of File

The special symbol EOF is returned if fgetc attempts to read a character past the end of a file. EOF is a macro. The previous program can be written as:

```
#include <stdio.h>
int main(void)
{
    FILE *fp;
    char c;
    fp = fopen("hello.txt", "r");
    while ((c = fgetc(fp)) != EOF)
        printf("%c\n", c);

    fclose(fp);
}
```

# Reading Lines From A Text File

The function fgets can be used to read lines from a text file. fgets returns NULL if there is an error or an attempt is made to read past the end of a file. Its signature is:

```
fgets(char* buffer, size_t sizeof_buffer, FILE* fptr)
```

The first parameter is a buffer large enough to hold a line. The second parameter is the size of the buffer. The third parameter is a pointer to a FILE structure.
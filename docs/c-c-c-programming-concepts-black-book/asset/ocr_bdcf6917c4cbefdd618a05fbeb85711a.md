```
```c
fp = fopen("D:\\_readme.txt","r");

if(!fp)
{
    printf("\n Failed to open the file");
    return 0;
}
while(!feof(fp))
{
    end_char = fgets(sentence, 100, fp);
    if(ferror(fp)) {
        printf("\n Error Occurred while reading ");
    }
    printf("%s \n",sentence);
}

fclose(fp); /* for closing the file pointer */
getch();

return 0;
}
```
```

In Listing 5.28, we are reading information from a file, which is opened in the read-only mode. While reading from the file, if we encounter any error, the error will be notified by the ferror() function and appropriate measures can be taken against it.

# ### fgetpos()

The signature of fgetpos() is given as follows:

```
```c
int fgetpos(FILE *stream, fpos_t *position);
```
```

The fgetpos() function stores the current value of the file pointer in the object pointed to by position. The object pointed to by position must be of type fpos_t. If an error occurs, then fgetpos() returns a non-zero value; else, it returns 0.

# ### freopen()

The freopen() function associates an existing stream with a different file. The end of file and error flags are cleared in the process. The signature of freopen() function is given as follows:

```
```c
FILE *freopen(const char *fname, const char *mode, FILE *stream);
```
```

The new file's name is pointed to by fname, the access mode is pointed to by mode, and the stream to be reassigned is pointed to by stream.

# ### ftell()

The ftell() function returns the current value of the file pointer for the specified stream. The signature of ftell() function is given as follows:

```
```c
long int ftell(FILE *stream);
```
```

For binary streams, the value is in number of bytes. For text streams, the return value may not be meaningful because of possible character translations, such as carriage return/linefeeds being substituted for newlines, which affect the apparent size of the file.

Next, let's discuss bitwise operators in C.
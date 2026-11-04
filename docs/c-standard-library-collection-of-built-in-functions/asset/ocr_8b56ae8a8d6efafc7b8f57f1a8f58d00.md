```
fp = fopen(filename, "w");

fprintf(fp, "%s", "This is tutorialspoint.com");
fclose(fp);

ret = remove(filename);

if(ret == 0)
{
    printf("File deleted successfully");
}
else
{
    printf("Error: unable to delete the file");
}

return(0);
}
```

Let us assume we have a text file file.txt having some content. So we are going to delete this file, using the above program. Let us compile and run the above program to produce the following message and the file will be deleted permanently.

```
File deleted successfully
```

# int rename(const char *old_filename, const char *new_filename)

# Description

The C library function int rename(const char *old_filename, const char *new_filename) causes the filename referred to by old_filename to be changed to new_filename.

# Declaration

Following is the declaration for rename() function.

```
int rename(const char *old_filename, const char *new_filename)
```

# Parameters
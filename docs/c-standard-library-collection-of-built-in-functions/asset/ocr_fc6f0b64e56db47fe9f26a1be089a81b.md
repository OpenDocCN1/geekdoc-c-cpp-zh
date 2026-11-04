```
int c;

fp = fopen("file.txt","r");
while(1)
{
    c = fgetc(fp);
    if( feof(fp) )
    {
        break ;
    }
    printf("%c", c);
}
fclose(fp);
return(0);
}
```

# ### size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)

# #### Description

The C library function **size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)** reads data from the given **stream** into the array pointed to, by **ptr**.

# #### Declaration

Following is the declaration for fread() function.

```
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)
```

# #### Parameters

+   *   **ptr** -- This is the pointer to a block of memory with a minimum size of *size***\***nmemb** bytes.
+   *   **size** -- This is the size in bytes of each element to be read.
+   *   **nmemb** -- This is the number of elements, each one with a size of **size** bytes.
+   *   **stream** -- This is the pointer to a FILE object that specifies an input stream.

# #### Return Value
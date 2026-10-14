```
if(fp == NULL)
{
    fprintf(stderr, "cat: can't open %s\n", argv[i]); continue;
}

while((c = getc(fp)) != EOF) putchar(c);
fclose(fp);
}

return 0;
}
```

As a historical note, the Unix cat program is so named because it can be used to concatenate two files together, like this: cat a b > c

This illustrates why it's a good idea to print error messages to stderr, so that they don't get redirected. The “can't open file" message in this example also includes the name of the program as well as the name of the file.

Yet another piece of information which it's usually appropriate to include in error messages is the reason why the operation failed, if known. For operating system problems, such as inability to open a file, a code indicating the error is often stored in the global variable errno. The standard library function strerror will convert an errno value to a human-readable error message string. Therefore, an even more informative error message printout would be

```
fp = fopen(argv[i], "r");
if(fp == NULL)
fprintf(stderr, "cat: can't open %s: %s\n",
```
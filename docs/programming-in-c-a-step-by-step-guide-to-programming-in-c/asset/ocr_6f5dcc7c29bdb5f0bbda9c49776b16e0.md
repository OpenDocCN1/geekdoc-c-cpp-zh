```
}
/* look for character */
while ((ch = getc(fp)) != EOF) /* where getc() is a */
if (ch == *argv[2]) { /* function to get one char */
printf("%c found",ch); /* from the file */
break;
}
fclose(fp);
}
```

# Self Assessment Questions

13.Command line argument is a parameter supplied to a program when the program is invoked. (True/False)

14.In the command line arguments of main(), argv is an array-of-pointersto________.

15.The __________ is a parameter supplied to a program when the program is invoked.

# 13.8 Summary

“Standard input" and “standard output" are two predefined I/O streams which are implicitly available to us. To actually open a file, and receive the “token" which you'll store in your file pointer variable, you call fopen. fopen accepts a file name (as a string) and a mode value indicating among other things whether you intend to read or write this file. The file pointer which keeps track (both for your sake and the library's) of which file you're talking about.

For each of the I/O library functions we've there's a companion function which accepts an additional file pointer argument telling it where to read from or write to. The standard I/O functions maintain two indicators with each
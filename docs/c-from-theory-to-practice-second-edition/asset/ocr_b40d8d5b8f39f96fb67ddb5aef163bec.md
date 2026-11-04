```
    break;
    printf("%c", ch);
}
fclose(fp);
    return 0;
}
```

The loop displays only the characters a and b and the next call of getc() ends it, since the next character is interpreted as the end of file. On the other hand, had we used the "w+b" mode, the program would have displayed all the characters since none character has a special significance in a binary file.

# The fseek() and ftell() Functions

Each read or write operation is normally performed sequentially. When necessary, however, a file can be read or written in any order. The fseek() function is used for random access within a file. It is declared in stdio.h:

```
int fseek(FILE *fp, long int offset, int origin);
```

fseek() moves the file pointer associated with fp to a new location offset bytes from the point indicated by origin. If offset is negative, the file pointer moves back. The value of origin must be one of the following constants, defined in stdio.h:

+   - SEEK_SET. The file pointer is moved offset bytes from the beginning of the file.
+   - SEEK_CUR. The file pointer is moved offset bytes from its current position.
+   - SEEK_END. The file pointer is moved offset bytes from the end of the file.

For example, to move to the end of the file, we would write:

```
fseek(fp, 0, SEEK_END);
```

To move 20 bytes from the beginning of the file, we would write:

```
fseek(fp, 20, SEEK_SET);
```

If fseek() is executed successfully, it returns 0. Otherwise, it returns a nonzero value.

When fseek() is used with text files, care is required with the new line character(s). For example, suppose that the following code writes some text in the first two lines of a text file. If the operating system expands '\n' to '\r' and '\n', the value of offset should be 6 (not 5) in order to move to the beginning of the second line.

```
fputs("text\n", fp);
fputs("another text\n", fp);
/* Move to the beginning of the second line. */
fseek(fp, 6, SEEK_SET);
```
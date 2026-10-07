3. The following is one of many possible solutions:

```
struct friend {
  char name[35+1];
  char street1[30+1];
  char street2[30+1];
  char city[15+1];
  char state[2+1];
  char zipcode[9+1];
  struct friend *next;
}
```

# # Answers for Lesson 17

# # Quiz

+   1. A text-mode stream automatically performs translation between the newline character (\n), which C uses to mark the end of a line, and the carriage-return linefeed pair that Windows uses to mark the end of a line. In contrast, a binary-mode stream performs no translations. All bytes are input and output without modification.

+   2. Open the file using the `fopen()` library function.

+   3. When using `fopen()`, you must specify the name of the disk file to open and the mode to open it in. The function `fopen()` returns a pointer to type FILE; this pointer is used in subsequent file access functions to refer to the specific file.

+   4. Formatted, character, and direct.

+   5. Sequential and random.

+   6. EOF is the end-of-file flag. It is a symbolic constant equal to -1.

+   7. EOF is used with text files to determine the end of the file has been reached.

+   8. In binary mode, you must use the `feof()` function. In text mode, you can look for the `EOF` character or use `feof()`.

+   9. The file position indicator indicates the position in a given file where the read or write operation will occur. You can modify the file position indicator with `rewind()` and `fseek()`.

+   10. The file position indicator points to the first character of the file, or offset 0. The one exception is if you open an existing file in append mode, in which case the position indicator points to the end of the file.
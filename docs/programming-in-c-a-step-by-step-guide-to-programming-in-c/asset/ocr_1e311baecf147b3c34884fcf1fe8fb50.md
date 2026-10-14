+   - unsigned void
+   - volatile
+   - while

All keywords must be written in lowercase. Some compilers may use additional keywords that must be identified from the C manual.

# Self Assessment Questions

+   11. All keywords must be written in __________.
+   12. `default` is not a valid keyword in C. (True/False)

# 3.6 Character Input and Output

The most basic way of reading input is by calling the function **getchar()**. **getchar()** reads one character from the “standard input,” which is usually the user's keyboard. **getchar()** returns (rather obviously) the character it reads, or, if there are no more characters available, the special value EOF (“end of file”). This value will be assigned within the stdio.h file. Typically, EOF will be assigned the value -1, but this may vary from one compiler to another.

The syntax of the **getchar()** function is written as

```
character variable = getchar()
```

where *character variable* refers to some previously declared character variable.

Example:

```
char c;

...
```
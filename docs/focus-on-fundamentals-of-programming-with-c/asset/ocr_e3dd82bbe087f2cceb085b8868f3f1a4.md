In the case of characters, one may read a single character as follows:

```
char c;
scanf_s("%c", &c, 1);
```

When reading multiple characters for non-null terminated strings, integers are used as the width specification and the buffer size.

```
char c[4];
scanf_s("%4c", &c, 4); // not null terminated
```

But plain-old scanf() is the ANSI standard, and it is not deprecated by anyone but Microsoft. Just make sure there is always a number between % and s in your format strings.

Note: If you want to strictly use ANSI C and not Microsoft C without getting the warning messages, add the following line of code before you include any header files.

```
#define _CRT_SECURE_NO_DEPRECATE
```
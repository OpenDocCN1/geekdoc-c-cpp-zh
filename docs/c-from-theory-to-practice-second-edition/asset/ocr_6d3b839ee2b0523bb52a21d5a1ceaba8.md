scanf() takes as an argument a pointer to the array that will hold the input string, Since we're using the name of the array as a pointer, we don't add the address operator & before its name. Because scanf() stops reading once it encounters the space character, only the word this is stored into str. Therefore, the program outputs this. To force scanf() to read multiple words, we can use a more complex form such as

```
scanf("%[^\n]", str);
```

> scanf() does not check if there is available memory to store all input characters. Therefore, if the user enters more characters than the allocated memory, the program will behave unpredictably.

For example, suppose that in the previous program the user enters a string with more than 20 characters. The first 20 characters will be stored into str, but the rest will be stored into a memory out of the bounds of the array, which causes the unpredictable behavior of the program. For example, if the value of i is stored into this memory, this value will change. To avoid a memory overflow, use %ns instead of %s, where n specifies the maximum number of characters to be stored.

Alternatively, we can use the fgets() function. Read its description in Chapter 15 to get an idea. Another function to read strings is gets(). It is declared in stdio.h:

```
char *gets(char *str);
```

Like scanf(), gets() reads characters from stdin and stores them in the memory pointed to by str. Because it is not possible to specify the maximum number of the characters to be read, gets() is extremely unsafe. There is always the possibility of memory overflow. Take a break, and read on the Internet how a virus program exploited this vulnerability of gets() to infect thousands of machines in 1988.

> Don't use gets() to read strings. It is unsafe.

fgets() is safer than gets() because the programmer can specify the maximum number of characters to be read.

> The pointer that is passed to a read function must point to a memory allocated to store the string.

For example, is the following code well written?

```
char *p, s[10];
p = s;
fgets(p, 10, stdin);
```

Yes, because p points to allocated memory. If the statement p = s; was missing, the code would be wrong. And, if in fgets(), we write sizeof(p) instead of 10, would be the same? Of course not, sizeof returns the size of the pointer, not the size of the memory that the pointer points to.
For example:

```
printf(stdout, "Hello, World!\n");    // exactly like printf("Hello, World!\n");
FILE* ff = fopen("My_file", "w");      // open My_file for writing
printf(ff, "Hello, World!\n");          // write "Hello, World!\n" to My_file
```

File handles are described in §27.6.3.

# 27.6.2  Input

The most popular stdio functions include

```
int scanf(const char* format, ...);   /* read from stdin using a format */
int getchar(void);                     /* get a char from stdin */
int getc(FILE* stream);                /* get a char from stream */
char* gets(char* s);                  /* get characters from stdin */
```

The simplest way of reading a string of characters is using **gets()**. For example:

```
char a[12];
gets(a);    /* read into char array pointed to by a until a '\n' is input */
```

Never do that! Consider **gets()** poisoned. Together with its close cousin **scanf("%s"), gets()** used to be the root cause of about a quarter of all successful hacking attempts. It is still a major security problem. In the trivial example above, how would you know that at most 11 characters would be input before a newline? You can’t know that. Thus, **gets()** almost certainly leads to memory corruption (of the bytes after the buffer), and memory corruption is a major tool of crackers. Don’t think that you can guess a maximum buffer size that is “large enough for all uses.” Maybe the “person” at the other end of the input stream is a program that does not meet your criteria for reasonableness.

The **scanf()** function reads using a format just as **printf()** writes using a format. Like **printf()** it can be very convenient:

```
void f()
{
    int i;
    char c;
    double d;
    char* s = (char*)malloc(100);
    /* read into variables passed as pointers: */
    scanf("%oi %c %g %s", &i, &c, &d, s);
    /* %s skips initial whitespace and is terminated by whitespace */
}
```
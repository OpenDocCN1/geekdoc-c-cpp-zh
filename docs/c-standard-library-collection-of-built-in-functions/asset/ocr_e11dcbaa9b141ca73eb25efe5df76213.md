```
```c
printf("Enter your website name: ");
scanf("%s", &str2);


printf("Entered Name: %s\n", str1);
printf("Entered Website:%s", str2);


return(0);
}
```
```

Let us compile and run the above program that will produce the following result in interactive mode:

```
```text
Enter name: admin
Enter your website name: www.tutorialspoint.com

Entered Name: admin
Entered Website: www.tutorialspoint.com
```
```

# ### int sscanf(const char \*str, const char \*format, ...)

# #### Description

The C library function **int sscanf(const char \*str, const char \*format, ...)** reads formatted input from a string.

# #### Declaration

Following is the declaration for sscanf() function.

```
```c
int sscanf(const char *str, const char *format, ...)
```
```

# #### Parameters

+   - **str** -- This is the C string that the function processes as its source to retrieve the data.
+   - **format** -- This is the C string that contains one or more of the following items: *Whitespace character, Non-whitespace character and Format specifiers*

A format specifier follows this prototype: `[=%[*][width][modifiers]type=]`

| argument | Description |
| --- | --- |
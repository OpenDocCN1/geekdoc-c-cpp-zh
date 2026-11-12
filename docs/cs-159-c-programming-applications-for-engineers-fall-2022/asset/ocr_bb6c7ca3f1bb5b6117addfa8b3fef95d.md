# Why does the compiler not approve of this particular assignment expression?

+   - The memory allocated to a statically declared array is fixed in terms of size and location.
+   - Based on the previous statement we would say the memory address to which an array refers is constant.

# Alternative - using the string.h function strcpy

The function strcpy will take the second argument and copy its value to the first. In this case, the contents of str1 are copied to str2.

```
char str1[SIZE];
char str2[SIZE];
getString(str1);
strcpy(str2, str1);
printf("Your input: %s\n", str1);
printf("Your output copy: %s\n", str2);
```

# Output:

Enter your string -> Go Purdue!
Your input: Go Purdue!
Your output copy: Go Purdue!

# Is there a concern with more data being copied than there were spaces reserved in memory?

+   - Yes! The strcpy function will continue to copy characters until the delimiter is found. Verify that the destination array has the needed capacity!
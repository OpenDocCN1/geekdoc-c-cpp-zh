rest of the data into the character array. If no error occurs at the time of reading, it returns the string; otherwise, it returns a null pointer.

Note that the usage of function gets is not recommended by experts. The reason is that the user cannot specify the length of the array passed to function gets. This creates a serious problem as the data entered can be of much larger size compared to the size of array. Thus, there is a possibility of buffer overflow, which may lead to application failure.

# ## Summary

In this chapter, we have learned about how to accept data from the user at run time and how to display the results. To accept data from the user, C language provides us inbuilt functions. The inbuilt functions use a temporary memory known as buffer. This buffer is then used as a text stream that connects the input or output device with the program. The default streams available with all C programs are stdin, stdout, and stderr. The inbuilt functions were classified as formatted and unformatted. The formatted function make use of conversion symbol known as format code to input or output data. On the other hand, unformatted functions only work on character data type.

# ## Review Questions

+   Q1. Explain the significance of strings in C language.

+   Q2. Name the three inbuilt streams used in C language. Give the usage of each of these streams.

+   Q3. Differentiate between formatted and unformatted functions.

+   Q4. Explain the significance of format string used in function scanf.

+   Q5. State whether the following statements are true or false:
i. The format string %g is used to read an integer data.
ii. A string in C language ends with a null character.
iii. To print a string left aligned we use syntax printf("%7s", string).
iv. We can print the ASCII value of an integer variable.
v. The library stdlib.h needs to be included to use function printf.
vi. The default stream stdout refers to keyboard device.

+   Q6. Give the output of the following programs:
i.

```
```c
#include <stdio.h>
main()
{
char c_string[] = "Learning C programming";
printf("%-5.8s",str1);
printf("%10s",str1);
return;
}
```
```

+   ii.

```
```c
#include <stdio.h>
main()
```
```
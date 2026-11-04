**Answer:** Recall from Chapter 8 that the name of an array when used as a pointer is a constant pointer, meaning that it is not allowed to change its value and point to some other address. Therefore, the statement temp = str1; is illegal. The same applies for the next two statements, so the program won't compile.

# ### C.10.5 What is the output of the following program?

```
```c
#include <stdio.h>
int main(void)
{
    char str1[] = "test", str2[] = "test";

    (str1 == str2) ? printf("One\n") : printf("Two\n");
    return 0;
}
```
```

**Answer:** Since the names of the two arrays are used as pointers, the expression str1 == str2 checks if the pointers point to the same address, not if the arrays are the same. Do str1 and str2 point to the same address?

Of course not; str1 and str2 have the same content, but they are stored in different memory. Therefore, the program displays Two.

What would be the output if we write:

```
```c
(*str1 == *str2) ? printf("One\n") : printf("Two\n");
```
```

Since str1 can be used as a pointer to its first element, *str1 is equal to 't'. Similarly, *str2 is equal to 't'. Therefore, the program would display One.

# ## Read Strings

Like printf(), scanf() uses the %s conversion specification to read a string. By default, scanf() reads characters until it encounters a white-space character (i.e., space, tab, or new line character). Then, it appends a null character at the end of the string. In the following program, suppose that the user enters the string this is the text:

```
```c
#include <stdio.h>
int main(void)
{
    char str[20];
    int i = 10;

    printf("Enter text: ");
    scanf("%s", str);
    printf("%s %d\n", str, i);
    return 0;
}
```
```
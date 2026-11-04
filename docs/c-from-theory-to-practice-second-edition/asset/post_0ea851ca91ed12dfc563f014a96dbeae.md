
We use fgets(), we'll see it later, to read a string and store it in str. Although it is allowed to call printf() in that way, printf() expects a pointer as its first argument, as shown in Appendix C, don't do that because if the character % is contained in the string, the compiler would interpret it as the beginning of a conversion specification and the behavior of the program would be unpredictable.

## Exercises

- **C.10.2** Write a program that creates a string with all lowercase and uppercase letters of the English alphabet.

```c
#include <stdio.h>
int main(void)
{
    char str[53];
    int i;

    for(i = 0; i < 26; i++)
    {
        str[i] = 'a'+i;
        str[26+i] = 'A'+i;
    }
    str[52] = '\0'; /* At the end, we add the null character. */
    printf("%s\n", str);
    return 0;
}
```

**Comments:** In each iteration, the ASCII value of the respective character is stored in str. For example, in the first iteration (i=0), we have str[0] = 'a'+0 = 'a' = 97 and str[26] = 'A'+0 = 'A' = 65.

- **C.10.3** What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    char str[] = "Right\'0\'Wrong";

    printf("%s\n", str);
    return 0;
}
```

**Answer:** Did you answer Right? Sorry, it is wrong.

The '0' does not represent the null character '\0', but it consists of the ' character, the zero character, and another '. Therefore, the program outputs Right'0'Wrong.

What would be the output if we had written the following?

```c
char str[] = "Right '\0'Wrong";
```

Since after the first ' the escape sequence \0 represents the null character, this time, you are right if you answered Right'.

## Pointers and String Literals

Since a string literal is stored as an array of characters, we can use it also as a pointer of type char* to the first character. The purpose of the next program is to show you this conversion in a really odd way. Although it looks absolutely weird, the program uses the string literal in two ways, as an array and as a pointer, and displays twice the fifth character of the string "message", that is, 'a'.

```c
#include <stdio.h>
int main(void)
{
    printf("%c %c\n", "message"[4], *("message"+4));
    return 0;
}
```

Don't get stuck on this program; what is really important to you is that expressions such as "c" and 'c' are different. The expression "c" is a string literal, which is stored in the memory as an array of two characters, the 'c' and '\0'. Essentially, it is represented by a pointer to that memory. On the other hand, the expression 'c' is just the character constant 'c' represented by its ASCII code.

A convenient way to handle a string literal is to declare a pointer variable and make it point to that string. For example:

```c
#include <stdio.h>
int main(void)
{
    char *ptr;
    int i;

    ptr = "This is text";
    for(i = 0; ptr[i] != '\0'; i++)
        printf("%c %c\n", *(ptr+i), ptr[i]);
    return 0;
}
```

With the statement ptr = "This is text"; the compiler allocates memory to store the string literal and the null character. Then, ptr points to the first character of the string, as depicted in Figure 10.1.

![](img/b8da5dcf9ba7f1fad5213c453d095246_279_0.png)

**FIGURE 10.1**

Pointers and string literals.

To access the characters of the string, we can use either pointer arithmetic or the pointer as an array and use array subscripting. The program uses both ways to display one by one the characters of the string. The loop is executed until the null character is met.

> Because the memory that the compiler allocates to store a string literal is typically read-only, it might not be allowed to modify it.

For example, an error message may be displayed when the following program is executed:

```c
#include <stdio.h>
int main(void)
{
    char *ptr = "This is text";
    ptr[0] = 'a';
    return 0;
}
```

As we've seen, we can use an array of characters to store a literal string. However, the declarations

```
char ptr[] = "This is text"; and char *ptr = "This is text";
```

although they may look similar, have quite different properties, as you already know from the section “Pointers and Arrays” in Chapter 8. In particular, the first declaration declares ptr as an array of 13 characters. We can store another string into ptr, provided that its length won't be more than 13 characters; otherwise, the program may behave unpredictably. The second declaration declares ptr as a pointer and makes it point to the memory that holds the string literal. As discussed, in the first case, we can write ptr[0] = 'a'; without any concern, while in the second case, this statement may cause a runtime error. The ptr pointer can point to another string during program execution, no matter what its length is. For example, consider the following program:

```c
#include <stdio.h>
int main(void)
{
    char *ptr = "First text";
    ptr = "This is a new text";
    printf("%c\n", *ptr);
    return 0;
}
```

At first, ptr points to the first character of the string literal "First text". Then, the statement ptr = "This is a new text"; makes ptr point to the new memory allocated to store that string. Since ptr points to its first character, *ptr is equal to 'T' and the program displays T.

As we've outlined in Chapter 8, before using a pointer, it must point to a valid address. Consider the following program:

```c
#include <stdio.h>
int main(void)
{
    char *ptr;

    ptr[0] = 'a';
    ptr[1] = 'b';
    ptr[2] = '\0';
    printf("%s", ptr);
    return 0;
}
```

Are the assignment ptr[0] = 'a'; and the next ones correct? Certainly not. Since ptr has not been initialized, writing the 'a', 'b', and '\0' characters somewhere in memory would cause the unpredictable behavior of the program. Even if the program displays ab, the code is erroneous.

> > Never forget that using an uninitialized pointer variable is a serious error.

Had we declared an array of characters and make ptr to point to it, like this:

```c
char str[3], *ptr;
ptr = str;
```

the program would have executed successfully.

## Exercises

- **C.10.4** The following program stores two strings in two arrays, swaps them, and displays their new content. Is there any error?

```c
#include <stdio.h>
int main(void)
{
    char temp[100], str1[100] = "Let's see", str2[100] = "Is everything OK?";

    temp = str1;
    str1 = str2;
    str2 = temp;
    printf("%s %s", str1, str2);
    return 0;
}
```

**Answer:** Recall from Chapter 8 that the name of an array when used as a pointer is a constant pointer, meaning that it is not allowed to change its value and point to some other address. Therefore, the statement temp = str1; is illegal. The same applies for the next two statements, so the program won't compile.

- **C.10.5** What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    char str1[] = "test", str2[] = "test";

    (str1 == str2) ? printf("One\n") : printf("Two\n");
    return 0;
}
```

**Answer:** Since the names of the two arrays are used as pointers, the expression str1 == str2 checks if the pointers point to the same address, not if the arrays are the same. Do str1 and str2 point to the same address?

Of course not; str1 and str2 have the same content, but they are stored in different memory. Therefore, the program displays Two.

What would be the output if we write:

```c
(*str1 == *str2) ? printf("One\n") : printf("Two\n");
```

Since str1 can be used as a pointer to its first element, *str1 is equal to 't'. Similarly, *str2 is equal to 't'. Therefore, the program would display One.

## Read Strings

Like printf(), scanf() uses the %s conversion specification to read a string. By default, scanf() reads characters until it encounters a white-space character (i.e., space, tab, or new line character). Then, it appends a null character at the end of the string. In the following program, suppose that the user enters the string this is the text:

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

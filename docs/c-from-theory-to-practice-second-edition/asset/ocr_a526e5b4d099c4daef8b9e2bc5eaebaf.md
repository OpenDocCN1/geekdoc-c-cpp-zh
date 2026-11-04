**Answer:** Did you answer Right? Sorry, it is wrong.

The '0' does not represent the null character '\0', but it consists of the ' character, the zero character, and another '. Therefore, the program outputs Right'0'Wrong.

What would be the output if we had written the following?

```
```c
char str[] = "Right '\0'Wrong";
```
```

Since after the first ' the escape sequence \0 represents the null character, this time, you are right if you answered Right'.

# ## Pointers and String Literals

Since a string literal is stored as an array of characters, we can use it also as a pointer of type char* to the first character. The purpose of the next program is to show you this conversion in a really odd way. Although it looks absolutely weird, the program uses the string literal in two ways, as an array and as a pointer, and displays twice the fifth character of the string "message", that is, 'a'.

```
```c
#include <stdio.h>
int main(void)
{
    printf("%c %c\n", "message"[4], *("message"+4));
    return 0;
}
```
```

Don't get stuck on this program; what is really important to you is that expressions such as "c" and 'c' are different. The expression "c" is a string literal, which is stored in the memory as an array of two characters, the 'c' and '\0'. Essentially, it is represented by a pointer to that memory. On the other hand, the expression 'c' is just the character constant 'c' represented by its ASCII code.

A convenient way to handle a string literal is to declare a pointer variable and make it point to that string. For example:

```
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
```

With the statement ptr = "This is text"; the compiler allocates memory to store the string literal and the null character. Then, ptr points to the first character of the string, as depicted in Figure 10.1.
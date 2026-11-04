```
```c
void test(int *ptr1, int *ptr2, int a)
{
    ptr1 = ptr2;

    *ptr1 = 100;
    *ptr2 = 200;
    a = *ptr1 + *ptr2;
    printf("%d\n", a);
}
```
```

**Answer:** When test() is called, we have ptr1 = &i, ptr2 = &j and a = k. The statement ptr1 = ptr2; makes ptr1 point to the address of j. Therefore, the statement *ptr1 = 100; makes j equal to 100. Since ptr2 points to the address of j, the statement *ptr2 = 200; changes the value of j to 200. Since the statement a = *ptr1 + *ptr2; is equivalent to a = j+j = 200+200 = 400, test() displays 400. Since any change in the value of a does not affect k, k remains the same. As a result, the program displays:

```
```
400
1 200 3
```
```

**C.11.27** Write a function that takes as parameters a character, an integer, and a string and uses it as a pointer to check whether the character exists in the string or not. If not, it should return NULL. Otherwise, if the integer is 0, it should return a pointer to its first occurrence, otherwise to the last one. Write a program that reads a string of less than 100 characters, a character, and an integer, calls the function, and displays the part of the string. For example, if the user enters "booststrap", 't' and 0, the program should display tstrap. If it is "booststrap", 't' and 3, the program should display trap.

```
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);
char *find(char str[], char ch, int f);

int main(void)
{
    char *ptr, ch, str[100];
    int flag;

    printf("Enter text: ");
    read_text(str, sizeof(str), 1);

    printf("Enter character to search: ");
    scanf("%c", &ch);

    printf("Enter choice (0-first, other-last): ");
    scanf("%d", &flag);

    ptr = find(str, ch, flag);
    if(ptr == NULL)
        printf("'%c' is not included in the text\n", ch);
    else
```
```
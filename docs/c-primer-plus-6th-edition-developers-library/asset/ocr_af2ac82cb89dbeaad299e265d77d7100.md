The atoi(), atol(), and atof() functions convert string representations of numbers to type int, long, and double forms, respectively. The strtol(), strtoul(), and strtod() functions convert string representations of numbers to type long, unsigned long, and double forms, respectively.

# Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

+   1. What’s wrong with this attempted declaration of a character string?

```
int main(void)
{
    char name[] = {'F', 'e', 's', 's'};
    ...
}
```

+   2. What will this program print?

```
#include <stdio.h>
int main(void)
{
    char note[] = "See you at the snack bar.";
    char *ptr;

    ptr = note;
    puts(ptr);
    puts(++ptr);
    note[7] = '\0';
    puts(note);
    puts(++ptr);
    return 0;
}
```

+   3. What will this program print?

```
#include <stdio.h>
#include <string.h>
int main(void)
{
    char food[] = "Yummy";
    char *ptr;

    ptr = food + strlen(food);
    while (--ptr >= food)
```
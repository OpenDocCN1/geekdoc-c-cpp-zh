Way 2:

```
```c
#include<stdio.h>
int main()
{
    char ch;
    printf("\nEnter The Character : ");
    scanf("%c", &ch);
    if (ch >= 97 && ch <= 122)
        printf("Character is Lowercase Letters");
    else
        printf("Character is Not Lowercase Letters");
    return (0);
}
```
```

# ## Questions

# ### Winter 2014

+   1. Explain strcat() and strcpy().
+   2. Define Array.Explain how to declare and initialize two-dimensional array with example.
+   3. Write a 'C' program for multiplication of m*n matrix.
+   4. Write a 'C' program to check if the given string is palindrome or not.
+   5. main()
+      {
+          char s[]="I am the best";
+          printf("%s",s);
+          printf("\n%c",s[3]);
+          printf("\n%c",s[8]);
+      }

# ### Summer 2015

+   1. Explain strlen() and strcpy().
+   2. Define string with an example.
+   3. How can Array be passed to functions? Explain with example.
+   4. Write a 'C' program to check if given string is palindrome or not using pointers.
+   5. main()
+      {
+          int a[5] {5,1,15,20,25};
+          int i,j,m;
+          i=++a[1];
+          j=a[1]++;
+      }
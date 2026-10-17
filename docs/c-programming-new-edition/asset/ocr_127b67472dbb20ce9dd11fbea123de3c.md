#include<string.h>.

Since you are running against time and it is practically impossible to explain each one of the functions you will be dealing with 4 major leaders of the cult.

+   - strlen();
+   - strcpy();
+   - strcat();
+   - strcmp();

You shall now deal with each one of the big boys individually and try to comprehend their duties.

strlen ()

The strlen() can be used to calculate the length of the string. To find the length of the string all you have to do is pass the string as a parameter within the parentheses and the strlen computes the length and returns it which can be captured in a suitable variables of yours. Note

The null byte is not counted during string length calculation:

```
#include<stdio.h>
#include<conio.h>
#include<string.h>
main()
{
char arr[]="martin";
int len1,len2;
clrscr();
len1=strlen(arr);
len2=strlen("short");
printf("\n%s length=%d",arr,len1); printf("\
%slength=%d","short",len2);
getch();
}
```

In the above program the first string whose length has to be found is initialized using an array and the second string is mentioned in the parentheses of the function itself.
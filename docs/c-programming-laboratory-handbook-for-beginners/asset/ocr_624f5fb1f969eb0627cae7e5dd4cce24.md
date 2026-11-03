```
```
Reversed String: olleh
3.
Enter the string to be reversed: Good morning
User Entered String: Good morning
Reversed String: gninrom dooG
```
```

# ## Outcomes

+   - Able to optimally reverse the string without using extra variables.
+   - Capable of writing user-defined functions for most of the standard string library functions.

# ## Related Programs

# ### Program 1

C program to compare two strings without using strcmp.

```
```c
#include<stdio.h>
#include<string.h>
void main()
{
  char a[100], b[100];
  int result;
  printf("\n Enter the first string: ");
  gets(a);
  printf("\n Enter the second string: ");
  gets(b);
  result=compare(a,b);
  if(result==0)
  printf("\n Entered strings are equal....\n");
  else
  printf("\n Entered strings are not equal.....\n");
}
int compare(char a[],char b[])
{
  int c=0;
  while(a[c]==b[c])
  {
    if(a[c]=='\0'||b[c]=='\0')
    break;
    c++;
  }
```
```
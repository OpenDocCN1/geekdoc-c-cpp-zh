```
{
charstr[50];
print("Enter a string:");
gets(str);
printf("Length of the string is %d\n",strlen(str));
}
```

**Output:**
nEnter a string: C in Depth
Length of the string is 8

strcmp() This function is used to compare two strings. If the two string match, strcmp()
return a value 0 otherwise it return a non-zero value. It compares the strings
character by character and the comparison stops when the end of the string
is reached or the corresponding characters in the two strings are not same.

strcmp(s1,s2)
return a value:
<0 when s1<s2
=0 when s1=s2
>0 when s1>s2

The exact value returned in case of dissimilar strings is not defined. We only
know if s1<s2, then a negative value will be returned and if s1>s2, then a
positive value will be returned.

**Example:**

```
/*String comparison................*/
#include <stdio.h>
#include <string.h>
void main()
{
char str1[10],str2[10];
printf("Enter two strings: ");
```
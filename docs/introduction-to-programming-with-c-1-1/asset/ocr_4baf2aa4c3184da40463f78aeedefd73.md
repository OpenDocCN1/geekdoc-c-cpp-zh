# String handling functions

String handling functions are defined in string.h header.

| strlen(str) | Returns length of the string str |
| strcpy(dest,src) | Copies the source string src to destination string dest |
| strncpy(dest,src,n) | Copies at most n characters of the source string src to destination string dest. |
| strcat(str1,str2) | Append string str2 to string str1 |
| strncat(str1,str2,n) | Append first n characters of string str2 to string str1 |
| strcmp(str1,str2) | compare two strings str1,str2 |
| strrev(str) | Reverses string |

# strlen(str)

This function returns the length of the string str i.e., it counts all the characters up to ‘\0’ except \0. So, an empty string has length zero.

/*program to display string length  using library function*/

```
#include<stdio.h>

#include<string.h>

void main()
{
    char s[]="hello";
    printf("length of string s=%d\n",strlen(s);
    getch();
}
```

Output

length of string s=5

/*program to display string length without using library function*/

```
#include<stdio.h>
```
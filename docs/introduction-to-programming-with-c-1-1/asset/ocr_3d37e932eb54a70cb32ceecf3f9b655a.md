```
```c
void main()
{
    char s[]="hello";
    inti=0;
    while(s[i]!='\0')
    {
        i++;
    }
    printf("length=%d\n",i);
    getch();
}
```
```

# Output

length=5

# strcpy(dest,src)

Copies the contents of source string **src** to destination string **dest** including '\0', So, the size of destination string **dest** should be greater or equal to the size of source string **src**. After copying, the original contents of destination string **dest** are lost.

```
```c
/*program to demonstrate strcpy()*/

#include<stdio.h>

#include<string.h>

void main()
{
    char s1[]=”hello”;
    char s2[10];
```
```
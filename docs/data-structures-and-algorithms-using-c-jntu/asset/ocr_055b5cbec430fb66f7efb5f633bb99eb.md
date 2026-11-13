Pass 2: In this pass, the text character 'F' and the pattern character 'M' are compared. In this case the comparison fails. The character 'F' is not present in the set of characters of the pattern. This case is referred to as the Bad Character Shift. In the shift table, the number of shifts for the character 'F' is 9. So, the pattern 'ALGORITHM' is moved 9 characters forward.

Pass 3: In this pass, the text character 'O' and the pattern character 'M' are compared. In this case the comparison fails. But the character 'O' is present in the set of characters of the pattern. In the shift table, the number of shifts for the character 'O' is 5. So, the pattern 'ALGORITHM' is moved 5 characters forward.

Pass 4: In this pass, the text character 'A' and the pattern character 'M' are compared. In this case the comparison fails. But the character 'A' is present in the set of characters of the pattern. This case is referred as the Good Suffix Shift. In the shift table, the number of shifts for the character 'A' is 8. So, the pattern 'ALGORITHM' is moved 8 characters forward.

Pass 5: In this pass, the text character 'M' and the pattern character 'M' are compared. In this case the comparison succeeded. So, the algorithm compares the character of the Text 'H' and the character of the pattern 'H' is compared. So again the immediate previous characters of the pattern and the text are compared until all the characters are compared. Because all the characters are matched, the index of the last character match will be returned.

# Program 15.2

```
```cpp
// Boyer-Moore
//#include<conio.h>
#include<string.h>
#include<iostream.h>
#include<stdio.h>
int build_table(char*p)
{
int last[128];
int i;
for(i=0;i<128;i++) last[i]=-1;
for(i=0;i<strlen(p);i++)
{
last[p[i]]=i;
}
return(last);
}

int min(int a,int b)
{
if(a>b) return(b);
else return(a);
}
int search(char*t,char*p)
{
int n=strlen(t);
int m=strlen(p);
```
```
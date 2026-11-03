```
printf("The first string is : %s\n",str3);
printf("The second string is : %s\n",str4);
```

# Problem 6

Write a program to read in a string and output the frequency, of each character, in that string.

```
* P9.28 *
#include<stdio.h>
main()
char str[10],ch;
int i,j,n,count;
printf("Enter a string : ");
scanf("%s",str);
n=strlen(str);
for(i=0;i<n;i++)
{
    ch=str[i];
    if(ch!=' ')
    {
        count=0;
        for(j=0;j<n;j++)
        {
            if(ch==str[j])
            {
                count++;
                str[j]=' ';
            }
        }
        printf("%c occurs %d times\n",ch,count );
    }
}
```

# Problem 7

Write a program to enter a 4 digit number and display it in words.

```
*P9.29*
#include<stdio.h>
main()
int n,num,d=0,dig[4];
char *ones[ ]={"","One","Two","Three","Four","Five","Six","Seven","Eight","Nine","Ten"};
char *el[ ]={"Ten","Eleven","Twelve","Thirteen","Fourteen","Fifteen","Sixteen","Seventeen","Eighteen","Nineteen"};
```
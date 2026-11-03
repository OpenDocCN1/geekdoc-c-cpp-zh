# Program

```
```c
#include<stdio.h>
void main()
{
    char str1[20],str2[20];
    int j;
    int matchany(char str1[40],char str2[40]);
    printf("\n Enter The First String : ");
    gets(str1);
    printf("\n Enter The Second String : ");
    gets(str2);
    j=matchany(str1,str2);
    if(j==-1)
    printf("\n No Match Found...\n");
    else
    printf("\n Match Found At Position %d  in str1 And The Character Is : %c\n",j,str1[j-1]);
}
int matchany(char str1[40],char str2[40])
{
    int i,j;
    for(i=0;str1[i]!='\0';i++)
    {
        for(j=0;str2[j]!='\0';j++)
        {
            if(str1[i]==str2[j])
            {
                return(i+1);
            }
        }
    }
    return -1;
}
```
```

# Output

1.
Enter The First String : computer
Enter The Second String : game
Match Found At Position 3 in str1 And The Character Is : m
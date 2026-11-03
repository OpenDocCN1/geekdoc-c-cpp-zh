```
char str1[10],str2[10];
printf("Enter the first string : ");
scanf("%s",str1);
printf("Enter the second string : ");
scanf("%s",str2);
if((strcmp(str1,str2))==0)
printf("Strings are same\n");
else
printf("Strings are not same\n");
}
```

Output:
Enter the first string : Bangalore
Enter the second string : Mangalore
Strings are not same



```
int strcmp(char str1[ ],char str2[ ])
{
int i=0;
while(str1[i]!='\0'&&str2[i]!='\0'&&str1[i]==str2[i])
i++;
if(str1[i]==str2[i])
return 0;
else
return(str1[i]-str2[i]);
}
```

```
int pstrcmp(char *str1,char *str2)
{
while(*str1!='\0'&&*str2!='\0'&&*str1==*str2)
{
str1++;
str2++;
}
if(*str1==*str2)
return 0;
else
return(*str1-*str2);
}
```



This function is used for copying one string to another string. strcpy( str1, str2 ) copies str2 to str1. Here str2 is the source string and str1 is destination string. If str2 = "suresh" then this function copies "suresh" into str1. This function takes pointers to two strings as arguments and returns the pointer to first string.
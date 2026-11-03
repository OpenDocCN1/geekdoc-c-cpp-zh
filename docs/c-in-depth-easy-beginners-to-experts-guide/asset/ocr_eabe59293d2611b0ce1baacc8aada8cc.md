```
printf("\n Enter first string");
gets(s1);

printf("\n Enter second string");
gets(s2);

p1=s1;
p2=s2;

while(*p1!='\0'||*p2!='\0')
{
if(*p1==*p2)
{
p1++;
p2++;
continue;
}
else
{
f=*p1-*p2;
break;
}
}
if(f==0)
printf("\n string are equal");
else
printf("\n string are not equal");
getch();
}
```

# **************
**STRUCTURES**
**************

102. WAP TO CREATE A STRUCTURE BOOK, READ AND DISPLAY INFORMATION OF A BOOK.
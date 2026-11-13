# Example - 2

Write a program to input a string and count how many vowels are in it.

```
#include<iostream.h>
void main()
{
char x[20];
int i,count=0;
cout<<"\n Enter a string";
gets(x);
cout<<"\n The Entered string is"<<x;
for(i=0; x[i]!='\0';i++)
if(toupper(x[i])=='A' || toupper(x[i])=='E'
|| toupper(x[i])=='I' || toupper(x[i])=='O' ||
toupper(x[i])=='U')
count++;
cout<<"\n The string"<<c<< "having"<<count<<"numbers of vowels";
}
```

# OUTPUT

Enter a string Wel Come
The entered string is Wel Come
The string Wel Come having 3 numbers of vowels.

# Example :

Write a program to find out the length of a string.

```
#include<iostream.h>
void main()
{
char x[20];
int i,len=0;
cout<<"\n Enter a string";
gets(x);
for(i=0;x[i]!='\0';i++)
len++;
cout<<"\n THE LENGTH OF"<<x<<"IS"<<len;
}
```
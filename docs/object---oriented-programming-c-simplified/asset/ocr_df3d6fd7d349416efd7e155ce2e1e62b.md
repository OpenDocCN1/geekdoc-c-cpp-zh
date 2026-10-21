12

data =12

**EXPLANATION :** For the conversion of basic data type to class, a constructor is created which accepts an argument of that data type. Here, we want to convert an int to class demo type. So we have written one argument int type constructor in the class. When statement demo d= num executes compiler automatically calls this one argument constructor with value num. This value num is assigned to data and show function is called which display the data.

# /* PROG 8.28 DEMO OF TYPE CONVERSION char* TO CLASS TYPE */

```
#include <iostream.h>
#include <ctype.h>
#include <string.h>
#include <conio.h>

class demo
{
    char str[20];
public :
    demo(char x[])
    {
        strcpy(str,x);
    }
    int countV()
    {
        int i=0,count=0;
        char ch;
        while(str[i]!=0)
        {
            ch=toupper(str[i]);
            switch(ch)
            {
            case 'A' :
            case 'E' :
            case 'I' :
            case 'O' :
            case 'U' : count++;
            }
            i++;
        }
```
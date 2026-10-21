```
clrscr();
str.input();
str.find_len();
str.show();

getch();
}
```

OUTPUT :
Enter a string
Hari Mohan
String :=Hari Mohan
Length :=11

EXPLANATION : The function getline scans the whole line till the enter key is pressed or max 19 characters are scanned first. The function scans even the white space character like space, tab, etc. This time the whole string is scanned and output is what we expected.

# /* PROG 6.25 CHANGING CASE OF STRING CHARACTERS */

```
#include <iostream.h>
#include <conio.h>
#include <ctype.h>
class demo_str_case
{
    char str[12];

public :

    void input();
    void change_case();
};
void demo_str_case ::input()
{
    int i=0;
    cout<<"ENTER A STRING \n";
    char ch;
    ch=cin.get();
    while(i<12)
    {
        str[i]=ch;
        if(ch=='\n' || i==11)
```
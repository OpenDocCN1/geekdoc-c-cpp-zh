```
than or
    equal to 25 characters and should not have any blank space
\n";
cin>>name;
int i;
for (i=0; name[i] != '\0'; i++);
char *getChar, *checkChar;
getChar = name;
checkChar = name;
getChar = getChar + i - 1;
while (*getChar != '\0')
{
    cout<<" "<< *getChar;
    if (*checkChar== *getChar)
    {
        break;
    }
    getChar--;
}
return 0;
}
```

# Output:

Enter the String You Want To Reverse
It should be less than or equal to 25 characters and should not have any blank space
Kogent-Solutions-Inc
c n I - s n o i t u l o S - t n e g o K

Q3. Create a program that accepts two strings from the user, joins them, and displays it on the screen. Use of a separate function is must to concatenate two strings.

Ans.

```
#include <iostream.h>
#include <string.h>

char* JoinString (char *toString, char *fromString)
{
    char *JoinedString = "";
    strcat(JoinedString, toString);
    strcat(JoinedString, fromString);
    return JoinedString;
}

int main ()
{
```
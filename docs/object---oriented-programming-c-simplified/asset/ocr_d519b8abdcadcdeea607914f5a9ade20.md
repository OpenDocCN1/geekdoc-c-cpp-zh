============================================================
Life is like an ice-cream. Eat it before it melts
============================================================

**EXPLANATION :** The write method displays the str onto the screen. It takes two parameters :

+   (a) **First one is the string.**
+   (b) **Second one is its length.**

Depending upon the length, that number of characters is displayed.

# /*PROG 11.8 DISPLAY PATTERN USING write METHOD */

```
#include <iostream.h>
#include <conio.h>
#include <string.h>

void main()
{
    char str [20];
    int i,len;
    clrscr();
    cout << "==================================================" << endl;
    cout << "Enter a string" << endl;
    cout << "==================================================" << endl;
    cin.getline(str,20);
    len = strlen(str);
    cout << "==================================================" << endl;
    cout << "Pattern is" << endl;
    for(i = 1; i <= len; i++)
    {
        cout.write(str,i);
        cout << endl;
    }
    for(i = len; i >= 1; i--)
    {
        cout.write(str,i);
        cout << endl;
    }
    cout << endl;
    cout << "==================================================" << endl;
    getch();
}
```
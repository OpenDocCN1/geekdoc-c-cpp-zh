The following segment of a program reads a line of text from the keyboard and displays it on the screen.

```
char c;
cin.get(c); // read a character
while(c != '\n')
{
cout.put(c); // display the character on screen
cin.get(c);
}
```

Program 10.1 illustrates the use of these two character handling functions.

# Program 10.1 Character I/O with get() and put()

```
#include <iostream>
using namespace std;

int main()
{
int count = 0;
char c;

cout << "INPUT TEXT\n";
cin.get(c);

while(c != '\n')
{
cout.put(c);
count++;
cin.get(c);
}
```
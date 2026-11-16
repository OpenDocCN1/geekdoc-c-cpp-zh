Output

Enter a line

I am A*man

Entered line is: I am A

See here, * is used as delimitative character.

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch[50];
    cout<<"Enter a line\n";
    cin.getline(ch,5,'*');
    cout<<"Entered line is: "<<ch;
}
```

Output

Enter a line

I am Am*am

Entered line is: I am

See here, out of second argument and third argument, second argument strikes earlier as it is telling the function to store only five characters, while * is at eighth character.

# cin.read(unsigned char*,int l)

This function is used to take a fixed number of inputs from the screen; this is very useful while dealing with the big data which can even cause the buffer overflow attacks. Following is a program which shows the use of cin.read():

#include<iostream>

using namespace std;
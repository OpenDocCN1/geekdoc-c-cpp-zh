# /*PROG 12.9 DEMO OF EOF FUNCTION AND APPEND MODE */

```
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream rw;
    char str[100];
    clrscr();
    rw.open("demo.txt",ios ::in);
    cout<< "data read from file";
    endl(cout);
    while(rw.eof() !=0)
    {
        rw.getline(str,100);
        cout<< str<< endl;
    }
    rw.close();
    rw.open("demo.txt",ios ::app);
    cin.getline(str,100);
    rw<< str<< endl;
    rw.close();
    rw.open("demo.txt",ios ::in);
    cout<< "File with append data \n";
    while(rw.eof() !=0)
    {
        rw.getline(str,100);
        cout<< str<< endl;
    }
    rw.close();
    getch();
}
```

# OUTPUT :

data read from file
This program for checking end of file
Hello C++
File with append data
This program for checking end of file
Hello C++
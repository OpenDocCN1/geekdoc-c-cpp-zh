the bits are cleared. The bad returns 0 as there is no I/O error. Eof was not reached so eof returns 0. Now checking from the figure, the rdstate will be as :

![](bbox=[0.175, 0.17, 0.815, 0.22])

Figure 12.16. Logical Implementation of rdstate( )

# 0010 is decimal 2, so rdstate return 2.

In the program if file was not opened and we try to write to the file then function bad returns true and badbit which indicates file input/output error. This can be cheked again as :

```
file << "WRITING TO THE FILE" << endl;
if(!file)
{
    cout << "WRITING ERROR";
    endl(cout);
}
//check all flags here;
```

```
/*PROG 12.29 DEMO OF FAIL AND GOOD */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>
void main()
{
    clrscr();
    ifstream file("num.txt",ios ::nocreate);
    if(file.good())
    {
        cout << "File is opened successfully" << endl;
        cout << "good flag :=" << file.good() << endl;
    }
    else if(file.fail())
    {
        cout << "Error in opening file \n";
        cout << "Fail flag :=" << file.bad() << endl;
    }
}

OUTPUT :
File is opened successfully
good flag := 1
```
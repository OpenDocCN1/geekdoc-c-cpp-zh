# Working with Constructor and Destructor

```
int pr, cp;
clrscr( );
cout << "Enter the price of Ipod" << endl;
cin >> pr;
cout << "Enter the memory capacity in MB" << endl;
cin >> cp;
Ipod ip1 = Ipod(pr,cp);
ip1.display( );
getch( );
}
```

OUTPUT :
Enter the price of Ipod
8000
Enter the memory capacity in MB
1024
Price = 8000
Capacity = 1024MB

EXPLANATION : The program is similar to the previous one with the difference that instead of taking values for data members from constructor, we take values in main in local variables and pass these values to two argument constructor of Ipod class for initializing object ip1.

```
/*PROG 7.17 DYNAMIC INITIALIZATION OF OBJECTS VER 3*/
#include <iostream.h>
#include <string.h>
#include <conio.h>
class mobile
{
	char cname[20];
	char setid[10];
	float price;

public :

```
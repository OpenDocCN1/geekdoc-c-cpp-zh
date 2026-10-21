# # Object-Oriented Programming C++ Simplified



+   - In main
+   - Local num =30 Global num =100
+   - In block1
+   - Local num =40 Global num =100
+   - In block2
+   - Local num =50 Global num =100



The :: as discussed earlier known as scope resolution operator. Any global variable say gb can be accessed anywhere in the program by writing :: gb. In the program we have declared num at four places in the program, one is global, second is in main function, third in one block and fourth is in the second block. A block can be created by {and}. The variable num of one block can be used only inside that block only but num of main can be used anywhere in the main function. Global num can be accessed by writing :: num. On the basis of this I think it will be easy to figure out the output of the program.

```
```cpp
/*PROG 4.2 DEMO OF SCOPE RESOLUTION OPERATOR :: VER 2*/
#include <iostream.h>
#include <conio.h>
int num =100;
void main( )
{
 int num=30;
 cout << "In main\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << endl;
 int copynum=num;
 {
 int num=40;
 cout << "In block 1\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << "\t";
 cout << "num of main =" << copynum << endl;
 }
 {
 int num=50;
 cout << "In block 2\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << "\t";
 cout << "Num of main =" << copynum << endl;
 }
}
```
```
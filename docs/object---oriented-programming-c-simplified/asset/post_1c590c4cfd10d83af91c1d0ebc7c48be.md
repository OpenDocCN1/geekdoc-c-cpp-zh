
> THE WELL OF PROVIDENCE IS DEEP. IT'S THE BUCKETS WE BRING TO IT THAT ARE SMALL

You entered

> THE WELL OF PROVIDENCE IS DEEP. IT'S THE BUCKETS WE BRING TO IT THAT ARE SMALL

EXPLANATION : In the earlier program, we were taking input character by character but here whole line is scanned at once using getline() function/method. The getline scan the line till 
 (new line) is not pressed or till the first 49 characters have been scanned (second parameter). It scans white space character also like tab, spaces etc.

```
/*PROG 11.7 ENTER A LINE OF TEXT AND DISPLAY IT BACK USING getline AND write FUNCTION */
#include <iostream.h>
#include <conio.h>
#include <string.h>

void main()
{
 char str[100];
 clrscr();
 cout << " " << endl;
 cout << "Enter a line of text" << endl;
 cout << " " << endl;
 cin.getline(str,100);
 cout << " " << endl;
 cout << "You have entered" << endl;
 cout << " " << endl;
 cout.write(str,strlen(str));
 cout << " " << endl;
 getch ();
}
```

```
====================================
Enter a line of text
====================================
Life is like an ice-cream. Eat it before it melts
====================================
You have entered
====================================
```

============================================================
Life is like an ice-cream. Eat it before it melts
============================================================

**EXPLANATION :** The write method displays the str onto the screen. It takes two parameters :

+   (a) **First one is the string.**
+   (b) **Second one is its length.**

Depending upon the length, that number of characters is displayed.

## /*PROG 11.8 DISPLAY PATTERN USING write METHOD */

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

## OUTPUT :

```
============================================
Enter a string
============================================
UNIVERSITY
============================================
Pattern is
U
UN
UNI
UNIV
UNIVE
UNIVER
UNIVERS
UNIVERSI
UNIVERSIT
UNIVERSITY
UNIVERSITY
UNIVERSIT
UNIVERSI
UNIVERS
UNIVER
UNIVE
UNIV
UNI
UN
U
============================================
```

## EXPLANATION : The first for loop

```
for(i=1;i<=len;i++)
{
    cout.write(str,i);
    cout<<endl;
}
```

Display the pattern as :

```
U
UN
UNI
```

+   UNIV
+   UNIVE
+   UNIVER
+   UNIVERS
+   UNIVERSI
+   UNIVERSIT
+   UNIVERSITY

As i varies from 1 to length of the string and this i is used as second argument of method write. Second for loop

```
for(i=len;i>=1;i--)
{
cout.write(str,i);
cout << endl;
}
```

Display the following pattern as :

+   UNIVERSITY
+   UNIVERSIT
+   UNIVERSI
+   UNIVERS
+   UNIVER
+   UNIVE
+   UNIV
+   UNI
+   UN
+   U

As i varies from len-1 to i decrementing in each iteration.

```
/*PROG 11.9 DISPLAYING FULL NAME USING write METHOD */
#include <iostream.h>
#include <string.h>
#include <conio.h>
void main()
{
char fname [20],lname[20];
cout << "Enter first name :";
cin >> fname;
cout << "Enter last name :";
cin >> lname;
cout << "Your full name is " << fname << " " << lname;
getch();
}
```

```
```cpp
cout << “Enter the last name := ”;
cin >> lname;

cout << “Your full name := ”;
ostream & refcout=cout.write(fname, strlen(fname));

refcout.write(“ ”, 1);
refcout.write(lname,strlen(lname));
cout << endl;

getch( );
}
```
```

## **OUTPUT :**

Enter first name : = HARI  
Enter the last name : = PANDEY  
Your full name : = HARI PANDEY

**EXPLANATION :** The statement given below as :

```
```cpp
ostream & refcout=cout.write(fname, strlen(fname));
```
```

First display fname onto the screen and then returns reference of ostream type which is stored in refcout. In the next statement we use this refcout to display lname using write method. The whole of the write statements can be written in the shorter form as:

```
```cpp
cout.write(fname, strlen (fname))
Write(“ ”,1).write (lname,strlen(lname));
```
```

## 11.4 FORMATTED INPUT/OUTPUT OPERATIONS

In C++ for formatting input and output we have three methods :

+   1. Use of functions and flags defined by ios class.
+   2. Use of manipulators (built-in)
+   3. User defined manipulators.

## 1. Use of Functions and Flags Defined by ios Class

## A. ios Function and Flags

The class ios provides number of formatting functions for input and output. The most frequently used are listed below :

## (a) The width ( ) Function

The function is used to set the width *i.e.*, field size for displaying a data value of type numeric or string. The syntax of this is as follows :

```
int width (int);
```

It can be used with cout object as follows :

```
cout.width (5);
cout << 123;
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_544_0.png)

Figure 11.2. Implementation of width function

For each data value to be printed separate width function has to be used. That is for the following.

```
cout.width(5);
cout << 123;
cout << 45;
```

Only for the first cout statement width is set and not for the second. For printing second cout statement in a width of 5 we will have to write.

```
cout.width(5);
cout << 123;
cout.width(5);
cout << 45;
```

## (b) The precision Function

The function is used for setting the number of digits to be displayed after a floating point number. Its syntax is :

```
int precision (int);
```

It can be used as :

```
cout.precision (3);
cout << 123.456789;
```

Output displayed is given as :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_544_1.png)

Figure 11.3. Implementation of precision function

# # Object-Oriented Programming C++ Simplified

i.e., output becomes 123.456

Unlike width function the precision takes the setting in the effect for all cout statements that follows after cout.precision. To change the new precision one has to provide new value inside precision function.

## (c) The fill Function

The fill function is used to fill the empty spaces in the given field size set by width function. Its syntax is given as :

```
char fill (char);
```

It can be used as :

```
cout.width (10);
cout.fill ('#');
cout << 23456;
```

The output for the above given code snippet is given as :

![](img/ad5299318df8d4d7c6df5eaa86590ea3_545_0.png)

# Figure 11.4 Implementation of fill function

This function is used for setting the various flags for controlling the output such as displaying such as displaying output left justified or right justified, displaying numbers in decimal, hex, octal, scientific notation etc. This function is discussed in detail later.

The function is used for clearing the flags previously set by setf function.

```
/*PROG 11.10 DEMO OF WIDTH FUNCTION VER 1*/
#include <iostream.h>
#include <conio.h>

void main()
{
int a = 1234, b = 645, c = 28, d = 8;
clrscr ();

```

```
```cpp
cout << "===============================" << endl;
cout << "THE DEMO OF width IS GIVEN BELOW" << endl;
cout << "===============================" << endl;
cout.width(8);

cout << a << endl;
cout << b << endl;
cout << c << endl;
cout << d << endl;

cout << "===============================" << endl;
getch();
}
```
```

## **OUTPUT :**

```
```
===============================
THE DEMO OF width IS GIVEN BELOW
===============================
  1234
   645
    28
     8
===============================
```
```

**EXPLANATION :** The aim of above program is to demonstrate the basic functionality of width function. When compiler control read the statement **cout.width (8);** it will create a block of **8 cells** and set the value **1234** as right alignment. Other value will be set as usual.

```
```cpp
/*PROG 11.11 DEMO OF WIDTH FUNCTION VER 2 */

#include <iostream.h>
#include <conio.h>

void main( )
{
    int a = 12345, b = 1234, c = 123, d = 12, e=1;
    clrscr( );
    cout << "===============================" << endl;
    cout << "\tTHE PATTERN IS GIVEN AS" << endl;
    cout << "===============================" << endl;
    cout.width(8);
```
```

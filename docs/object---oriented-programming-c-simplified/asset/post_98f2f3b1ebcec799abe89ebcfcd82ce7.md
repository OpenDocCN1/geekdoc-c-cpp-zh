
**EXPLANATION :** The program is self explanatory. For better understanding point see the explanation of the previous program.

```cpp
/*PROG 11.30 DEMO OF BUILT-IN MANIPULATORS VER 5*/

#include <iostream.h>
#include <conio.h>

void main()
{
    int oct_enter;
    clrscr();
    cout<<"========================================"<<endl;
    cout<<"ENTER AN OCTAL VALUE \n";
    cout<<"========================================"<<endl;
    cin>>oct>>oct_enter;
    cout<<"========================================"<<endl;
    cout<<"HEX VALUE :="<<hex<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    cout<<"DEC VALUE :="<<dec<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    cout<<"OCT VALUE :="<<oct<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    getch();
}
```

**OUTPUT :**

```text
========================================
ENTER AN OCTAL VALUE
========================================
17
========================================
HEX VALUE :=f
========================================
DEC VALUE :=15
========================================
OCT VALUE :=17
========================================
```

**EXPLANATION :** See the explanation of the program 11.28.

```cpp
/*PROG 11.31 DEMO OF BUILT-IN MANIPULATORS VER 5*/
#include <iostream.h>
#include <conio.h>

void main( )
{
	clrscr( );
	cout << "************************";
	endl(cout);
	cout << "FIRST LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "SECOND LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "THIRD LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "FOURTH LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	getch( );
}
```

**OUTPUT :**

```text
************************
FIRST LINE
************************
SECOND LINE
************************
THIRD LINE
************************
FOURTH LINE
************************
```

**EXPLANATION :** All the manipulators take an argument of `ostream` by reference so we can pass `cout` as an argument of `endl`. So writing `endl(cout);` works as writing `cout<<endl;`

## 11.5.1 Creating Your Own Manipulators

Apart from using the built-in manipulators of C++, you can create your own manipulator for whatever purpose you want. For creating your own manipulator which does not take any argument the syntax is as shown earlier :

```cpp
ostream & manip_name (ostream & mycout)
{
    _____________;
    _____________;
    _____________;
    return mycout;
}
```

All user defined manipulator must take an argument by reference of ostream type and return ostream type by reference. As we pass reference of cout when use this manipulator, actual changes done by manipulator occur as if we are working with cout. For example consider a manipulator which emulates double space i.e., when we use it leaves two spaces in the stream and continues.

```cpp
ostream & DS(ostream & mycout)
{
    mycout << " ";
    return mycout;
}
```

To use this we can write as **cout<<DS<<"hello"<<DS;**

This first leaves two spaces, prints "hello" and then again leaves two spaces. As mentioned earlier the main advantage of manipulators whether user defined or built-in that they can be put into the **cin** and **cout** stream easily using **>>** and **<<**. This advantage of manipulator makes them popular.

We present few program for better understanding point of view.

```cpp
/*PROG 11.32 CREATING YOUR OWN MANIPULATOR VER 1*/

#include <iostream.h>
#include <conio.h>

ostream & DS(ostream & mycout)
{
    mycout << " ";
    return mycout;
}

void main()
{
    clrscr();
    cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
    endl(cout);
    cout << "After applying own manipulator";
    endl(cout);
    cout << DS << "HELLO" << DS;
    getch();
}
```

**OUTPUT :**

```text
Before Applying manipulator
HELLO
After applying own manipulator
    HELLO
```

**EXPLANATION :** In the program the following given statements just used to print "hello"

```cpp
cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_574_0.png)

Figure 11.18 : Logical implementation of user defined manipulator

```cpp
/*PROG 11.33 CREATING YOUR OWN MANIPULATOR VER 2*/

#include <iostream.h>
#include <conio.h>

/* Manipulator for two spaces */
ostream & DSD(ostream & mycout)
{
    mycout << "  ";
    return mycout;
}

/*Manipulator for three spaces */
ostream & DST(ostream & mycout)
{
    mycout << "   ";
    return mycout;
}

void main( )
{
    clrscr( );
    cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
    endl(cout);
    cout << "After applying own manipulator DSD";
    endl(cout);
    cout << DSD << "HELLO" << DSD;
    endl(cout);
    cout << "After applying own manipulator DST";
    endl(cout);
    cout << DST << "HELLO" << DST;
    getch( );
}
```

**OUTPUT :**

```text
Before Applying manipulator
HELLO
After applying own manipulator DSD
  HELLO
After applying own manipulator DST
   HELLO
```

**EXPLANATION :** This program is very much similar to previous one, only the difference is that in this we have declared one more user defined manipulator for putting three spaces in the beginning the desired string **"HELLO"**. The below shown figure shows the actual implementation of manipulators.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_576_0.png)

```cpp
/* PROG 11.34 CREATING YOUR OWN MANIPULATOR VER 3 */

#include <iostream.h>
#include <conio.h>
/* CREATION OF MANIPULATOR */
ostream & Rup(ostream & mycout)
{
        mycout << "Rs ";
        return mycout;
}
void main( )
{
        int money = 8000;
        clrscr( );
        cout << "==============================";
        endl(cout);
        cout << "AMOUNT IS SHOWN HERE";
        endl(cout);
        cout << "==============================";
        endl(cout);
        cout << Rup << money << "-/" << endl;
        cout << "==============================";
        endl(cout);
        getch();
}
```

**OUTPUT :**

```text
==================================
AMOUNT IS SHOWN HERE
==================================
Rs 8000/-
==================================
```

**EXPLANATION :** The user defined manipulator Rup simply displays "Rs" where it is used in the cout statement. It can be used in this manner also.

```cpp
Rup (cout);
cout << money << endl;
```

As Rup takes a reference of ostream type and we are sending cout in it.

```cpp
/* PROG 11.35 CREATING YOUR OWN MANIPULATOR VER 4 */

#include <iostream.h>
#include <conio.h>
#include <iomanip.h>
ostream & format(ostream & mycout)
{
    mycout << setw(8) << setfill('$');
    return mycout;
}

void main()
{
    int num1 = 1234;
    float num2 = 35.56;
    char *str = "HELLO";
    clrscr();
    cout << format << num1 << endl;
    cout << format << num2 << endl;
    cout << format << str << endl;
    getch();
}
```

**OUTPUT :**

```text
$$$1234
$$$35.56
$$$HELLO
```

The manipulator format does two things when called with cout, its sets width of 8 and fill character as '$'. For all three data num1, num2, and str a single call to format sets the width and sets fill character '$'. You can use any formatting manipulator as per your requirement and make one as your own manipulator.

```cpp
/*PROG 11.36 CREATING YOUR OWN MANIPULATOR VER 5*/
#include <iostream.h>
#include <conio.h>

/*CREATION OF MANIPULATOR STARTS */

ostream & tab (ostream & mycout)
{
    mycout << "<t>";
    return mycout;
}

ostream & new_line(ostream & mycout)
{
    mycout << "\n";
    return mycout;
}

ostream & bell_alert(ostream & mycout)
{
    mycout << "\a";
    return mycout;
}

ostream & ver_tab(ostream & mycout)
{
    mycout << "\v";
    return mycout;
}

ostream & wel_mssg(ostream & mycout)
{
    mycout << "WELCOME";
    return mycout;
}
/* CREATION OF MANIPULATOR FINISH HERE */

void main()
{
    int a=5,b=6;
    char *name = "hari";
    clrscr();
    cout << "---------------------" << endl;
    cout << "DEMO OF TAB AND NEW LINE" << endl;
    cout << "---------------------" << endl;
    cout << a << tab << b << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << "DEMO OF VERTICAL TAB AND NEW LINE" << endl;
    cout << "---------------------" << endl;
    cout << a << ver_tab << b << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << wel_mssg << name << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << "DEMO OF BELL ALERT" << endl;
    cout << "---------------------" << endl;
    cout << bell_alert << a << tab << bell_alert << b << new_line;
    getch();
}
```

**OUTPUT :**

```text
----------------
DEMO OF TAB AND NEW LINE
----------------
5 6
----------------
DEMO OF VERTICAL TAB AND NEW LINE
----------------
5
```

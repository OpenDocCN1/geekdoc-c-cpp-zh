
```
void main( )
{
    clrscr( );
    sub obj;
    obj.sub_show( );
    getch( );
}
```

**OUTPUT :**  
ERROR : ‘super ::num’ cannot access private member declared in class ‘super’

![](img/ad5299318df8d4d7c6df5eaa86590ea3_431_0.png)

*Figure 9.6. Showing the compilation error during the execution of the program*

**EXPLANATION :** If no access specifier is specified than by default all members of a class are private, so num is private. Again mode of inheritance is given while inheriting class super in sub, so default mode private is assumed *i.e.*, the following statement :

```
class sub : super
```

Is equivalent to

```
class sub :private super
```

As private members are never inherited, accessing num in the following sub_show procedure error.

```
/*PROG 9.13 DEMO OF SINGLE LEVEL PRIVATE INHERITANCE VER 4 */
#include <iostream.h>
#include <conio.h>

class super
{
protected :
int num;
void input(int x)
{
num = x;
}
};
class sub :super
{
public :
void sub_show( )
{
input(100);
cout << "num = " << num << endl;
}
};
void main( )
{
clrscr ( );
sub obj;
obj.sub_show( );
getch( );
}

OUTPUT :
num=100
```

In the super class num and function input is protected. In the class sub we are inheriting class super in private mode. In private mode all protected members of base class become private for the derived class and they can only be used inside the member functions of the derived class and not outside i.e., in the main. In the main when obj.sub_show( ); executes it call the function sub_show, in side input with value 100 is called which assigns value of 100 to num. Later we display this value of num.

```
/* PROG 9.14 DEMO OF SINGLE LEVEL PROTECTED INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>

class super
{
public :
    void show()
    {
        cout<<"hello from super"<<endl;
    }
};
class sub :protected super
{
};

void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}
```

OUTPUT :
ERROR :'show' cannot access public member declared in class 'super'

![](img/ad5299318df8d4d7c6df5eaa86590ea3_433_0.png)

Figure 9.7. Compile time error during the execution of program 9.14

EXPLANATION : In class sub we are inheriting class super in protected mode. So, all public members of class super become protected for the class sub and protected members can only be accessed inside the member functions of the class. So, the error.

```
/* PROG 9.15 DEMO OF SINGLE LEVEL PROTECTED INHERITANCE VER 2 */

#include <iostream.h>
#include <conio.h>

class super
{
    void show()
    {
        cout<<"hello from super"<<endl;
    }
};

class sub :protected super
{
};

void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}

OUTPUT :
ERROR : ‘show’ cannot access private member delared in class ‘super’
```

EXPLANATION : Private members are never inherited. So we cannot access show in main and any of the member function of the derived class. That’s why the above error.

```
/*PROG 9.16 DEMO ACCESSING PRIVATE MEMBERS IN PRIVATE INHERITANCE */

#include <iostream.h>
#include <conio.h>
class super
{
    int num;
public :
    void input(int x)
    {
        num = x;
    }
    int getnum()
    {
        return num;
    }
};
class sub :super
{
public :
    void show()
    {
        input(50);
        cout << "The square of num is"
            << getnum()*getnum() << endl;
    }
};

void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}

OUTPUT :
The square of num is 2500
```

EXPLANATION : The variable num is private in class super. The class sub inherits class super in private mode so num won't be accessible in class sub. Then how can we use num in class sub ? The solution is simple which we have seen earlier. We make a function in public mode which returns in the value of num. We have made function getnum which returns the value of num. Through this getnum we can easily compute the square of the num.

```
/* PROG 9.17 ACCESSING PRIVATE MEMBERS IN PRIVATE INHERITANCE AND MODIFYING THEM */

#include <iostream.h>
#include <conio.h>

class super
{
    int num;
public :
    void input(int x)
    {
        num = x;
    }
    int &getnum()
    {
        return num;
    }
    void super_show()
    {
        cout << "Num in class super is" << num << endl;
    }
};
class sub :super
{
public :
    void show()
    {
        input(50);
        cout << "Num in class sub is" << getnum() << endl;
        getnum() = getnum() * getnum();
        super_show();
    }
};
void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}
```

# OUTPUT :

Num in class sub is 50
Num in class super is 2500

## Object-Oriented Programming C++ Simplified

EXPLANATION : Whenever we want to modify the private members of the base class we must have a public member function in base class which returns reference of private data members. As getnum return the reference of num it can be put on the left side of assignment operator (=). Inside the function show we modify the value of num using getnum on the left side of =, and assigning getnum() * getnum() which stores 2500 into num. As we got reference of num through getnum this change of value occurs in the num. So, when supper_show is called it displays this value of num as 2500.

```
/*PROG 9.18 FINDING AREA AND VOLUME USING INHERITANCE VER 1 */
#include <iostream.h>
#include <conio.h>
class Area
{
protected :
int length, width;
public :
void inputa()
{
cout << "Enter the lenght :=";
cin >> length;
cout << endl << "Enter the width :=";
cin >> width;
}
};
class volume :public Area
{
int height;
public :
void inputv()
{
inputa();
cout << "Enter the height :=";
cin >> height;
}
void show()
{
cout << "Length = " << length << endl;
cout << "Width = " << width << endl;
cout << "Area = " << length*width << endl;
cout << "Height = " << height << endl;
}
```
```
```cpp
cout << "Volume=" << length*width*height << endl;
}
};
void main( )
{
    clrscr( );
    volume v;
    v.inputv( );
    v.show( );
    getch( );
}
```
```

# **OUTPUT :**

Enter the length : =12  
Enter the width : =13  
Enter the height : =14  
Length = 12  
Width = 13  
Area = 156  
Height = 14  
Volume = 2184

**EXPLANATION :** In the class Area we have two protected data members length and width. Function inputa( ) takes input from keyboard into these data items directly. The class Volume inherits class Area in the public mode. This class Volume contains one data member height. The class calculates area by using the inherited data members length and width and with the aid of height with length and width finds volume. Note we have called only the derived class function inputv( ) inside the main. This function in turns calls inputa( ) of the area class and takes input from keyboard. The function show calculates area and volume and displays.

```
```cpp
/* PROG 9.19 FINDING AREA AND VOLUME USING INHERITANCE VER 2 */

#include <iostream.h>
#include <conio.h>

class Area
{
    int l, w;
public :
    void input_A(int x,int y)
    {
        l = x;
```
```

## Object-Oriented Programming C++ Simplified

```
class Area {
int l, w;
public :
void input_A(int x, int y)
{
l = x;
w = y;
}
int get_l()
{
return l;
}
int get_w()
{
return w;
}
};
class Rectangle : public Area
{
int h;
public :
void input_R(int x, int y, int z)
{
input_A(x,y);
h = z;
}
void show()
{
cout << "Length : " << get_l() << endl;
cout << "Width : " << get_w() << endl;
cout << "Area : " << get_l() * get_w() << endl;
cout << "Height : " << h << endl;
cout << "Volume : " << get_l() * get_w() * h << endl;
}
};
class Volume :public Area
{
int h;
public :
void input_V(int x, int y, int z)
{
input_A(x,y);
h = z;
}
void show()
{
cout << "Length : " << get_l() << endl;
cout << "Width : " << get_w() << endl;
cout << "Area : " << get_l() * get_w() << endl;
cout << "Height : " << h << endl;
cout << "Volumen : " << get_l() * get_w() * h << endl;
}
};
void main()
{
clrscr();
Volume v;
v.input_V(5,10,15);
v.show();
getch();
}
```

Length : = 5
Width : = 10
Area : = 50
Height : = 15
Volumen : = 750


```
demo operator *(int x,demo T)
{
    demo temp;
    temp.num = x*T.num;
    return temp;
}
void main()
{
    clrscr();
    demo d1(200),d2;
    d2 = 10*d1;
    d1.show("of object d1");
    d2.show("of object d2");
    getch();
}

OUTPUT :
num of object d1 = 200
num of object d2 = 2000
```

EXPLANATION : In the main when d2=10*d1 executes, it is interpreted as operator*(10, d1) and compiler searches an overloaded *function which takes two arguments : as int and an object of demo class type. As we have overloaded *operator function is called. Inside the function temporary object is created and temp.num contains the multiplication of 10 and d1.num. This object is returned and assigned to d2.

## /* PROG 8.19 OVERLOADING UNARY OPERATOR - USING FRIEND VER 1 */

```
#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo() {}
    demo(int x)
    {
        num = x;
    }
    friend demo operator -(demo d)
{
```
```
friend demo operator -(demo d)
{
    demo temp;
    temp.num = -d.num;
    return temp;
}
demo operator +(demo d)
{
    demo A;
    A.num = num + d.num;
    return A;
}
void show(char *s)
{
    cout << "num of object " << s << " = " << num << endl;
}
};
void main()
{
    clrscr();
    demo d1(100),d2(200), d3;
    d3 = - d1 + d2;
    d1.show("d1");
    d2.show("d2");
    d3.show("d3");
    getch();
}

OUTPUT :
num of object d1 =100
num of object d2 =200
num of object d3 =100
```

EXPLANATION : Priority of unary – is higher than binary + so in the expression –d1 + d2, d1 calls operator - which return a temporary object A whose num is -100. Next this A object calls overloaded binary + operator function of class demo and send d2 as argument in the following manner : A.operator + (d2). In the operator + function sum of num of temp and d2 is calculated and assigned to num of temporary object A which is returned.

## /* PROG 8.21 OVERLOADING >> AND << OPERATOR USING FRIEND VER 1 */

```
#include <iostream.h>
#include <conio.h>

class demo
{
    int dx, dy;
public :
    friend void operator <<(ostream &, demo &);
    friend void operator >>(istream &, demo &);
};
void operator <<(ostream & mycout, demo & d)
{
    mycout << "dx = " << d.dx << "\t" << "dy = " << d.dy << endl;
}
void operator >>(istream & mycin, demo & d)
{
    mycin >> d.dx >> d.dy;
}
void main()
{
    demo d;
    clrscr();
    cout << "Enter the two numbers" << endl;
    cin >> d;
    cout << "You entered" << endl;
    cout << d;
    getch();
}

OUTPUT :
Enter the two numbers
40, 70
You entered
dx = 40 dy = 70
```

# EXPLANATION :

Object cout is considered an object of ostream type and cin is an object of istream type. The operator >> and << are overloaded internally for all basic data types so when you write cout<<40; internally it is treated as cout.operator <<(40). Similarly when cin>>x is written it is treated as cin.operator >>(x). The problem with these operators is that they are overloaded only for basic data types. They are not overloaded for inputting class object using cin or displaying class objects using cout. For that in the program we have overloaded >> and << operator using friend.

```
cin>>d1>>d2;
cout<<"You have entered"<<endl;
cout<<d1<<d2<<endl;
getch();
}

OUTPUT :
Enter two name
Hari
Mohan
You have entered
name = Hari
name = Mohan
```

EXPLANATION : Here we have modified the overloaded operator function >> and << by returning a reference of ostream from << and of istream from >>. In the main when we write cin>>d1>>d2, it is called as operator>> (cin, d1). In the function >> after taking data values for object d1 the function returns reference to cin which is used in calling the second object d2. Assume returned reference is cin, function is called again as operator>> (cin, d2). Same analogy applies to cout<<d1<<d2.

## /* PROG 8.23 OVERLOADING SUBSCRIPT OPERATOR */

```
#include <iostream.h>
#include <conio.h>

class demo
{
    int *p;
public :
    demo()
    {
        p=new int [5];
        for(int i=0; i<5; i++)
            p[i]=i+1;
    }
    int operator [](int x)
    {
        return p[x];
    }
};
```
```
void main()
{
    demo d;
    clrscr();
    for(int i=0; i<5;i++)
        cout << d[i] << " ";
    getch();
}

OUTPUT :
1 2 3 4 5
```

# EXPLANATION :

Expression d[i] is interpreted internally as d.operator [ ] (x). In each iteration of for loop we call the overloaded operator function [ ] and pass the value of ‘i’ which returns the corresponding array elements. Though d was not array but we have made it to be like array by overloading [ ] subscript operator.

## /*PROG 8.24 OVERLOADING COMMA (,)OPERATOR */

```
#include <iostream.h>
#include <conio.h>
class demo
{
    int x;
public :
    demo()
    {}
    demo(int p)
    {
        x=p;
    }
    demo operator,(demo d)
    {
        demo temp;
        temp.x=x;
        return temp;
    }
    void show()
    {
        cout << "x=" << x << endl;
    }
};
```
```
void main()
{
    clrscr();
    demo d1(30), d2(50), d3(70), d4;
    d4=(d1,d2,d3);
    d1.show();
    d2.show();
    d3.show();
    d4.show();
    getch();
}

OUTPUT :
x=30
x=50
x=70
x=30
```

EXPLANATION : In the above code comma (,) operator has been overloaded. In the default working of comma operator processing is done from left to right and right most operand becomes result for the comma operator. So initially d1 will call the comma operator and send d2 as argument like d1.operator,(d2). When temporary object return from operator function, it will call again overloaded function, again this time sending d3 as argument. The final object returnd will be assingned to d4 which will be d3.

## /* PROG 8.25 DEMO OF OVERLOADING -> OPERATOR */

```
#include <iostream.h>
#include <conio.h>
#include <string.h>

class demo
{
public :
    demo* operator -> ()
    {
        return this;
    }
    char str[20];
};
```
```
void main()
{
    demo d;
    clrscr();
    strcpy(d.str,"MPSTME");
    cout << d.str << endl;
    strcpy(d->str,"NMIMS University");
    cout << d->str << endl;
    getch();
}

OUTPUT :
MPSTME
NMIMS University
```

EXPLANATION : The operator -> allow us to treat object like a pointer. When overloading it is considered as a unary operator. The overloaded -> operator must return address of the current object. The next expression d->str internally treated as :

```
(d.operator -> ( )) str
```

## /* PROG 8.26 OVERLOADING OF FUNCTION CALL ( ) OPERATOR */

```
#include <iostream.h>
#include <conio.h>

class demo
{
    int x,y;
public :
    demo()
    {}
    void operator ()(int, int);
    void show(char*s)
    {
        cout << s << endl;
        cout << "x=" << x << endl;
        cout << "y=" << y << endl;
    }
};
void demo ::operator ()(int a, int b)
{
```
- 5. Binary operators overloaded through member function of the class take one argument and overloaded through friend function take two arguments.
- 6. Unary operators overloaded through member function of the class does not take any argument and overloaded through friend function must take one argument.
- 7. There are certain operators which cannot be overloaded. They are:

| S.No. | Operators | Name of Operator |
|---|---|---|
| 1. | :: | Scope resolution operator |
| 2. | . | Dot membership operator |
| 3. | .* | Pointer to member operator |
| 4. | ? : | Conditional operator |
| 5. | sizeof | The size of operator |

8. There are operators which cannot be overloaded using friend function. They are given as :

| S.No. | Operators | Name of Operator |
|---|---|---|
| 1. | = | Assignment operator |
| 2. | -> | Pointer to member operator |
| 3. | [ ] | Subscript operator |
| 4. | ( ) | Function call operator. |

## 8.7 TYPE CONVERSION

Many times in programming situations we like to convert one data type into another. Converting data types of a variable into other data type is known as type conversion. We have studied it earlier when we convert int to float, char to int, double to int etc. Compiler also does implicit type conversion. But all we studied involved all built-in types. In this section, we study type conversion with respect to user data type viz. class. We divide the study of type conversion into three parts.

- 1. Conversion from Built-in types to class type.
- 2. Conversion from class type to built-in types.
- 3. Conversion from one class type to another.

## 1. Conversion from Built-in Types to Class Type

When we want to convert basic built-in types into class types, the simple methods is to define parameterized constructor which takes an argument of basic type which you want to convert to class type. For example, when you want an int to be converted to class type say demo, define a one argument constructor type int in demo class as :


A static variable can be accessed either by using an object or by using the class name and the scope resolution operator. By using static member variables, the need for global variables can be eliminated. Since static variables are associated with the class itself rather than the class object, they are also called class variables.

### A.5.2 Static Member Functions

Similar to a member variable, member functions can also be declared as static. There are some restrictions on member functions to be static, which are listed as follows:

- 1. They can access static members of the same class.
- 2. They do not have ‘this’ pointer.
- 3. There cannot be a static and a non-static version of the same function.
- 4. They can be called using a class name as class_name::function_name.

Program Code A.14 demonstrates the use of a static member function. For a particular company, the record of all its salesman is maintained as name, city, total sale amount, etc. The company has branches in Delhi, Cochin, Akola, and Nashik. The program reads information about its n salesmen and computes the sales amount in each city and also the total sales amount.

```cpp
// Sample program with static member function
#include <iostream.h>
#include <conio.h>
#include <string.h>
class sale
{
static int Delhi_Sale, Cochin_Sale, Akola_Sale,
Nashik_Sale;
static int Total_Sale_Amount;
char name[10], city[10];
int sale_amt;
public:
void get_data()
{
cout << "\nEnter name, city, & sale amount for a salesman:";
cin >> name;
cin >> city;
cin >> sale_amt;
}
void display_data()
{
cout << "\n" << name << city << sale_amt;
}
void add_saleamt()
{
    int x;
    x = strcmp(city, "Delhi");
    if(x == 0)
    {
        Delhi_Sale = Delhi_Sale + sale_amt;
    }
    x = strcmp(city, "Nashik");
    if(x == 0)
    {
        Nashik_Sale = Nashik_Sale + sale_amt;
    }
    x = strcmp(city, "Cochin");
    if(x == 0)
    {
        Cochin_Sale = Cochin_Sale + sale_amt;
    }
    x = strcmp(city, "Akola");
    if(x == 0)
    {
        Akola_Sale = Akola_Sale + sale_amt;
    }
    Total_Sale_Amount = Akola_Sale + Cochin_Sale + Delhi_Sale + Nashik_Sale;
}
// static member function
static void display_saleamt()
{
    cout << "\n Total sale amount in Akola = " << Akola_Sale;
    cout << "\n Total sale amount in Delhi = " << Delhi_Sale;
    cout << "\n Total sale amount in Cochin = " << Cochin_Sale;
    cout << "\n Total sale amount in Nashik = " << Nashik_Sale;
    cout << "\n Total sale amount of a company in all cities = ";
    cout << Total_Sale_Amount;
}
}; // end of class
//define static variables
int sale::Delhi_Sale, Cochin_Sale, Akola_Sale, Nashik_Sale;
int sale::Total_Sale_Amount;
void main()
{
    ...
    sale::display_saleamt();
} // end of main
```

Note that as static variables are created before any object of its class, the fundamental use of static member functions is to initialize private static data before any object is actually created.

## A.6 OBJECT AS FUNCTION PARAMETER

Similar to other parameters, objects may be passed to functions. They may be passed by value or by reference. The following sections explain this concept in more detail.

### A.6.1 Passing Objects to Functions

If functions are invoked according to call-by-value then the function arguments are copied to the stack through copy constructors. For larger objects, this affects the performance. Hence objects are normally passed by reference. This avoids costly duplication and allows other functions to use the same object as the calling function.

### A.6.2 Returning Objects from Functions

A function may return an object to the caller. Program Code A.15 adds two complex numbers.

```cpp
// Adding two complex numbers
#include <iostream.h>
#include <conio.h>
class complex
{
 int Real, Imag;
 public:
 void GetNo(int a, int b)
 {
 Real = a;
 Imag = b;
 }
 void GetNo()
 {
 cout << "\n Please Input Real = " << Real;
 cout << "\n Please Input Imaginary = " << Imag;
 }
 complex AddNo(complex C2)
 {
 complex C3;
 C3.Real = Real + C2.Real;
 C3.Imag = Imag + C2.Imag;
 return(C3);
 }
 void DisplayNo()
 {
 cout << Real << "+i" << Imag;
 cout << endl;
 }
}; // end of class

void main()
{
complex C1, C2, C3;
C1.GetNo(10, 20);
C2.GetNo(30, 40);
C3 = C1.AddNo(C2);
C1.DisplayNo();
C2.DisplayNo();
cout << "\n Sum of these two numbers is ";
C3.DisplayNo();
}
Output:
10 + i20
30 + i40
Sum of these two numbers is 40 + i60
```

### A.6.3 Arrays of Objects

Similar to any other variable, an array of objects can be created. Program Code A.16 demonstrates the use of array of objects.

```cpp
// Array of objects
#include <iostream.h>
class sample
{
int a;
public:
void GetA()
{
    cout << "\n Enter a = ";
    cin >> a;
}
void PutA()
{
    cout << "\n\t" << a;
}
}; // end of class

void main()
{
    sample S[5];
    int i;
    for(i = 0; i < 5; i++)
    {
        S[i].GetA();
    }
    cout << "\n You entered the following values: ";
    for(i = 0; i < 5; i++)
        S[i].PutA();
}

Output:
Enter a = 1
Enter a = 2
Enter a = 3
Enter a = 4
Enter a = 5
You entered the following values: 1 2 3 4 5
```

### A.6.4 Pointers to Objects

Public members of a class can be accessed through the dot (.) operator. Members of a class can be accessed through a pointer to the class. When accessing members of a class using a pointer to the object, we use the arrow (->) operator instead of the dot (.) operator as in Program Code A.17.

```cpp
// Pointer to class
#include <iostream.h>
class student
{
 int RollNo;
 char Name[];
 public:
 void Getdata()
 {
 cout << "\n Enter RollNo = ";
 cin >> RollNo;
 cout << "\n Enter Name = ";
 cin >> Name;
 }
 void Putdata()
 {
 cout << "\nRollNo = ";
 cout << RollNo;
 cout << "\n Name = ";
 cout << Name;
 }
}; // end of class

void main()
{
student S1, *p;
p = &S1;
p->Getdata(); // This is the same as S1.Getdata()
p->Putdata(); // This is the same as S1.Putdata()
}
```

## A.7 "this" POINTER

When a member function is called, it is automatically passed an implicit argument that is a pointer to the object which called the function. Such a pointer is called the 'this' pointer. Program Code A.18 uses this pointer.

```cpp
// Use of 'this' pointer
#include <iostream.h>
class sample
{
int a;
float b;
char c;
public:
void Getdata()
{
    cout << "\n Enter integer value = ";
    cin >> a;
    cout << "\n Enter float value = ";
    cin >> b;
    cout << "\n Enter a character = ";
    cin >> c;
}
void Putdata()
{
    cout << "\n Integer = " << a;
    cout << "\n Float = " << b;
    cout << "\n Character = " << c;
}
}; // end of class

void main()
{
    sample S1;
    S1.Getdata();
    cout << "You have entered the following" << endl;
    S1.Putdata();
}

/* Here, 'this' pointer points to the object 'S1';
'this->a' refers to object S1's copy of 'a'. So the
functions get_data() and display_data() can be written
as follows */

void Getdata1()
{
    cout << "Enter int, float, char values = ";
    cin >> this->a;
    cin >> this->b;
    cin >> this->c;
}
void Displaydata2()
{
    cout << "Integer = " << this->a;
    cout << "Float = " << this->b;
    cout << "Char = " << this->c;
}
Output:
Enter integer value = 5
Enter float value = 7.8
Enter a character = g
You have entered the following data:
Integer = 5
Float = 7.8
Character = g
```

## A.8 FUNCTION OVERLOADING

Function overloading is the process of using the same name for two or more functions. However, each function should have either different types or different numbers of parameters. Through this difference, the compiler knows which function to call in any given situation. Program Code A.19 illustrates the use of overloaded functions.

```cpp
// To add two integers or two float numbers
#include <iostream.h>
void main()
{
    int inNum1 = 5, inNum2 = 6;
    float fNum1 = 5.5, fNum2 = 6.7;
    void AddNo(int, int);
    void AddNo(float, float);
    AddNo(inNum1, inNum2); // calls version 1
    AddNo(fNum1, fNum2); // calls version 2
}

void AddNo(int i1, int i2) // version 1
{
    cout << "Addition of integers = " << (i1 + i2);
}

void AddNo(float f1, float f2) // version2
{
    cout << "Addition of float nos = " << (f1 + f2);
}
```

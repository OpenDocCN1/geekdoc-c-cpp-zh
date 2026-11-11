```
```cpp
matrix m1,m2,m3;
m1.readmatrix();//read the data for 1st matrix
m2.readmatrix();//read the data for 2nd matrix
m1+m2;

cout<<"The result of addition of two matrices"<<endl;
m1.matdis();             //add the data of 2 matrices
getch();

m3=m1*m2;                //multiply the data of 2
matrices
cout<<endl<<"The result of multiplication of two matrices"<<endl;
m3.matdis();
getch();
}
```
```

Q35: Write a program to create to calculate area and perimeter of circle and increment the value of radius using operator overloading function, + .

Ans:

```
```cpp
#include<iostream.h>
#include<string.h>
#include<stdio.h>
#include<iomanip.h>
#include<conio.h>
#include<process.h>
#include<math.h>
#include<ctype.h>
# define PI 3.14

class circle          //description of the class circle
{
int radius,intc;
int area,peri;
public:
  circle();
  circle(int r);
  circle(int r,int inr);
  circle operator +(circle obj);
  void calarea();
  void per();
  void display();
};
```
```
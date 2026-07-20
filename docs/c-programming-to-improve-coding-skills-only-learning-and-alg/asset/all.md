![](image_rsrc483F.jpg)

C PROGRAMMING

To Improve Coding Skills

Only Learning & Algorithm based

Programs with Source Code

1st Edition (Jan-2024)

by  Atul Soni

Copyright © 2024 by Atul Soni

All rights reserved. No part of this work may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without the prior written permission of the copyright owner.

Cover design by: Atul Soni

Email ID: atul.soni09@gmail.com

For my wonderful family.  For all your love and support.

- Atul Soni

Introduction

This book covers all the concepts that the programmers need to develop their skills:

➢ Contains 500 learning and algorithm based programs with source code.

➢ Contains only programs source code and output snapshots (it doesn’t contain any theory, for theory there are many books available).

➢ We use MinGW compiler for C Programming.

➢ We use text editor VS Code, which is popular among beginner and professional programmers and works well on all operating systems.

➢ Each chapter contains well planned and organized collection of programs.

➢ This book will also be very helpful for beginners, teachers and trainers of C programming language.

➢ We use small variable or identifier names for better readability in digital media like kindle, ipad, tab and mobile.

➢ This book contains much simpler approach to coding.

➢ A simpler approach is used to organize the programs for beginners as well as professional.

➢ Each program in this ebook starts from new page for better readability/understandability.

About the Author

![IMG_20240110_124143-removebg-preview (6).png](image_rsrc483G.jpg)

Atul Soni

is an engineer whose main interests and expertise are programming languages, algorithms, data structure, data analytics, web technologies and android mobile application development.  He writes many programming tutorials.  He has extensive experience in teaching programming languages to engineers and software developers.

He is a programmer, writer and android app developer.  He develops many tutorial app of different programming languages like, C, C++, Java, Python, Android, VB.Net, C#, PHP, HTML5, CSS3, SQL & PL/SQL, JavaScript, jQuery etc.  When he’s not writing or programming, he enjoys reading books, touring by car and spending time with his family.

Table of Contents

Chapter-1 : C Introduction ​

Chapter-2 : Variables, Constants & Data Types ​

Chapter-3 : Operators & Expressions ​

Chapter-4 : Selection ​

Chapter-5 : Iteration / Loop ​

Chapter-6 : Series ​

Chapter-7 : Patterns

Chapter-8 : Arrays  ​

Chapter-9 : Strings ​

Chapter-10 : Functions ​

Chapter-11 : Structure, Union & Enum ​

Chapter-12 : Pointers ​

Chapter-13 : Dynamic Memory Allocation ​

Chapter-14 : Preprocessors ​

Chapter-15 : Input/Output Formatting ​

Chapter-16 : File Handling ​

Chapter − 1

C - Introduction

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 1 :

Program to display a String Literal in C using printf() function.

Code :

#include <stdio.h>

int  main()

{

       printf( " Let\'s learn C Programming Language." );

       return 0;

}

Output :

![](image_rsrc483J.jpg)![](image_rsrc483K.jpg)

______________  ****  ______________

Program No. - 2 :

Program to use system( "cls" ) to clear output screen in Terminal of VSCode and use system( "pause" ) to pause output screen in VSCode ( It implicitly shows "Press any key to continue . . ." in Visual Studio Code ).

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Let\'s learn C Programming Language.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483M.jpg)

______________  ****  ______________

Program No. - 3 :

Program to define comments in C programming.

Code :

/* Linking section.  */

#include <stdio.h>

/*  program starts from main function.  */

int  main()

{

       system( "cls" );​/*  to clear output screen.  ​*/

       printf( "Let\'s learn C  Programming.\n" );  /*  Output. */

       system("pause");​/* to hold output screen.  ​*/

       return 0;

} ​/* end of main  */

Output :

![](image_rsrc483N.jpg)

______________  ****  ______________

Program No. - 4 :

Program to explain that the C is a Free-form Language.

Code :

#include <stdio.h>

int  main() { system( “cls” ); printf(

"Let\'s learn C Programming.\n" );

system( "pause" ); return 0; }

Output :

![](image_rsrc483P.jpg)

______________  ****  ______________

Program No. - 5 :

Program to display single line using multiple printf() statements.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Let\'s learn " );

       printf( "C Programming.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483R.jpg)

______________  ****  ______________

Program No. - 6 :

Program to display multiple lines using single printf() statement.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Let\'s \nlearn \nC.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483S.jpg)

______________  ****  ______________

Program No. - 7 :

Program to explain that you can skip return 0; statement from int main() function in Visual Studio Code.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Let\'s learn C Programming.\n" );

       system( "pause" );

}

Output :

![](image_rsrc483T.jpg)

______________  ****  ______________

Program No. - 8 :

Program to explain variable declaration and assignment.

Code :

#include <stdio.h>

int  main()

{

       int  n1, n2, s;​​/*  Variable declaration */

       system( "cls" );

       n1 = 10;​​ /*  Variable assignment  */

       n2 = 20;

       s = n1 + n2;

       printf( "Sum = " );

       printf( "%d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483U.jpg)

______________  ****  ______________

Program No. - 9 :

Program to read data from keyboard using scanf statement.

Code :

#include <stdio.h>

int  main()

{

       int n1, n2, s;

       system( "cls" );

       printf( "Enter First Number: " );

       scanf( "%d", &n1 );

       printf( "Enter Second Number: " );

       scanf( "%d", &n2 );

       s = n1 + n2;

       printf( "Sum = " );

       printf( "%d\n", s );

​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483V.jpg)

______________  ****  ______________

Program No. - 10 :

Program to explain input and display multiple values in single printf and scanf statement..

Code :

#include <stdio.h>

int  main()

{

       int  n1, n2, s;

       system( "cls" );

       printf( "Enter Two Numbers: " );

       scanf( "%d %d", &n1, &n2 );

       s = n1 + n2;

       printf( "%d + %d = %d\n", n1, n2,  s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483W.jpg)

______________  ****  ______________

Program No. - 11 :

Program to calculate Volume of Cylinder.

Code :

/*

This program is used to explain Multiple line

comment and Single line comment.

*/

#include <stdio.h>

int  main()

{

       float  r, h, v;​​   /* Variable Declaration.  */

       system( "cls" );

       printf( "Enter Radius & Height of Cylinder : " );

       scanf( "%f %f", &r, &h );  /* Reading data from KB. */

       v = 3.14 * r * r * h ;​   /* Calculation of volume. */

       printf( "\nVolume of Cylinder  = %f\n", v );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483X.jpg)

______________  ****  ______________

Program No. - 12 :

Program to find the Area and Circumference of Circle.

Code :

#include <stdio.h>

int  main()

{

       float radius, area, circum;

       system( "cls" );

       printf( "Enter Radius : " );

       scanf( "%f", &radius );

       area = 3.14 * radius * radius;

       circum = 2 * 3.14 * radius;

       printf( "\nArea of Circle = %f\n", area );

       printf( "Circumference of Circle = %f\n", circum );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483Y.jpg)

______________  ****  ______________

Program No. - 13 :

Program to Swap two numbers using Third Variable.

Code :

#include <stdio.h>

int  main()

{

       int  n1, n2, t;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &n1, &n2 );

       printf( "\nn1 = %d, n2 = %d\n", n1, n2 );

​

       t = n1;

       n1 = n2;

       n2 = t;

​

       printf( "n1 = %d, n2 = %d\n", n1, n2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc483Z.jpg)

______________  ****  ______________

Program No. - 14 :

Program to Swap two numbers without using Third Variable.

Code :

#include <stdio.h>

int  main()

{

       int  n1, n2;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &n1, &n2 );

       printf( "\nn1 = %d, n2 = %d\n", n1, n2 );

​

       n1 = n1 + n2;

       n2 = n1 − n2;

       n1 = n1 − n2;

​

       printf( "n1 = %d, n2 = %d\n", n1, n2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4840.jpg)

______________  ****  ______________

Program No. - 15 :

Program to show output in required format.

Code :

#include <stdio.h>

int  main()

{

       int a = 12, b = 123, c = 1234;

       system( "cls" );

       printf( "Without formatting : \n" );

       printf( "%d\n", a );

       printf( "%d\n", b );

       printf( "%d\n", c );

       printf( "\nWith formatting : \n" );

       printf( "%7d\n", a );

       printf( "%7d\n", b );

       printf( "%7d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4841.jpg)

______________  ****  ______________

Program No. - 16 :

Program to calculate Simple Interest.

Code :

#include <stdio.h>

int  main( )

{

       system( "cls" );

       float p, r, t, si ;

       printf( "Enter Principal, Rate & Time : " ) ;

       scanf( "%f %f %f", &p, &r, &t ) ;

       si = ( p * r * t ) / 100;

       printf( "\nSimple Interest = %.2f\n", si ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4842.jpg)

______________  ****  ______________

Program No. - 17 :

Program to convert Upper-case letter to Lower-case letter.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a Capital / Upper case Letter : " );

       scanf( "%c", &ch );

       printf( "\nLower case Equivalent : %c\n", ( ch + 32 ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4843.jpg)![](image_rsrc4844.jpg)![](image_rsrc4845.jpg)

______________  ****  ______________

Program No. - 18 :

Program to calculate the Car’s average from the given total distance travelled (in kms) and fuel consumed (in litres).

Code :

#include <stdio.h>

int  main()

{

       float km, ltr, avg;

       system( "cls" );

       printf( "Enter Total Distance in km : " );

       scanf( "%f", &km );

       printf( "Enter Total Fuel consumed in litres : " );

       scanf( "%f", &ltr );

       avg = km / ltr;

       printf( "\nCar's Average (km/ltr) %.2f\n", avg );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4846.jpg)

______________  ****  ______________

Program No. - 19 :

Program to compute the Perimeter and Area of a rectangle with a length and width.

Code :

#include <stdio.h>

int  main()

{

       float l = 10.0, w = 5.0;

       float peri, area;

       system( "cls" );

       peri = 2 * ( l + w );

       printf( "Perimeter of Rectangle : %f\n", peri );

       area = l * w;

       printf( "Area of Rectangle : %f\n", area );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4847.jpg)

______________  ****  ______________

Program No. - 20 :

Program to accepts two item’s weight and number of each items and calculate the average weight per item.

Code :

#include <stdio.h>

int  main()

{

       float wt1, wt2, n1, n2, avg;

       system( "cls" );

       printf( "Weight of Item1 : " );

       scanf( "%f", &wt1 );

       printf( "No. of Item1 : ");

       scanf( "%f", &n1 );

       printf( "Weight of Item2 : " );

       scanf( "%f", &wt2 );

       printf( "No. of Item2 : " );

       scanf( "%f", &n2);

       avg = ((wt1 * n1) + (wt2 * n2)) / (n1 + n2);

       printf( "Average Weight per Item : %f\n", avg );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4848.jpg)

______________  ****  ______________

Program No. - 21 :

Program to calculate the Total Surface Area of Sphere.

Code :

#include <stdio.h>

int main()

{

       system( "cls" );

       double radius, tsa;

       printf( "Enter Radius : " );

       scanf( "%lf", &radius );

       tsa =  4.0 * 3.14 * radius * radius ;

       printf( "\nTotal Surface Area of Sphere : %lf\n", tsa );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4849.jpg)

______________  ****  ______________

Program No. - 22 :

Program to calculate the area of Triangle.

Code :

#include <stdio.h>

int main()

{

       system( "cls" );

       double base = 5.0, height = 4.0, area;

       area = 0.5 * base * height;

       printf( "Area of Triangle : %lf\n", area );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484A.jpg)

______________  ****  ______________

Program No. - 23 :

Program to calculate Total Surface Area of Cuboid.

Code :

#include <stdio.h>

int  main()

{

       float l, b, h, tsa;

       system( "cls" );

       printf( "Enter Length, Breath and Height : " );

       scanf( "%f %f %f", &l, &b, &h );

       tsa = 2 * ((l*b) + (b*h) + (h*l));

       printf( "\nTotal Surface Area of cuboid = %f\n", tsa );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484B.jpg)

______________  ****  ______________

Program No. - 24 :

Program to calculate Area of Trapezium.

Code :

#include <stdio.h>

int  main()

{

       float area, h, b1, b2;

       system( "cls" );

       printf( "Enter Two Parallel Sides of Trapezium : " );

       scanf( "%f %f", &b1, &b2 );

       printf( "Enter Height of Trapezium : " );

       scanf( "%f",&h );

       area = (1.0 / 2.0) * h * (b1 + b2);

       printf( "\nArea of Trapezium = %f\n", area );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484C.jpg)

______________  ****  ______________

Program No. - 25 :

Program to input Basic Monthly Salary and calculate HRA, DA and Gross Monthly Salary.

Code :

#include <stdio.h>

int main()

{

       float bs, gs, da, hra ;

       system( "cls" );

       printf ( "Enter Basic Monthly Salary : " ) ;

       scanf ( "%f", &bs ) ;

       hra = bs * 20 / 100 ;

       da = bs * 45 / 100 ;

       gs = bs + hra + da ;

       printf ( "\nBasic Monthly Salary : Rs. %f\n", bs ) ;

       printf ( "HRA............................. : Rs. %f\n", hra ) ;

       printf ( "DA................................ : Rs. %f\n", da ) ;

       printf ( "Gross Monthly Salary.. : Rs. %f\n", gs ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484D.jpg)

______________  ****  ______________

Program No. - 26 :

Program to explain Simple C Program Structure.

Code :

// File Inclusion Section

#include <stdio.h>

// Global Declaration & Definition Section

int  x, y = 20;

void  show();

// main Function

int  main()

{

       int  a, b = 40;

       system( "cls" );

       x = 10;

       a = 30;

       printf( "a  = %d, b = %d\n", a, b );

       show();

       system( "pause" );

       return 0;

}

// Function Definition

void  show()

{

       printf( "x  = %d, y = %d\n", x, y );

}

Output :

![](image_rsrc484E.jpg)

______________  ****  ______________

Chapter − 2

Variables, Constants  &  Data Types

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 27 :

Program to explain Variable Declaration and Assignment.

Code :

#include <stdio.h>

int  main()

{

       int length; ​​// Variable Declaration.

       system( "cls" );

       length = 10; ​​// Assignment.

       printf( "The length is " );

       printf( "%d\n", length );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484F.jpg)

______________  ****  ______________

Program No. - 28 :

Program to explain Variable Initialization.

Code :

#include <stdio.h>

int  main()

{

       float radius = 10.0, height = 10.0;

       float volume;

       system( "cls" );

       volume = 3.1416 * radius * radius * height;

       printf( "Volume is : %f\n", volume );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484G.jpg)

______________  ****  ______________

Program No. - 29 :

Program to define and use Constants using const keyword.

Code :

#include <stdio.h>

int main()

{

       const int MAX = 100;

       const float PI = 3.14159;

       system( "cls" );

       printf( "SIZE : %d\n", MAX );

       printf( "PI   : %f\n", PI );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484H.jpg)

______________  ****  ______________

Program No. - 30 :

Program to explain Constant definition.

Code :

#include <stdio.h>

int  main()

{

       float  rad, vol;

       const  float  PI = 3.14159;

       system( "cls" );

       printf( "Enter Radius of Sphere : " );

       scanf( "%f", &rad );

       vol = ( 4.0 / 3.0 ) * PI * rad * rad * rad;

       printf( "\nVolume of Sphere is = %f\n", vol );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484J.jpg)

______________  ****  ______________

Program No. - 31 :

Program to define and use Constants using #define preprocessor.

Code :

#include <stdio.h>

#define MAX 100

#define PI 3.14159

int main()

{

       system( "cls" );

       printf( "SIZE : %d\n", MAX );

       printf( "PI   : %f\n", PI );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484K.jpg)

______________  ****  ______________

Program No. - 32 :

Program to create constant using #define preprocessor.

Code :

#include <stdio.h>

#define   PI   3.14159

int  main()

{

       float   r, vol;

       system( "cls" );

       printf( "Enter Radius of Hemi-Sphere : " );

       scanf( "%f", &r );

       vol = ( 2.0 / 3.0 ) * PI * r * r * r;

       printf( "\nVolume of Hemi-Sphere = %f\n", vol );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484M.jpg)

______________  ****  ______________

Program No. - 33 :

Program to explain Variable definition and use.

Code :

#include <stdio.h>

int  main()

{

       float  rad, area;

       system( "cls" );

       printf( "Enter Radius of Circle : " );

       scanf( "%f", &rad );

       area = 3.14 * rad * rad;

       printf( "\nArea of Circle is = %f\n", area );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484N.jpg)

______________  ****  ______________

Program No. - 34 :

Program to explain Global & Local Variable.

Code :

#include <stdio.h>

int  x = 10;​​/* ​Global Variable​*/

int  main()

{

       int  y = 20;​​/* ​Local Variable ​*/

       system( "cls" );

       printf( "x = %d, y = %d\n", x,  y );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484P.jpg)

______________  ****  ______________

Program No. - 35 :

Program to use Character Data Type.

Code :

#include <stdio.h>

int  main()

{

       char  ch;

       system( "cls" );

       ch = 'A';  

       printf( "ch = %c\n", ch );

       ch = 97;   ​​/* ASCII value of a */

       printf( "ch = %c\n", ch );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484R.jpg)

______________  ****  ______________

Program No. - 36 :

Program to print ASCII value of given Character.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a Character : " );

       scanf( "%c", &ch );

       printf( "\nThe ASCII value of \'%c\' is : %d\n", ch, ch );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484S.jpg)

______________  ****  ______________

Program No. - 37 :

Program to use Escape Sequence / Back-Slash character.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "A\nB \n" );

       printf( "A\tB \n" );

       printf( "\"ATUL\" \n" );

       printf( "\'ATUL\' \n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484T.jpg)

______________  ****  ______________

Program No. - 38 :

Program to explain the input of single character using getchar() function.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a Character : " );

       ch = getchar();

       printf( "ch = %c\n", ch );

​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484U.jpg)

______________  ****  ______________

Program No. - 39 :

Program to use User-defined Type declaration ( typedef ).

Code :

#include <stdio.h>

typedef  int  integer;

typedef  float  real;

int  main()

{

       integer  a = 100;

       real  b = 12.345;

       system( "cls" );

       printf( "a = %d, b = %f\n", a, b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484V.jpg)

______________  ****  ______________

Program No. - 40 :

Program to calculate Compound Interest by using Math library function pow().

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       float  ci, p, r, n, a;

       system( "cls" );

       printf( "Enter Principal, Rate & Time : " );

       scanf( "%f %f %f", &p, &r, &n );

       a = p * pow( ( 1 + ( r / 100 ) ), n ) ;

       ci = a − p ;

       printf( "\nCompound interest = Rs. %f\n", ci );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484W.jpg)

______________  ****  ______________

Program No. - 41 :

Program to calculate Area of Triangle by using Math library function sqrt().

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       float  s, a, b, c, ar;

       system( "cls" );

       printf( "Enter the value a, b & c : " );

       scanf( "%f %f %f", &a, &b, &c );

       s = (a + b + c) / 2;

       ar = sqrt( s * (s − a) * (s − b) * (s − c) );

       printf( "\nArea of Triangle is = %f\n", ar );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484X.jpg)

______________  ****  ______________

Program No. - 42 :

Program to calculate the distance between the two points.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       float x1, y1, x2, y2, dist;

       system( "cls" );

       printf( "Enter value of x1 : " );

       scanf( "%f", &x1 );

       printf( "Enter value of y1 : " );

       scanf( "%f", &y1 );

       printf( "Enter value of x2 : " );

       scanf( "%f", &x2 );

       printf( "Enter value of y2 : ");

       scanf( "%f", &y2 );

       dist = sqrt(((x2 − x1) * (x2 − x1)) + ((y2 − y1) * (y2 − y1)));

       printf( "\nDistance between Two Points : %.4f\n", dist );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484Y.jpg)

______________  ****  ______________

Program No. - 43 :

Program to display the range of different character and integer data types using pre-defined constants.

Code :

#include <stdio.h>

#include <limits.h>

int  main()

{

       int i;

       system( "cls" );

       printf( "CHAR_MIN : %d\n", CHAR_MIN );

       printf( "CHAR_MAX : %d\n", CHAR_MAX );

       printf( "SHRT_MIN : %d\n", SHRT_MIN );

       printf( "SHRT_MAX : %d\n", SHRT_MAX );

       printf( "INT_MIN : %d\n", INT_MIN );

       printf( "INT_MAX : %d\n", INT_MAX );

       printf( "LONG_MIN : %ld\n", LONG_MIN );

       printf( "LONG_MAX : %ld\n", LONG_MAX );

       printf( "LLONG_MIN : %lld\n", LLONG_MIN );

       printf( "LLONG_MAX : %lld\n", LLONG_MAX );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc484Z.jpg)

______________  ****  ______________

Program No. - 44 :

Program to display the upper limit of different unsigned character and integer data types using pre-defined constants.

Code :

#include <stdio.h>

#include <limits.h>

int  main()

{

       int i;

       system( "cls" );

       printf( "UCHAR_MAX : %d\n", UCHAR_MAX );

       printf( "USHRT_MAX : %d\n", USHRT_MAX );

       printf( "UINT_MAX : %u\n", UINT_MAX );

       printf( "ULONG_MAX : %lu\n", ULONG_MAX );

       printf( "ULLONG_MAX : %llu\n", ULLONG_MAX );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4850.jpg)

______________  ****  ______________

Program No. - 45 :

Program to explain unsigned modifier.

Code :

#include <stdio.h>

int  main()

{

       int var1 = 1500000000;

       unsigned int var2 = 1500000000;

       system( "cls" );

       var1 = ( var1 * 2 ) / 3;

       var2 = ( var2 * 2 ) / 3;

       printf( "Signed variable = %d\n", var1 );

       printf( "Unsigned variable = %d\n", var2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4851.jpg)

______________  ****  ______________

Chapter – 3

Operators  &  Expressions

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 46 :

Program to explain all Unary Operators ( +, −, !, ++, −−, ~ ).

Code :

#include <stdio.h>

int  main()

{

       int a, b;      

       system( "cls" );

       printf( "Unary Operators : \n" );

       a = +10;        ​​// Positive

       b = −10;        ​​// Negative

       printf( "a = %d \nb = %d\n", a, b );

       a = 1;

       b = !a;         ​​// Not

       printf( "\n!a = %d\n", b );

       a = 10;

       b = ++a;        ​​// Increment

       printf( "\n++a = %d\n", b );

       a = 10;

       b = −−a;        ​​// Decrement

       printf( "−−a = %d\n", b );

       a = 10;

       b = ~a;         ​​// Complement

       printf( "\n~a = %d\n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4852.jpg)

______________  ****  ______________

Program No. - 47 :

Program to use Arithmetic operators  (  +   −   *   /   %  ).

Code :

#include <stdio.h>

int  main()

{

       int  a = 20, b = 3;

       int  sum, sub, mul, rem, idiv ;

       float  rdiv;

       system( "cls" );

       sum = a + b;

       sub = a − b;

       mul = a * b;

       idiv = a / b;

       rem = a % b;

       rdiv = (float)a / (float)b;

       printf( "sum = %d\n", sum );

       printf( "sub = %d\n", sub );

       printf( "mul = %d\n", mul );

       printf( "idiv = %d\n", idiv );

       printf( "rem = %d\n", rem );

       printf( "\nrdiv = %f\n", rdiv );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4853.jpg)

______________  ****  ______________

Program No. - 48 :

Program to explain Relational Operators ( <, >, <=, >=, ==, != ).

Code :

#include <stdio.h>

int  main()

{

       int n;

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%d", &n );

       printf( "\n(n < 10) is = %d\n", ( n < 10 ) );

       printf( "(n > 10) is = %d\n", ( n > 10 ) );

       printf( "(n <= 10) is = %d\n", ( n <= 10 ) );

       printf( "(n >= 10) is = %d\n", ( n >= 10 ) );

       printf( "(n == 10) is = %d\n", ( n == 10 ) );

       printf( "(n != 10) is = %d\n", ( n != 10 ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4854.jpg)

______________  ****  ______________

Program No. - 49 :

Program to explain the Relational operator.

( <  >  <=  >=  ==  != ).

Code :

#include <stdio.h>

int  main()

{

       int a;

       system( "cls" );

       a = ( 10 < 20 );

       printf( "(10 < 20) = %d\n", a ) ;

       a = ( 10 > 20 );

       printf( "(10 > 20) = %d\n", a ) ;

       a = ( 10 <= 20 );

       printf( "(10 <= 20) = %d\n", a ) ;

       a = ( 10 >= 20 );

       printf( "(10 >= 20) = %d\n", a ) ;

       a = ( 20 == 20 );

       printf( "(20 == 20) = %d\n", a ) ;

       a = ( 20 != 20 );

       printf( "(20 != 20) = %d\n", a ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4855.jpg)

______________  ****  ______________

Program No. - 50 :

Program to explain Logical And ( && ) operator.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "0 && 0 = %d\n", (0 && 0) );

       printf( "0 && 1 = %d\n", (0 && 1) );

       printf( "1 && 0 = %d\n", (1 && 0) );

       printf( "1 && 1 = %d\n", (1 && 1) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4856.jpg)

______________  ****  ______________

Program No. - 51 :

Program to explain Logical Or ( || ) operator.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "0 || 0 = %d\n", (0 || 0) );

       printf( "0 || 1 = %d\n", (0 || 1) );

       printf( "1 || 0 = %d\n", (1 || 0) );

       printf( "1 || 1 = %d\n", (1 || 1) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4857.jpg)

______________  ****  ______________

Program No. - 52 :

Program to explain Logical Not ( ! ) operator.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "!0 = %d\n", (!0) );

       printf( "!1 = %d\n", (!1) ); 

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4858.jpg)

______________  ****  ______________

Program No. - 53 :

Program to explain the Logical AND ( && ) operator.

Code :

#include <stdio.h>

int  main()

{

       int a;

       system( "cls" );

       a = ( 2< 1 ) && ( 4 < 3 );

       printf( "(2<1) && (4<3) = %d\n", a ) ;

       a = ( 2< 1 ) && ( 4 > 3 );

       printf( "(2<1) && (4>3) = %d\n", a ) ;

       a = ( 2> 1 ) && ( 4 < 3 );

       printf( "(2>1) && (4<3) = %d\n", a ) ;

       a = ( 2> 1 ) && ( 4 > 3 );

       printf( "(2>1) && (4>3) = %d\n", a ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4859.jpg)

______________  ****  ______________

Program No. - 54 :

Program to explain the Logical OR ( || ) operator.

Code :

#include <stdio.h>

int  main()

{

       int a;

       system( "cls" );

       a = ( 2 < 1 ) || ( 4 < 3 );

       printf( "(2<1) || (4<3) = %d\n", a ) ;

       a = ( 2 < 1 ) || ( 4 > 3 );

       printf( "(2<1) || (4>3) = %d\n", a ) ;

       a = ( 2 > 1 ) || ( 4 < 3 );

       printf( "(2>1) || (4<3) = %d\n", a ) ;

       a = ( 2 > 1 ) || ( 4 > 3 );

       printf( "(2>1) || (4>3) = %d\n", a ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485A.jpg)

______________  ****  ______________

Program No. - 55 :

Program to explain the Logical NOT ( ! ) operator.

Code :

#include <stdio.h>

int  main()

{

       int a;

       system( "cls" );

       a = !( 2 < 1 );

       printf( "!(2<1) = %d\n", a ) ;

       a = !( 2 > 1 );

       printf( "!(2>1) = %d\n", a ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485B.jpg)

______________  ****  ______________

Program No. - 56 :

Program to use Assignment Operator ( = ).

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, d;

       system( "cls" );

       a = 10;​​/*  10 = a;  ​invalid  */

       b = a;

       c = a + b;​​/*  a + b = c;  ​invalid  */  

       d = 10;

       d = d + 10;​​/*  equivalent to  d += 10;  */

       printf( "a = %d, b = %d\n", a, b );

       printf( "c = %d, d = %d\n", c, d );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485C.jpg)

______________  ****  ______________

Program No. - 57 :

Program to use Assignment Operator ( = ).

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, d, e, f;

       system( "cls" );

       a = b = c = d = e = f = 10;

       printf( "a = %d, b = %d\n", a, b );

       printf( "c = %d, d = %d\n", c, d );

       printf( "e = %d, f = %d\n", e, f );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485D.jpg)

______________  ****  ______________

Program No. - 58 :

Program to explain Short-hand Assignment( Compound Assignment ) Operator.

Code :

#include <stdio.h>

int  main()

{

       int num = 25;

       system( "cls" );

       printf( "Num : %d\n", num );

       num += 10;

       printf( "Num += 10 : %d\n", num );

       num −= 5;

       printf( "Num −= 5 : %d\n", num );

       num *= 2;

       printf( "Num *= 2 : %d\n", num );

       num /= 3;

       printf( "Num /= 3 : %d\n", num );

       num %= 3;

       printf( "Num %= 3 : %d\n", num );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485E.jpg)

______________  ****  ______________

Program No. - 59 :

Program to explain the Prefix and Postfix Increment ( ++ ) operator.

Code :

#include <stdio.h>

int  main( )

{

       int  a = 10, b;

       system( "cls" );

       b = ++a;

       printf( "After Prefix Increment  : " );

       printf( "a = %d and b = %d\n", a, b );

       a = 10;

       b = a++;

       printf( "After Postfix Increment : " );

       printf( "a = %d and b = %d\n", a, b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485F.jpg)

______________  ****  ______________

Program No. - 60 :

Program to explain the Prefix and Postfix Decrement (−−) operator.

Code :

#include <stdio.h>

int  main( )

{

       int  a = 10, b;

       system( "cls" );

       b = −−a;

       printf( "After Prefix Decrement  : " );

       printf( "a = %d and b = %d\n", a, b );

       a = 10;

       b = a−−;

       printf( "After Postfix Decrement : " );

       printf( "a = %d and b = %d\n", a, b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485G.jpg)

______________  ****  ______________

Program No. - 61 :

Program to explain the use of Prefix Increment( ++ ) Operator.

Code :

#include <stdio.h>

int  main()

{

       int a = 10, b = 20 ,c;

       system( "cls" );

       c = (++a) + (++b);

       printf( "Value of a = %d\n", a );

       printf( "Value of b = %d\n", b );

       printf( "Value of c = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485H.jpg)

______________  ****  ______________

Program No. - 62 :

Program to explain the use of Postfix Increment( ++ ) Operator.

Code :

#include <stdio.h>

int  main()

{

       int a = 10, b = 20 ,c;

       system( "cls" );

       c = (a++) + (b++);

       printf( "Value of a = %d\n", a );

       printf( "Value of b = %d\n", b );

       printf( "Value of c = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485J.jpg)

______________  ****  ______________

Program No. - 63 :

Program to explain the use of Prefix Decrement Operator ( −− ).

Code :

#include <stdio.h>

int  main()

{

       int  a = 10, b = 20 ,c;

       system( "cls" );

       c = (−−a) + (−−b);

       printf( "Value of a = %d\n", a );

       printf( "Value of b = %d\n", b );

       printf( "Value of c = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485K.jpg)

______________  ****  ______________

Program No. - 64 :

Program to explain the use of Postfix Decrement Operator ( −− ).

Code :

#include <stdio.h>

int  main()

{

       int  a = 10, b = 20 ,c;

       system( "cls" );

       c = (a−−) + (b−−);

       printf( "Value of a = %d\n", a );

       printf( "Value of b = %d\n", b );

       printf( "Value of c = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485M.jpg)

______________  ****  ______________

Program No. - 65 :

Program to explain the use of Bitwise Operators ( &, |, ^, ~, <<, >> ).

Code :

#include <stdio.h>

int  main()

{

       int a = 3, b = 6, c;

       system( "cls" );

       printf( "a = %d\n", a );

       printf( "b = %d\n", b );

       c = a & b;

       printf( "a & b = %d\n", c );

       c = a | b;

       printf( "a | b = %d\n", c );

       c = a ^ b;

       printf( "a ^ b = %d\n", c );

       c = ~a;

       printf( "~a = %d\n", c );

       c = a << 3;

       printf( "a << 3 = %d\n", c );

       c = b >> 2;

       printf( "b >> 2 = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485N.jpg)

______________  ****  ______________

Program No. - 66 :

Program to use sizeof() operator.

Code :

#include <stdio.h>

int  main()

{

       int a = 100, b;

       system( "cls" );

       b = sizeof( a );

       printf( "The size of a : %d\n", b );

       b = sizeof( double );

       printf( "The size of double : %d\n", b );

       b = sizeof( 123L );

       printf( "The size of 123L : %d\n", b );

       b = sizeof( 123.45 );

       printf( "The size of 123.45 : %d\n", b );

       b = sizeof( 123.45f );

       printf( "The size of 123.45f : %d\n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485P.jpg)

______________  ****  ______________

Program No. - 67 :

Program to explain sizeof() operator.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "The size of a char is:\t\t" );

       printf( "%d bytes.\n", sizeof( char ) );

       printf( "The size of a short int is:\t" );

       printf( "%d bytes.\n", sizeof( short ) );

       printf( "The size of an int is:\t\t" );

       printf( "%d bytes.\n", sizeof( int ) );

       printf( "The size of a long int is:\t" );;

       printf( "%d bytes.\n", sizeof( long ) );

       printf( "The size of a long long int is:\t" );;

       printf( "%d bytes.\n", sizeof( long long ) );

       printf( "The size of a float is:\t\t" );

       printf( "%d bytes.\n", sizeof( float ) );

       printf( "The size of a double is:\t" );

       printf( "%d bytes.\n", sizeof( double ) );

       printf( "The size of a long double is:\t" );

       printf( "%d bytes.\n", sizeof( long double ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485R.jpg)

______________  ****  ______________

Program No. - 68 :

Program to explain the use Comma( , ) Operator.

Code :

#include <stdio.h>

int  main()

{

       int a, b, c;

       system( "cls" );

       c = ( a=10, b=20, a+b );

       printf( "a : %d\n", a );

       printf( "b : %d\n", b );

       printf( "c : %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485S.jpg)

______________  ****  ______________

Program No. - 69 :

Program to use Comma ( , ) operator.

Code :

#include <stdio.h>

int  main()

{

       int  num, sq, cube;

       system( "cls" );

       num = 10;

       sq = ( num * num ), cube = ( num * num * num );

       printf( "The square of %d is : %d\n", num, sq );

       printf( "The cube of %d is   : %d\n", num, cube );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485T.jpg)

______________  ****  ______________

Program No. - 70 :

Program to explain the Comma Operator ( , ).

Code :

#include <stdio.h>

int  main()

{

       int a = 10, b = 10;

       system( "cls" );

       // Comma Operator ( L −> R )

       printf( "Value = %d\n", ( a *= 2, b ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485U.jpg)

______________  ****  ______________

Program No. - 71 :

Program to rotate values of three variables in single statement using comma operator.

Code :

#include <stdio.h>

int  main()

{

       int a = 1, b = 2, c = 3, t;      

       system( "cls" );

       printf( "a = %d, b = %d, c = %d", a, b, c );

       t=a, a=b, b=c, c=t;  ​​/* comma operator */

       printf( "\nAfter Rotation : \n" );

       printf( "a = %d, b = %d, c = %d\n", a, b, c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485V.jpg)

______________  ****  ______________

Program No. - 72 :

Program to explain the use Conditional / Ternary Operator( ? : ).

Code :

#include <stdio.h>

int  main()

{

       int a, b, max;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       max = ( (a > b) ? a : b );

       printf( "\nMaximum Value is : %d\n", max );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485W.jpg)

______________  ****  ______________

Program No. - 73 :

Program to find biggest of three numbers using ternary operator / conditional operator ( ? : ).

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, max;

       system( "cls" );

       printf( "Enter Three Numbers : " );

       scanf( "%d %d %d", &a ,&b, &c );

       max = ( (a>b) ? ((a>c)?a:c) : ((b>c)?b:c) );

       printf( "\nMaximum = %d\n", max );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485X.jpg)

______________  ****  ______________

Program No. - 74 :

Program to check whether the given number is Positive or Negative number using Conditional Operator (?:) in puts() function.

Code :

#include <stdio.h>

int  main()

{

       int n;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       puts( (n >= 0) ? "\nPositive Number." :

"\nNegative Number." );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc485Y.jpg)![](image_rsrc485Z.jpg)

______________  ****  ______________

Program No. - 75 :

Program to explain the Expression.

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, d, x;

       system( "cls" );

       printf( "Enter 4 Integers : " );

       scanf( "%d %d %d %d", &a, &b, &c, &c );

       x = ( a + b ) / ( c − d );

       printf( "Value = %d\n", x );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4860.jpg)

______________  ****  ______________

Program No. - 76 :

Program to explain Operator Precedence.

Code :

#include <stdio.h>

int  main()

{

       float result;

       system( "cls" );

       result = 1.0 + 2.0 * 3.0 / 4.0;

       printf( "%f\n", result );

       result = 1.0 / 2.0 + 3.0;

       printf( "%f\n", result );

       result = (1.0 + 2.0) / 3.0;

       printf( "%f\n", result );

       result = (1.0 + 2.0 / 3.0) + 4.0;

       printf( "%f\n", result );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4861.jpg)

______________  ****  ______________

Program No. - 77 :

Program to explain Automatic or Implicit Type Conversion.

Code :

#include <stdio.h>

int  main()

{

       int  a = 10, b = 20;

       float c = 10.50;

       long d = 20L, e;

       system( "cls" );

       e = ( ( a + c ) * d ) + b;

       printf( "Value of e : %ld\n", e );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4862.jpg)

______________  ****  ______________

Program No. - 78 :

Program to use Type Casting or Explicit Conversion.

Code :

#include <stdio.h>

int  main()

{

       int  a = 10, b = 20;

       float c = 10.50;

       long d = 20L, e;

       system( "cls" );

       e = ( ( ( (long)a + (long)c ) * d ) + (long)b );

       printf( "Value of e : %ld\n", e );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4863.jpg)

______________  ****  ______________

Program No. - 79 :

Program to explain the Type Casting.

Code :

#include <stdio.h>

int  main( )

{

       float  a ;

       int  x = 6, y = 4 ;

       system( "cls" );

       a = x / y ;

       printf( "Value of a (without casting ) = %f\n", a ) ;

       a = (float) x / y ;

       printf( "Value of a (with casting ) = %f\n", a ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4864.jpg)

______________  ****  ______________

Program No. - 80 : 

Program to use Explicit Conversion or Type Casting.

Code :

#include <stdio.h>

int  main()

{

       int  a = 2000000000, b = 2000000000;

       system( "cls" );

       a = ( (long long)a * 10 ) / 20;

       b = ( b * 10 ) / 20;

       printf( "a : %d\n", a );

       printf( "b : %d\n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4865.jpg)

______________  ****  ______________

Program No. - 81 :

Program to explain Automatic / Implicit type conversion.

Code :

#include <stdio.h>

// implicit conversion

int main()

{

       system( "cls" );

       long l = 100;     ​​/* int −> long */\

       double d = l;   ​​/* long −> double */

       printf( "l = %ld\n", l );

       printf( "d = %lf\n", d );

       d = 25 + 10.5; ​​/* int −> double */

       printf( "d = %lf\n", d );

       int i = 325.5; ​   /* double −> int (data loss possiblity) */

       char c = i;   ​​/* int −> char (data loss possiblity)  */    

       printf( "i = %d\n", i );

       printf( "c = %c\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4866.jpg)

______________  ****  ______________

Program No. - 82 :

Program to explain Type Casting / Explicit type conversion.

Code :

#include <stdio.h>

// explicit conversion

int main()

{

       system( "cls" );

       int i = (int)12.5;     ​​/* double −> int */

       char c = (char)65;     ​/* int −> char */

       printf( "i = %d\n", i );

       printf( "c = %c\n", c );

       i = 25 + (int)10.5;     ​​/* double −> int */

       printf( "i = %d\n", i );

       i = (int)325.5; ​/* double −> int (data loss possiblity) */

       c = (char)i;   ​​/* int −> char (data loss possiblity)  */

       printf( "i = %d\n", i );

       printf( "c = %c\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4867.jpg)

______________  ****  ______________

Program No. - 83 :

Program to convert Total number of days into years, months, weeks and days.

Code :

#include <stdio.h>

int  main()

{

       int  d, y, m, w;

       system( "cls" );

       printf( "Enter Total Number of Days : " );

       scanf( "%d", &d );

       y = d / 365;

       d = d % 365;

       m = d / 30;

       d = d % 30;

       w = d / 7;

       d = d % 7;

       printf( "Years  = %d\n", y );

       printf( "Months = %d\n", m );

       printf( "Weeks  = %d\n", w );

       printf( "Days   = %d\n", d );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4868.jpg)

______________  ****  ______________

Program No. - 84 :

Program to find value of Hundred, Tens and Unit place of given Three Digit Number.

Code :

#include <stdio.h>

int  main()

{

       int  n, u, t, h;

       system( "cls" );

       printf( "Enter a Three Digit Number : " );

       scanf( "%d", &n );

       u = n % 10;

       n = n / 10;

       t = n % 10;

       h = n / 10;

       printf( "Hundred Place = %d\n", h );

       printf( "Tens Place    = %d\n", t );

       printf( "Unit Place    = %d\n", u );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4869.jpg)

______________  ****  ______________

Program No. - 85 :

Program to Swap of two numbers using Bitwise operator.

Code :

#include <stdio.h>

int  main()

{

       int a, b;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       printf( "\nBefore Swapping : a = %d, b = %d\n", a, b );

       a = a ^ b;

       b = a ^ b;

       a = a ^ b;

       printf( "After Swapping  : a = %d, a = %d\n", a, b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486A.jpg)

______________  ****  ______________

Chapter – 4

Selection

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 86 :

Program to explain Simple If statement.

Code :

#include <stdio.h>

int  main()

{

       int  n;

       system( "cls" );

       printf( "Enter a number : " );

       scanf( "%d", &n );

       if( n > 100 )

       {

              printf( "\nNumber is greater than 100.\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486B.jpg)![](image_rsrc486C.jpg)

______________  ****  ______________

Program No. - 87 :

Program to explain If-else statement.

Code :

#include <stdio.h>

int  main()

{

       int  n;

       system( "cls" );

       printf( "Enter Number : " );

       scanf( "%d", &n );

       if( n > 100 )

       {

              printf( "\nNumber is greater than 100.\n" );

       }

       else

       {

              printf( "\nNumber is smaller than or equal to 100.\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486D.jpg)![](image_rsrc486E.jpg)

______________  ****  ______________

Program No. - 88 :

Program to find maximum of three numbers using simple if statement.

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, max = 0;

       system( "cls" );

       printf( "Enter Three Numbers : " );

       scanf( "%d %d %d", &a, &b, &c );

       max = a;

       if( b > max )

              max = b;

       if( c > max )

              max = c;

       printf( "\nMaximum : %d\n", max );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486F.jpg)

______________  ****  ______________

Program No. - 89 :

Program to find Maximum of Two Numbers using If-Else statement.

Code :

#include <stdio.h>

int  main()

{

       int  a, b, max;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       if( a > b )

              max = a;

       else

              max = b;

       printf( "\nMaximum = %d\n", max );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486G.jpg)![](image_rsrc486H.jpg)

______________  ****  ______________

Program No. - 90 :

Program to check whether the given number is Even or Odd ?

Code :

#include <stdio.h>

int  main()

{

       int  n;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       if( n % 2 == 0 )

              printf( "\n%d is an Even number.\n", n );

       else

              printf( "\n%d is an Odd number.\n", n );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486J.jpg)![](image_rsrc486K.jpg)

______________  ****  ______________

Program No. - 91 :

Program to check whether the given number is Positive or Negative ?

Code :

#include <stdio.h>

int  main()

{

       int  n;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       if( n >= 0 )

              printf( "\n%d is a Positive number.\n", n );

       else

              printf( "\n%d is a Negative number.\n", n );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486M.jpg)![](image_rsrc486N.jpg)

______________  ****  ______________

Program No. - 92 :

Program to check whether the given character is Alphanumeric or not.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       int  ch;

       system( "cls" );

       printf( "Enter a character : " );

       ch = getchar();

       if( isalnum( ch ) )

              printf( "\nIt is an alpha-numeric character.\n" );

       else

              printf( "\nThis is not an alpha-numeric character.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486P.jpg)![](image_rsrc486R.jpg)

______________  ****  ______________

Program No. - 93 :

Program to check whether the given year is Leap year or not.

Code :

#include <stdio.h>

int main()

{

       int year;

       system( "cls" );

       printf( "Enter Year (yyyy) : " );

       scanf( "%d", &year );

       if( year % 4 == 0 )

              printf( "\n%d is Leap Year.\n", year );

       else

              printf( "\n%d is Not a Leap Year.\n", year );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486S.jpg)![](image_rsrc486T.jpg)

______________  ****  ______________

Program No. - 94 :

Program to find Maximum of Three Numbers using Nested If statement.

Code :

#include <stdio.h>

int  main()

{

       int a, b, c, g;

       system( "cls" );

       printf( "Enter Three Numbers : " );

       scanf( "%d %d %d", &a, &b, &c );

       if( a > b )

       {

              if( a > c )

                     g = a;

              else

                     g = c ;

       }

       else

        {

              if( b > c)

                     g = b;

              else

                     g = c;

       }

       printf( "\nGreatest Number is : %d\n", g );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486U.jpg)![](image_rsrc486V.jpg)

______________  ****  ______________

Program No. - 95 :

Program to find Grade using Nested If statement on the basis of Range of Marks.

​  Marks​       Grade

​80 to 100​​A+

​70 to 80​​A

​60 to 70​​B

​40 to 60​​C

​ 0 to 40​​F

Code :

#include <stdio.h>

int  main()

{

       int  m;

       system( "cls" );

       printf( "Enter the Marks : " );

       scanf( "%d", &m );

       if( m >= 80 )

       {

              printf( "\nGrade = A+ \n" );

       }

       else

       {

              if( m >= 70 )

              {

                     printf( "\nGrade = A \n" );

              }

              else​

              {

                     if( m >= 60 )

                     {

                            printf( "\nGrade = B \n" );

                     }

                     else

                     {

                            if( m >= 40 )

                            {

                                   printf( "\nGrade = C \n" );

                            }

                            else

                            {

                                   printf( "\nGrade = F \n" );

                            }

                     }

              }

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486W.jpg)![](image_rsrc486X.jpg)![](image_rsrc486Y.jpg)

______________  ****  ______________

Program No. - 96 :

Program to check whether the given number is Positive, Negative or Zero.

Code :

#include <stdio.h> >

int  main()

{

       int n;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       if( n > 0 )

              printf( "\nPositive Number.\n" );

       else if( n < 0 )

              printf( "\nNegative Number.\n" );

       else

              printf( "\nZero.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc486Z.jpg)![](image_rsrc4870.jpg)![](image_rsrc4871.jpg)

______________  ****  ______________

Program No. - 97 :

Program to find Maximum of three numbers using Nested If.

Code :

#include <stdio.h>

int main()

{

       int n1, n2, n3;

       system( "cls" );

       printf( "Enter Three Numbers : " );

       scanf( "%d %d %d", &n1, &n2, &n3 );

       if( ( n1 > n2 ) && ( n1 > n3 ) )

              printf( "\nGreatest Number : %d\n", n1 );

       else

       {

              if( n2 > n3 )

                     printf( "\nGreatest Number : %d\n", n2 );

              else

                     printf( "\nGreatest Number : %d\n", n3 );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4872.jpg)

______________  ****  ______________

Program No. - 98 :

Program to find Maximum of three numbers using Nested If.

Code :

#include <stdio.h>

int main()

{

       int n1, n2, n3, n4;

       system( "cls" );

       printf( "Enter Four numbers : " );

       scanf( "%d %d %d %d", &n1, &n2, &n3, &n4 );

       if( ( n1 > n2 ) && ( n1 > n3 ) && ( n1 > n4 ) )

              printf( "\nGreatest Number : %d\n", n1 );

       else

              if( ( n2 > n3 ) && ( n2 > n4 ) )

                     printf( "\nGreatest Number : %d\n", n2 );

              else

                     if( n3 > n4 )

                            printf( "\nGreatest Number : %d\n", n3 );

                     else

                            printf( "\nGreatest Number : %d\n", n4 );             

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4873.jpg)

______________  ****  ______________

Program No. - 99 :

Program to find Grade using Else If ladder statement on the basis of Range of Marks.

​  Marks​       Grade

​80 to 100​​A+

​70 to 80​​A

​60 to 70​​B

​40 to 60​​C

​ 0 to 40​​F

Code :

#include <stdio.h>

int  main()

{

       int  m;

       system( "cls" );

       printf( "Enter the Marks : " );

       scanf( "%d", &m );

       if( m >= 80 )

       {

              printf( "\nGrade = A+ \n" );

       }

       else if( m >= 70 )

       {

              printf( "\nGrade = A \n" );

       }

       else if( m >= 60 )

       {

              printf( "\nGrade = B \n" );

       }

       else if( m >= 40 )

       {

              printf( "\nGrade = C \n" );

       }

       else

       {

              printf( "\nGrade = F \n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4874.jpg)![](image_rsrc4875.jpg)![](image_rsrc4876.jpg)

______________  ****  ______________

Program No. - 100 :

Program to check whether the Given Year is Leap or Not.

Code :

#include <stdio.h>

int  main()

{

       int  y;

       system( "cls" );

       printf( "Enter the year (4-digit) : " );

       scanf( "%d", &y );

       if( y % 100 == 0 )

       {

              if( y % 400 == 0 )

                     printf( "\nIt is a LEAP Year.\n" );

              else

                     printf( "\nIt is NOT a LEAP Year.\n" );

       }

       else if( y % 4 == 0 )

              printf( "\nIt is a LEAP Year.\n" );

       else

              printf( "\nIt is NOT a LEAP Year.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4877.jpg)![](image_rsrc4878.jpg)![](image_rsrc4879.jpg)![](image_rsrc487A.jpg)

______________  ****  ______________

Program No. - 101 :

Program to create Menu Based (Choice Based) Program for Temperature Conversion.

Code :

#include <stdio.h>

int  main()

{

       int choice;

       float temp, cnvtemp;

       system( "cls" );

       printf( "Temp. conversation menu : \n" );

       printf( "1\. Fahrenheit to Celsius.\n" );

       printf( "2\. Celsius to Fahrenheit.\n" );

       printf( "Enter your choice  : " );

       scanf( "%d", &choice );​

       if( choice == 1 )

       {

              printf( "\nEnter temp. in Fahrenheit : " );

              scanf( "%f", &temp );

              cnvtemp = ( temp − 32 ) / 1.8;

              printf( "\nThe temp in Celsius is = %f \n", cnvtemp );

       }

       else

       {

              printf( "\nEnter temp in Celsius : " );

              scanf( "%f", &temp );​

              cnvtemp = ( 1.8 * temp ) + 32;

              printf( "\nThe temp in Fahrenheit is = %f \n", cnvtemp );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487B.jpg)![](image_rsrc487C.jpg)

______________  ****  ______________

Program No. - 102:

Program to use Arithmetic Operators.

Code :

#include <stdio.h>

int  main()

{

       char op;

       int a, b, res;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       printf( "Enter the Operator (+, −, *, /, %) : " );

       fflush( stdin );

       scanf( "%c", &op );

       if( op == '+' )

       {

              res = a + b;

       }

       else if( op == '−' )

       {

              res = a − b;

       }

       else if( op == '*' )

       {

              res = a * b;

       }

       else if( op == '/' )

       {​

              res = a / b;

       }

       else if( op == '%' )

       {

              res = a % b;

       }

       else

       {

              printf( "Invalid operator.\n" );

       }

       printf( "\n%d %c %d = %d\n", a, op, b, res );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487D.jpg)![](image_rsrc487E.jpg)![](image_rsrc487F.jpg)

______________  ****  ______________

Program No. - 103 :

Program to display the name of the week day on the basis of Week Day Number ( 1 to 7 ).

Code :

#include <stdio.h>

int  main()

{

       int d;

       system( "cls" );

       printf( "Enter Day Number(1-7) : " );

       scanf( "%d", &d );

       if( d == 1 )

       {      

              printf( "\nMonday.\n" );

       }

       else if( d == 2 )

       {

              printf( "\nTuesday.\n" );

       }

       else if( d == 3 )

       {

              printf( "\nWednesday.\n" );

       }

       else if( d == 4 )

       {

              printf( "\nThursday.\n" );

       }

       else if( d == 5 )​

       {

              printf( "\nFriday.\n" );

       }

       else if( d == 6 )

       {

              printf( "\nSaturday.\n" );

       }

       else if( d == 7 )

       {

              printf( "\nSunday.\n" );

       }

       else

       {

              printf( "\nInvalid Day Number.\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487G.jpg)![](image_rsrc487H.jpg)

______________  ****  ______________

Program No. - 104 :

Program to display the name of the week day on the basis of Week Day Number ( 1 to 7 ).

Code :

#include <stdio.h>

int  main()

{

       int  d;

       system( "cls" );

       printf( "Enter Day Number (1-7): " );

       scanf( "%d", &d );

       switch( d )

       {

              case 1:

                     printf( "\nMonday\n" );

                     break;

              case 2:

                     printf( "\nTuesday\n" );

                     break;

              case 3:

                     printf( "\nWednesday\n" );

                     break;

              case 4:

                     printf( "\nThursday\n" );

                     break;

              case 5:

                     printf( "\nFriday\n" );

                     break;​

              case 6:

                     printf( "\nSaturday\n" );

                     break;

              case 7:

                     printf( "\nSunday\n" );

                     break;

              default :

                     printf( "\nWrong Day Number.\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487J.jpg)![](image_rsrc487K.jpg)

______________  ****  ______________

Program No. - 105 :

Program to use Elseif ladder for multiple values of single variable.

Code :

#include <stdio.h>

int main()

{

       int a = 3;

       system( "cls" );

       if( a == 1 )

       {

              printf( "One.\n" );

       }

       else if( a == 2 )

       {

              printf( "Two.\n" );

       }

       else if( a == 3 )

       {

              printf( "Three.\n" );

       }

       else

       {

              printf( "Other Number.\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487M.jpg)

______________  ****  ______________

Program No. - 106 :

Program to use switch-case for multiple values of single variable.

Code :

#include <stdio.h>

int main()

{

       int a = 3;

       system( "cls" );

       switch( a )

       {

              case 1:

                     printf( "One.\n" );

                     break;

              case 2:

                     printf( "Two.\n" );

                     break;

              case 3:

                     printf( "Three.\n" );

                     break;

              default:

                     printf( "Other Number.\n" );

                     break;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487N.jpg)

______________  ****  ______________

Program No. - 107 :

Program to perform Arithmatic Operation using Switch-case statement.

Code :

#include <stdio.h>

int  main()

{

       char op;

       int a, b, res;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       printf( "Enter the operator (+, −, *, /, %) : " );

       fflush( stdin );

       scanf( "%c", &op );

       switch( op )

       {

              case '+':

                     res = a + b;

                     break;

              case '−':

                     res = a − b;

                     break;

              case '*':

                     res = a * b;

                     break;

              case '/':

                     res = a / b;​

                     break;

              case '%':

                     res = a % b;

                     break;

              default:

                     printf( "\nInvalid operator.\n" );

                     break;

       }

       printf( "\n%d %c %d = %d\n", a, op, b, res );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487P.jpg)![](image_rsrc487R.jpg)

______________  ****  ______________

Program No. - 108 :

Program to use char datatype in switch-case statement.

Code :

#include <stdio.h>

int main()

{

       char chart;

       system( "cls" );

       printf( "Chart : Bar/Scatter/Line/Pie/Exit.\n" );

       printf( "Press first letter of the chart you want : " );

       chart = toupper( getchar() );

       switch( chart )

       {

              case 'B':

                     printf( "\nDrawing Bar Chart.\n" );

                     break;

              case 'S':

                     printf( "\nDrawing Scatter Chart.\n" );

                     break;

              case 'L':

                     printf( "\nDrawing Line Chart.\n" );

                     break;

              case 'P':

                     printf( "\nDrawing Pie Chart.\n" );

                     break;

              default:

                     printf( "\nWrorng Choice.\n" );

                     break;​

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487S.jpg)

______________  ****  ______________

Program No. - 109 :

Program to explain Nested Switch-Case Statement.

Code :

#include <stdio.h>

int  main()

{

       int a = 100;

       int b = 200;

       system( "cls" );

       switch( a )

       {

              case 100:

                     printf( "In Outer Switch.\n" );

                     switch( b )

                     {

                            case 200:

                                   printf( "In Inner Switch.\n" );

                     }

       }

       printf( "Value of a is : %d \n", a );

       printf( "Value of b is : %d \n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487T.jpg)

______________  ****  ______________

Program No. - 110 :

Program to check whether the given character is Vowel or not.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter an Alphabet : " );

       scanf( "%c", &ch );

       switch( ch )

       {

              case 'a':

              case 'A':

              case 'e':

              case 'E':

              case 'i':

              case 'I':

              case 'o':

              case 'O':

              case 'u':

              case 'U':

                     printf( "\n%c is a Vowel.\n", ch );

                     break;

              default :

                     printf( "\n%c is not a Vowel.\n", ch );

                     break;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487U.jpg)![](image_rsrc487V.jpg)

______________  ****  ______________

Program No. - 111 :

Program to check whether the given character is Vowel or not.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter an Alphabet : " );

       scanf( "%c", &ch );

       if( (ch == 'a' ) || ( ch == 'e' ) || ( ch == 'i' ) || ( ch == 'o' ) || ( ch == 'u' ) || ( ch == 'A' ) || ( ch == 'E' ) || ( ch == 'I' ) || ( ch == 'O' ) || ( ch == 'U' ) )

       {

              printf( "\n%c is a Vowel.\n", ch );

       }

       else

       {

              printf( "\n%c is not a Vowel.\n", ch );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487W.jpg)![](image_rsrc487X.jpg)

______________  ****  ______________

Program No. - 112 :

Program to test whether a particular bit in a given number is ON or OFF using Bitwise AND operator.

Code :

#include <stdio.h>

int  main()

{

       int  a = 45, b ;

       system( "cls" ) ;

       printf( "Value of a = %d", a ) ;

       b = a & 32 ;

       if( b == 0 )

              printf( " and its fifth bit is OFF.\n" ) ;

       else

              printf( " and its fifth bit is ON.\n" ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487Y.jpg)

______________  ****  ______________

Program No. - 113 :

Program to check whether the given character is Uppercase, Lowercase , Digits or Special Symbols.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter any Character : " );

       scanf( "%c", &ch );

       if( ch >= 65 && ch <= 90 )

              printf( "\nUpper Case Letter.\n" );

       else if( ch >= 97 && ch <= 122 )

              printf( "\nLower Case Letter.\n" );

       else if( ch >= 48 && ch <= 57 )

              printf( "\nDigit.\n" );

       else

              printf( "\nSpecial Symbol.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc487Z.jpg)

______________  ****  ______________

Program No. - 114 :

Program to check whether the given character is Uppercase, Lowercase , Digits or Special Symbols.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter any Character : " );

       scanf( "%c", &ch );

       if( ch >= 'A' && ch <= 'Z' )

              printf( "\nUpper Case Letter.\n" );

       else if( ch >= 'a' && ch <= 'z' )

              printf( "\nLower Case Letter.\n" );

       else if( ch >= '0' && ch <= '9' )

              printf( "\nDigit.\n" );

       else

              printf( "\nSpecial Symbol.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4880.jpg)

______________  ****  ______________

Program No. - 115 :

Program to check whether the given character is Uppercase, Lowercase , Digits or Special Symbols.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter any Character : " );

       scanf( "%c", &ch );

       if( isupper( ch ) )

              printf( "\nUpper Case Letter.\n" );

       else if( islower( ch ) )

              printf( "\nLower Case Letter.\n" );

       else if( isdigit( ch ) )

              printf( "\nDigit.\n" );

       else

              printf( "\nSpecial Symbol.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4881.jpg)

______________  ****  ______________

Program No. - 116 :

Program to change the Case of a character ( upper to lower or lower to upper ).

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter any Alphabet : " );

       scanf( "%c", &ch );

       if( ch >= 'A' && ch <= 'Z' )

              printf( "\nLower Case : %c\n", ( ch + 32 ) );

       else if( ch >= 'a' && ch <= 'z' )

              printf( "\nUpper Case : %c\n", ( ch − 32 ) );

       else

              printf( "\nNon-alphabet : %c\n", ch );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4882.jpg)![](image_rsrc4883.jpg)![](image_rsrc4884.jpg)

______________  ****  ______________

Program No. - 117 :

Program to calculate Net Price after Discount on the basis of quantity purchase using Conditional Operator ( ?: ).

​Quantity​       Discount (%)

​    > 10​​5 %

​    > 25 ​​10 %

​    > 50 ​​15 %

Code :

#include <stdio.h>

int main()

{

       const float price = 250.0;

       const float discount1 = 0.05;

       const float discount2 = 0.1; 

       const float discount3 = 0.15;

       float total_price = 0.0;

       int quantity = 25;

       system( "cls" );

       total_price = quantity * price * ( 1.0 -

                     ( quantity>50 ? discount3 :

                            ( quantity>20 ? discount2 :

                                   ( quantity>10 ? discount1 : 0.0 ) ) ) );

       printf( "The price for %d is Rs. %.2f\n", quantity, total_price );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4885.jpg)

______________  ****  ______________

Program No. - 118 :

Program to find Smallest value of 4 numbers using conditional operators ( ?: ).

Code :

#include <stdio.h>

int main()

{

       int a ,b, c, d, small;

       system( "cls" );

       printf( "Enter 4 Numbers : " );

       scanf( "%d %d %d %d", &a, &b, &c, &d );

       small = ( (a<b) ? ((a<c)?((a<d)?a:d):((c<d)?c:d)) :

                                   ((b<c)?((b<d)?b:d):((c<d)?c:d)) );

       printf( "\nSmallest Number : %d\n", small );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4886.jpg)

______________  ****  ______________

Chapter − 5

Iteration / Loop

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 119 :

Program to display first N natural number using for loop.

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number : " );

       scanf( "%d", &n );

       for( i=1 ; i<= n ; i++ )

       {

              printf( "  %d", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4887.jpg)

______________  ****  ______________

Program No. - 120 :

Program to explain Simple While Loop.

Code :

#include <stdio.h>

int  main()

{

       int n = 1;

       system( "cls" );

       while( n != 0 )

       {

              printf( "Enter No.( 0 for exit) : " );

              scanf( "%d", &n );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4888.jpg)

______________  ****  ______________

Program No. - 121 :

Program to display first N natural number using while loop.

Code :

#include <stdio.h>

int  main()

{

       int  i, n;

       system( "cls" );

       printf( "Enter Number : " );

       scanf( "%d", &n );

       i = 1;

       while( i <= n  )

       {

              printf( "  %d", i );

              i++;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4889.jpg)

______________  ****  ______________

Program No. - 122 :

Program to explain Simple Do-While Loop.

Code :

#include <stdio.h>

int  main()

{

       int n = 0;

       system( "cls" );

       do

       {

              printf( "Enter No.( 0 for exit) : " );

              scanf( "%d", &n );

       }while( n != 0 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488A.jpg)

______________  ****  ______________

Program No. - 123 :

Program to display first N natural number using do-while loop.

Code :

#include <stdio.h>

int  main()

{

       int  i, n;

       system( "cls" );

       printf( "Enter Number : " );

       scanf( "%d", &n );

       i = 1;

       do

       {

              printf( "  %d", i );

              i++;

       }while( i <= n  );

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488B.jpg)

______________  ****  ______________

Program No. - 124 :

Program to display series 1 to 10 using for loop.

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       for( i=1 ; i<=10 ; i++ )

       {

              printf( "%d  ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488C.jpg)

______________  ****  ______________

Program No. - 125 :

Program to display series 1 to 10 using for loop (in for loop initialization part is optional).

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       i = 1;

       for( ; i<=10 ; i++ )

       {

              printf( "%d  ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488D.jpg)

______________  ****  ______________

Program No. - 126 :

Program to display series 1 to 10 using for loop (in for loop increment part is optional).

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       i = 1;

       for( ; i<=10 ; )

       {

              printf( "%d  ", i );

              i++;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488E.jpg)

______________  ****  ______________

Program No. - 127 :

Program to display series 1 to 10 using for loop (in for loop condition part is optional).

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       i = 1;

       for( ; ; )

       {

              if( i > 10 )

              {

                     break;

              }

              printf( "%d  ", i );

              i++;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488F.jpg)

______________  ****  ______________

Program No. - 128 :

Program to initialize and increment multiple variables in for loop.

Code :

#include <stdio.h>

int  main()

{

       int  i, j;

       system( "cls" );

       for( i=1, j=10 ; i<j ; i++, j-- )

       {

              printf( "i : %d, j : %d\n", i, j );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488G.jpg)

______________  ****  ______________

Program No. - 129 :

Program to use Character variable in for loop.

Code :

#include <stdio.h>

int main()

{

       char ch;

       system( "cls" );

       for( ch='A' ; ch<='E' ; ch++ )

       {

              printf( "...%c", ch );

       }

       printf( "\n"  );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488H.jpg)

______________  ****  ______________

Program No. - 130 :

Program to calculate the Factorial of given Number.

Code :

#include <stdio.h>

int  main()

{

       long int n, f, i;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%ld", &n );

       f = 1;

       for( i=1 ; i<=n ; i++ )

       {

              f = f * i;

       }

       printf( "\nFactorial of %ld = %ld\n", n, f );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488J.jpg)

______________  ****  ______________

Program No. - 131 :

Program to calculate x raise to the power n using while loop.

Code :

#include <stdio.h>

int  main()

{

       int x, n, p, i;

       system( "cls" );

       printf( "%s", "Enter Base: " );

       scanf( "%d", &x );

       printf( "%s", "Enter Power: " );

       scanf( "%d", &n );

       i = 1;

       p = 1;

       while( i <= n )

       {

              p *= x;

              i++;

       }                                        

       printf( "\nPower : %d\n", p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488K.jpg)

______________  ****  ______________

Program No. - 132 :

Program to calculate x raise to the power n using for loop.

Code :

#include <stdio.h>

int  main()

{

       int x, n, p, i;

       system( "cls" );

       printf( "%s", "Enter Base: " );

       scanf( "%d", &x );

       printf( "%s", "Enter Power: " );

       scanf( "%d", &n );

       p = 1;

       for( i=1 ; i<=n ; i++ )

       {

              p *= x;

       }                                        

       printf( "\nPower : %d\n", p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488M.jpg)

______________  ****  ______________

Program No. - 133 :

Program to Count Number of Digits in a given Number.

Code :

#include <stdio.h>

int  main()

{

       long int  n, c;

       system( "cls" );

       printf( "Enter a Positive number : " );

       scanf( "%ld", &n );

       c = 0;

       while( n != 0 )

       {

              n = n / 10;

              c = c + 1;​​/*​c++; ​*/

       }

       printf( "\nThe number of the digits = %ld\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488N.jpg)

______________  ****  ______________

Program No. - 134 :

Program to find Sum of Digits of given Number.

Code :

#include <stdio.h>

int  main()

{

       long int  n, r, s;

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%ld", &n );

       s = 0;

       while( n != 0 )

       {

              r = n % 10;

              s = s + r;

              n = n / 10;

       }

       printf( "\nThe Sum of the Digits = %ld\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488P.jpg)

______________  ****  ______________

Program No. - 135 :

Program to find Reverse of given Number.

Code :

#include <stdio.h>

int  main()

{

       long int n, r, rev;

       system( "cls" );

       printf( "Enter any number : " );

       scanf( "%ld", &n );

       rev = 0;

       while( n != 0 )

       {

              r = n % 10;

              rev = ( rev * 10 ) + r;

              n = n / 10;

       }

       printf( "\nReversed number is = %ld\n", rev );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488R.jpg)

______________  ****  ______________

Program No. - 136 :

Program to chech whether the given Number is Palindrome Number or not.

Code :

#include <stdio.h>

int  main()

{

       long int n, r, x, rev;

       system( "cls" );

       printf( "Enter any number : " );

       scanf( "%ld", &n );

       x = n;

       rev = 0;

       while( n != 0 )

       {

              r = n % 10;

              rev = ( rev * 10 ) + r;

              n = n / 10;

       }

       printf( "\nReversed number is = %ld\n", rev );

       if( rev == x )

              printf( "It is a Palindrome Number.\n" );

       else

              printf( "It is Not a Palindrome Number.\n" );

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc488S.jpg)![](image_rsrc488T.jpg)

______________  ****  ______________

Program No. - 137 :

Program to check whether the given number is Perfect Number or not.

(e.g. : 6 =  1 + 2 +3 )

Code :

#include <stdio.h>

int  main()

{

       int  i, n, s;

       system( "cls" );

       printf( "Enter a number : " );

       scanf( "%d", &n );

       s = 0;

       for( i=1 ; i<=n/2 ; i++ )

       {

              if( n % i == 0 )

              {

                     s = s + i;

              }

       }

       if( s == n )

       {

              printf( "It is a PERFECT Number.\n" );

       }

       else

       {

              printf( "It is NOT a PERFECT Number.\n" );

       }​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488U.jpg)![](image_rsrc488V.jpg)

______________  ****  ______________

Program No. - 138 :

Program to check whether the given number is Prime Number or not.

Code :

#include <stdio.h>

int  main()

{

       int  n, i, flag;

       system( "cls" );

       printf( "Enter the Number : " );

       scanf( "%d", &n );

       flag = 1;

       for( i=2 ; i<=n/2 ; i++ )

       {

              if( n % i == 0 )

              {

                     flag = 0;

                     break;

              }

       }

       if( flag == 1 )​​/*​if( flag )​*/

              printf( "%d is a Prime Number.\n", n );

       else

              printf( "%d is not a Prime Number.\n", n );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488W.jpg)![](image_rsrc488X.jpg)

______________  ****  ______________

Program No. - 139 :

Program to check whether the given three digit number is Armstrong Number or Not.

(e.g. : 153 = 13 + 53 + 33 )

Code :

#include <stdio.h>

int  main()

{

       int x, n, r, s;

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%d", &n );

       x = n;

       s = 0;

       while( n != 0 )

       {

              r = n % 10;

              s = s + ( r * r * r );

              n = n / 10;

       }

       if( s == x )

              printf("\n%d is a Armstrong Number.\n", x );

       else

              printf( "\n%d is not a Armstrong Number.\n", x );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc488Y.jpg)![](image_rsrc488Z.jpg)

______________  ****  ______________

Program No. - 140 :

Program to check whether the given number is Strong Number or Not.

(e.g. : 145 = 1! + 4! + 5! )

Code :

#include <stdio.h>

int  main()

{

       int n, x, r, s, i, f;

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%d", &n );

       x = n;

       s = 0;

       while( n != 0 )

       {

              r = n % 10;

              f = 1;

              for( i=1 ; i<=r ; i++ )

              {

                     f = f * i;

              }

              s = s + f;​

              n = n / 10;

        }

       if( s == x )

              printf( "\n%d is a STRONG Number.\n", x );​

       else

              printf( "\n%d is not a STRONG Number.\n", x );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4890.jpg)![](image_rsrc4891.jpg)

______________  ****  ______________

Program No. - 141 :

Program to find HCF and LCM of Two Number.

Code :

#include <stdio.h>

int  main()

{

       int a, b, s, hcf, i, lcm;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       if( a< b )

              s = a;

       else

              s = b;

       for( i=1 ; i<=s ; i++ )

       {

              if( ( a % i == 0 ) && ( b % i == 0 ) )

              {

                     hcf = i;

              }

       }

       printf( "\nThe HCF of given Numbers = %d\n", hcf );

       lcm = ( a * b ) / hcf;

       printf( "The LCM of given Numbers = %d\n", lcm );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4892.jpg)

______________  ****  ______________

Program No. - 142 :

Program to find LCM and HCF of Two Number.

Code :

#include <stdio.h>

int  main()

{

       int a, b, g, hcf, i, lcm;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &a, &b );

       if( a > b )

              g = a;

       else

              g = b;

       for( i=g ; i<=(a*b) ; i++ )

       {

              if( ( i % a == 0 ) && ( i % b == 0 ) )

              {

                     lcm = i;

                     break;

              }

       }

       printf( "\nThe LCM of given Numbers = %d\n", lcm );

​

       hcf = ( a * b ) / lcm;

       printf( "The HCF of given Numbers = %d\n", hcf );​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4893.jpg)

______________  ****  ______________

Program No. - 143 :

Program to find HCF and LCM of two given numbers.

Code :

#include <stdio.h>

int main()

{

       int  x, y, a, b, hcf, lcm, t;

       system( "cls" );

       printf( "Enter two Numbers : " );

       scanf( "%d %d", &x, &y );

       if( x > y )

       {

              a = x;

              b = y;

       }

       else

       {

              a = y;

              b = x;

       }

       while( b != 0 )

       {

              t = b;

              b = a % b;

              a = t;

       }

       hcf = a;​

       printf( "\nHCF of %d & %d : %d\n", x, y, hcf );

       lcm = (x * y) / hcf;

       printf( "LCM of %d & %d : %d\n", x, y, lcm );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4894.jpg)

______________  ****  ______________

Program No. - 144 :

Program to convert Binary number to Decimal number.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       long i, n, r, num = 0;

       system( "cls" );

       printf( "Enter a Binary Number : " );

       scanf( "%d", &n );

       i = 0;

       while( n != 0 ) 

       {

              r = n % 10;

              num = num + ( r * pow( 2, i ) );

              n = n / 10;

              i++;

       }

       printf( "\nDecimal Equivalent : %d\n", num ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4895.jpg)

______________  ****  ______________

Program No. - 145 :

Program to convert Octal number to Decimal number.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       long i, n, r, num = 0;

       system( "cls" );

       printf( "Enter a Octal Number : " );

       scanf( "%d", &n );

       i = 0;

       while( n != 0 ) 

       {

              r = n % 10;

              num = num + ( r * pow( 8, i ) );

              n = n / 10;

              i++;

       }

       printf( "\nDecimal Equivalent : %d\n", num ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4896.jpg)

______________  ****  ______________

Program No. - 146 :

Program to convert Decimal number to Binary number.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       long i, n, r, num = 0;

       system( "cls" );

       printf( "Enter a Decimal Number : " );

       scanf( "%ld", &n );

       i = 0;

       while( n > 0 ) 

       {

              r = n % 2;          ​

              num = num + ( r * pow( 10, i ) );

              n = n / 2;

              i++;

       }

       printf( "\nBinary Equivalent : %ld\n", num );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4897.jpg)

______________  ****  ______________

Program No. - 147 :

Program to convert Decimal number to Octal number.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       long i, n, r, num = 0;

       system( "cls" );

       printf( "Enter a Decimal Number : " );

       scanf( "%d", &n );

       i = 0;

       while( n != 0 ) 

       {

              r = n % 8;

              num = num + ( r * pow( 10, i ) );

              n = n / 8;

              i++;

       }

       printf( "\nOctal Equivalent : %d\n", num );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4898.jpg)

______________  ****  ______________

Program No. - 148 :

Program to Display Multiplication Table of given number.

Code :

#include <stdio.h>

int  main()

{

       int  n, i, a;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       for( i=1 ; i<=10 ; i++ )

       {

              a = i * n;

              printf( "\n%2d * %2d = %2d", n, i, a );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc4899.jpg)

______________  ****  ______________

Program No. - 149 :

Program to Display Multiplication Table from 1 to 10.

Code :

#include <stdio.h>

int  main()

{

       int  i, j, a;

       system( "cls" );

       printf( " No|" );

       for( i=1 ; i<=10 ; i++ )

       {

              printf( " %3d", i );

       }

       printf( "\n________________________________\n" );

       for( i=1 ; i<=10 ; i++ )

       {

              printf( "%2d |", i );

              for( j=1 ; j<=10 ; j++ )

              {

                     a = i * j;

                     printf( " %3d", a );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489A.jpg)

______________  ****  ______________

Program No. - 150 :

Program to find Largest value in “n” number of given numbers.

Code :

#include <stdio.h>

int  main()

{

       int i, n, x, large = −2147483648;

       system( "cls" );

       printf( "Enter No. of Values : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ ) 

       {

              printf( "Enter Number-%d : ", i+1 );

              scanf( "%d", &x );

              if( x > large )

                     large = x;

       }

       printf( "\nLargest Value : %d\n", large );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489B.jpg)

______________  ****  ______________

Program No. - 151 :

Program to find Largest value & Smallest value in “n” number of given numbers.

Code :

#include <stdio.h>

int  main()

{

       int i, n, x, large = −2147483648, small = 2147483647;

       system( "cls" );

       printf( "Enter No. of Values : " );

       scanf( "%d", &n );​

       for( i=0 ; i<n ; i++ ) 

       {

              printf( "Enter Number-%d : ", i+1 );

              scanf( "%d", &x );

              if( x > large )

                     large = x;

              if( x < small )

                     small = x;

       }

       printf( "\nLargest Value : %d\n", large );

       printf( "Smallest Value : %d\n", small );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489C.jpg)

______________  ****  ______________

Program No. - 152 :

Program to display all Leap years between two given years.

Code :

#include <stdio.h>

int main()

{

       int y1, y2;

       system( "cls" );

       printf( "Enter Year Range : " );

       scanf( "%d %d", &y1, &y2 );

       while( y1 <= y2 )

       {

              if( (y1 % 400 == 0) || ( y1 % 100 != 0 && y1 % 4 == 0 ))

              {

                     printf( "\nLeap Year : %d", y1 );

              }

              y1++;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489D.jpg)

______________  ****  ______________

Program No. - 153 :

Program to show Cube Table of 1 to 10.

Code :

#include <stdio.h>

int main()

{

       int pow = 1;

       int num = 1;

       system( "cls" );

       printf( "1 to 10 Cube Table : \n" );

       while( pow <= 1000 )

       {

              pow = num * num * num;

              printf( "%3d :%5d\n", num, pow );

              num++;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489E.jpg)

______________  ****  ______________

Program No. - 154 :

Program to calculate Squares of given values.

Code :

#include <stdio.h>

int main()

{

       char  another = 'y' ;

       int  num ;

       system( "cls" );

       while ( another == 'y' )

       {

              printf ( "Enter a number : " ) ;

              scanf ( "%d", &num ) ;

              printf ( "Square of %d : %d", num, (num * num) ) ;

              printf ( "\nWant to enter another number (y/n) : " ) ;

              scanf ( " %c", &another ) ;

       }

       printf( "\n"  );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489F.jpg)

______________  ****  ______________

Program No. - 155 :

Program to display all Pythogorus Triplets from 2 to N.

Code :

#include <stdio.h>

int main()

{

       int i, j, k;

       int num;

       system( "cls" );

       printf( "Enter Upper limit for Pythogorus Triplet : " );

       scanf( "%d", &num );

       for( i=2 ; i<=num ; i++ )

       {

              for( j=i ; j<=num ; j++ )

              {

                     for( k=j ; k<=num ; k++ )

                     {

                            if( (i*i)+(j*j) == (k*k) )

                            {

                                   printf( "\nSq(%d) + Sq(%d)\t= sq(%d)",  i, j, k );

                            }

                     }

               }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489G.jpg)

______________  ****  ______________

Program No. - 156 :

Program to explain break statement.

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       for( i=1 ; i<=10 ; i++ )

       {

              if( i == 5 )

              {

                     break;

              }

              printf( "  %d", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489H.jpg)

______________  ****  ______________

Program No. - 157 :

Program to explain continue statement.

Code :

#include <stdio.h>

int  main()

{

       int  i;

       system( "cls" );

       for( i=1 ; i<=10 ; i++ )

       {

              if( i == 5 )

              {

                     continue;

              }

              printf( "  %d", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489J.jpg)

______________  ****  ______________

Program No. - 158 :

Program to explain the break and continue Jump statements.

Code :

#include <stdio.h>

int  main()

{

       int i;

       system( "cls" );

       for( i=1 ; i<=20 ; i++ )

       {

              if( i % 2 )

                     continue;   ​​/* start next iteration */

              else if ( i == 16 )

                     break;      ​​/* end the loop */

              printf( "%d  ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489K.jpg)

______________  ****  ______________

Program No. - 159 :

Program to explain goto statement with forward jump.

Code :

#include <stdio.h>

int  main()

{

       int a = 10;

       system( "cls" );

       printf( "AAA\n" );

       printf( "BBB\n" );

       if( a == 10 )

       {

              goto  LBL;

       }

       printf( "CCC\n" );

       printf( "DDD\n" );

       LBL:

       printf( "EEE\n" );

       printf( "FFF\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489M.jpg)

______________  ****  ______________

Program No. - 160 :

Program to explain goto statement with backward jump.

Code :

#include <stdio.h>

int  main()

{

       int i;

       system( "cls" );

       i = 1;

       LABEL1:

       printf( "  %d", i );

       i++;

       if( i <= 10 )

       {

              goto  LABEL1;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489N.jpg)

______________  ****  ______________

Program No. - 161 :

Program to display Even numbers and using continue.

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       for( i=1 ; i<= (2 * n) ; i++ )

       {

              if( i % 2 != 0 )

              {

                     continue;

              }

              printf( "  %d", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489P.jpg)

______________  ****  ______________

Program No. - 162 :

Program to use continue statement.

Code :

#include <stdio.h>

int  main()

{

       long dividend, divisor;

       char ch;

       system( "cls" );

       do

       {

              printf( "Enter Dividend : " );

              scanf( "%ld", &dividend );

              printf( "Enter Divisor : " );

              scanf( "%ld", &divisor );

              if( divisor == 0 )

              {

                     printf( "\nILLEGAL Divisor.\n" );

                     continue;

              }

              printf( "\nQuotient = %d\n", ( dividend / divisor ) );

              printf( "Remainder = %d\n", ( dividend % divisor ) );

              printf( "Do another ? (y/n) : " );​

              fflush( stdin );

              scanf( "%c", &ch );

       }while( ch != 'n' );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489R.jpg)

______________  ****  ______________

Program No. - 163 :

Program to use exit() function to check whether the given Number is Prime Number or Not.

Code :

#include <stdlib.h>​​/*  #include <process.h>​*/

#include <stdio.h>

int  main()

{

       int n, i;

       system( "cls" );

       printf( "Enter the Number : " );

       scanf( "%d", &n );

       for( i=2 ; i<=n/2 ; i++ )

       {

              if( n % i == 0 )

              {

                     printf( "\n%d is not a Prime Number.\n", n );

                     system( "pause" );

                     exit( 0 );

              }

       }

       printf( "\n%d is a Prime Number.\n", n );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489S.jpg)![](image_rsrc489T.jpg)

______________  ****  ______________

Program No. - 164 :

Program to display all Perfect number between 1 to 100.

Code :

#include <stdio.h>

int main()

{

       int  n, i, sum;

       system( "cls" );

       printf( "Perfect Numbers between 1 to 100 : \n" );

       for( n=1 ; n<=100 ; n++ )

       {

              sum = 0;

              i = 1;

              while( i <= (n/2) )

              {

                     if( n % i == 0 )

                            sum = sum + i;

                     i++;

              }

              if( sum == n )

                     printf( "Perfect Number : %d\n", n );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489U.jpg)

______________  ****  ______________

Program No. - 165 :

Program to display all Prime numbers from 2 to 100 and count it.

Code :

#include <stdio.h>

#include <math.h>

int main()

{

       int i, x, n, r, flag, cnt = 0;

       system( "cls" );

       printf( "Prime Numbers 2 to 100 : \n" );

       for( n=2 ; n<=100 ; n++ )

       {

              flag = 1;

              for( i=2 ; i<=sqrt(n) ; i++ )

              {

                     if( n % i == 0 )

                     {

                            flag = 0;

                            break;

                     }

              }

              if( flag == 1 )

              {

                     printf( "  %2d", n );

                     cnt++;

                     if( cnt % 10 == 0)

                            printf( "\n" );

              }​

       }

       printf( "\nTotal Prime Numbers : %d\n", cnt );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489V.jpg)

______________  ****  ______________

Program No. - 166 :

Program to display all three digits Armstrong Numbers and count it.

Code :

#include <stdio.h>

int main()

{

       int i, x, n, r, s, cnt=0;

       system( "cls" );

       printf( "Armstrong Numbers 100 to 999 : \n" );

       for( i=100 ; i<=999 ; i++ )

       {

              x = n = i;

              s = 0;

              while( n != 0 )

              {

                     r = n % 10;

                     s = s + ( r * r * r );

                     n = n / 10;

              }

              if( s == x )

              {

                     printf( "  %d", x );

                     cnt++;

              }

       }

       printf( "\nTotal Armstrong Numbers : %d\n", cnt );

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc489W.jpg)

______________  ****  ______________

Program No. - 167 :

Program to display all Strong Numbers between 1 and 100000.

Code :

#include <stdio.h>

int main()

{

       int n, r, sum, f, i, j;

       system( "cls" );

       for( i=1 ; i<=100000 ; i++ )

       {

              n = i;

              sum = 0;​

              while( n > 0 )

              {

                     r = n % 10;

                     n = n / 10;

                     f = 1;

                     for( j=1 ; j<=r ; j++ )

                     {

                            f = f * j;

                     }

                     sum = sum + f;

              }

              if( sum == i )

                     printf( "%d is a Strong Number.\n", i );

       }

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc489X.jpg)

______________  ****  ______________

Program No. - 168 :

Program to display Truth Table for Boolean expression xy+z.

Code :

#include <stdio.h>

int main()

{

       int x, y, z;

       system( "cls" );

       printf( "x\ty\tz\txy+z\n" );

       printf( "___________________________" );

       for( x=0 ; x<=1 ; x++ )

       {

              for( y=0 ; y<=1 ; y++ )

              {

                     for( z=0 ; z<=1 ; z++ )

                     {

                            if( ((x==1) && (y==1)) || (y==1) )

                                   printf( "\n%d\t%d\t%d\t1", x, y, z );

                            else

                                   printf( "\n%d\t%d\t%d\t0", x, y, z );

                     }

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489Y.jpg)

______________  ****  ______________

Program No. - 169 :

Program to calculate Lucky Number from Date of Birth.

Code :

#include <stdio.h>

int main()

{

       int  num, sum, r;

       system( "cls" );

       printf( "Enter Date of Birth (DDMMYYYY) : " );​

       scanf( "%d", &num );

       while( num > 10 )

       {

              sum = 0;

              while( num != 0 )

              {

                     r = num % 10;

                     sum += r;

                     num = num / 10;

              }

              if( sum > 10 )

                     num = sum;

       }

       printf( "\nYour Lucky Number : %d\n", sum );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc489Z.jpg)

______________  ****  ______________

Program No. - 170 :

Program to find Prime Factors of given number.

Code :

#include <stdio.h>

int main()

{

       int num, i=1, j, cnt;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &num );

       printf( "\nPrime Factors of %d are : ", num );

       while( i <= num )

       {

              cnt = 0;

              if( num % i == 0 )

              {

                     j = 2;

                     while( j <= i )

                     {

                            if( i % j == 0 )

                                   cnt++;

                            j++;

                     }

                     if( cnt == 1 )

                            printf( "%3d", i );

              }

              i++;

       }​

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A0.jpg)![](image_rsrc48A1.jpg)

______________  ****  ______________

Chapter – 6

Series

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 171 :

Program to display first n natural numbers.

​1  2  3  4  5 ...  ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              printf( "%d  ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A2.jpg)

______________  ****  ______________

Program No. - 172 :

Program to find sum of first n natural numbers.

​1 + 2 + 3 + ... ... + n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0;

       for( i=1 ; i<=n ; i++ )

       {

              s = s + i;

       }

       printf( "\nSum of Series = %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A3.jpg)

______________  ****  ______________

Program No. - 173 :

Program to find sum of first n natural numbers.

​1 + 2 + 3 + ... ... + n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       s = 0;

       for( i=1 ; i<=n ; i++ )

       {

              if( i == 1 )

                     printf( "%d", i );

              else

                     printf( " + %d", i );

              s = s + i;

       }

       printf( " = %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A4.jpg)

______________  ****  ______________

Program No. - 174 :

Program to display first n terms of given series :

​2  4  6  8  ...  ... n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=2 ; i<=(2*n) ; i+=2 )

       {

              printf( "%d ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A5.jpg)

______________  ****  ______________

Program No. - 175 :

Program to display first n terms of given series :

​2  4  6  8  ...  ... n terms

Code :

#include <stdio.h>

int main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=(2*n) ; i++ )

       {

              if( i % 2 == 0 )

              {

                     printf( "%d  ", i );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A6.jpg)

______________  ****  ______________

Program No. - 176 :

Program to display first n terms of given series :

​2  4  6  8  ...  ... n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              t = 2 * i;

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A7.jpg)

______________  ****  ______________

Program No. - 177 :

Program to display first n terms of given series :

1   3   5   7  ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );​

       printf( "\n" );

       for( i=1 ; i<=(2*n) ; i+=2 )

       {

              printf( "%d  ", i );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A8.jpg)

______________  ****  ______________

Program No. - 178 :

Program to display first n terms of given series :

1   3   5   7  ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=(2*n) ; i++ )

       {

              if( i % 2 == 1 )​​/*  if( i % 2 != 0 )   */

              {

                     printf( "%d  ", i );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48A9.jpg)

______________  ****  ______________

Program No. - 179 :

Program to display first n terms of given series :

1   3   5   7  ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              t = 2 * i − 1;

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AA.jpg)

______________  ****  ______________

Program No. - 180 :

Program to display first n terms of given series :

​−1    2   −3    4    −5  ... ...  n terms.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              t = i * pow( (−1), i );

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AB.jpg)

______________  ****  ______________

Program No. - 181 :

Program to display first n terms of given series :

​1    −2    3    −4    5  ... ...  n terms.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              t = i * pow( (−1), (i + 1) );

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AC.jpg)

______________  ****  ______________

Program No. - 182 :

Program to find the sum of all Even values & all Odd values in “n” number of terms of natural number series.

Code :

#include <stdio.h>

int  main()

{

       int n, i, esum = 0, osum = 00;

       system( "cls" );

       printf( "Enter No. of Terms : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ ) 

       {

              printf( " %d", i );

              if( i % 2 == 0 )

                     esum += i;

              else

                     osum += i;

       }

       printf( "\nSum of Even Numbers : %d\n", esum );

       printf( "Sum of Odd Numbers  : %d\n", osum );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AD.jpg)

______________  ****  ______________

Program No. - 183 :

Program to display the squares of “n” number of terms of natural number series and also find the sum.

​1   4   9   16   25   36  …  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, t, s, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0;

       for( i=1 ; i<=n ; i++ ) 

       {

              t = i * i;

              printf( " %d", t );

              s = s + t;

       }   

       printf( "\nSum of Series : %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AE.jpg)

______________  ****  ______________

Program No. - 184 :

Program to display “n” terms of given series.

​1   2   4   8   16   32  …  n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, t, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ ) 

       {

              t = pow( 2, i );

              printf( " %d", t );

       }   

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AF.jpg)

______________  ****  ______________

Program No. - 185 :

Program to find the sum of “n” number of terms of Sine series.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, j, n, f;

       float x, t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "Enter Degree for Sine Series : " );

       scanf( "%f", &x );

       x = x * ( 3.14159 / 180 );

       s = 0;

       for( i=1 ; i<=n ; i++ ) 

       {

              f = 1;

              for( j=1 ; j<=(2*i-1) ; j++ ) 

              {

                     f = f * j;

              }

              t = ( pow( x, (2*i−1) ) * pow( −1, (i+1) ) ) / f;

              s = s + t;

       }   ​

       printf( "\nSum of Sine Series : %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AG.jpg)

______________  ****  ______________

Program No. - 186 :

Program to find sum of “n” number of terms of Cosine series.

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, j, n, f;

       float x, t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "Enter Degree for Cosine Series : " );

       scanf( "%f", &x );​

       x = x * ( 3.14159 / 180 );

       s = 1;

       for( i=1 ; i<n ; i++ ) 

       {

              f = 1;

              for( j=1 ; j<=(2*i) ; j++ ) 

              {

                     f = f * j;

              }

              t = ( pow( x, (2*i) ) * pow( −1, i ) ) / f;

              s = s + t;

       }   ​

       printf( "\nSum of Cosine Series : %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AH.jpg)

______________  ****  ______________

Program No. - 187 :

Program to find the sum first n terms of given series :

​x + 2x2 + 3x3 + 4x4 + ... ...  n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, n, x, t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "Enter Value of x : " );

       scanf( "%d", &x );

       s = 0;

       for( i=1 ; i<=n ; i++ )

       {

              t = i * pow( x, i );

              s = s + t;

       }

       printf( "\nSum of Series = %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AJ.jpg)

______________  ****  ______________

Program No. - 188 :

Program to find the sum first n terms of given series :

​1 + 1/2 + 1/3 + 1/4 + ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       float t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0.0;

       for( i=1 ; i<=n ; i++ )

       {

              t = 1.0 / i;

              s = s + t;

       }

       printf( "\nSum of Series = %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AK.jpg)

______________  ****  ______________

Program No. - 189 :

Program to find the sum first n terms of given series :

​1/2 + 2/3 + 3/4 + ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       float t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0.0;

       for( i=1 ; i<=n ; i++ )

       {

              t = (float) i / ( i + 1 );

              s = s + t;

       }

       printf( "\nSum of Series = %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AM.jpg)

______________  ****  ______________

Program No. - 190 :

Program to find the sum first n terms of given series :

​1/(2*3) + 2/(3*4) + 3/(4*5) + ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n;

       float t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0.0;

       for( i=1 ; i<=n ; i++ )

       {

              t = (float) i / ( ( i + 1 ) * ( i + 2 ) );

              s = s + t;

       }

       printf( "\nSum of Series = %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AN.jpg)

______________  ****  ______________

Program No. - 191 :

Program to find the sum first n terms of given series :

​1/1! + 1/2! + 1/3! + ... ...  n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, j, f;

       float t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0.0;

       for( i=1 ; i<=n ; i++ )

       {

              f = 1;

              for( j=1 ; j<=i ; j++ )

              {

                     f = f * j;

              }

              t = 1.0 / f;

              s = s + t;

       }

       printf( "\nSum of Series = %f\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AP.jpg)

______________  ****  ______________

Program No. - 192 :

Program to find the sum first n terms of given series :

−(2x1)/1! + (3x2)/2! − (4x3)/3! + ... ...  n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, n, x, j, f;

       float t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( "Enter Value of x : " );

       scanf( "%d", &x );

       s = 0.0;

       for( i=1 ; i<=n ; i++ )

       {

              f = 1;

              for( j=1 ; j<=i ; j++ )

              {

                     f = f * j;

              }

              t = ( ( i+1 ) * pow( x, i ) * pow( −1, i ) ) / f;

              s = s + t;

       }

       printf( "\nSum of Series = %f\n", s );​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AR.jpg)

______________  ****  ______________

Program No. - 193 :

Program to find the sum first n terms of given series :

​1 + (1+2) + (1+2+3) + ... ... + n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, j, t, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       s = 0;

       for( i=1 ; i<=n ; i++ )

       {

              t = 0;

              for( j=1 ; j<=i ; j++ )

              {

                     t = t + j;

              }

              s = s + t;

       }

       printf( "\nSum of Series = %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AS.jpg)

______________  ****  ______________

Program No. - 194 :

Program to display first n terms of Fibonacci Series.

0    1    1    2    3    5 ... ... n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, a, b, c;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       a = 0;

       b = 1;

       printf( "%d  %d  ", a, b );

       for( i=1 ; i<=(n−2) ; i++ )

       {

              c = a + b;

              printf( "%d  ", c );

              a = b;

              b = c;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AT.jpg)

______________  ****  ______________

Program No. - 195 :

Program to display first n terms of Lucas Series.

1    1    1    3    5    9 ... ... n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, a, b, c, d;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       a = 1;

       b = 1;

       c = 1;

       printf( "%d  %d  %d  ", a, b, c );

       for( i=1 ; i<=(n−3) ; i++ )

       {

              d = a + b + c;

              printf( "%d  ", d );

              a = b;

              b = c;

              c = d;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AU.jpg)

______________  ****  ______________

Program No. - 196 :

Program to display first n terms of following Series.

1     11     111     1111  ... ... n terms

Code :

#include <stdio.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       t = 0;

       for( i=0 ; i<n ; i++ )

       {

              t = t * 10 + 1;

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AV.jpg)

______________  ****  ______________

Program No. - 197 :

Program to display first n terms of following Series.

1     11     111     1111  ... ... n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int i, n, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       t = 0;

       for( i=0 ; i<n ; i++ )

       {

              t = t + pow( 10, i );

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AW.jpg)

______________  ****  ______________

Program No. - 198 :

Program to display first n terms of given Series.

−1     4   −7     10  ... ... n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int  i, t, n;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ )

       {

              t = ( 3 * i + 1 ) * pow( (-1), ( i + 1 ) );

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AX.jpg)

______________  ****  ______________

Program No. - 199 :

Program to find sum of first n terms of given series :

​x − 2x2 + 3x3 −  ... ...  n terms

Code :

#include <stdio.h>

#include <math.h>

int  main()

{

       int n, i, x, t, sum;

       system( “cls” );

       printf( " Enter Number of Terms : " );

       scanf( "%d", &n );

       printf( " Enter a Value x : " );

       scanf( "%d", &x );

       sum = 0;

       for( i=1 ; i<=n ; i++ )

       {

              t = i * pow( (−1), ( i + 1 ) ) * pow( x, i );

              sum = sum + t;

       }

       printf( "\n Sum of Series = %d" , sum );

       system( “pause” );

       return 0;

}

Output :

![](image_rsrc48AY.jpg)

______________  ****  ______________

Program No. - 200 :

Program to display first n terms of given Series.

1     4     9     16  ... ... n terms

Code :

#include <stdio.h>

int  main()

{

       int n, i, t;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              t = ( i * i );

              printf( "%d  ", t );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48AZ.jpg)

______________  ****  ______________

Chapter – 7

Patterns

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 201 :

Program to display the following design pattern :

​1

​1 2

​1 2 3

​1 2 3 4

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B0.jpg)

______________  ****  ______________

Program No. - 202 :

Program to display the following design pattern :

​1

​2 2

​3 3 3

​4 4 4 4

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", i );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B1.jpg)

______________  ****  ______________

Program No. - 203 :

Program to display the following design pattern :

​*

​* *

​* * *

​* * * *

Code :

#include <stdio.h>

#include <conio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " *" );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B2.jpg)

______________  ****  ______________

Program No. - 204 :

Program to display the following design pattern :

​A

​A B

​A B C

​A B C D

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %c", ( j + 64 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B3.jpg)

______________  ****  ______________

Program No. - 205 :

Program to display the following design pattern :

​a

​a b

​a b c

​a b c d

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %c", ( j + 96 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B4.jpg)

______________  ****  ______________

Program No. - 206 :

Program to display the following design pattern :

​A

​B B

​C C C

​D D D D

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %c", ( i + 64 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B5.jpg)

______________  ****  ______________

Program No. - 207 :

Program to display the following design pattern :

​a

​b b

​c c c

​d d d d

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %c", ( i + 96 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B6.jpg)

______________  ****  ______________

Program No. - 208 :

Program to display the following design pattern :

​             1

​         1 2

​     1 2 3

​ 1 2 3 4

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              printf( "\n" );

       }

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc48B7.jpg)

______________  ****  ______________

Program No. - 209 :

Program to display the following design pattern :

​             1

​         1 2 1

​     1 2 3 2 1

​ 1 2 3 4 3 2 1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     printf( " %d", l );

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B8.jpg)

______________  ****  ______________

Program No. - 210 :

Program to display the following design pattern :

             1

         1 2 1

     1 2 3 2 1

 1 2 3 4 3 2 1

     1 2 3 2 1

         1 2 1

             1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              for( l=i−1 ; l>=1 ; l−− )​

              {

                     printf( " %d", l );

              }

              printf( "\n" );

       }

       for( i=n−1 ; i>=1 ; i−− )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     printf( " %d", l );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48B9.jpg)

______________  ****  ______________

Program No. - 211 :

Program to display the following design pattern :

          1

       1    1

    1          1

 1                1

    1          1

       1    1

           1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 )

                            printf( " %d", j );

                     else​

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }

              printf( "\n" );

       }

       for( i=n−1 ; i>=1 ; i−− )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BA.jpg)

______________  ****  ______________

Program No. - 212 :

Program to display the following design pattern :

          1

       1    1

    1          1

 1       4       1

    1          1

       1    1

          1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 || j == n )

                            printf( " %d", j );

                     else​

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }

              printf( "\n" );

       }

       for( i=n−1 ; i>=1 ; i−− )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BB.jpg)

______________  ****  ______________

Program No. - 213 :

Program to display the following design pattern :

            1

        1     1

     1            1

 1 2 3 4 3 2 1

     1            1

        1      1

            1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 || i == n )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 || i == n )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }

              printf( "\n" );

       }

       for( i=n−1 ; i>=1 ; i−− )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BC.jpg)

______________  ****  ______________

Program No. - 214 :

Program to display the following design pattern :

           1

       1 2 1

    1    3    1

 1       4       1

    1    3    1

       1 2 1

           1

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, l, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 || j == i )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " );​

              }

              printf( "\n" );

       }

       for( i=n−1 ; i>=1 ; i−− )

       {

              for( k=1 ; k<=(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     if( j == 1 || j == i )

                            printf( " %d", j );

                     else

                            printf( "  " );

              }

              for( l=i−1 ; l>=1 ; l−− )

              {

                     if( l == 1 )

                            printf( " %d", l );

                     else

                            printf( "  " ); ​

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BD.jpg)

______________  ****  ______________

Program No. - 215 :

Program to display the following design pattern (Floyd’s Triangle) :

​1

​2 3

​4 5 6

​7 8 9 10

Code :

#include <stdio.h>

int  main()

{

       int i, j, n, a;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       a = 1;

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( "%3d", a );

                     a++;

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BE.jpg)

______________  ****  ______________

Program No. - 216 :

Program to display the following design pattern :

​1

​0 0

​1 1 1

​0 0 0 0

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     if( i % 2 == 0 )

                            printf( "%2d", 0 );

                     else

                            printf( "%2d", 1 );​

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BF.jpg)

______________  ****  ______________

Program No. - 217 :

Program to display the following design pattern :

​1

​0 0

​1 1 1

​0 0 0 0

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( "%2d", ( i % 2 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BG.jpg)

______________  ****  ______________

Program No. - 218 :

Program to display the following design pattern :

​1

​1 0

​1 0 1

​1 0 1 0

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     if( j % 2 == 0 )

                            printf( "%2d", 0 );

                     else

                            printf( "%2d", 1 );​

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BH.jpg)

______________  ****  ______________

Program No. - 219 :

Program to display the following design pattern :

​1

​1 0

​1 0 1

​1 0 1 0

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=i ; j++ )

              {

                     printf( "%2d", ( j % 2 ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BJ.jpg)

______________  ****  ______________

Program No. - 220 :

Program to display the following design pattern :

​*   *   *   *   *

​*   *   *   *   *

​*   *   *   *   *

​*   *   *   *   *

​*   *   *   *   *

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=n ; j++ )

              {

                     printf( " *" );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BK.jpg)

______________  ****  ______________

Program No. - 221 :

Program to display the following design pattern :

​*   *   *   *   *

​*                 *

​*                 *

​*                 *

​*   *   *   *   *

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=n ; j++ )

              {

                     if( i == 1 || i == n || j == 1 || j == n )

                            printf( " *" );

                     else

                            printf( "  " );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BM.jpg)

______________  ****  ______________

Program No. - 222 :

Program to display the following design pattern :

​*   *   *   *   *

​*   *       *    *

​*        *        *

​*   *        *   *

​*   *   *   *   *

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=n ; j++ )

              {

                     if( i == 1 || i == n || j == 1 || j == n || i == j ||

                                   ( i+j ) == (n+1) )

                            printf( " *" );

                     else

                            printf( "  " );

              }

              printf( "\n" );

       }       ​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BN.jpg)

______________  ****  ______________

Program No. - 223 :

Program to display the following design pattern :

​               1

​           1 2 3

​       1 2 3 4 5

​   1 2 3 4 5 6 7

Code :

#include <stdio.h>

int  main()

{

       int i, j, k, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=1 ; i<2*n ; i+=2 )

       {

              for( k=1 ; k<=(2*n−i) ; k++ )

              {

                     printf( " " );

              }

              for( j=1 ; j<=i ; j++ )

              {

                     printf( " %d", j );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BP.jpg)

______________  ****  ______________

Program No. - 224 :

Program to display the following design pattern :

​C

​C O

​C O M

​C O M P

​C O M P U

​C O M P U T

​C O M P U T E

​C O M P U T E R

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       int i, j, k;

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%s", str );

       k = strlen( str );

       for( i=0 ; i< k ; i++ )

       {

              for( j=0 ; j <= i ; j++ )

              {

                     printf( " %c", str[ j ] );

              }​

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BR.jpg)

______________  ****  ______________

Program No. - 225 :

Program to display the following design pattern :

​ C O M P U T E R

​     O M P U T E R

​          M P U T E R

​               P U T E R

                               U T E R

​                       T E R

​                           E R

​                               R

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       int i, j, k, l;

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%s", str );

       l = strlen( str );

       for( i=0 ; i< l ; i++ )

       {

              for( k=0 ; k <i ; k++ )

              {

                     printf( "  " );

              }

              for( j=i ; j < l ; j++ )​

              {

                     printf( " %c", str[ j ] );

               }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BS.jpg)

______________  ****  ______________

Program No. - 226 :

Program to display the following design pattern :

               I

           I N I

       I N D N I

   I N D I D N I

I N D I A I D N I

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       int i, j, k, l, len;

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%s", str );

       len = strlen( str );

       for( i=0 ; i<len ; i++ )

       {

              for( k=0 ; k<( len – i ) ; k++ )

              {

                     printf( "  " );

              }

              for( j=0 ; j<i ; j++ )

              {

                     printf( " %c", str[ j ] );

              }​

              for( l=i; l>=0 ; l−− )

              {

                     printf( " %c", str[ l ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BT.jpg)

______________  ****  ______________

Program No. - 227 :

Program to display the Pascal Triangle :

​                       1

​                    1    1

​                 1    2    1

​              1    3    3   1

Code :

#include <stdio.h>

int  main()

{

       int n, i, j, k, t;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ )

       {

              for( k=0 ; k<(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=0 ; j<=i ; j++ )

              {

                     if( j == 0 || i == 0 )

                            t = 1;

                     else

                            t =  ( t * ( i − j + 1 ) ) / j ;

                     printf( "   %d", t );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BU.jpg)

______________  ****  ______________

Program No. - 228 :

Program to display following pattern using break :

​1

​2 4

​3 6 9

​4 8 12 16

Code :

#include <stdio.h>

int  main()

{

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       printf( "\n" );

       for( i=1 ; i<=n ; i++ )

       {

              for( j=1 ; j<=n ; j++ )

              {

                     printf( "%3d", ( i * j ) );

                     if( i == j )

                            break;

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BV.jpg)

______________  ****  ______________

Program No. - 229 :

Program to explain use of break statement with following pattern :

​1

​1 2

​1 2 3

​1 2 3 4

​1 2 3 4 5

Code :

#include <stdio.h>

int main()

{

       int  i, j;

       system( "cls" );

       for( i=1 ; i<=5 ; i++ )

       {

              for( j=1 ; j<=10 ; j++ )

              {

                     printf ( " %d", j ) ;

                     if ( i == j )

                            break ;

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BW.jpg)

______________  ****  ______________

Program No. - 230 :

Program to explain use of break statement with following pattern :

​1

​1 2

​1 2 3

​1 2 3 4

​1 2 3 4 5

Code :

#include <stdio.h>

int main()

{

       int  i, j;

       system( "cls" );

       for( i=1 ; i<=10 ; i++ )

       {

              for( j=1 ; j<=10 ; j++ )

               {

                     printf ( " %d", j ) ;

                     if ( i == j )

                            break ;

              }

              printf( "\n" );

              if( i == 5 )

                     break;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BX.jpg)

______________  ****  ______________

Program No. - 231 :

Program to explain use of break statement with following pattern :

​1 2 3 4 5

​1 2 3 4

​1 2 3

​1 2

​1

Code :

#include <stdio.h>

int main()

{

       int i, j;

       system( "cls" );

       for( i=1 ; i<=5 ; i++ )

       {

              for( j=1 ; j<=5 ; j++ )

              {

                     if ( i > j )

                            continue ;

                     printf( " %d", j );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BY.jpg)

______________  ****  ______________

Chapter – 8

Arrays

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 232 :

Program to use Simple Array.

Code :

#include <stdio.h>

int  main()

{

       int  num[5];

       int  i;

       system( "cls" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Enter value %d : ", (i + 1) );

              scanf( "%d", &num[ i ] );

       }

       printf( "\nThe elements are : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d",  num[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48BZ.jpg)

______________  ****  ______________

Program No. - 233 :

Program to explain Initialization of an Array.

Code :

#include <stdio.h>

int  main()

{

       int  i;

       int  num[10] = { 10, 20, 30, 40, 50, 60, 70, 80, 90, 100 };

       system( "cls" );

       for( i=0 ; i<10 ; i++ )

       {

              printf( " %d : %d\n", (i + 1), num[ i ] );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C0.jpg)

______________  ****  ______________

Program No. - 234 :

Program to find Average of an Array.

Code :

#include <stdio.h>

int  main()

{

       float a[5];

       float s, avg;

       int i;

       system( "cls" );

       for ( i=0 ; i<5 ; i++ )

       {

              printf( "Enter Value : " );

              scanf( "%f", &a[ i ] );

       }

       s = 0.0;

       for( i=0 ; i<5 ; i++ )

       {

              s = s + a[ i ];

       }

       avg = s / 5;

       printf( "\nSum     : %f\n", s );

       printf( "Average : %f\n", avg );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C1.jpg)

______________  ****  ______________

Program No. - 235 :

Program to twice the value of all elements of Array.

Code :

#include <stdio.h>

int main()

{

       int ar[50], n,i;

       system( "cls" );

       printf(​"Enter No. of Array Elements : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ )

       {

              printf( "Enter [%d] element : ", i+1 );

              scanf( "%d", &ar[ i ] );

       }

       printf( "\nArray with doubled elements : " );

       for( i=0 ; i<n ; i++ )

       {

              ar[ i ] *= 2;

              printf( "%d  ", ar[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C2.jpg)

______________  ****  ______________

Program No. - 236 :

Program to find Maximum and Minimum of Array elements.

Code :

#include <stdio.h>

int  main()

{

       int  i, arr[5], min, max;

       system( "cls" );

       printf( "Enter Five Numbers : " );

       for( i=0 ; i<5 ; i++ )

       {

              scanf( "%d", &arr[ i ] );

       }

       min = arr[0];

       max = arr[0];

       for( i=1 ; i<5 ; i++ )

       {

              if( min > arr[ i ] )​

                     min = arr[ i ];

              if( max < arr[ i ] )​

                     max = arr[ i ];

       }

       printf( "\nMinimum value = %d\n", min );

       printf( "Maximum value = %d\n",  max );

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc48C3.jpg)

______________  ****  ______________

Program No. - 237 :

Program to search an element in array using Linear Search.

Code :

#include <stdio.h>

int  main()

{

       int  num[10], i, pos = −1, value;

       system( "cls" );

       printf( "Enter Ten Numbers : " );

       for( i=0 ; i<10 ; i++ )

       {

              scanf( "%d", &num[ i ] );

       }

       printf( "Enter the number to be searched : " );

       scanf( "%d", &value );

       for( i=0 ; i<10 ; i++ )

       {

              if( value == num[ i ] )

              {

                     pos = i + 1;

                     break;

              }

       }

       if( pos == −1 )             

              printf( "\nThe element %d not found.\n", value );​

       else

              printf( "\nThe position of %d : %d\n", value, pos );

​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C4.jpg)![](image_rsrc48C5.jpg)

______________  ****  ______________

Program No. - 238 :

Program to search an element in array using Binary Search.

Code :

#include <stdio.h>

int  main()

{

       int num[10], i, beg, end, mid, pos = -1, value;

       system( "cls" );

       printf( "Enter Ten Numbers in Ascending Order: " );

       for( i=0 ; i<10 ; i++ )

       {

              scanf( "%d", &num[ i ] );

       }

       printf( "Enter the number to be searched : " );

       scanf( "%d", &value );

       beg = 0;

       end = 10 − 1;

       while( beg<= end )

       {

              mid = ( beg + end ) / 2;

              if( value == num[mid] )

              {

                     pos = mid + 1;

                     break;

              }

              else if( value > num[mid] )​

                     beg = mid + 1;

              else

                     end = mid − 1;

       }

       if( pos == −1 )

              printf( "\nThe element %d not found.\n", value );

       else

              printf( "\nThe position of %d : %d\n" , value, pos );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C6.jpg)![](image_rsrc48C7.jpg)

______________  ****  ______________

Program No. - 239 :

Program to Reverse an Array elements without using Second Array.

Code :

#include <stdio.h>

int  main()

{

       int  arr[5];

       int  i, j, t;

       system( "cls" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Enter Value %d : ", (i + 1) );

              scanf( "%d", &arr[ i ] );

       }

       printf( "\nArray before reversing are : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", arr[ i ] );

       }

       for( i=0, j=5−1 ; i<5/2 ; i++, j−− )

       {

              t = arr[ i ];

              arr[ i ] = arr[ j ];

              arr[ j ] = t;

       }

       printf( "\nArray after reversing are  : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", arr[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C8.jpg)

______________  ****  ______________

Program No. - 240 :

Program to Sort elements of array using Bubble Sort.

Code :

#include <stdio.h>

int  main()

{

       int  i, j, t;

       int  n[ ] = { 30, 40, 50, 10, 20 };

       system( "cls" );

       printf( "Before Sorting :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       for( i=0 ; i<5-1 ; i++ )

       {

              for( j=0 ; j<5−1−i ; j++ )

              {

                     if( n[ j ] > n[ j+1] )

                     {

                            t = n[ j ];

                            n[ j ] = n[ j+1];

                            n[ j+1] = t;

                     }

              }

       }

       printf( "\n\nAfter Sorting  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48C9.jpg)

______________  ****  ______________

Program No. - 241 :

Program to Sort elements of array using Selection Sort.

Code :

#include <stdio.h>

int  main()

{

       int  i, j, small, pos, tmp ;

       int  n[ ] = { 30, 40, 50, 10, 20 };

       system( "cls" );

       printf( "Before Sorting :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       for( i=0 ; i<5 ; i++ )

       {

              small = n[ i ];

              pos = i;

              for( j=i+1 ; j<5 ; j++ )

              {

                     if( n[ j ] < small )

                     {

                            small = n[ j ];

                            pos = j;

                     }

              }

              tmp = n[ i ];

              n[ i ] = n[pos]; ​

              n[pos] = tmp;

        }

       printf( "\n\nAfter Sorting  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CA.jpg)

______________  ****  ______________

Program No. - 242 :

Program to Sort elements of array using Insertion Sort.

Code :

#include <stdio.h>

int  main()

{

       int  i, j, tmp;

       int  n[ ] = { 0, 30, 40, 50, 10, 20 };

       system( "cls" );

       printf( "Before Sorting :" );

       for( i=1 ; i<=5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       n[0] = −2147483648;

       for( i=1 ; i<=5 ; i++ )

       {

              tmp = n[ i ];

              j = i − 1;​

              while( tmp < n[ j ] )

              {

                     n[ j + 1 ] = n[ j ];

                     j−−;

              }

              n[ j + 1 ] = tmp;

       }

       printf( "\n\nAfter Sorting  :" );​

       for( i=1 ; i<=5 ; i++ )

       {

              printf( "  %d", n[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CB.jpg)

______________  ****  ______________

Program No. - 243 :

Program to create Fibonacci Series in an Array.

Code :

#include <stdio.h>

int  main()

{

       int  i, n, a[50];

       system( "cls" );

       printf( "Enter the Number of Terms : " );

       scanf( "%d", &n );

       a[0] = 0;

       a[1] = 1;

       for( i=2 ; i<n ; i++ )

       {

              a[ i ] = a[ i – 1 ] + a[ i – 2 ];

       }

       printf( "\n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "  %d", a[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CC.jpg)

______________  ****  ______________

Program No. - 244 :

Program to check whether the given number is Unique Number or Not.

Code :

#include <stdio.h>

int main()

{

       int i, t, n, x, r, flag;

       int a[10] = {0};

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       x = n;

       while( n != 0 ) 

       {

              r = n % 10;

              a[ r ]++;

              n = n / 10;

       }   

       flag = 1;

       for( i=0 ; i<10 ; i++ ) 

       {

              if( a[ i ] > 1 )

              {

                     flag = 0;

                     break;

              }​

       }

       if( flag )          ​//  if( flag == 1 )

              printf( "\n%d is a Unique Number.\n", x );

       else

              printf( "\n%d is not a Unique Number.\n", x );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CD.jpg)![](image_rsrc48CE.jpg)

______________  ****  ______________

Program No. - 245 :

Program to Swap two one dimentsional array of same size.

Code :

#include <stdio.h>

int main()

{

       int a[5], b[5];

       int i, t;

       system( "cls" );

       printf( "Enter Values of Array-1 : \n" );

       for( i=0 ; i<5 ; i++ )

       {

               scanf( "%d", &a[ i ] );​

       }

       printf( "Enter Values of Array-2 : \n" );

       for( i=0 ; i<5 ; i++ )

       {

              scanf( "%d", &b[ i ] );

       }

       printf( "\nArrays before Swapping : " );

       printf( "\nArray-1 : " );

       for( i=0 ; i<5 ; i++ )

       {​

              printf( "%d ", a[ i ] ); ​

       }

       printf( "\nArray-2 : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "%d ", b[ i ] );

       }

       for( i=0 ; i<5 ; i++ )

       {

              t = a[ i ];

              a[ i ] = b[ i ];

              b[ i ] = t;

       }

       printf( "\n\nArrays After Swapping : " );

       printf( "\nArray-1 : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "%d ", a[ i ] ); ​

       }

       printf( "\nArray-2 : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "%d ", b[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CF.jpg)

______________  ****  ______________

Program No. - 246 :

Program to find First Biggest and Second Biggest of array elements.

Code :

#include <stdio.h>

#include <limits.h>

int main()

{

       int a[5];

       int i, t, big, sbig;

       system( "cls" );

       printf( "Enter Values of Array : \n" );

       for( i=0 ; i<5 ; i++ )

       {​

              scanf( "%d", &a[ i ] );

       }

       printf( "\nArray : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "%d ", a[ i ] );​

       }

       big = a[0];

       for( i=1 ; i<5 ; i++ )

       {

              if( big < a[ i ] )  

                     big = a[ i ];

       }

       sbig = INT_MIN;         ​// −2147483648

       for( i=0 ; i<5 ; i++ )

       {

              if( ( sbig < a[ i ] ) && ( a[ i ] != big ) )

                     sbig = a[ i ];

       }

       printf( "\nFirst Biggest  : %d\n", big );

       printf( "Second Biggest : %d\n", sbig );  

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CG.jpg)

______________  ****  ______________

Program No. - 247 :

Program to Insert an element in given array at specific location.

Code :

#include <stdio.h>

int main()

{

       int ar[25], pos, i, n, value;

       system( "cls" );

       printf( "Enter number of elements in array : " );

       scanf( "%d", &n );

       printf( "Enter %d elements :\n", n );

       for( i=0 ; i<n ; i++ )

       {

              scanf( "%d", &ar[ i ] );

       }

       printf( "Enter the Location to Insert : " );

       scanf( "%d", &pos );

       printf( "Enter the Value to Insert : " );

       scanf( "%d", &value );

       printf( "\nArray before Insertion : \n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "%d ", ar[ i ] );

       }

       for( i=n−1 ; i>=pos−1; i−− )

       {

              ar[ i+1] = ar[ i ];​

       }

       ar[pos−1] = value;

       n++;

       printf( "\n\nArray after Insertion : \n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "%d ", ar[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CH.jpg)

______________  ****  ______________

Program No. - 248 :

Program to Delete an element from given array.

Code :

#include <stdio.h>

int main()

{

       int ar[25], pos, i, j, n, value, flag;

       system( "cls" );

       printf( "Enter number of elements in array : " );

       scanf( "%d", &n );

       printf( "Enter %d elements :\n", n );

       for( i=0 ; i<n ; i++ )

       {

              scanf( "%d", &ar[ i ] );

       }

       printf( "Enter the Value to Delete : " );

       scanf( "%d", &value );

       printf( "\nArray before Deletion : \n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "%d ", ar[ i ] );​

       }

       flag = 0;

       for( i=0 ; i<n; i++ )

       {

              if( value == ar[ i ] )

              {

                     for( j=i ; j<n−1 ; j++ )

                     {

                            ar[ j ] = ar[ j+1];

                     }

                     n−−;

                     flag = 1;

              }

       }

       if( ! flag )     ​​// (flag == 0)

       {

              printf( "\n\nValue %d not in Array.", value );

       }

       else

       {

              printf( "\n\nArray after Deletion : \n" );

              for( i=0 ; i<n ; i++ )

              {

                     printf( "%d ", ar[ i ] );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CJ.jpg)![](image_rsrc48CK.jpg)

______________  ****  ______________

Program No. - 249 :

Program to remove all duplicate elements from array.

Code :

#include <stdio.h>

int main()

{

       int ar[25], pos, i, j, k, n, flag;

       system( "cls" );

       printf( "Enter number of elements in array : " );

       scanf( "%d", &n);

       printf("Enter %d elements :\n", n );

       for( i=0 ; i<n ; i++ )

       {

              scanf( "%d", &ar[ i ] );

       }

       printf( "\nOriginal Array : \n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "%d ", ar[ i ] );

       }

       flag = 0;

       for( i=0 ; i<n; i++ )

       {

              for( j=i+1 ; j<n ; j++ )

              {

                     if( ar[ j ] == ar[ i ] )

                     {

                            for( k=j ; k<(n−1) ; k++ )

                            {

                                   ar[k] = ar[k+1];

                            }  

                            n−−;

                            flag = 1;

                     }

              }

       }

       if( ! flag )     ​​// (flag == 0)

       {

              printf( "\n\nNo Duplicates in Array." );

       }

       else

       {

              printf( "\n\nArray without Duplicates : \n" );

              for( i=0 ; i<n ; i++ )

              {

                     printf( "%d ", ar[ i ] );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CM.jpg)![](image_rsrc48CN.jpg)

______________  ****  ______________

Program No. - 250 :

Program to Delete an element at specific location in array.

Code :

#include <stdio.h>

int main()

{

       int ar[25], pos, i, n;

       system( "cls" );

       printf( "Enter number of elements in array : " );

       scanf( "%d", &n );

       printf( "Enter %d elements :\n", n );

       for( i=0 ; i<n ; i++ )

       {

              scanf( "%d", &ar[ i ] );

       }

       printf( "Enter the Location of element to Delete : " );

       scanf( "%d", &pos );

       printf( "\nArray before Deletion : \n" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "%d ", ar[ i ] );

       }

       if( (pos < 1) || (pos > n) )

       {

              printf( "\n\nLocation %d is out of Range.", pos );

       }

       else

       {

              for( i=pos−1 ; i<n−1; i++ )

              {

                     ar[ i ] = ar[ i+1];

              }

              n−−;

              printf( "\n\nArray after Deletion : \n" );

              for( i=0 ; i<n ; i++ )

              {

                     printf( "%d ", ar[ i ] );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CP.jpg)![](image_rsrc48CR.jpg)

______________  ****  ______________

Program No. - 251 :

Program to Input and display a Matrix ( 2-D Array ).

Code :

#include <stdio.h>

int  main()

{

       int  a[2][3];

       int  i, j;

       system( "cls" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter value : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       printf( "\nThe Matrix is : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "%d      ", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CS.jpg)

______________  ****  ______________

Program No. - 252 :

Program to Initialize a Matrix ( 2-D Array ).

Code :

#include <stdio.h>

int  main()

{

       int a[2][3] = { { 10, 20, 30 },

                                    { 40, 50, 50 } };

       int i, j;

       system( "cls" );

       printf( "Matrix A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d",  a[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CT.jpg)

______________  ****  ______________

Program No. - 253 :

Program for Addition of Two Matrices.

Code :

#include <stdio.h>

int  main()

{

       int  a[2][3], b[2][3], c[2][3];

       int  i, j;

       system( "cls" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter value of A : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter value of B : " );

                     scanf( "%d", &b[ i ][ j ] );

              }

       }

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     c[ i ][ j ] = a[ i ][ j ] + b[ i ][ j ] ;

              }

       }

       printf( "\nMatrix A is :\n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Matrix B is :\n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d",  b[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Matrix C is ::: \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", c[ i ][ j ] );​

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CU.jpg)

______________  ****  ______________

Program No. - 254 :

Program to find Transpose of given Matrix.

Code :

#include <stdio.h>

int  main()

{

       int  a[2][3], b[3][2];

       int  i, j;

       system( "cls" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter Value : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     b[ j ][ i ] = a[ i ][ j ] ;

              }

       }

       printf( "\nMatrix A is :\n" );

       for( i=0 ; i<2 ; i++ )

       {​

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Matrix B is :\n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<2 ; j++ )

              {

                     printf( "  %d", b[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CV.jpg)

______________  ****  ______________

Program No. - 255 :

Program to Transpose a Square Matrix without using Second matrix.

Code :

#include <stdio.h>

int  main()

{

       int  a[10][10];

       int  n, i, j, temp;

       system( "cls" );

       printf( "Enter order of matrix (n x n) : " );

       scanf( "%d", &n );

       printf( "Enter the elements of Matrix :\n" );

       for( i=0 ; i<n ; i++ )

       {

              for( j=0 ; j<n ; j++ )

              {

                     printf( "Enter element : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       printf( "\nThe Original matrix is :\n" );

       for( i=0 ; i<n ; i++ )

       {

              for( j=0 ; j<n ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );​

              }

              printf( "\n" );

       }

       for( i=0 ; i<n ; i++ )

       {

              for( j=0 ; j<n ; j++ )

              {

                     if( i < j )

                     {

                            temp = a[ i ][ j ];

                            a[ i ][ j ] = a[ j ][ i ];

                            a[ j ][ i ] = temp;

                     }

              }

       }

       printf( "\nThe Transposed matrix is :\n" );

       for( i=0 ; i<n ; i++ )

       {

              for( j=0 ; j<n ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CW.jpg)

______________  ****  ______________

Program No. - 256 :

Program to Multiply Two Matrices.

Code :

#include <stdio.h>

int  main()

{

       int a[2][3], b[3][2], c[2][2];

       int i, j, k;

       system( "cls" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter Value of A : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<2 ; j++ )

              {

                     printf( "Enter Value of B : " );

                     scanf( "%d", &b[ i ][ j ] );

              }

       }

       for( i=0 ; i<2 ; i++ )

       {​

              for( j=0 ; j<2 ; j++ )

              {

                     c[ i ][ j ] = 0;

                     for( k=0 ; k<3 ; k++ )

                     {

                            c[ i ][ j ] = c[ i ][ j ] + ( a[ i ][ k ] * b[ k ][ j ] );

                     }

              }

       }

       printf( "\nMatrix A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Matrix B : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<2 ; j++ )

              {

                     printf( "  %d", b[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Matrix C : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<2 ; j++ )

              {

                     printf( "  %d",  c[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CX.jpg)

______________  ****  ______________

Program No. - 257 :

Program to find Sum of Principle Diagonal, Other Diagonal, Upper Triangle, Lower Triangle and All elements of Square Matrix.

Code :

#include <stdio.h>

int  main()

{

       int a[3][3];

       int i, j, spd=0, sod=0, sut=0, slt=0, sa=0;

       system( "cls" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter Value of A : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     if( i == j )

                            spd = spd + a[ i ][ j ];

                     if( (i + j ) == 2 )

                            sod = sod + a[ i ][ j ];

                     if( i <= j )​

                            sut = sut + a[ i ][ j ];

                     if( i >= j )

                            slt = slt + a[ i ][ j ];

                     sa = sa + a[ i ][ j ];

              }

        }

       printf( "\nMatrix A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "Sum of All elements      : %d\n", sa );

       printf( "Sum of Principal Diagonal: %d\n", spd );

       printf( "Sum of Other Diagonal    : %d\n", sod );

       printf( "Sum of Upper Triangle    : %d\n", sut );

       printf( "Sum of Lower Triangle    : %d\n", slt );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CY.jpg)

______________  ****  ______________

Program No. - 258 :

Program to find Row-wise Sum and Column-wise Sum and Sum of all elements of Matrix.

Code :

#include <stdio.h>

int  main()

{

       int a[3][3];

       int  i, j, gt=0;

       int  rs[3] = {0}, cs[3] = {0};

       system( "cls" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "Enter Value of A : " );

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     rs[ i ] = rs[ i ] + a[ i ][ j ];

                     cs[ j ] = cs[ j ] + a[ i ][ j ];

                     gt = gt + a[ i ][ j ];

              }

       }​

       printf( "\nMatrix A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "%4d", a[ i ][ j ] );

              }

              printf( " | %d \n", rs[ i ] );

       }

       printf( " ___________________\n" );

       for( i=0 ; i<3 ; i++ )

       {

              printf( "%4d",  cs[ i ] );

       }

       printf( " | %d \n", gt );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48CZ.jpg)

______________  ****  ______________

Program No. - 259 :

Program to check whether the Two Matrices are Equal or not.

Code :

#include <stdio.h>

int  main()

{

       int  n1[5][5], n2[5][5];

       int  i, j, r, c, flag;

       system( "cls" );

       printf( "Enter Order of Matrices : " );

       scanf( "%d %d", &r, &c );

       printf( "Enter Values of Matrix A : \n " );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {   

                     scanf( "%d", &n1[ i ][ j ] );

              }

       }

       printf( "Enter Values of Matrix B : \n " );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {   

                     scanf( "%d", &n2[ i ][ j ] );

              }​

       }

       flag = 0;

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {

                     if( n1[ i ][ j ] != n2[ i ][ j ] )

                     {

                            flag = 1;

                            break;

                     }

              }

              if( flag == 1 )​​/*  if( flag )​*/

                     break;

       }

       if( flag == 1 )​​/*  if( flag )​*/

              printf( "\nBoth Matrices are Unequal.\n" );

       else

              printf( "\nBoth Matrices are Equal.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D0.jpg)![](image_rsrc48D1.jpg)

______________  ****  ______________

Program No. - 260 :

Program to check whether the given matrix is Identity Matrix or Not.

Code :

#include <stdio.h>

#include <stdlib.h>

int  main()

{

       int  a[5][5];

       int  i, j, r, c, flag;

       system( "cls" );

       printf( "Enter Order of Matrices : " );

       scanf( "%d %d", &r, &c );

       if( r != c )

       {

              printf("\nNot an Identity Matrix (rows!=columns).\n" );

              exit(0);

       }

       printf( "Enter Values of Matrix : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {     

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       printf( "\nMatrix-A : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {     

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       flag = 1;

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {

                     if( (i==j && a[i][j] != 1) || (i!=j && a[i][j] != 0)  )

                     {   

                            flag = 0;

                            break;

                     }

              }

              if( flag == 0 )        ​/*   if( ! flag )    */

                     break;

       }

       if( flag == 1 )          ​​/*   if( flag )    */

              printf( "\nMatrix is an Identity Matrix.\n" );

       else

              printf( "\nMatrix is not an Identity Matrix.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D2.jpg)![](image_rsrc48D3.jpg)![](image_rsrc48D4.jpg)

______________  ****  ______________

Program No. - 261 :

Program to check whether the given matrix is Sparse Matrix or Not.

Code :

#include <stdio.h>

int  main()

{

       int  a[5][5];

       int  i, j, r, c, zcnt=0;

       system( "cls" );

       printf( "Enter Order of Matrices : " );

       scanf( "%d %d", &r, &c );

       printf( "Enter Values of Matrix : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {     

                     scanf( "%d", &a[ i ][ j ] );

                     if( a[ i ][ j ] == 0 )

                            zcnt++;

              }

       }

       printf( "\nMatrix-A : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {     

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       if( zcnt > ((r * c) / 2) )        

              printf( "\nMatrix is a Sparse Matrix.\n" );

       else

              printf( "\nMatrix is not a Sparse Matrix (Dense).\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D5.jpg)![](image_rsrc48D6.jpg)

______________  ****  ______________

Program No. - 262 :

Program to find No. of even values and No. of odd values in given matrix.

Code :

#include <stdio.h>

int main()

{

       int a[5][5];

       int i, j, r, c, ecnt, ocnt;

       system( "cls" );

       printf( "Enter Order of Matrices : " );

       scanf( "%d %d", &r, &c );

       printf( "Enter Values of Matrix : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       ecnt = ocnt = 0;

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++ )

              {

                     if( a[ i ][ j ] % 2 == 0 )

                            ecnt++;

                     if( a[ i ][ j ] % 2 != 0 )

                            ocnt++;

              }

       }

       printf( "\nMatrix-A : \n" );

       for( i=0 ; i<r ; i++ )

       {

              for( j=0 ; j<c ; j++)

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "\nNo. of Even Values : %d\n", ecnt );

       printf( "No. of Odd Values  : %d\n", ocnt );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D7.jpg)

______________  ****  ______________

Program No. - 263 :

Program to display Upper-Trianglar matrix of given Square matrix.

Code :

#include <stdio.h>

int main()

{

       int a[3][3];

       int i, j;

       system( "cls" );

       printf( "Enter Values of Matrix : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       printf( "\nGiven Matrix-A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "\nUpper Triangular Matrix-A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     if( i <= j )

                             printf( "  %d", a[ i ][ j ] );

                     else

                             printf( "  0", a[ i ][ j ] );​

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D8.jpg)

______________  ****  ______________

Program No. - 264 :

Program to display Lower-Trianglar matrix of given Square matrix.

Code :

#include <stdio.h>

int main()

{

       int a[3][3];

       int i, j;

       system( "cls" );

       printf( "Enter Values of Matrix : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     scanf( "%d", &a[ i ][ j ] );

              }

       }

       printf( "\nGiven Matrix-A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       printf( "\nLower Triangular Matrix-A : \n" );

       for( i=0 ; i<3 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     if( i >= j )

                            printf( "  %d", a[ i ][ j ] );

                     else

                            printf( "  0", a[ i ][ j ] );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48D9.jpg)

______________  ****  ______________

Chapter – 9

Strings

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 265 :

Program to Input and Display String.

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter Name : " );

       scanf( "%s", str );

       printf( "\nName = %s\n",  str );

       printf( "Name = " );

       puts( str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DA.jpg)

______________  ****  ______________

Program No. - 266 :

Program to Input Multiple Words String (Embedded Blanks) using gets() function.

Code :

#include <stdio.h>

int  main()

{

       char str[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DB.jpg)

______________  ****  ______________

Program No. - 267 :

Program to Initialize a String.

Code :

#include <stdio.h>

int  main()

{

       char  s1[ ] = "Atul";

       char  s2[ ] = { 'A', 't', 'u', 'l', '\0' };

       char  s3[5];

       system( "cls" );

       s3[0] = 'A';

       s3[1] = 't';

       s3[2] = 'u';

       s3[3] = 'l';

       s3[4] = '\0';

       printf( "s1 = %s\n", s1 );

       printf( "s2 = %s\n", s2 );

       printf( "s3 = %s\n", s3 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DC.jpg)

______________  ****  ______________

Program No. - 268 :

Program to display a string character-wise.

Code :

#include <stdio.h>

int  main()

{

       char  name[ ] = "ATUL" ;

       int  i = 0 ;

       system( "cls" );

       while( name[ i ] != '\0' )

       {

              printf( " %c\n", name[ i ] ) ;

              i++ ;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DD.jpg)

______________  ****  ______________

Program No. - 269 :

Program to explain that multiple strings are cancatenated.

Code :

#include <stdio.h>

int  main()

{

       char s1[25] = "Atul" "Kumar" "Soni";

       system( "cls" );

       puts( s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DE.jpg)

______________  ****  ______________

Program No. - 270 :

Program to find the length of string using strlen( ) function.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char  str[ ] = "Atul Kumar Soni" ;

       int  len ;

       system( "cls" ) ;

       len = strlen( str ) ;

       printf( "String = %s \nLength = %d\n", str, len ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DF.jpg)

______________  ****  ______________

Program No. - 271 :

Program to copy a string using strcpy( ) function.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char  str1[ ] = "INDIA" ;

       char  str2[25] ;

       system( "cls" );

       strcpy( str2, str1 ) ;

       printf( "String-1 = %s\n", str1 ) ;

       printf( "String-2 = %s\n", str2 ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DG.jpg)

______________  ****  ______________

Program No. - 272 :

Program to Concat string using strcat( ) function.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char name[50] = "Atul";

       system( "cls" );

       strcat( name, " Kumar" );

       strcat( name, " Soni" );

       printf( "Full Name : %s\n", name );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DH.jpg)

______________  ****  ______________

Program No. - 273 :

Program to Concat Strings using strcat() function.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char name[50];

       system( "cls" );

       strcpy( name, "Atul" );

       strcat( name, " " );

       strcat( name, "Kumar" );

       strcat( name, " " );

       strcat( name, "Soni" );

       printf( "Full Name : %s\n", name );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DJ.jpg)

______________  ****  ______________

Program No. - 274 :

Program to use strcmp() function to Compare String.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char str1[25] = "ATUL";

       char str2[25] = "ATul";

       int d = 0;

       system( "cls" );

       d = strcmp( str1, str2 );

       printf( "str1 : %s\n", str1 );

       printf( "str2 : %s\n", str2 );

       printf( "\nDifference = %d\n", d );

       if( d == 0 )

              printf( "Strings are same.\n" );

       else

              printf( "Strings are different.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DK.jpg)

______________  ****  ______________

Program No. - 275 :

Program to use strcmpi() function to Compare String.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char pass[20] = "INDIA", ps[20];

       int ctr = 0;

       system( "cls" );

       printf( "Enter Your Password : " );

       scanf( "%s", ps );

       ctr = strcmpi( pass, ps );

       if( ctr == 0 )

              printf( "\nCorrect password!!!\n" );

       else

              printf( "\nWrong password!!!\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DM.jpg)![](image_rsrc48DN.jpg)

______________  ****  ______________

Program No. - 276 :

Program to Swap Two Strings.

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char str1[25], str2[25], t[25];

       system( "cls" );

       printf( "Enter Two Strings : " );

       scanf( "%s %s", str1, str2 );

       printf( "\nStrings Before Swapping are : \n" );

       printf( " 1\. %s \t 2\. %s\n", str1, str2 );

       strcpy( t, str1 );

       strcpy( str1, str2 );

       strcpy( str2, t );

       printf( "\nStrings After Swapping are : \n" );

       printf( " 1\. %s \t 2\. %s\n", str1, str2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DP.jpg)

______________  ****  ______________

Program No. - 277 :

Program to explain the use of strrev() string library function .

Code :

#include <stdio.h>

#include <string.h>

int main()

{

       char s1[25] = "GREEN";

       system( "cls" );

       printf( "Original String : %s\n", s1 );

       strrev( s1 );

       printf( "Reversed String : %s\n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DR.jpg)

______________  ****  ______________

Program No. - 278 :

Program to check whether the given string is Palindrome or Not using string library functions.

Code :

#include <stdio.h>

#include <string.h>

int main()

{

       char s1[25] = "RADAR";

       //  char s1[25] = "INDIA";

       char s2[25];

       system( "cls" );

       printf( "Original String : %s\n", s1 );

       strcpy( s2, s1 );

       strrev( s2 );

       printf( "Reversed String : %s\n", s2 );

       if( strcmp(s1, s2) == 0 )

              printf( "%s is a Palindrome.\n", s1 );

       else

              printf( "%s is not a Palindrome.\n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DS.jpg)![](image_rsrc48DT.jpg)

______________  ****  ______________

Program No. - 279 :

Program to Remove all Vowels from given string.

Code :

#include <stdio.h>

#include <string.h>

int main()

{

       char s1[25] = "INDIA";

       char s2[25];

       int i, j;

       system( "cls" );

       printf( "Original String : %s\n", s1 );

       j = 0;

       for( i=0 ; s1[ i ]!='\0' ; i++ )

       {

              if( s1[ i ]!='A' && s1[ i ]!='a' && s1[ i ]!='E' &&

                      s1[ i ]!='e' && s1[ i ]!='I' && s1[ i ]!='i' &&

                      s1[ i ]!='O' && s1[ i ]!='o' && s1[ i ]!='U' &&

                      s1[ i ]!='u' )

               {

                     s2[ j ] = s1[ i ];

                     j++;

              }

       }

       s2[ j ] = '\0';

       printf( "String without Vowels : %s\n", s2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DU.jpg)

______________  ****  ______________

Program No. - 280 :

Program to Remove all Vowels from the given string without using second string.

Code :

#include <stdio.h>

int main()

{

       char s1[25] = "INDIA";

       int i, j;

       system( "cls" );

       printf( "Original String : %s\n", s1 );

       i = 0;

       while( s1[ i ] != '\0' )

       {

              if( s1[ i ]=='A' || s1[ i ]=='a' || s1[ i ]=='E' ||

                     s1[ i ]=='e' || s1[ i ]=='I' || s1[ i ]=='i' ||

                     s1[ i ]=='O' || s1[ i ]=='o' || s1[ i ]=='U' ||

                     s1[ i ]=='u' )

              {

                     for( j=i ; s1[ j ]!='\0' ; j++ )

                            s1[ j ] = s1[ j+1];

              }

              else

                     i++;

       }

       printf( "String without Vowels : %s\n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DV.jpg)

______________  ****  ______________

Program No. - 281 :

Program to find Length of String without using strlen() function.

Code :

#include <stdio.h>

int  main()

{

       char str[50];

       int  i, len;

       system( "cls" );

       printf( "Enter String : " );

       gets( str );

       for( i=0 ; str[ i ] != '\0' ; i++ );

       len = i;

       printf( "\nLength of String : %d\n",  len );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DW.jpg)

______________  ****  ______________

Program No. - 282 :

Program to copy String without using strcpy() function.

Code :

#include <stdio.h>

int  main()

{

       char str1[25] = "Atul Kumar Soni";

       char str2[25];

       int i;

       system( "cls" );

       for ( i=0 ; str1[ i ] != '\0' ; i++ )

       {

              str2[ i ] = str1[ i ];

       }

       str2[ i ] = '\0';

       printf( "str1 = %s\n", str1 );

       printf( "str2 = %s\n", str2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DX.jpg)

______________  ****  ______________

Program No. - 283 :

Program to concat String without using strcat() function.

Code :

#include <stdio.h>

int  main()

{

       char str1[50] = "Atul";

       char str2[ ] = " Soni";

       int  i, l;

       system( "cls" );

       for ( i=0 ; str1[ i ] != '\0' ; i++ );

       l = i;

       for ( i=0 ; str2[ i ] != '\0' ; i++)

       {

              str1[ l + i ] = str2[ i ];

       }

       str1[ l + i ] = '\0';

       printf( "str1 = %s\n", str1 );

       printf( "str2 = %s\n", str2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DY.jpg)

______________  ****  ______________

Program No. - 284 :

Program to Reverse a String without using String function.

Code :

#include <stdio.h>

int  main()

{

       char str1[25], str2[25];

       int i, j, l;

       system( "cls" );

       printf( "Enter a string : " );

       gets( str1 );

       for( i=0 ; str1[ i ] != '\0' ; i++ ) ;

       l = i;

       for( i=0, j=l−1 ; j >= 0 ; j−−, i++ )

       {  

              str2[ i ] = str1[ j ];

       }

       str2[ i ] = '\0';

       printf( "\nReverse : %s\n", str2 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48DZ.jpg)

______________  ****  ______________

Program No. - 285 :

Program to check whether the Input String is Palindrome or not.

Code :

#include <stdio.h>

int  main()

{

       char str[26];

       int i, j, len, flag;

       system( "cls" );

       printf( "Enter the string : " );

       gets( str );

       for( len=0 ; str[len] != '\0' ; len++ ) ;

       flag = 1;

       for( i=0, j=len−1 ; i<len/2 ; i++, j−− )

       {

              if( str[ i ] != str[ j ] )

              {

                     flag = 0;

                     break;

              }

        }

       if( flag == 1 )​​/*  if( flag )  */

              printf( "\nIt is Palindrome.\n" );

       else

              printf( "\nIt is not a Palindrome.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E0.jpg)![](image_rsrc48E1.jpg)

______________  ****  ______________

Program No. - 286 :

Program to Reverse a String without using String functions and Second String.

Code :

#include <stdio.h>

int  main()

{

       int   i, j, len;

       char  ch, str[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( str );

       printf( "\nGiven String = %s\n", str );

       for( len=0 ; str[ len ] != '\0' ; len++ ) ;

       for( i=0, j=len−1 ; i<len/2 ; i++, j−− )

       {

              ch = str[ i ];

              str[ i ] = str[ j ];

              str[ j ] = ch;

       }

       printf( "\nReversed String = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E2.jpg)

______________  ****  ______________

Program No. - 287 :

Program to Count the Number of Vowels in the Sentence.

Code :

#include <conio.h>

int  main()

{

       int  i, j, c;

       char  str[50];

       system( "cls" );

       printf( "Enter String : " );

       gets( str );

       c = 0;

       for( i=0 ; str[ i ] != '\0' ; i++ )

       {

              if( ( str[ i ]=='a' ) || ( str[ i ]=='e' ) || ( str[ i ]=='i' ) ||

                     ( str[ i ]=='o' ) || ( str[ i ]=='u' ) || ( str[ i ]=='A' ) ||

                     ( str[ i ]=='E' ) || ( str[ i ]=='I' ) || ( str[ i ]=='O' ) ||

                     ( str[ i ]=='U' ) )

              {

                     c++;

              }

       }

       printf( "\nNumber of Vowels = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E3.jpg)

______________  ****  ______________

Program No. - 288 :

Program to convert lowercase characters of string to uppercase characters.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       char s1[ ] = "india";

       int i;

       system( "cls" );

       printf( "s1 : %s \n", s1 );

       for( i=0 ; s1[ i ] != '\0' ; i++ )

              if( (s1[ i ] >= 97) && (s1[ i ] <= 122) )

                     s1[ i ] = toupper( s1[ i ] );

       printf( "s1 : %s \n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E4.jpg)

______________  ****  ______________

Program No. - 289 :

Program to convert uppercase characters of string to lowercase characters.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       char s1[ ] = "INDIA";

       int i;

       system( "cls" );

       for( i=0 ; s1[ i ] != '\0' ; i++ )

              if( (s1[ i ] >= 65) && (s1[ i ] <= 90) )

                     s1[ i ] = tolower( s1[ i ] );

       printf( "s1 : %s \n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E5.jpg)

______________  ****  ______________

Program No. - 290 :

Program to Count the Number of Vowels in the Sentence.

Code :

#include <stdio.h>

int  main()

{

       int  c, i;

       char  str[50];

       system( "cls" );

       printf( "Enter String : " );

       gets( str );

       c = 0;

       for( i=0 ; str[ i ] != '\0' ; i++ )

       {

              switch( str[ i ] )

              {

                     case 'a':

                     case 'A':

                     case 'e':

                     case 'E':

                     case 'i':

                     case 'I':

                     case 'o':

                     case 'O':

                     case 'u':

                     case 'U':

                            c++;

              }

       }

       printf( "\nNumber of Vowels = %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E6.jpg)

______________  ****  ______________

Program No. - 291 :

Program to count Number of Words and Number of Characters in Given String.

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       int  i, c = 0, w = 1;

       system( "cls" );

       printf( "Enter String : " );

       gets( str );

       for( i=0 ; str[ i ] != '\0' ; i++ )

       {

              if( ( str[ i ] == ' ' ) && ( str[ i−1 ] != ' ' ) )​

                     w++;

              else if( str[ i ] != '.' )

                     c++;

       }

       printf( "\nNumber of words : %d\n", w );

       printf( "Number of characters : %d\n", c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E7.jpg)

______________  ****  ______________

Program No.- 292 :

Program to show the use of while loop in string.

Code :

#include <stdio.h>

int  main()

{

       char  name[ ] = "Atul Kumar Soni" ;

       int  i = 0 ;

       system( "cls" );

       while( name[ i ] != '\0' )  ​​/* while( name[ i ] ) */

       {

              printf( "%c", name[ i ] ) ;

              i++ ;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E8.jpg)

______________  ****  ______________

Program No. - 293 :

Program to use pointer to access string character-wise.

Code :

#include <stdio.h>

int  main()

{

       char  name[ ] = "Atul Kumar Soni" ;

       char  *ptr ;

       system( "cls" );

       ptr = name ;​​/* store base address of string */

       while( *ptr != '\0' )

       {

              printf( "%c", *ptr ) ;

              ptr++ ;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48E9.jpg)

______________  ****  ______________

Program No. - 294 :

Program to Sort all characters of string in Ascending Order.

Code :

#include <stdio.h>

#include <string.h>

int main()

{

       char s1[25] = "INDIA", ch;

       int i, j, l;

       system( "cls" );

       printf( "Original String : %s\n", s1 );

       len = strlen( s1 );

       for( i=0 ; i<len-1 ; i++ )

       {

              for( j=0 ; j<len−1−i ; j++ )

              {

                     if( s1[ j ] > s1[ j+1] )

                     {

                            ch = s1[ j ];

                            s1[ j ] = s1[ j+1];

                            s1[ j+1] = ch;

                     }

              }

       }

       printf( "Sorted String : %s\n", s1 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EA.jpg)

______________  ****  ______________

Program No. - 295 :

Program to check whether input character is Capital letter, Small letter, Digit or Special Symbol.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a character : " );

       scanf( "%c", &ch );

       if( isupper( ch ) )

              printf( "\nCharacter %c is in Upper Case.\n", ch );

       else if( islower( ch ) )

              printf( "\nCharacter %c is in Lower Case.\n", ch );

       else if( isdigit( ch ) )

              printf( "\nCharacter %c is a Digit.\n", ch );

       else

              printf( "\nCharacter %c is a Special Symbol.\n", ch );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EB.jpg)![](image_rsrc48EC.jpg)![](image_rsrc48ED.jpg)![](image_rsrc48EE.jpg)

______________  ****  ______________

Program No. - 296 :

Program to count number of Capital letters, Small letters, Digits and Special Symbols.

Code :

#include <stdio.h>

int  main()

{

       int i, c = 0, sm = 0, d = 0, ss = 0;

       char s[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( s );

       for( i=0 ; s[ i ] != '\0' ; i++ )

       {

              if( s[ i ] >= 65 && s[ i ] <= 90 )

                     c++;

              else if( s[ i ] >= 97 && s[ i ] <= 122 )

                     sm++;

              else if( s[ i ] >= 48 && s[ i ] <= 57 )

                     d++;

              else

                     ss++;

       }

       printf( "\nNumber of Capital Letters : %d\n", c );

       printf( "Number of Small Letters   : %d\n", sm );

       printf( "Number of Digits          : %d\n", d );

       printf( "Number of Special Symbols : %d\n", ss );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EF.jpg)

______________  ****  ______________

Program No. - 297 :

Program to count number of Capital letters, Small letters, Digits and Special Symbols.

Code :

#include <stdio.h>

int  main()

{

       int i, c = 0, sm = 0, d = 0, ss = 0;

       char s[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( s );

       for( i=0 ; s[ i ] != '\0' ; i++ )

       {

              if( s[ i ] >= 'A' && s[ i ] <= 'Z' )

                     c++;

              else if( s[ i ] >= 'a' && s[ i ] <= 'z' )

                     sm++;

              else if( s[ i ] >= '0' && s[ i ] <= '9' )

                     d++;

              else

                     ss++;

       }

       printf( "\nNumber of Capital Letters : %d\n", c );

       printf( "Number of Small Letters   : %d\n", sm );

       printf( "Number of Digits          : %d\n", d );

       printf( "Number of Special Symbols : %d\n", ss );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EG.jpg)

______________  ****  ______________

Program No. - 298 :

Program to count number of Capital letters, Small letters, Digits and Special Symbols.

Code :

#include <stdio.h>

#include <ctype.h>

int  main()

{

       int i, c = 0, sm = 0, d = 0, ss = 0;

       char s[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( s );

       for( i=0 ; s[ i ] != '\0' ; i++ )

       {

              if( isupper( s[ i ] ) )

                     c++;

              else if( islower( s[ i ] ) )

                     sm++;

              else if( isdigit( s[ i ] ) )

                     d++;

              else

                     ss++;

       }

       printf( "\nNumber of Capital Letters : %d\n", c );

       printf( "Number of Small Letters   : %d\n", sm );

       printf( "Number of Digits                   : %d\n", d );                     

       printf( "Number of Special Symbols : %d\n", ss );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EH.jpg)

______________  ****  ______________

Program No. - 299 :

Program to explain the array of strings.

Code :

#include <stdio.h>

int  main()

{

       char str[ ][15] =  { "RED", "GREEN", "BLUE" };

       int i;

       system( "cls" );

       for( i = 0 ; i<3 ; i++ )

       {

              printf( " %s\n", str[ i ] );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EJ.jpg)

______________  ****  ______________

Program No. - 300 :

Program to sort array of strings ( two dimensional char  array ).

Code :

#include <stdio.h>

#include <string.h>

int  main()

{

       char  colors[5][10] = {

                                                 "RED",

                                                 "GREEN",

                                                 "BLUE",

                                                 "ORANGE",

                                                 "YELLOW"

                                          };

       int  i, j;

       char  temp[10];

       system( "cls" );

       printf( "Colors before Sorting :\n" );

       for( i = 0 ; i<5 ; i++ )

       {

              printf( " %s\n", colors[ i ] );

       }

       for( i=0 ; i<5−1 ; i++ )

       {

              for( j=0 ; j<5−1−i ; j++ )

              {

                     if( strcmp( colors[ j ], colors[ j + 1 ] ) > 0 )

                     {

                            strcpy( temp, colors[ j ] );

                            strcpy( colors[ j ], colors[ j + 1 ] );

                            strcpy( colors[ j + 1 ], temp );

                     }

              }

       }

       printf( "\nColors after Sorting :\n" );

       for( i = 0 ; i<5 ; i++ )

       {

              printf( " %s\n", colors[ i ] );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EK.jpg)

______________  ****  ______________

Program No. - 301 :

Program to convert each digits of a number in English word.

Code :

#include <stdio.h>

int main()

{

       int num, i=0, j, dig;

       char *word[10] = { "Zero", "One", "Two",

                                                 "Three", "Four", "Five", "Six",

                                                 "Seven", "Eight", "Nine" };

       char *num_names[10];

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%d", &num );

       i = 0;​

       while( num )               /* while( num != 0 )  */

       {

              dig = num % 10;

              num_names[ i++ ] = word[ dig ];

              num = num / 10;

       }

       for( j=i−1 ; j>=0 ; j−− )

       {

              printf( "%s ", num_names[ j ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EM.jpg)

______________  ****  ______________

Program No. - 302 :

Program to convert each digits of a number in English word.

Code :

#include <stdio.h>

int main()

{

       int num, i=0, j, dig;

       char *num_names[10];

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%d", &num );

       i = 0;​

       while( num )

       {

              dig = num % 10;

              num = num / 10;

              switch( dig )

              {

                     case 0: num_names[ i ] = "Zero"; break;

                     case 1: num_names[ i ] = "One"; break;

                     case 2: num_names[ i ] = "Two"; break;

                     case 3: num_names[ i ] = "Three"; break;

                     case 4: num_names[ i ] = "Four"; break;

                     case 5: num_names[ i ] = "Five"; break;

                     case 6: num_names[ i ] = "Six"; break;

                     case 7: num_names[ i ] = "Seven"; break;

                     case 8: num_names[ i ] = "Eight"; break;

                     case 9: num_names[ i ] = "Nine"; break;

              }

              i++;

       }

       for( j=i−1 ; j>=0 ; j−− )

       {

              printf( "%s ", num_names[ j ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48EN.jpg)

______________  ****  ______________

Chapter – 10

Functions

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 303 :

Program to Simple Function.

Code :

#include <stdio.h>

void  show( int x );​// Function Declaration/Prototype

int  main()

{

       int a = 10;

       system( "cls" );

       show( a );​​// Calling of Function

       system( "pause" );

       return 0;

}

void  show( int x )​​// Function Definition

{

       printf( "x = %d\n", x );

}

Output :

![](image_rsrc48EP.jpg)

______________  ****  ______________

Program No. - 304 :

Program to Eliminate Function Declaration with Function Definition at Top.

Code :

#include <stdio.h>

// Eliminating declaration.

void  show( int x )

{

       printf( "x = %d\n", x );

}

int  main()

{

       int a = 10;

       system( "cls" );

       show( a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48ER.jpg)

______________  ****  ______________

Program No. - 305 :

Program to explain returning value from function.

Code :

// returning value

#include <stdio.h> >

int sum( int, int );

int  main( void )

{

       int s1;

       system( "cls" );

       s1 = sum( 10, 20 );

       printf( "Sum : %d\n", s1 );

       system( "pause" );

       return 0;

}

int sum( int x, int y )

{

       return (x + y);

}

Output :

![](image_rsrc48ES.jpg)

______________  ****  ______________

Program No. - 306 :

Program to explain the calling of function from printf() statement.

Code :

// calling in printf()

#include <stdio.h>

int sum( int, int );

int  main( void )

{

       system( "cls" );

       printf( "\nSum : %d\n", sum( 10, 20 ) );

       system( "pause" );

       return 0;

}

int sum( int x, int y )

{

       return (x + y);

}

Output :

![](image_rsrc48ET.jpg)

______________  ****  ______________

Program No. - 307 :

Program to calculate Simple Interest using Function ( No Argument and No Return Value ).

Code :

#include <stdio.h>

void  Simp_Int();

int  main()

{

       system( "cls" );

       Simp_Int();

       system( "pause" );

       return 0;

}

void  Simp_Int()

{

       float p, r, t, si;

       printf( "Enter Principal, Rate and Time : " );

       scanf( "%f %f %f", &p, &r, &t );

       si = ( p * r * t ) / 100;

       printf( "\nSimple Interest = %f\n", si );

}

Output :

![](image_rsrc48EU.jpg)

______________  ****  ______________

Program No. - 308 :

Program to calculate Simple Interest using Function ( No Argument but Return Value ).

Code :

#include <stdio.h>

float  Simp_Int();

int  main()

{

       float si1;

       system( "cls" );

       si1 = Simp_Int();

       printf( "\nSimple Interest = %f\n", si1 );

       system( "pause" );

       return 0;

}

float  Simp_Int()

{

       float p, r, t, si;

       printf( "Enter Principal, Rate and Time : " );

       scanf( "%f %f %f", &p, &r, &t );

       si = ( p * r * t ) / 100;

       return si;

}

Output :

![](image_rsrc48EV.jpg)

______________  ****  ______________

Program No. - 309 :

Program to calculate Simple Interest using Function ( Argument but No Return Value ).

Code :

#include <stdio.h>

void  Simp_Int( float, float, float );

int  main()

{

       float p1, r1, t1;

       system( "cls" );

       printf( "Enter Principal, Rate and Time : " );

       scanf( "%f %f %f", &p1, &r1, &t1 );

       Simp_Int( p1, r1, t1 );

       system( "pause" );

       return 0;

}

void  Simp_Int( float p, float r, float t )

{

       float si;

       si = ( p * r * t ) / 100;

       printf( "\nSimple Interest = %f\n", si );

}

Output :

![](image_rsrc48EW.jpg)

______________  ****  ______________

Program No. - 310 :

Program to calculate Simple Interest using Function ( Argument and Return Value ).

Code :

#include <stdio.h>

float  Simp_Int( float, float, float );

int  main()

{

       float p1, r1, t1, si1;

       system( "cls" );

       printf( "Enter Principal, Rate and Time : " );

       scanf( "%f %f %f", &p1, &r1, &t1 );

       si1 = Simp_Int( p1, r1, t1 );

       printf( "\nSimple Interest = %f\n", si1 );

       system( "pause" );

       return 0;

}

float  Simp_Int( float p, float r, float t )

{

       float si;

       si = ( p * r * t ) / 100;

       return si;

}

Output :

![](image_rsrc48EX.jpg)

______________  ****  ______________

Program No. - 311 :

Program to use return statement in void function to terminate the function.

Code :

#include <stdio.h>

void show();

int  main()

{

       system( "cls" );

       printf( "Red\n" );

       show();

       printf( "Blue\n" );

       system( "pause" );

       return 0;

}

void show()

{

       printf( "Green\n" );

       return;

       printf( "Orange\n" );

}

Output :

![](image_rsrc48EY.jpg)

______________  ****  ______________

Program No. - 312 :

Program to explain Call By Value.

Code :

#include <stdio.h>

void  cube( int );

int  main()

{

       int a = 10;

       system( "cls" );

       cube( a );

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

void  cube( int  x )

{

       x = x * x * x;

       printf( "x = %d\n", x );

}

Output :

![](image_rsrc48EZ.jpg)

______________  ****  ______________

Program No. - 313 :

Program to explain Call By Address / Pointer.

Code :

#include <stdio.h>

void  cube( int* );

int  main()

{

       int a = 10;

       system( "cls" );

       cube( &a );

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

void  cube( int *pa )

{

       *pa = (*pa) * (*pa) * (*pa);

       printf( "*pa = %d\n", *pa );

}

Output :

![](image_rsrc48F0.jpg)

______________  ****  ______________

Program No. - 314 :

Program to Swap two numbers using Call By Value.

Code :

#include <stdio.h>

void  swap( int, int );

int  main()

{

       int a = 10, b = 20;

       system( "cls" );

       printf( "Before Swapping (in main) : a = %d, b = %d\n", a, b );

       swap( a, b );

       printf( "After Swapping (in main)  : a = %d, b = %d\n", a, b );

       system( "pause" );

       return 0;

}

void  swap( int x, int y )

{

       int t;

       printf( "Before Swapping (in swap) : x = %d, y = %d\n", x, y );

       t = x;

       x = y;

       y = t;

       printf( "After Swapping (in swap)  : x = %d, y = %d\n", x, y );

}

Output :

![](image_rsrc48F1.jpg)

______________  ****  ______________

Program No. - 315 :

Program to Swap two numbers using Call By Reference / Address / Pointer.

Code :

#include <stdio.h>

void  swap( int*, int* );

int  main()

{

       int a = 10, b = 20;

       system( "cls" );

       printf( "Before Swapping (in main) : a = %d, b = %d\n", a, b );

       swap( &a, &b );

       printf( "After Swapping (in main)  : a = %d, b = %d\n", a, b );

       system( "pause" );

       return 0;

}

void  swap( int *pa, int *pb )

{

       int t;

       printf( "Before Swapping (in swap) : *pa = %d, *pb = %d\n", *pa, *pb );

       t = *pa;

       *pa = *pb;

       *pb = t;

       printf( "After Swapping (in swap)  : *pa = %d, *pb = %d\n", *pa, *pb );

}

Output :

![](image_rsrc48F2.jpg)

______________  ****  ______________

Program No. - 316 :

Program to explain Returning By Reference / Address / Pointer.

Code :

#include <stdio.h>

int*  max( int*, int* );

int  main()

{

       int a = 10, b = 20, *p;

       system( "cls" );

       p = max( &a, &b );

       printf( "Maximum = %d\n", *p );

       system( "pause" );

       return 0;

}

int*  max( int *pa, int *pb )

{

       if( *pa > *pb )

              return pa;

       else

              return pb;

}

Output :

![](image_rsrc48F3.jpg)

______________  ****  ______________

Program No. - 317 :

Program for passing Array to function.

Code :

#include <stdio.h>

/* void  display( int* );​*/

void  display( int[ ] );

int  main()

{

       int a[ ] = { 10, 20, 30, 40, 50 };

       system( "cls" );

       display( a );

       printf( "\n" );

       system( "pause" );

       return 0;

}

/* void  display( int *x )​*/

void  display( int x[ ] )

{

       int i;

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", x[ i ] );   ​/*   *( x + i ) ​*/

       }

}

Output :

![](image_rsrc48F4.jpg)

______________  ****  ______________

Program No. - 318 :

Program for passing 2D Array to function.

Code :

#include <stdio.h>

void  display( int[ ][3] );

int  main()

{

       int a[ ][3] = { { 10, 20, 30 },

                                   { 40, 50, 60 } };

       system( "cls" );

       display( a );

       system( "pause" );

       return 0;

}

void  display( int x[ ][3] )

{

       int i, j;

       printf( "Matrix-A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", x[ i ][ j ] );

              }

              printf( "\n" );

       }

}

Output :

![](image_rsrc48F5.jpg)

______________  ****  ______________

Program No. - 319 :

Program for passing String to function.

Code :

#include <stdio.h>

/* void  display( char* );​*/

void  display( char[ ] );

int  main()

{

       char s[ ] = "ATUL";

       system( "cls" );

       display( s );

       system( "pause" );

       return 0;

}

/* void  display( char *s1 )​*/

void  display( char s1[ ] )

{

       int i;

       printf( "%s\n", s1 );

       for( i=0 ; s1[ i ] != '\0' ; i++ )

       {

              printf( "%c\n", s1[ i ] );  ​ ​/*  *( s1 + i )   */

       }

}

Output :

![](image_rsrc48F6.jpg)

______________  ****  ______________

Program No. - 320 :

Program for passing Array of Strings to function.

Code :

#include <stdio.h>

void  display( char[ ][10] );

int  main()

{

       char s[ ][10] = { "Red", "Green", "Blue" };

       system( "cls" );

       display( s );

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  display( char s1[ ][10] )

{

       int i;

       printf( "Colors are :" );

       for( i=0 ; i<3 ; i++ )

       {

              printf( " %s", s1[ i ] );

       }

}

Output :

![](image_rsrc48F7.jpg)

______________  ****  ______________

Program No. - 321 :

Program for passing Array Elements by value to function.

Code :

#include <stdio.h>

void  display( int );

int  main( )

{

       int  i ;

       int  a[ ] = { 10, 20, 30, 40, 50 } ;

       system( "cls" );

       for ( i = 0 ; i< 5 ; i++ )

       {

              display( a[ i ] ) ;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  display( int n )

{

       printf( "  %d", n ) ;

}

Output :

![](image_rsrc48F8.jpg)

______________  ****  ______________

Program No. - 322 :

Program for passing array elements by reference to function.

Code :

#include <stdio.h>

void  display( int* );

int  main( )

{

       int  i ;

       int  a[ ] = { 10, 20, 30, 40, 50 } ;

       system( "cls" );

       for( i = 0 ; i< 5 ; i++ )

       {

              display( &a[ i ] ) ;

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  display( int *p )

{

       printf( "  %d", *p ) ;

}

Output :

![](image_rsrc48F9.jpg)

______________  ****  ______________

Program No. - 323 :

Program to find Factorial of given Number without Recursion.

Code :

#include <stdio.h>

long  fact( long );

int  main()

{

       long n, f;

       system( "cls" );

       printf( "Enter the Number : " );

       scanf( "%ld", &n );

       f = fact( n );

       printf( "\nFactorial = %ld\n", f );

       system( "pause" );

       return 0;

}

long  fact( long a )

{

       long f = 1;

       int i;

       for( i=1 ; i<= a ; i++ )

       {

              f = f * i;

       }

       return f;

}

Output :

![](image_rsrc48FA.jpg)![](image_rsrc48FB.jpg)

______________  ****  ______________

Program No. - 324 :

Program to calculate Factorial using Recursion.

Code :

#include <stdio.h>

long  fact( long );

int  main()

{

       long n, f;

       system( "cls" );

       printf( "Enter any Number : " );

       scanf( "%ld", &n );

       f = fact( n );

       printf( "\nFactorial = %ld\n", f );

       system( "pause" );

       return 0;

}

long  fact( long a )

{

       if( a == 1 )

              return 1;

       else

              return   a * fact( a − 1 );

}

Output :

![](image_rsrc48FC.jpg)

______________  ****  ______________

Program No. - 325 :

Program to find the sum of first n Natural number by recursive function.

Code :

#include <stdio.h>

int  sum( int );

int  main()

{

       int num, s;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &num );

       s = sum( num );

       printf( "\nSum of %d Natural Number = %d\n", num, s );

       system( "pause" );

       return 0;

}

int  sum( int n )

{

       if( n == 1 )

              return 1;

       else

              return  n + sum( n − 1 );

}

Output :

![](image_rsrc48FD.jpg)

______________  ****  ______________

Program No. - 326 :

Program to find nth power of x using Recursion.

Code :

#include <stdio.h>

int  power( int, int );

int  main()

{

       int  x, n, p;

       system( "cls" );

       printf( "Enter the Base : " );

       scanf( "%d", &x );

       printf( "Enter the Exponent/Power : " );

       scanf( "%d", &n );

       p = power( x, n );

       printf( "\nPower = %d\n", p );

       system( "pause" );

       return 0;

}

int  power( int x, int n )

{

       if( n == 0 )

              return 1;

       else

              return  x * power( x, n − 1 );

}

Output :

![](image_rsrc48FE.jpg)

______________  ****  ______________

Program No. - 327 :

Program to find nth term of Fibonacci Series using Recursion.

Code :

#include <stdio.h>

int  fibo( int );

int  main()

{

       int n, t;

       system( "cls" );

       printf( "Enter Term Position : " );

       scanf( "%d", &n );

       t = fibo( n );

       printf( "\n%dth term of Fibonacci series = %d\n", n, t );

       system( "pause" );

       return 0;

}

int  fibo( int n )

{

       if( n == 0 || n == 1 )

              return n;

       else

              return  fibo( n − 1 ) + fibo( n − 2 );

}

Output :

![](image_rsrc48FF.jpg)

______________  ****  ______________

Program No. - 328 :

Program to find nth term of Lucas Series using Recursion.

Code :

#include <stdio.h>

int  lucas( int );

int  main()

{

       int n, t;

       system( "cls" );

       printf( "Enter Term Position : " );

       scanf( "%d", &n );

       t = lucas( n );

       printf( "\n%dth term of Lucas series is = %d\n", n, t );

       system( "pause" );

       return 0;

}

int  lucas( int n )

{

       if( n == 0 || n == 1 || n == 2 )

              return 1;

       else

              return  lucas(n − 1) + lucas(n − 2) + lucas(n − 3);

}

Output :

![](image_rsrc48FG.jpg)

______________  ****  ______________

Program No. - 329 :

Program to find Length of String using function ( Passing String ).

Code :

#include <stdio.h>

int  length( char s[ ] )

{

       int i, l = 0;

       for( i=0 ; s[ i ] != '\0' ; i++ );

       l = i;

       return l;

}

int  main()

{

       int  len = 0;

       char str[50];

       system( "cls" );

       printf( "Enter a String : " );

       gets( str );

       len = length( str );

       printf( "\nLength of the String = %d\n", len );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48FH.jpg)

______________  ****  ______________

Program No. - 330 :

Program to explain Constant Argument to function.

Code :

#include <stdio.h>

void  show( const int );

int  main()

{

       int a = 10;

       system( "cls" );

       show( a );

       printf( "a = %d\n",  a );

       system( "pause" );

       return 0;

}

void  show( const int b )

{

       /*  b = 20; ​*/​​/*  can't be changed.   */

       printf( "b = %d\n", b );

}

Output :

![](image_rsrc48FJ.jpg)

______________  ****  ______________

Program No. - 331 :

Program to explain Function with Constant Argument.

Code :

#include <stdio.h>

const  float  PI = 3.1415926;

float  area( const float r )

{

       return ( PI * r * r );

}

int  main()

{

       float radius, ar;

       system( "cls" );

       printf( "Enter the radius of a Circle : " );

       scanf( "%f", &radius );

       ar = area( radius );

       printf( "\nThe area of circle is %f\n", ar );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48FK.jpg)

______________  ****  ______________

Program No. - 332 :

Program to Return Multiple Values from Function using Reference.

Code :

#include <stdio.h>

void  AreaCircum( float, float*, float* );

int  main()

{

       float radius, area, circum;

       system( "cls" );

       printf( "Enter a Radius : " );

       scanf( "%f", &radius );

       AreaCircum( radius, &area, &circum );

       printf( "\nArea of Circle = %f\n", area );

       printf( "Circumference of Circle = %f\n", circum );

       system( "pause" );

       return 0;

}

void  AreaCircum( float r, float *par, float *pcir )

{

       *par = 3.14 * r * r;

       *pcir = 2 * 3.14 * r;

}

Output :

![](image_rsrc48FM.jpg)

______________  ****  ______________

Program No. - 333 :

Program to Return Multiple Values from Function using call by reference.

Code :

#include <stdio.h>

int  main()

{

       void intfrac( float, float*, float* );

       float number, intpart, fracpart;

       system( "cls" );

       printf( "Enter a Real Number : " );

       scanf( "%f", &number );

       intfrac( number, &intpart, &fracpart );

       printf( "\nInteger part  = %.0f\n", intpart );       

       printf( "Fraction part = %f\n", fracpart );

       system( "pause" );

       return 0;

}

void  intfrac( float n, float *intp, float *fracp )

{

       *intp = (float)( (long)n ) ;

       *fracp = n - *intp;

}

Output :

![](image_rsrc48FN.jpg)

______________  ****  ______________

Program No. - 334 :

Program to explain Nesting of Functions.

Code :

#include <stdio.h>

void  func2();

void  func1()

{

       printf( "function1-1 \n" );

       func2();

       printf( "function1-2 \n" );

}

void  func2()

{

       printf( "function2-1 \n" );

}

int  main()

{

       system( "cls" );

       printf( "main-1 \n" );

       func1();

       printf( "main-2 \n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48FP.jpg)

______________  ****  ______________

Program No. - 335 :

Program to explain Nested function call.

Code :

#include <stdio.h>

int main()

{

       int add( int, int );

       int a = 10, b = 15, s;

       system( "cls" );

       s = add( add(a, b), add(a, b) );

       printf( "Result : %d \n", s );

       system( "pause" );

       return 0;

}

int add( int a, int b )

{

       return ( a + b );

}

Output :

![](image_rsrc48FR.jpg)

______________  ****  ______________

Program No. - 336 :

Program to Find the Number of Permutations without repeatation.

(i.e.,  nPr = n! / (n−r)!.

Code :

#include <stdio.h>

int  fact( int );

int  main()

{

       int n, r, p;

       system( "cls" );

       printf( "Enter Value of n and r : " );

       scanf( "%d %d", &n, &r );

       p = fact( n ) / fact( n − r );

       printf( "\nnPr : %d\n", p );

       system( "pause" );

       return 0;

}

int  fact( int a )

{

       int  i, f=1;

       for( i=1 ; i<=a ; i++ )

       {

              f = f * i;

       }

       return  f;

}

Output :

![](image_rsrc48FS.jpg)

______________  ****  ______________

Program No. - 337 :

Program to Find the Number of Combinations without repeatation.

(i.e.,  nCr = n! / ( r! * (n−r)!).

Code :

#include <stdio.h>

int  fact( int );

int  main()

{

       int n, r, p;

       system( "cls" );

       printf( "Enter Value of n and r : " );

       scanf( "%d %d", &n, &r );

       p = fact( n ) / ( fact( r ) * fact( n − r ) );

       printf( "\nnCr : %d\n", p );

       system( "pause" );

       return 0;

}

int  fact( int a )

{

       int  i, f=1;

       for( i=1 ; i<=a ; i++ )

       {

              f = f * i;

       }

       return  f;

}

Output :

![](image_rsrc48FT.jpg)

______________  ****  ______________

Program No. - 338 :

Program to check​whether a number can be expressed as sum of two prime numbers or not.

Code :

#include <stdio.h>

int main()

{

       int n, i, flag=0;

       system( "cls" );

       printf( "Enter a Number : " );

       scanf( "%d", &n );

       for( i=2 ; i<=n/2 ; i++ )

       {

              if( (isprime( i ) != 0) && (isprime( n−i ) != 0) )

              {

                     printf( "%2d = %2d + %2d\n", n, i, (n−i) );

                     flag = 1;

              }

       }

       if( flag == 0 )

              printf( "%d can not be expressed as sum of two Prime Numbers.\n", n );

       system( "pause" );

       return 0;

}

int  isprime( int n )

{

       int i, flag=1;

       for( i=2 ; i<=n/2 ; i++ )

       {

              if( n % i == 0 )

                     flag = 0;

       }

       return flag;

}

Output :

![](image_rsrc48FU.jpg)![](image_rsrc48FV.jpg)![](image_rsrc48FW.jpg)

______________  ****  ______________

Program No. - 339 :

Program to display Pascal Triangle.

                   1                

                1   1

             1   2   1

          1   3   3   1

       1   4   6   4   1

Code :

#include <stdio.h>

int fact( int );

int main()

{

       int n, i, j, k, t;

       system( "cls" );

       printf( "Enter Number of Rows : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ )

       {

              for( k=0 ; k<(n−i) ; k++ )

              {

                     printf( "  " );

              }

              for( j=0 ; j<=i ; j++ )

              {

                     t = fact( i ) / ( fact( j ) * fact( i – j ) );

                     printf( "   %d", t );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

int fact( int n )

{

       int i, f;

       f = 1;

       for( i=1 ; i<=n ; i++ )

       {

              f *= i;

       }

       return f;

}

Output :

![](image_rsrc48FX.jpg)

______________  ****  ______________

Program No. - 340 :

Program to check whether the given two strings are Anagram Strings or Not.

Code :

#include <stdio.h>

#include <string.h>

void sort_string( char s1[ ] );

int main()

{

       char s1[25] = "silent";

       char s2[25] = "listen";

       int i, j, l;

       system( "cls" );

       printf( "Original String-1 : %s\n", s1 );

       printf( "Original String-2 : %s\n", s2 );

       sort_string( s1 );

       sort_string( s2 );

       if( strcmp(s1, s2) == 0 )

              printf( "\nStrings are Anagram strings.\n" );

       else

              printf( "\nStrings are not Anagram strings.\n" );

       system( "pause" );

       return 0;

}

void sort_string( char s1[ ] )

{

       int i, j, len;

       char ch;

       len = strlen( s1 );

       for( i=0 ; i<len−1 ; i++ )

       {

              for( j=0 ; j<len−1−i ; j++ )

              {

                     if( s1[ j ] > s1[ j+1] )

                     {

                            ch = s1[ j ];

                            s1[ j ] = s1[ j+1];

                            s1[ j+1] = ch;

                     }

              }

       }

}

Output :

![](image_rsrc48FY.jpg)![](image_rsrc48FZ.jpg)

______________  ****  ______________

Program No. - 341 :

Program to check whether the given two strings are Anagram Strings or Not.

Code :

#include <stdio.h>

#include <string.h>

int is_anagram( char s1[ ], char s2[ ] );

int main()

{

       char s1[25] = "silent";

       char s2[25] = "listen";

       int i, j, l;

       system( "cls" );

       printf( "Original String-1 : %s\n", s1 );

       printf( "Original String-2 : %s\n", s2 );

       if( is_anagram(s1, s2) )

              printf( "\nStrings are Anagram strings.\n" );

       else

              printf( "\nStrings are not Anagram strings.\n" );

       system( "pause" );

       return 0;

}

int is_anagram( char s1[ ], char s2[ ] )

{

       char chars1[256] = {0}, chars2[256] = {0};

       int i;

       for( i=0 ; s1[ i ] && s2[ i ] ; i++ )

       {

              chars1[ i ]++;

              chars2[ i ]++;

       }

       if( s1[ i ] || s2[ i ] )

              return 0;

       for( i=0 ; i<256 ; i++ )

       {

               if( chars1[ i ] != chars2[ i ] )

                      return 0;

       }

       return 1;

}

Output :

![](image_rsrc48G0.jpg)![](image_rsrc48G1.jpg)

______________  ****  ______________

Program No. - 342 :

Program to explain Linear Search using Function.

Code :

#include <stdio.h>

int  Lsearch( int ar[ ], int size, int item );

int  main()

{

       int  ar[50], item, n, index, i;

       system( "cls" );

       printf( "Enter Desired Array Size(max. 50) : " );

       scanf( "%d", &n );

       printf( "Enter Array Elements : " );

       for( i=0 ; i<n ; i++)

       {

              scanf( "%d", &ar[ i ] );

       }

       printf( "Enter Element to be searched for : " );

       scanf( "%d", &item );

       index = Lsearch( ar, n, item );

       if( index == −1 )

              printf( "\nSorry!! Element not found.\n" );

       else

       {

              printf( "\nElement found at index : %d", index );

              printf( ", Position : %d\n", ( index + 1 ) );

       }

       system( "pause" );

       return 0;

}

int  Lsearch( int ar[ ], int size, int item )

{

       int  i;

       for( i=0 ; i<size ; i++ )

       {

              if( item == ar[ i ] )

                     return i;

       }

       return  −1;

}

Output :

![](image_rsrc48G2.jpg)![](image_rsrc48G3.jpg)

______________  ****  ______________

Program No. - 343 :

Write a program to SORT a given element of an array in Ascending order using Bubble Sort?

Code :

#include <stdio.h>

#include <conio.h>

void  bubble_sort( int*, int );

int  main()

{

       int a[5] = { 30, 50, 40, 20, 10 };

       int i;

       system( "cls" );

       printf( "Before Sorting : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", a[ i ] );

       }

       bubble_sort( a, 5 );

       printf( "\nAfter Sorting  : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", a[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  bubble_sort( int *p, int n )

{

       int i, j, t;

       for( i=0 ; i<n−1 ; i++ )

       {

              for( j=0 ; j<n−i−1 ; j++ )

              {

                     if( *(p+j) > *(p+j+1) )    /* if( p[ j ] > p[ j+1] ) */

                     {

                            t = *(p+j);​​   /* t = p[ j ];​*/

                            *(p+j) = *(p+j+1);​/* p[ j ] = p[ j+1]; */

                            *(p+j+1) = t;​ ​  /*  p[ j+1] = t;​*/

                     }

              }

       }

}

Output :

![](image_rsrc48G4.jpg)

______________  ****  ______________

Program No. - 344 :

Program to Merge Two Array using Function.

Code :

#include <stdio.h>

void  Merge( int [ ], int, int[ ], int, int[ ] );

int  main()

{

       int A[50], B[50], C[100], MN = 0, M, N, i;

       system( "cls" );

       printf( "Enter Number of Elements in First Array : " );

       scanf( "%d", &M );

       printf( "Enter First Array elements [ASCENDING]: " );

       for( i=0 ; i<M ; i++ )

       {

              scanf( "%d", &A[ i ] );

       }

       printf( "\nEnter Number of Elements in Second Array : " );

       scanf( "%d", &N );

       printf( "Enter Second Array elements [ASCENDING]: " );

       for( i=0 ; i<N ; i++ )

       {

              scanf( "%d", &B[ i ] );

       }

       MN = M + N;

       Merge( A, M, B, N, C );​

       printf( "\nThe Sorted Array After Merging = \n" );

       for( i=0 ; i<MN ; i++ )

       {

              printf( "%d  ", C[ i ] );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  Merge( int A[ ], int M, int B[ ], int N, int C[ ] )

{

       int a, b, c;

       for( a=0, b=0, c=0 ; a<M && b<N ; )

       {

              if( A[a] < B[b] )

                     C[c++] = A[a++];

              else

                     C[c++] = B[b++];

       }

       if( a < M )

       {

              while( a < M )

                     C[c++] = A[a++];

       }

       else

       {

              while( b < N )

                     C[c++] = B[b++];

       }

}

Output :

![](image_rsrc48G5.jpg)

______________  ****  ______________

Program No. - 345 :

Program to explain Local Variable.

Code :

#include <stdio.h>

void localVar();

int main()

{

       system( "cls" );

       int x = 10;

       printf( "x in main() : %d\n", x );

       for( int i=1 ; i<=3 ; i++ )

       {

              localVar();

       }

       printf( "x in main() : %d\n", x );

       system( "pause" );

       return 0;

}

void localVar()

{

       int x = 20;

       printf( "x in localVar() : %d\n", x );

       x++;

       printf( "x in localVar() : %d\n", x );

}

Output :

![](image_rsrc48G6.jpg)

______________  ****  ______________

Program No. - 346 :

Program to explain Global Variable.

Code :

#include <stdio.h>

void globalVar();

int x = 10;

int main()

{

       system( "cls" );

       printf( "x in main() : %d\n", x );

       x++;

       for( int i=1 ; i<=3 ; i++ )

       {

              globalVar();

       }

       x++;

       printf( "x in main() : %d\n", x );

       system( "pause" );

       return 0;

}

void globalVar()

{

       x++;

       printf( "x in globalVar() : %d\n", x );

}

Output :

![](image_rsrc48G7.jpg)

______________  ****  ______________

Program No. - 347 :

Program to explain Static Variable.

Code :

#include <stdio.h>

void staticVar();

int main()

{

       system( "cls" );

       int x = 10;

       printf( "x in main() : %d\n", x );

       for( int i=1 ; i<=3 ; i++ )

       {

              staticVar();

       }

       printf( "x in main() : %d\n", x );

       system( "pause" );

       return 0;

}

void staticVar()

{

       static int x = 20;

       printf( "x in staticVar() : %d\n", x );

       x++;

}

Output :

![](image_rsrc48G8.jpg)

______________  ****  ______________

Program No. - 348 :

Program to explain Local variables.

Code :

#include <stdio.h>

int main()

{

       system( "cls" );

       int a = 10, i;  

       printf( "%d ", a );

       {  

              int a = 200;   

              for( i=0 ; i<3 ; i++ )  

              {  

                     printf( "%d ", a );

              }

       }

       printf( "%d\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48G9.jpg)

______________  ****  ______________

Program No. - 349 :

Program to input multiptle numbers and find average after each input.

Code :

#include <stdio.h>

float avg( float );

int main()

{

       float val = 1, av, i;

       system( "cls" );

       while( val != 0 )

       {

              printf( "Enter a Value ( 0 to exit) : " );

              scanf( "%f", &val );

              if( val == 0 )

                     break;

              av = avg( val );

              printf( "New average : %f\n",av );

       }

       system( "pause" );

       return 0;

}

float avg( float value )

{

       static float sum = 0;

       static int count = 0;

       count++;

       sum += value;

       return (sum / count);

}

Output :

![](image_rsrc48GA.jpg)

______________  ****  ______________

Program No. - 350 :

Program to explain Register variable with it default value.

Code :

#include <stdio.h>

int main()

{

       system( "cls" );

       // Memory : CPU register

       register int a;

       // Default value : 0

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GB.jpg)

______________  ****  ______________

Program No. - 351 :

Program to explain External variable.

Code :

#include <stdio.h>

int a;

int main()

{

       system( "cls" );

       extern int a;

       // Default value : 0   

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GC.jpg)

______________  ****  ______________

Chapter − 11

Structure, Union  &  Enum

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 352 :

Program to explain Simple Structure.

Code :

#include <stdio.h>

/* Global Structure  */

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct Distance d1;

       system( "cls" );

       d1.feet = 12;

       d1.inches = 9.5;

       printf( "Feet   : %d\n", d1.feet );

       printf( "Inches : %f\n", d1.inches );

​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GD.jpg)

______________  ****  ______________

Program No. - 353 :

Program to input Structure elements.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct Distance d1;

       system( "cls" );

       printf( "Enter feet : " );

       scanf( "%d", &d1.feet );

       printf( "Enter inches : " );

       scanf( "%f", &d1.inches );

       printf( "\nFeet   : %d\n",  d1.feet );

       printf( "Inches : %f\n",  d1.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GE.jpg)

______________  ****  ______________

Program No. - 354 :

Program to explain Global Structure with Global and Local structure variable.

Code :

#include <stdio.h>

/* ​Global Structure​*/

struct  Distance

{

       int feet;

       float inches;

};

struct  Distance d1; ​​/*   Global variable​*/

int  main()

{

       struct Distance d2; ​​/*   Local variable   */

       system( "cls" );

       d1.feet = 12;

       d1.inches = 9.5;

       d2.feet = 15;

       d2.inches = 3.5;

       printf( "%d\'-%f\" \n", d1.feet, d1.inches );

       printf( "%d\'-%f\" \n", d2.feet, d2.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GF.jpg)

______________  ****  ______________

Program No. - 355 :

Program to explain Local Structure with Local structure variable.

Code :

#include <stdio.h>

int  main()

{

       /*  Local Structure​*/

       struct  Distance

       {

              int feet;

              float inches;

       }d1;

       struct  Distance d2; ​​/*  Local variable  */

       system( "cls" );

       d1.feet = 12;

       d1.inches = 9.5;

       d2.feet = 15;

       d2.inches = 3.5;

       printf( "%d\'-%f\" \n", d1.feet, d1.inches );

       printf( "%d\'-%f\" \n", d2.feet, d2.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GG.jpg)

______________  ****  ______________

Program No. - 356 :

Program to use Multiple Structure Variables.

Code :

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct  Distance d1, d2;

       system( "cls" );

       d1.feet = 12;

       d1.inches = 9.5;

       /*   Reading Distance from Keyboard.​*/

       printf( "Enter feet : " );

       scanf( "%d", &d2.feet );

       printf( "Enter inches : " );

       scanf( "%f", &d2.inches );

       printf( "%d\'-%f\" \n", d1.feet, d1.inches );

       printf( "%d\'-%f\" \n", d2.feet, d2.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GH.jpg)

______________  ****  ______________

Program No. - 357 :

Program to Initialize Structure Variable and expain Structure Assignment.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct Distance d1 = { 15, 6.5 };

       struct Distance d2, d3;

       system( "cls" );

       /*   Element-wise Assignment.​*/

       d2.feet = d1.feet;

       d2.inches = d1.inches;

       /*   Structure Variable Assignment.   */

       d3 = d1;

       printf( "d1 = %d\'-%f\" \n", d1.feet, d1.inches );

       printf( "d2 = %d\'-%f\" \n", d2.feet, d2.inches );

       printf( "d3 = %d\'-%f\" \n", d3.feet, d3.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GJ.jpg)

______________  ****  ______________

Program No. - 358 :

Program to explain the Anonymous Structure( without tagname ).

Code :

#include <stdio.h>

//  Structure without Tag name

struct

{

       int feet;

       float inches;

}d1, d2 = { 15, 6.5 };

int  main()

{

       system( "cls" );

       d1.feet = 12;

       d1.inches = 9.5;

       printf( "d1 : %d\'-%.1f\" \n", d1.feet, d1.inches );

       printf( "d2 : %d\'-%.1f\" \n", d2.feet, d2.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GK.jpg)

______________  ****  ______________

Program No. - 359 :

Program to explain the element-wise comparison of structure variable.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

} d1, d2 = { 15, 6.5 };

int  main()

{

       system( "cls" );

       d1.feet = 15;

       d1.inches = 6.5;

       if( ( d1.feet == d2.feet ) && ( d1.inches == d2.inches ) )

              printf( "(d1 == d2)\n" );

       else

              printf( "(d1 != d2)\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48GM.jpg)

______________  ****  ______________

Program No. - 360 :

Program to.create and use a simple rectangle structure.

Code :

#include <stdio.h>

struct rectangle

{

       int  l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1;

       r1.l = 10;

       r1.b = 5;

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GN.jpg)

______________  ****  ______________

Program No. - 361 :

Program to.input data of rectangle structure.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1;

       printf( "Enter length & breadth : " );

       scanf( "%d %d", &r1.l, &r1.b );

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GP.jpg)

______________  ****  ______________

Program No. - 362 :

Program to initialize rectangle structure.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1 = { 10, 8 };

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GR.jpg)

______________  ****  ______________

Program No. - 363 :

Program to.create structure variables with rectangle structure definition.

Code :

#include <stdio.h>

struct rectangle

{

      int l, b;

} r1, r2;

int main()

{

       system( "cls" );

       r1.l = 10;

       r1.b = 5;

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GS.jpg)

______________  ****  ______________

Program No. - 364 :

Program to.create structure variables with nameless structure definition.

Code :

#include <stdio.h>

/* nameless structure */

struct

{

       int l, b;

} r1, r2;

int main()

{

       system( "cls" );

       r1.l = 10;

       r1.b = 5;

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GT.jpg)

______________  ****  ______________

Program No. - 365 :

Program to use typedef for alias to the rectangle structure.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

typedef struct rectangle rect;

int main()

{

       system( "cls" );

       rect r1;

       r1.l = 10;       

       r1.b = 5;

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GU.jpg)

______________  ****  ______________

Program No. - 366 :

Program to typedef for alias with rectangle structure definition.

Code :

#include <stdio.h>

typedef struct rectangle

{

       int l, b;

} rect;

int main()

{

       system( "cls" );

       rect r1;

       r1.l = 10;

       r1.b = 5;

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GV.jpg)

______________  ****  ______________

Program No. - 367 :

Program to initialize structure variable with rectangle structure definition.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

} r1 = { 20, 10 };

int main()

{

       system( "cls" );

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GW.jpg)

______________  ****  ______________

Program No. - 368 :

Program to explain named initialization of structure variable.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1 = { .b = 10, .l = 20 };

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48GX.jpg)

______________  ****  ______________

Program No. - 369 :

Program to initialize a structure variable with another structure variable.

Code :

#include <stdio.h>

struct rectangle

{

      int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1 = { 20, 10 };

       struct rectangle r2 = r1;  

       printf( "length = %d\n", r2.l );

       printf( "breadth = %d\n", r2.b );

       system( "pause" );

}

Output :

![](image_rsrc48GY.jpg)

______________  ****  ______________

Program No. - 370 :

Program to assign a structure variable to another structure variable.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1 = { 20, 10 };

       struct rectangle r2;

       r2 = r1;  

       printf( "length = %d\n", r2.l );

       printf( "breadth = %d\n", r2.b );

       system( "pause" );

}

Output :

![](image_rsrc48GZ.jpg)

______________  ****  ______________

Program No. - 371 :

Program to Add Two Structure Variables.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct Distance d1, d3;

       struct Distance d2 = { 12, 6.5 };

       system( "cls" );

       printf( "Enter feet   : " );

       scanf( "%d", &d1.feet );

       printf( "Enter inches : " );

       scanf( "%f", &d1.inches );

       d3.feet = d1.feet + d2.feet;

       d3.inches = d1.inches + d2.inches;

       if( d3.inches >= 12.0 )

       {

              d3.inches −= 12.0;

              d3.feet++;

       }

       printf( "\n%d\'-%.2f\"", d1.feet, d1.inches );

       printf( " + %d\'-%.2f\"", d2.feet, d2.inches );

       printf( " = %d\'-%.2f\" \n", d3.feet, d3.inches );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48H0.jpg)

______________  ****  ______________

Program No. - 372 :

Program to explain Array of Structure.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

int  main()

{

       struct  Distance d[5];

       int i;

       system( "cls" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Enter Feet & Inches : " );

              scanf( "%d %f", &d[ i ].feet, &d[ i ].inches );

       }

       for( i=0 ; i<5 ; i++ )

       {

              printf( "%d\'-%f\" \n", d[ i ].feet, d[ i ].inches );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48H1.jpg)

______________  ****  ______________

Program No. - 373 :

Program to explain Array within Structure.

Code :

#include <stdio.h>

struct  Student

{

       int rno;

       char name[25];

       float marks[5];

};

int  main()

{

       int i;

       struct  Student s;

       system( "cls" );

       printf( "Enter Roll Number : " );

       scanf( "%d", &s.rno );

       printf( "Enter Name : " );

       fflush( stdin );

       gets( s.name );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Enter Marks-%d : ", ( i+1 ) );

              scanf( "%f", &s.marks[ i ] );

       }

​

       printf( "\nRoll Number : %d\n", s.rno );

       printf( "Name : %s\n", s.name );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Marks-%d : %f\n", (i+1), s.marks[ i ] );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48H2.jpg)

______________  ****  ______________

Program No. - 374 :

Program to explain the concept of Array within Structure & Array of Structure.

Code :

#include <stdio.h>

struct  Student

{

       int rno;

       char name[25];

       float marks[5];

};

int  main()

{

       struct  Student s[10];

       int i, j, n;

       system( "cls" );

       printf( "Enter Number of student : " );

       scanf( "%d", &n );

       for( i=0 ; i<n ; i++ )

       {

              printf( "Enter Roll Number : " );

              scanf( "%d", &s[ i ].rno );​

              fflush( stdin );

              printf( "Enter Name : " );

              gets( s[ i ].name );

              for( j=0 ; j<5 ; j++ )

              {

                     printf( "Enter marks-%d : ", (j+1) );

                     scanf( "%f", &s[ i ].marks[ j ] );

              }

       }

       printf( "\n%5s %−15s %7s %7s %7s %7s %7s", "R.No.", "Name", "M-1", "M-2", "M-3", "M-4", "M-5" );

       for( i=0 ; i<n ; i++ )

       {

              printf( "\n%−5d", s[ i ].rno );

              printf( " %−15s", s[ i ].name );

              for( j=0 ; j<5 ; j++ )

              {

                     printf( " %7.2f", s[ i ].marks[ j ] );

              }

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48H3.jpg)

______________  ****  ______________

Program No. - 375 :

Program to pass a structure variable to function as pass by value.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

void show( struct rectangle );

int main()

{

       system( "cls" );

       struct rectangle r1 = { 20, 10 };

       show( r1 );

       system( "pause" );

}

void show( struct rectangle r )

{

       printf( "length = %d\n", r.l );

       printf( "breadth = %d\n", r.b );

}

Output :

![](image_rsrc48H4.jpg)

______________  ****  ______________

Program No. - 376 :

Program to pass a structure variable to function as pass by address/pointer.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

void show( struct rectangle* );

int main()

{

       system( "cls" );

       struct rectangle r1 = { 20, 10 };

       show( &r1 );

       system( "pause" );

}

void show( struct rectangle *p )

{

       printf( "length = %d\n", p−>l );

       printf( "breadth = %d\n", p−>b );

}

Output :

![](image_rsrc48H5.jpg)

______________  ****  ______________

Program No. - 377 :

Program to pass a structure variable to function as pass by address/pointer.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

void show( struct rectangle* );

int main()

{

       system( "cls" );

       struct rectangle r1 = { 20, 10 };

       show( &r1 );

       system( "pause" );

}

void show( struct rectangle *p )

{

       printf( "length = %d\n", (*p).l );

       printf( "breadth = %d\n", (*p).b );

}

Output :

![](image_rsrc48H6.jpg)

______________  ****  ______________

Program No. - 378 :

Program to initialize structure variable using function.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

void init( struct rectangle* );

int main()

{

       system( "cls" );

       struct rectangle r1;

       init( &r1 );

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

void init( struct rectangle *p )

{

       p−>l = 10;

       p−>b = 5;

}

Output :

![](image_rsrc48H7.jpg)

______________  ****  ______________

Program No. - 379 :

Program to input structure variable using function.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

void init( struct rectangle* );

int main()

{

       system( "cls" );

       struct rectangle r1;

       init( &r1 );

       printf( "length = %d\n", r1.l );

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

void init( struct rectangle *p )

{

       printf( "Enter length & breadth : " );

       scanf( "%d %d", &p−>l, &p−>b );

}

Output :

![](image_rsrc48H8.jpg)

______________  ****  ______________

Program No. - 380 :

Program to pass Structure Variable to Function.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

void  display( struct Distance d )

{

       printf( "Distance = %d\'-%f\" \n", d.feet, d.inches );

}

int  main()

{

       struct  Distance d1;

       struct  Distance d2;

       system( "cls" );

       printf( "Enter feet and inches : " );

       scanf( "%d %f", &d1.feet, &d1.inches );

       // Structure Variable Assignment.

       d2 = d1;

       display( d1 );

       display( d2 );

       system( "pause" );​

       return 0;

}

Output :

![](image_rsrc48H9.jpg)

______________  ****  ______________

Program No. - 381 :

Program to Pass Structure Variable to Function.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

void  display( struct Distance d )

{

       printf( "Distance = %d\'-%f\" \n", d.feet, d.inches );

}

void  add_dist( struct Distance, struct Distance );

int  main()

{

       struct Distance d1;

       struct Distance d2;

       system( "cls" );

       printf( "Enter feet and inches : " );

       scanf( "%d %f", &d1.feet, &d1.inches );

       printf( "Enter feet and inches : " );

       scanf( "%d %f", &d2.feet, &d2.inches );

       display( d1 );

       display( d2 );​

       add_dist( d1, d2 );

       system( "pause" );

       return 0;

}

void  add_dist( struct Distance dd1, struct Distance dd2 )

{

       struct Distance dd3;

       dd3.feet = dd1.feet + dd2.feet;

       dd3.inches = dd1.inches + dd2.inches;

       if( dd3.inches >= 12.0 )

       {

              dd3.inches −= 12.0;

              dd3.feet++;

       }

       display( dd3 );

}

Output :

![](image_rsrc48HA.jpg)

______________  ****  ______________

Program No. - 382 :

Program to Return Structure Variable from Function.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

void  display( struct Distance d )

{

       printf( "Distance = %d\'-%f\" \n", d.feet, d.inches );

}

struct  Distanceadd_dist( struct Distance, struct Distance );

int  main()

{

       struct Distance d1, d2, d3;

       system( "cls" );

       printf( "Enter feet and inches : " );

       scanf( "%d %f", &d1.feet, &d1.inches );

       printf( "Enter feet and inches : " );

       scanf( "%d %f", &d2.feet, &d2.inches );

       display( d1 );

       display( d2 );​

       d3 = add_dist( d1, d2 );

       display( d3 );

       system( "pause" );

       return 0;

}

struct  Distanceadd_dist( struct Distance dd1, struct Distance dd2 )

{

       struct  Distance dd3;

       dd3.feet = dd1.feet + dd2.feet;

       dd3.inches = dd1.inches + dd2.inches;

       if( dd3.inches >= 12.0 )

       {

              dd3.inches −= 12.0;

              dd3.feet++;

       }

       return  dd3;

}

Output :

![](image_rsrc48HB.jpg)

______________  ****  ______________

Program No. - 383 :

Program to explain Nested Structure.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

struct  Room

{

       struct Distance length;

       struct Distance width;

};

int  main()

{

       float  l, w, a;

       struct  Room drawing = { { 15, 6.0 }, { 12, 9.0 } };

       system( "cls" );

       l = drawing.length.feet + drawing.length.inches / 12.0;

       w = drawing.width.feet + drawing.width.inches / 12.0;

       a = l * w;

       printf( "Area of Drawing Room = %.2f square feet.\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HC.jpg)

______________  ****  ______________

Program No. - 384 :

Program to explain the concept of Nested Structure ( Structure within Structure ).

Code :

#include <stdio.h>

struct  Room

{

       struct  Dist

       {

              int feet;

              float inches;

       }l, b;

};

int  main()

{

       struct  Room  dr;

       float l1, b1, a;

       system( "cls" );

       dr.l.feet = 15;

       dr.l.inches = 6.0;

       dr.b.feet = 12;

       dr.b.inches = 9.0;

       l1 = dr.l.feet + ( dr.l.inches / 12.0 );

       b1 = dr.b.feet + ( dr.b.inches / 12.0 );

       a = l1 * b1;

       printf( "Area of Drawing Room = %.3f sq. ft.\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HD.jpg)

______________  ****  ______________

Program No. - 385 :

Program to create Book Structure.

Code :

#include <stdio.h>

struct  Book

{

       char name[25];

       char author[20];

       float price;

};

int  main()

{

       struct  Book b;

       system( "cls" );

       printf( "Enter the Name of Book : " );

       gets( b.name );

       printf( "Enter the Author's Name : " );

       gets( b.author );

       printf( "Enter the Price of the book : " );

       scanf( "%f", &b.price );

       printf( "\nName of the Book   : %s\n", b.name );

       printf( "Author of the Book : %s\n", b.author );

       printf( "Price of the Book  : %f\n", b.price );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HE.jpg)

______________  ****  ______________

Program No. - 386 :

Program to explain String within Structure.

Code :

#include <stdio.h>

struct  Book

{

       char name[25];

       int page;

       int price;

};

int  main()

{

       int i;

       struct  Book b1[3];

       system( "cls" );

       for( i=0 ; i<3 ; i++ )

       {

              printf( "Enter Name of Book : " );​

              fflush( stdin );

              gets( b1[ i ].name );

              printf( "Enter Number of Pages : " );

              scanf( "%d", &b1[ i ].page );

              printf( "Enter Price of Book : " );

              scanf( "%d", &b1[ i ].price );

       }

       for( i=0 ; i<3 ; i++ )

       {

              printf( "\nName of Book  = %s\n", b1[ i ].name );

              printf( "Number of Page = %d\n", b1[ i ].page ); ​

              printf( "Price of Book  = %d\n",  b1[ i ].price );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HF.jpg)

______________  ****  ______________

Program No. - 387 :

Program to Pass Structure Variable to Function by Reference / Address / Pointer.

Code :

#include <stdio.h>

struct  Distance

{

       int feet;

       float inches;

};

void  scale( struct Distance*, float );

void  display( struct Distance );

int  main()

{

       struct Distance d1 = { 12, 6.0 };

       struct Distance d2 = { 10, 6.0 };

       system( "cls" );

       printf( "Dist1 = " );

       display( d1 );

       printf( "Dist2 = " );

       display( d2 );

       scale( &d1, 0.5 );

       scale( &d2, 0.25 );

       printf( "\nDist1 = " );

       display( d1 );

       printf( "Dist2 = " );

       display( d2 );

       system( "pause" );

       return 0;

}

void  scale( struct Distance *p, float factor )

{

       float inches = ( p−>feet * 12 + p−>inches ) * factor;

       p−>feet = inches / 12;

       p−>inches = inches − ( p−>feet * 12 );

}

void  display( struct Distance dd )

{

       printf( "%d\'-%.2f\"\n", dd.feet, dd.inches );

}

Output :

![](image_rsrc48HG.jpg)

______________  ****  ______________

Program No. - 388 :

Program to explain bit-field with structure.

Code :

#include <stdio.h>

/* bit field*/

struct test

{

       unsigned int a : 4;

       unsigned int b : 4;

       unsigned int c : 10;

} t1;

int main()

{

       system( "cls" );

       struct test t2;

       t1.a = 5;

       t1.b = 10;

       t1.c = 200;

       printf( "t1.a = %d\n", t1.a );

       printf( "t1.b = %d\n", t1.b );

       printf( "t1.c = %d\n", t1.c );

       printf( "sizeof(t1) = %d\n", sizeof(t1) );

       system( "pause" );

}

Output :

![](image_rsrc48HH.jpg)

______________  ****  ______________

Program No. - 389 :

Program to explain Enum.

Code :

#include <stdio.h>

enum  days_of_week { SUN, MON, TUE, WED, THU, FRI, SAT };

int  main()

{

       enum  days_of_week day1, day2;

       int diff;

       system( "cls" );

       day1 = MON;

       day2 = THU;

       diff = day2 − day1;

       printf( "Days between day1 & day2 = %d\n", diff );

       if( day1 < day2 )

              printf( "Day1 comes before Day2.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HJ.jpg)

______________  ****  ______________

Program No. - 390 :

Program to show an Enumeration type ( enum ).

Code :

#include <stdio.h>

enum  Colors { Red, Green, Blue };

int  main()

{

       enum  Colors c1, c2;

       int d;

       system( "cls" );

       c1 = Red;

       c2 = Green;

       d = c2 − c1;

       printf( "Difference = %d\n", d );

       if( c1 < c2 )

              printf( "RED comes before GREEN.\n" );

       else

              printf( "GREEN comes before RED.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HK.jpg)

______________  ****  ______________

Program No. - 391 :

Program to show an Enumeration type ( enum ).

Code :

#include <stdio.h>

enum  Colors { Red=10, Green, Blue };

int  main()

{

       enum  Colors c1, c2;

       int d;

       system( "cls" );

       c1 = Red;

       c2 = Blue;

       printf( "c1 = %d\n", c1 );

       printf( "c2 = %d\n", c2 );

       d = c2 − c1;

       printf( "Difference = %d\n", d );

       if( c1 < c2 )

              printf( "RED comes before GREEN.\n" );

       else

              printf( "GREEN comes before RED.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HM.jpg)

______________  ****  ______________

Program No. - 392 :

Program to show an Enumeration type ( enum ).

Code :

#include <stdio.h>

enum  Colors { Red=10, Green=20, Blue=30 };

int  main()

{

       enum  Colors c1, c2;

       int d;

       system( "cls" );

       c1 = Red;

       c2 = Blue;

       printf( "c1 = %d\n", c1 );

       printf( "c2 = %d\n", c2 );

       d = c2 − c1;

       printf( "Difference = %d\n", d );

       if( c1 < c2 )

              printf( "RED comes before GREEN.\n" );

       else

              printf( "GREEN comes before RED.\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HN.jpg)

______________  ****  ______________

Program No. - 393 :

Program to explain Union.

Code :

#include <stdio.h>

union  Abc

{

       char c;

       int i;

       float f;

};

int  main()

{

       union Abc x;

       system( "cls" );

       x.c = 'A';

       printf( "x.c = %c\n", x.c );

       x.i = 100;

       printf( "x.i = %d\n", x.i );

       x.f = 123.45;

       printf( "x.f = %f\n", x.f );

       system( "pause" );

}

Output :

![](image_rsrc48HP.jpg)

______________  ****  ______________

Program No. - 394 :

Program to differentiate Structure and Union.

Code :

#include <stdio.h>

union  ABC

{

       char a;

       int b;

       float c;

};

struct  XYZ

{

       char x;

       int y;

       float z;

};

int  main()

{

       union  ABC p;

       struct  XYZ q;

       system( "cls" );

       printf( "Size of Structure : %d\n", sizeof( struct XYZ ) );

       q.x = 'A';

       q.y = 100;

       q.z = 12.345;

        printf( "q.x = %c\nq.y = %d\nq.z = %f\n", q.x, q.y, q.z );

       printf( "\nSize of Union : %d\n", sizeof( union ABC ) );

       p.a = 'C';

       printf( "p.a : %c\n", p.a );

       p.b = 100;

       printf( "p.b : %d\n", p.b );

       p.c = 12.345;

       printf( "p.c : %f\n", p.c );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HR.jpg)

______________  ****  ______________

Program No. - 395 :

Program to explain the use of pointer to structure.

Code :

#include <stdio.h>

int  main()

{

       struct  date

       {

              int dd, mm, yy;

       }dt = { 5, 4, 2022 };

       struct  date *ptr;

       system( "cls" );

       ptr = &dt;

       printf( "Using Structure Variable :\n" );

       printf( "dd = %d, mm = %d, yy = %d\n", dt.dd, dt.mm, dt.yy );

       printf( "\nUsing Structure Pointer  :\n" );

       printf( "dd = %d, mm = %d, yy = %d\n", ptr−>dd, ptr−>mm, ptr−>yy );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HS.jpg)

______________  ****  ______________

Program No. - 396 :

Program to explain Nested Structure by employee structure.

Code :

#include <stdio.h>

struct  address

{

       char  phone[15] ;

       char  city[25] ;

       long  pin ;

} ;

struct  emp

{

       char  name[25] ;

       struct  addressadr ;

} ;

int  main()

{

       struct  emp  e = { "Harsh", "099999888888", "Bhilai", 490006 };

       system( "cls" ) ;

       printf( "Name = %s  \nPhone = %s\n", e.name, e.adr.phone ) ;

       printf( "City = %s \nPin = %ld\n", e.adr.city, e.adr.pin ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HT.jpg)

______________  ****  ______________

Program No. - 397 :

Program to explain the concept of Passing Structure by Reference to function by Book Structure example.

Code :

#include <stdio.h>

struct  book

{

       char  name[25] ;

       char  author[25] ;

       float  price;

} ;

void  display( struct book  *b );

int  main()

{

       struct  book  b1 = { "C Programming", "Atul", 500.00 } ;

       system( "cls" );

       display ( &b1 ) ;

       system( "pause" );

       return 0;

}

void  display( struct book  *b )

{

       printf( "Book Name: %s\n", b−>name );

       printf( "Author   : %s\n", b−>author );

       printf( "Price    : %.2f\n", b−>price ) ;

}

Output :

![](image_rsrc48HU.jpg)

______________  ****  ______________

Program No. - 398 :

Program to explain the use of user-defined Type Declaration ( typedef ).

Code :

#include <stdio.h>

struct  book

{

       char  name[25];

       char  author[25];

       float  price;

};

typedef  struct  book BOOK;

void  display( BOOK  *b );

int  main()

{

       BOOK b1 = { "C Programming", "Atul", 500.00 } ;

       system( "cls" );

       display( &b1 ) ;

       system( "pause" );

       return 0;

}

void  display( BOOK  *b )

{

       printf( "Book Name: %s\n", b−>name );

       printf( "Author   : %s\n", b−>author );

       printf( "Price    : %.2f\n", b−>price ) ;

}

Output :

![](image_rsrc48HV.jpg)

______________  ****  ______________

Chapter − 12

Pointers

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 399 :

Program to explain simple use of Pointer.

Code :

#include <stdio.h>

int  main()

{

       int a = 10;

       int * p;

       system( "cls" );

       p = &a;

       printf( "a = %d\n", a );

       printf( "&a = %u\n", &a );

       printf( "p = %u\n", p );

       printf( "*p = %d\n", *p );

       printf( "&p = %u\n", &p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HW.jpg)

______________  ****  ______________

Program No. - 400 :

Program to explain that a pointer can point differnt variable at different point of time.

Code :

#include <stdio.h>

int  main()

{

       int a = 10, b = 20, c = 30;

       int * p;

       system( "cls" );

       p = &a;

       printf( "*p = %d\n", *p );

       p = &b;

       printf( "*p = %d\n", *p );

       p = &c;

       printf( "*p = %d\n", *p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HX.jpg)

______________  ****  ______________

Program No. - 401 :

Program to explain that a pointer can point differnt variable at different point of time.

Code :

#include <stdio.h>

int  main()

{

       int a = 10;

       int *p1, *p2, *p3;

       system( "cls" );

       p1 = &a;

       p2 = &a;

       p3 = &a;

       printf( "*p1 = %d\n", *p1 );

       printf( "*p2 = %d\n", *p2 );

       printf( "*p3 = %d\n", *p3 );

       *p2 = 50;

       printf( "*p1 = %d\n", *p1 );

       printf( "*p2 = %d\n", *p2 );

       printf( "*p3 = %d\n", *p3 );

       *p3 = *p1 + *p2;

       printf( "*p1 = %d\n", *p1 );

       printf( "*p2 = %d\n", *p2 );

       printf( "*p3 = %d\n", *p3 );​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HY.jpg)

______________  ****  ______________

Program No. - 402 :

Program to explain new format spacifier %p for address of variable, i.e. pointer.

Code :

#include <stdio.h>

int  main()

{

       int a = 10;

       int *ptr = &a;

       system( "cls" );

       printf( "a : %d\n", *ptr );

       printf( "&a : %p\n", ptr );

       printf( "&a : %u\n", ptr );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48HZ.jpg)

______________  ****  ______________

Program No. - 403 :

Program to calculate Volume of cylinder by using pointer.

Code :

#include <stdio.h>

int  main()

{

       float r, h, v;

       float *pr, *ph, *pv;

       const float PI = 3.14;

       system( "cls" );

       pr = &r;

       ph = &h;

       pv = &v;

       printf( "Enter Radius & Height : " );

       scanf( "%f %f", pr, ph );

       *pv = PI * (*pr) * (*pr) * (*ph);

       printf( "\nVolume of Cylinder = %f\n", *pv );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48J0.jpg)

______________  ****  ______________

Program No. - 404 :

Program to explain array of pointers.

Code :

#include <stdio.h>

int  main()

{

       int a = 10, b = 20, c = 30;

       int *p[3], *t;

       int i;

       system( "cls" );

       p[0] = &a;

       p[1] = &b;

       p[2] = &c;

       printf( "Values are : " );

       for( i=0 ; i<3 ; i++ )

       {

              printf( "  %d", *p[ i ] );

       }

       t = p[0];

       p[0] = p[2];

       p[2] = t;

       printf( "\nValues are : " );

       for( i=0 ; i<3 ; i++ )

       {

              printf( "  %d", *p[ i ] );

       }​

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48J1.jpg)

______________  ****  ______________

Program No. - 405 :

Program to explain array and  pointers.

Code :

#include <stdio.h>

int  main()

{

       int a[ ] = { 10, 20, 30, 40, 50 };

       int *p;

       int i;

       system( "cls" );

       p = &a[0];​​/*   p = a;  */

       printf( "Array Elements are (a[i])  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", a[ i ] );

       }

       printf( "\nArray Elements are (i[a])  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", i[a] );

       }

       printf( "\nArray Elements are (*(a+i)):" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *( a + i ) );

       }

       printf( "\nArray Elements are (*(p+i)):" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *( p + i ) );

       }

       printf( "\nArray Elements are (p[i])  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", p[ i ] );

       }

       printf( "\nArray Elements are (*p++)  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *p++ );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48J2.jpg)

______________  ****  ______________

Program No. - 406 :

Program to pass Array to Function using Pass by Pointer.

Code :

#include <stdio.h>

void  display( int* );

int  main()

{

       int a[ ] = { 10, 20, 30, 40, 50 };

       system( "cls" );

       display( a );

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  display( int *p )

{

       int i;

       printf( "Array Elements are :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *( p + i ) );

       }

}

Output :

![](image_rsrc48J3.jpg)

______________  ****  ______________

Program No. - 407 :

Program to pass a Character Array (String) by Pointer.

Code :

#include <stdio.h>

void  display( char* );

int  main()

{

       char s[ ] = "Atul Kumar Soni";

       system( "cls" );

       display( s );

       system( "pause" );

       return 0;

}

void  display( char *ps )

{

       printf( "String : %s\n", ps );

}

Output :

![](image_rsrc48J4.jpg)

______________  ****  ______________

Program No. - 408 :

Program to explain Pass by Value.

Code :

#include <stdio.h>

void  square( int  );

int  main()

{

       int a = 10;

       system( "cls" );

       square( a );

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

void  square( int  x )

{

       x = x * x;

       printf( "x = %d\n", x );

}

Output :

![](image_rsrc48J5.jpg)

______________  ****  ______________

Program No. - 409 :

Program to explain Pass by Reference / Address / Pointer.

Code :

#include <stdio.h>

void  square( int* );

int  main()

{

       int a = 10;

       system( "cls" );

       square( &a );

       printf( "a = %d\n", a );

       system( "pause" );

       return 0;

}

void  square( int *pa )

{

       *pa = *pa * *pa;

       printf( "*pa = %d\n", *pa );

}

Output :

![](image_rsrc48J6.jpg)

______________  ****  ______________

Program No. - 410 :

Program to explain Returning by reference ( returning by pointer ).

Code :

#include <stdio.h>

int*  max( int*, int* );

int  main()

{

       int a = 10, b = 20, *p;

       system( "cls" );

       p = max( &a, &b );

       printf( "Maximum = %d\n", *p );

       system( "pause" );

       return 0;

}

int*  max( int *pa, int *pb )

{

       if( *pa > *pb )

              return pa;

       else

              return pb;

}

Output :

![](image_rsrc48J7.jpg)

______________  ****  ______________

Program No. - 411 :

Program to pass a string by pointer.

Code :

#include <stdio.h>

void  display( char* );

int  main()

{

       char a[ ] = "INDIA";

       system( "cls" );

       display( a );       

       printf( "\n" );

       system( "pause" );

       return 0;

}

void  display( char *p )

{

       int i;

       printf( "String : " );

       for( i=0 ; *(p+i) != '\0' ; i++ )

       {

              printf( " %c", *( p + i ) );

       }

}

Output :

![](image_rsrc48J8.jpg)

______________  ****  ______________

Program No. - 412 :

Program to explain Pointer and 2-D Array.

Code :

#include <stdio.h>

int  main()

{

       int a[2][3] = { { 10, 20, 30 },

                                    { 40, 50, 60 } };

       int *p;

       int i, j;

       system( "cls" );

       printf( "Matrix-A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", *( *( a + i ) + j ) );

              }

              printf( "\n" );

       }

       printf( "\nMatrix-A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", *( a[ i ] + j ) );

              }

              printf( "\n" );

       }

       p = &a[0][0];

       printf( "\nMatrix-A : \n" );

       for( i=0 ; i<2 ; i++ )

       {

              for( j=0 ; j<3 ; j++ )

              {

                     printf( "  %d", *( p + 3 * i + j ) );

              }

              printf( "\n" );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48J9.jpg)

______________  ****  ______________

Program No. - 413 :

Program to explain Pointer to Function.

Code :

#include <stdio.h>

void  Add( int, int );

void  Sub( int, int );

int  main()

{

       int a = 10, b = 20;

       void (*pf)( int, int );

       system( "cls" );​

       pf = Add;       

       (*pf)( a, b );​​/*  Add( a, b );  */

       pf = Sub;       

       (*pf)( a, b );​​/*  Sub( a, b );  */

       system( "pause" );

       return 0;

}

void  Add( int x, int y )

{

       int s;

       s = x + y;

       printf( "Sum = %d\n", s );

}

void  Sub( int x, int y )

{

       int d;

       d = x − y;

       printf( "Difference = %d\n", d );

}

Output :

![](image_rsrc48JA.jpg)

______________  ****  ______________

Program No. - 414 :

Program to explain Chain of Pointers.

Code :

#include <stdio.h>

int  main()

{

       int a = 10;

       int *p, **pp, ***ppp, ****pppp;

       system( "cls" );

       p = &a;

       printf( "p = %u\n", p );

       printf( "*p = %d\n", *p );

       pp = &p;

       printf( "\npp = %u\n", pp );

       printf( "*pp = %u\n", *pp );

       printf( "**pp = %d\n", **pp);

       ppp = &pp;

       printf( "\nppp = %u\n", ppp );

       printf( "*ppp = %u\n", *ppp );

       printf( "**ppp = %u\n", **ppp );

       printf( "***ppp = %d\n", ***ppp );

       pppp = &ppp;

       printf( "\npppp = %u\n", pppp );

       printf( "*pppp = %u\n", *pppp );

       printf( "**pppp = %u\n", **pppp );

       printf( "***pppp = %u\n", ***pppp );

       printf( "****pppp = %d\n", ****pppp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JB.jpg)

______________  ****  ______________

Program No. - 415 :

Program to explain Pointer to structure.

Code :

#include <stdio.h>

struct rectangle

{

       int l, b;

};

int main()

{

       system( "cls" );

       struct rectangle r1;

       struct rectangle *p;

       p = &r1;

       p−>l = 10;

       p−>b = 5;

       printf( "length = %d\n", r1.l );       

       printf( "breadth = %d\n", r1.b );

       system( "pause" );

}

Output :

![](image_rsrc48JC.jpg)

______________  ****  ______________

Program No. - 416 :

Write a program to SORT a given element of an array in Ascending order using Bubble Sort?

Code :

#include <stdio.h>

int  main()

{

       int a[5] = { 30, 50, 40, 20, 10 };

       int i, j, t;

       int *p;

       system( "cls" );

       p = a;​​/* p = &p[0];   */

       printf( "Before Sorting :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *( p + i ) );

       }

       for( i=0 ; i<5−1 ; i++ )

       {

              for( j=0 ; j<5−1−i ; j++ )

              {

                     if( *( p + j ) > *( p + j + 1 ) )

                     {

                            t = *( p + j );

                            *( p + j ) = *( p + j + 1 );

                            *( p + j + 1 ) = t;

                     }

              }

       }

       printf( "\n\nAfter Sorting  :" );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "  %d", *( p + i ) );

       }

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JD.jpg)

______________  ****  ______________

Chapter – 13

Dynamic  Memory  Allocation

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 417 :

Program to explain Dynamic Memory Management.

Code :

#include <stdio.h>

#include <stdlib.h>

int  main()

{

       int *p;

       system( "cls" );

       p = ( int* ) malloc( 1 * sizeof( int ) );

       *p = 10;

       printf( "Value : %d\n",  *p );

       free( p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JE.jpg)

______________  ****  ______________

Program No. - 418 :

Program to explain Dynamic Memory Management.

Code :

#include <stdio.h>

#include <stdlib.h>

int  main()

{

       int *p;

       system( "cls" );

       p = ( int* ) calloc( 1,  sizeof( int ) );

       *p = 10;

       printf( "Value : %d\n",  *p );

       free( p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JF.jpg)

______________  ****  ______________

Program No. - 419 :

Program to explain Dynamic Memory  Allocation for String.

Code :

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

int  main()

{

       char s1[25] = "Atul Kumar Soni";

       int len = strlen( s1 );

       char *ps;

       system( "cls" );

       ps = ( char* ) malloc( ( len + 1 ) * sizeof( char ) );

       strcpy( ps, s1 );

       printf( "ps = %s\n",  ps );

       free( ps );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JG.jpg)

______________  ****  ______________

Program No. - 420 :

Program to explain Dynamic Memory Management for Array.

Code :

#include <stdio.h>

#include <stdlib.h>

int  main()

{

       int *p;

       int i;

       system( "cls" );

       p = ( int* ) malloc( 5 * sizeof( int ) );

       for( i=0 ; i<5 ; i++ )

       {

              printf( "Enter Value : " );

              scanf( "%d", ( p + i ) );

       }

       printf( "\nValues are : " );

       for( i=0 ; i<5 ; i++ )

       {

              printf( " %d", *( p + i ) );

       }

       free( p );

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JH.jpg)

______________  ****  ______________

Program No. - 421 :

Program to use malloc( ) function.

Code :

#include <stdio.h>

#include <malloc.h>

int  main()

{

       int *p;

       int i, n, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       p = (int *) malloc( n * sizeof( int ) );

       if( !p )

              printf( "\nUnable to allocate size. \n" );

       else

       {

              for( i=0 ; i<n ; i++ )

              {

                     printf( "Enter Value : " );

                     scanf( "%d", ( p + i ) );

              }

              printf( "\nValues are : " );

              s = 0;

              for( i=0 ; i<n ; i++ )

              {

                     printf( "  %d", *( p + i ) );

                     s = s + *( p + i );

              }

              printf( "\nSum of elements = %d\n", s );

       }

       free( p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JJ.jpg)

______________  ****  ______________

Program No. - 422 :

Program to use calloc( ) function.

Code :

#include <stdio.h>

#include <malloc.h>

int  main()

{

       int *p;

       int i, n, s;

       system( "cls" );

       printf( "Enter Number of Terms : " );

       scanf( "%d", &n );

       p = (int *)calloc( n, sizeof( int ) );

       if( ! p )

              printf( "\nUnable to allocate size.\n" );

       else

       {

              for( i=0 ; i<n ; i++ )

              {

                     printf( "Enter Value : " );

                     scanf( "%d", ( p + i ) );

              }

              printf( "\nValues are : " );

              s = 0;

              for( i=0 ; i<n ; i++ )

              {

                     printf( "  %d", *( p + i ) );

                     s = s + *( p + i );

              }

              printf( "\nSum of Elements = %d\n", s );

       }

       free( p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JK.jpg)

______________  ****  ______________

Program No. - 423 :

Program to use realloc( ) function.

Code :

#include <stdio.h>

#include <malloc.h>

#include <stdlib.h>​​/*  #include <process.h>​*/

int  main()

{

       int *p;

       int i, x, n, s;

       system( "cls" );

       printf( "Enter Size of Dynamic Array : " );

       scanf( "%d", &n );

       p = (int *)malloc(n * sizeof( int ) );

       if( ! p )

              printf( "\nUnable to allocate size.\n" );

       else

       {

              for( i=0 ; i<n ; i++ )

              {

                     printf( "Enter Value : " );

                     scanf( "%d", ( p + i ) );

              }

              printf( "\nValues are : " );

              s = 0;

              for( i=0 ; i<n ; i++ )

              {

                     printf( "  %d", *( p + i ) );

                     s = s + *( p + i );

              }

              printf( "\nSum of Elements = %d", s );

              x = n;

              printf( "\n\nEnter New Size of Dynamic Array : " );

              scanf( "%d", &n );

              realloc( p, n * sizeof( int ) );

              if( !p )

              {

                      printf( "\nUnable to allocate size.\n" );

                      exit( 1 );

              }

              for( i=x ; i<n ; i++ )

              {

                     printf( "Enter Additional Value : " );

                     scanf( "%d", ( p + i ) );

              }

              printf( "\nValues are : " );

              s = 0;

              for( i=0 ; i<n ; i++ )

              {

                     printf( "  %d", *( p + i ) );

                     s = s + *( p + i );

              }

              printf( "\nSum of elements = %d\n", s );

        }

       free( p );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JM.jpg)

______________  ****  ______________

Chapter − 14

Preprocessors

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 424 :

Program to explain Simple Macro Substitution( #define ).

Code :

#include <stdio.h>

#define   PI  3.14159

int  main()

{

       system( "cls" );

       printf( "Value of PI : %f\n",  PI );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JN.jpg)

______________  ****  ______________

Program No. - 425 :

Program to explain Simple Macro Substitution( #define ).

Code :

#include <stdio.h>

#define  PI  3.14159

int  main()

{

       float r, a;

       system( "cls" );

       printf( "Enter Radius : " );

       scanf( "%f", &r );

       a = PI * r * r;

       printf( "Area of Circle : %f\n",  a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JP.jpg)

______________  ****  ______________

Program No. - 426 :

Program to use Macro Substitution with Arguments.

Code :

#include <stdio.h>

#define  MIN(a,b)  (((a)<(b))?a:b)

int  main()

{

       int x, y;

       system( "cls" );

       x = 10;

       y = 20;

       printf( "Minimum = %d\n",  MIN(x, y) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JR.jpg)

______________  ****  ______________

Program No. - 427 :

Program to explain Nested Macro Substitution.

Code :

#include <stdio.h>

#define   PI   3.14159

#define   Volume(r)   (4.0/3.0)*PI*(r)*(r)*(r)

int  main()

{

       float r, v;

       system( "cls" );

       printf( "Enter Radius of Sphere : " );

       scanf( "%f", &r );

       v = Volume( r );

       printf( "\nVolume of Sphere : %f\n",  v );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JS.jpg)

______________  ****  ______________

Program No. - 428 :

Program to Swap two numbers using #define preprocessor.

Code :

#include <stdio.h>

#define  SWAP(a,b)  {int temp; temp=a; a=b; b=temp;}

int  main()

{

       int x, y;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       scanf( "%d %d", &x, &y );

       printf( "x : %d, y : %d\n", x, y );

       SWAP( x, y );

       printf( "x : %d, y : %d\n", x, y );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JT.jpg)

______________  ****  ______________

Program No. - 429 :

Program to use #include Preprocessor.

Code [ myheader.h ] :

//  Save this file as “myheader.h” in current directory.

int  add( int x, int y)

{

       int s;

       s = x + y;

       return s;

}

int  sub( int x, int y)

{

       int d;

       d = x − y;

       return d;

}

Code :

//  Save this file with .cpp file extension.

#include <stdio.h>

#include "myheader.h"

int  main()

{

       int a = 20, b = 10, res;

       system( "cls" );

       res = add( a, b );

       printf( "Sum = %d\n",  res );

       res = sub( a, b );

       printf( "Difference = %d\n",  res );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JU.jpg)

______________  ****  ______________

Program No. - 430 :

Program to create user-defined header file use it in the program.

Code [ myfile.h ] :

int square( int n )

{

       int r;

       r = n * n;

       return r;

}

Code :

#include <stdio.h>

#include "myfile.h"

int  main()

{

       int s, n = 10;

       system( "cls" );

       s = square( n );

       printf( "Square : %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JV.jpg)

______________  ****  ______________

Program No. - 431 :

Program to include user-defined Header file using Absolute Path.

Code [ d:\myfile.h ] :

int square( int n )

{

       int r;

       r = n * n;

       return r;

}

Code :

#include <stdio.h>

#include "d:\myfile.h"  ​​// absolute path

int  main()

{

       int s, n = 10;

       system( "cls" );

       s = square( n );

       printf( "Square : %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JW.jpg)

______________  ****  ______________

Program No. - 432 :

Program to include user-defined Header file using Relative Path.

Code [ .\CPrograms\myfile.h ] :

int square( int n )

{

       int r;

       r = n * n;

       return r;

}

Code :

#include <stdio.h>

#include ".\CPrograms\myfile.h"  ​  // relative path

int  main()

{

       int s, n = 10;

       system( "cls" );

       s = square( n );

       printf( "Square : %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JX.jpg)

______________  ****  ______________

Program No. - 433 :

Program to include user-defined Header file using Relative Path.

Code [ ..\myfile.h ] :

int square( int n )

{

       int r;

       r = n * n;

       return r;

}

Code :

#include <stdio.h>

#include "..\myfile.h "  ​​// relative path

int  main()

{

       int s, n = 10;

       system( "cls" );

       s = square( n );

       printf( "Square : %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48JY.jpg)

______________  ****  ______________

Program No. - 434 :

Program to use Compiler Control Directives ( #if and #endif ).

Code :

#include <stdio.h>

#define  INDIA  1

// #define  USA  1

#if( defined  INDIA )

       #define  PI   3.14159

#endif

#if( defined USA )

       #define   PI   3.14

#endif

int  main()

{

       float r, a;

       system( "cls" );

       printf( "Enter Radius : " );

       scanf( "%f", &r );

       a = PI * r * r;

       printf( "\nArea of Circle : %f\n",  a );

       system( "pause" );

       return 0;

}

Output ( If INDIA defined ):

![](image_rsrc48JZ.jpg)

Output ( If USA defined ):

![](image_rsrc48K0.jpg)

______________  ****  ______________

Program No. - 435 :

Program to use Compiler Control Directives ( #ifdef and #endif ).

Code :

#include <stdio.h>

#define  INDIA  1

// #define  USA  1

#ifdef  INDIA​

       #define  PI   3.14159

#endif

#ifdef  USA

       #define   PI   3.14

#endif

int  main()

{

       float r, a;

       system( "cls" );

       printf( "Enter Radius : " );

       scanf( "%f", &r );

       a = PI * r * r;

       printf( "\nArea of Circle : %f\n", a );

       system( "pause" );

       return 0;

}

Output ( If INDIA defined ):

![](image_rsrc48JZ.jpg)

Output ( If USA defined ):

![](image_rsrc48K0.jpg)

______________  ****  ______________

Program No. - 436 :

Program to use Compiler Control Directives ( #ifndef and #endif ).

Code :

#include <stdio.h>

#define  INDIA  1

// #define  USA  1

#ifndef   USA

       #define  PI   3.14159

#endif

#ifndef   INDIA

       #define   PI   3.14

#endif

int  main()

{

       float r, a;

       system( "cls" );

       printf( "Enter Radius : " );

       scanf( "%f", &r );

       a = PI * r * r;

       printf( "\nArea of Circle : %f\n",  a );

       system( "pause" );

       return 0;

}

Output ( If USA not defined ):

![](image_rsrc48JZ.jpg)

Output ( If INDIA not defined ):

![](image_rsrc48K0.jpg)

______________  ****  ______________

Program No. - 437 :

Program to use #define Preprocessor.

Code :

#include <stdio.h>

#define pf printf

#define sf scanf

int  main()

{

       int a, b, s;

       system( "cls" );

       pf( "Enter Two Numbers : " );

       sf( "%d %d", &a, &b );

       s = a + b;

       pf( "\nSum = %d\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K1.jpg)

______________  ****  ______________

Program No. - 438 :

Program to use Compiler Control Directives ( #undef ).

Code :

#include <stdio.h>

#define  VAL  40

#ifdef   VAL

       #undef  VAL

#endif

#define  VAL  50     

int  main()

{

       system( "cls" );

       printf( "Value = %d\n",  VAL );  

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K2.jpg)

______________  ****  ______________

Program No. - 439 :

Program to use Compiler Control Directives ( #if ).

Code :

#include <stdio.h>

#define  MAX  1

int  main()

{

       int a = 10, b = 20;

       system( "cls" );

       #if  MAX == 1

              printf( "Maximum = %d\n",  (a>b?a:b) );

       #else

              printf( "Minimum = %d\n",  (a<b?a:b) );

       #endif

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K3.jpg)

______________  ****  ______________

Program No. - 440 :

Program to use #line Preprocessor & __LINE__, __DATE__, __TIME__.

Code :

#include <stdio.h>

int  main()        

{                     

       system( "cls" );

       #line 101

       printf( "Line No.: %d\n", __LINE__ );

       #line 201

       printf( "Line No.: %d\n", __LINE__ );

       printf( "Current Date: %s\n", __DATE__ );

       printf( "Current Time: %s\n", __TIME__ );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K4.jpg)

______________  ****  ______________

Program No. - 441 :

Program to use Macro Continuation Operator (\) and Stringizing Operator (#).

Code :

#include <stdio.h>

#define  message(a, b)  \

​printf( "Learn " #a " and " #b "\n")

int  main()

{

       system( "cls" );

       message( C, C++ );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K5.jpg)

______________  ****  ______________

Program No. - 442 :

Program to use Stringizing( # ) Operator.

Code :

#include <stdio.h>

#define  MKSTR(x)  #x

int  main()

{

       system( "cls" );

       printf( "\n%s\n", MKSTR(Atul Kumar Soni) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K6.jpg)

______________  ****  ______________

Program No. - 443 :

Program to use Token Pasting( ## ) Operator.

Code :

#include <stdio.h>

#define  concat(a,b)  a##b

int  main()

{

       int  xy = 100;

       system( "cls" );

       printf( "Value : %d\n",  concat(x, y) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K7.jpg)

______________  ****  ______________

Chapter – 15

Input / Output  Formatting

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 444 :

Program to find ASCII value of given character.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a Char : " );

       ch = getchar();

       printf( "\nASCII code of %c = %d\n", ch, ch );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K8.jpg)

______________  ****  ______________

Program No. - 445 :

Program to use getchar() and putchar() function.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       printf( "Enter a Char : " );

       ch = getchar();

       putchar( ch );

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48K9.jpg)

______________  ****  ______________

Program No. - 446 :

Program to print integer value inside a string.

Code :

#include <stdio.h>

int  main()

{

       int num;

       system( "cls" );

       num = 100;

       printf( "\nnum =  %d\n", num );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KA.jpg)

______________  ****  ______________

Program No. - 447 :

Program to use calculation inside the printf() statement.

Code :

#include <stdio.h>

int  main()

{

       int length, width, height;

       system( "cls" );

       printf( "Enter length : " );

       scanf( "%d", &length );

       printf( "Enter width : " );

       scanf( "%d", &width );

       printf( "Enter height : " );

       scanf( "%d", &height );

       printf( "\nVolume = %d\n", ( length * width * height ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KB.jpg)

______________  ****  ______________

Program No. - 448 :

Program to use integer literal inside printf() statement.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Integer Literal = %d\n", 100 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KC.jpg)

______________  ****  ______________

Program No. - 449 :

Program to input a integer using scanf().

Code :

#include <stdio.h>

int  main()

{

       int n;

       system( "cls" );

       printf( "Enter a Number : ");

       scanf( "%d", &n );

       printf( "\nSquare of Number is = %d\n", (n * n) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KD.jpg)

______________  ****  ______________

Program No. - 450 :

Program to print literals of different data types using printf().

Code :

#include <stdio.h>

int  main()

{

       char c;

       int i;

       long l;

       long longll;

       float f;

       double d;

       long double ld;

       system( "cls" );

       c = 'A';

       i = 10;

       l = 100L;

       ll = 1000LL;

       f = 12.34f;

       d = 12.34;

       ld = 12.34;

       printf( "c = %c\n", c );

       printf( "i = %d\n", i );

       printf( "l = %ld\n", l );

       printf( "ll = %lld\n", ll );

       printf( "\nf = %f\n", f );

       printf( "d = %lf\n", d );

       printf( "ld = %Lf\n", ld );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KE.jpg)

______________  ****  ______________

Program No. - 451 :

Program to use decimal, octal and hexadecimal integer values in C program.

Code :

#include <stdio.h>

int  main()

{

       int dec = 12;

       int oct = 015;

       int hex = 0x2F;

       system( "cls" );

       printf( "dec : %d\n", dec );

       printf( "oct : %o\n", oct );

       printf( "dec(oct) : %d\n", oct );

       printf( "hex : %x\n", hex );

       printf( "dec(hex) : %d\n", hex );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KF.jpg)

______________  ****  ______________

Program No. - 452 :

Program to explain the use of escape sequence ( \0 ) in printf().

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Atul\0 Kumar Soni" );

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KG.jpg)

______________  ****  ______________

Program No. - 453 :

Program to use escape sequences ( backslash characters ).

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "Red\nGreen\nBlue\n" );

       printf( "Red\tGreen\tBlue\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KH.jpg)

______________  ****  ______________

Program No. - 454 :

Program to input single word string using scanf().

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%s", str );

       printf( "\nString : %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KJ.jpg)

______________  ****  ______________

Program No. - 455 :

Program to display string literal using puts().

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       puts( "Atul" );

       puts( "Kumar" );

       puts( "Soni" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KK.jpg)

______________  ****  ______________

Program No. - 456 :

Program to display string variable using puts().

Code :

#include <stdio.h>

int  main()

{

       char str[25] = "Atul Kumar Soni";

       system( "cls" );

       puts( str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KM.jpg)

______________  ****  ______________

Program No. - 457 :

Program to using getchar() and putchar() to input and display a single character.

Code :

#include <stdio.h>

int  main()

{

       char ch;

       system( "cls" );

       ch = getchar();

       putchar( ch );

​

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KN.jpg)

______________  ****  ______________

Program No. - 458 :

Program to input multiple integer using scanf().

Code :

#include <stdio.h>

int  main()

{

       int a, b, c;

       system( "cls" );

       printf( "Enter Two Numbers : " );

       c = scanf( "%d%d", &a, &b );

       printf( "\nNumber of Inputs = %d\n", c );

       printf( "a = %d\nb = %d\n", a, b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KP.jpg)

______________  ****  ______________

Program No. - 459 :

Program to input a integer in hexadecimal format using scanf().

Code :

#include <stdio.h>

int  main()

{

       int n;

       system( "cls" );

       printf( "Enter a Hex Number : " );

       scanf( "%x", &n );

       printf( "\nDecimal Equivalent = %d\n", n );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KR.jpg)

______________  ****  ______________

Program No. - 460 :

Program to input and display different types of integer values.

Code :

#include <stdio.h>

int  main()

{

       unsigned int u;

       long l;

       short int s;

       system( "cls" );

       printf( "Enter an Unsigned : " );

       scanf( "%u", &u );

       printf( "Enter a Long : " );

       scanf( "%ld", &l );

       printf( "Enter a Short : " );

       scanf( "%hd", &s );

       printf( "\nUnsigned Number = %u\n", u );

       printf( "Long Number = %ld\n", l );

       printf( "Short Number = %hd\n", s );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KS.jpg)

______________  ****  ______________

Program No. - 461 :

Program to input two three digits integer values using scanf().

Code :

#include <stdio.h>

int  main()

{

       int a, b;

       system( "cls" );

       printf( "Enter Two 3-digit Numbers : ");

       scanf( "%3d %3d", &a, &b );

       printf( "\na = %d\n", a );

       printf( "b = %d\n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KT.jpg)

______________  ****  ______________

Program No. - 462 :

Program to input multiple word string using gets().

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter String : " );

       gets( str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KU.jpg)

______________  ****  ______________

Program No. - 463 :

Program to use gets() function in different way.

Code :

#include <stdio.h>

int  main()

{

       char str[25], *p;

       system( "cls" );

       printf( "Enter a String : " );

       p = gets( str );

       if( p ) ​​/* if not null */

       {

              printf( "\n%s\n", str );

              printf( "%s\n", p );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KV.jpg)

______________  ****  ______________

Program No. - 464 :

Program to input single word string using scanf().

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%s", str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KW.jpg)

______________  ****  ______________

Program No. - 465 :

Program to input a string maximum 15 characters.

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter a String : " );

       scanf( "%15s", str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KX.jpg)

______________  ****  ______________

Program No. - 466 :

Program to input a string that contain only Alphabets.

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter Letters only : " );

       scanf( "%[a-zA-Z]", str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KY.jpg)

______________  ****  ______________

Program No. - 467 :

Program to input a string that contain Alphabets with space.

Code :

#include <stdio.h>

int  main()

{

       char str[25];

       system( "cls" );

       printf( "Enter Letters and Space : " );

       scanf( "%[a-zA-Z ]", str );

       printf( "\nString = %s\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48KZ.jpg)

______________  ****  ______________

Program No. - 468 :

Program to use expression directly in printf().

Code :

#include <stdio.h>

int  main()

{

       float radius = 10.0f;

       const float PI = 3.14159f;

       system( "cls" );

       printf( "Circumference = %.2f\n", ( 2.0f * PI * radius ) );

       printf( "Area = %.2f\n", ( PI * radius * radius ) );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M0.jpg)

______________  ****  ______________

Program No. - 469 :

Program to use printf() for integer formatting.

Code :

#include <stdio.h>

int  main()

{

       int a = 123;

       long b = 987654;

       system( "cls" );

       printf( "|%7d|\n", a );

       printf( "|%−7d|\n", a );

       printf( "|%07d|\n", a );

       printf( "|%2d|\n", a );

       printf( "\n|%10ld|\n", b );

       printf( "|%−10ld|\n", b );

       printf( "|%010ld|\n", b );

       printf( "|%3ld|\n", b );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M1.jpg)

______________  ****  ______________

Program No. - 470 :

Program to use printf() for integer formatting.

Code :

#include <stdio.h>

int main()

{

       system( "cls" );

       printf( "%4d\n", 1 );

       printf( "%4d\n", 12 );

       printf( "%4d\n", 123 );

       printf( "%4d\n", 1234 );

       printf( "%4d\n\n", 12345 );

       printf( "%4d\n", -1 );

       printf( "%4d\n", -12 );

       printf( "%4d\n", -123 );

       printf( "%4d\n", -1234 );

       printf( "%4d\n", -12345 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M2.jpg)

______________  ****  ______________

Program No. - 471 :

Program to use different format specifiers for floating-point values.

Code :

#include <stdio.h>

int  main()

{

       float x = 123.45f;

       system( "cls" );

       printf( "x : %f", x );

       printf( "\nx : %g", x );

       printf( "\nx : %e\n", x );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M3.jpg)

______________  ****  ______________

Program No. - 472 :

Program to use printf() for floating-point formatting.

Code :

#include <stdio.h>

int  main()

{

       float a = 987.654;

       system( "cls" );

       printf( "|%12.4f|\n", a );

       printf( "|%12.2f|\n", a );

       printf( "|%−12.4f|\n", a );

       printf( "|%−12.2f|\n", a );

       printf( "|%f|\n", a );

       printf( "\n|%12.4e|\n", a );

       printf( "|%12.2e|\n", a );

       printf( "|%−12.4e|\n", a );

       printf( "|%−12.2e|\n", a );

       printf( "|%e|\n", a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M4.jpg)

______________  ****  ______________

Program No. - 473 :

Program to use printf() for floating-point formatting.

Code :

#include <stdio.h>

int  main()

{

       float a = 987.654;

       system( "cls" );

       printf( "|%*.*f|\n", 12, 4, a );

       printf( "|%−*.*f|\n", 12, 4, a );

       printf( "\n|%*.*e|\n", 12, 4, a );

       printf( "|%−*.*e|\n", 12, 4, a );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M5.jpg)

______________  ****  ______________

Program No. - 474 :

Program to explain Floating-point formatting.

Code :

#include <stdio.h>

int  main()

{

       system( "cls" );

       printf( "%.2f\n", 123.2999353210643 );

       printf( "%.3f\n", 123.2999353210643 );

       printf( "%.4f\n", 123.2999353210643 );

       printf( "%.5f\n", 123.2999353210643 );

       printf( "%.10f\n", 123.2999353210643 );

       printf( "%.12f\n", 123.2999353210643 );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M6.jpg)

______________  ****  ______________

Program No. - 475 :

Program to use printf() for string formatting.

Code :

#include <stdio.h>

int  main()

{

       char str[25] = "Atul Kumar Soni";

       system( "cls" );

       printf( "|%25s|\n", str );

       printf( "|%−25s|\n", str );

       printf( "|%25.10s|\n", str );

       printf( "|%−25.10s|\n", str );

       printf( "|%.4s|\n", str );

       printf( "|%10s|\n", str );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M7.jpg)

______________  ****  ______________

Chapter − 16

File  Handling

______________  ****  ______________

![](image_rsrc483H.jpg)

Program No. - 476 :

Program to write char values to File using putc() or fputc() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char ch;

       system( "cls" );

       fp = fopen( "demo", "w" );

       printf( "Enter String ( ctrl+z to end ) : " );

       ch = getchar();

       while( ch != EOF )

       {

              putc( ch, fp );​​/*  ​fputc( ch, fp );   ​*/

              ch = getchar();

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M8.jpg)

______________  ****  ______________

Program No. - 477 :

Program to read char values from File using getc() or fgetc() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char ch;

       system( "cls" );

       fp = fopen( "demo", "r" );

       printf( "String : " );

       ch = getc( fp );​​/*  ch = fgetc( fp );   */

       while( ch != EOF )

       {

              printf( "%c", ch );

              ch = getc( fp );​/*  ch = fgetc( fp );   */

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48M9.jpg)

______________  ****  ______________

Program No. - 478 :

Program to write integer values to File using putw() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       int n;

       system( "cls" );

       fp = fopen( "demo1", "w" );

       while( 1 )

       {

              printf( "Enter Number ( −1 to end ) : " );

              scanf( "%d", &n );

              if( n == −1 )

                     break;

              putw( n, fp );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MA.jpg)

______________  ****  ______________

Program No. - 479 :

Program to read integer values from File using getw() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       int n;

       system( "cls" );

       fp = fopen( "demo1", "r" );

       printf( "Numbers are :" );

       n = getw( fp );

       while( n != EOF )

       {

              printf( "  %d", n );

              n = getw( fp );

       }

       fclose( fp );

       printf( "\n" );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MB.jpg)

______________  ****  ______________

Program No. - 480 :

Program to write string to File using fputs() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char s[50];

       system( "cls" );

       fp = fopen( "demo2", "w" );

       printf( "Enter String : " );

       gets( s );

       fputs( s, fp );

       fputs( "\n", fp );

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MC.jpg)

______________  ****  ______________

Program No. - 481 :

Program to read string values from File using fgets() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char s[50];

       system( "cls" );

       fp = fopen( "demo2", "r" );

       printf( "String = " );

       fgets( s, 50, fp );

       printf( "%s", s );

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MD.jpg)

______________  ****  ______________

Program No. - 482 :

Program to write multiple lines of text to File using fputs() function..

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char s[50];

       system( "cls" );

       fp = fopen( "demo2", "w" );

       printf( "Enter Lines of Text : \n" );

       gets( s );

       while( strlen( s ) > 0 )

       {

              fputs( s, fp );

              fputs( "\n", fp );

              gets( s );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48ME.jpg)

______________  ****  ______________

Program No. - 483 :

Program to read multiple lines of text from file using fgets() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char s[50];

       system( "cls" );

       fp = fopen( "demo2", "r" );

       printf( "Strings are : \n" );

       fgets( s, 50, fp );

       while( ! feof( fp ) )

       {

              printf( "%s", s );

              fgets( s, 50, fp );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MF.jpg)

______________  ****  ______________

Program No. - 484 :

Program to write different types of values to File using fprintf() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       int rno = 101;

       char name[50] = "Animesh";

       float marks = 92.5;

       system( "cls" );

       fp = fopen( "test", "w");

       fprintf( fp, "%d %s %f\n", rno, name, marks );

       printf( "Details saved in file.\n" );

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MG.jpg)

______________  ****  ______________

Program No. - 485 :

Program to read different types of values from File using fscanf() function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       int rno;

       char name[50];

       float  marks;

       system( "cls" );

       fp = fopen( "test", "r" );

       fscanf( fp, "%d %s %f", &rno, name, &marks );

       printf( "Details from file : \n" );

       printf( "Roll No. : %d\n", rno );

       printf( "Name     : %s\n", name );

       printf( "Marks    : %.2f\n", marks );

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MH.jpg)

______________  ****  ______________

Program No. - 486 :

Program to use getc() & putc() function with console (stdin & stdout).

Code :

#include <stdio.h>

int  main()

{

       char  ch ;

       system( "cls" ) ;

       printf( "Enter String( ctrl+z to end ):\n" );

       while( ( ch = getc ( stdin ) ) != EOF )

       {

              putc( ch, stdout ) ;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MJ.jpg)

______________  ****  ______________

Program No. - 487 :

Program to write structure variable to File using fwrite() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "wb" );

       printf( "Enter Roll No. : " );

       scanf( "%d", &s.rno );

       printf( "Enter Name : " );

       fflush( stdin );

       gets( s.name );

       printf( "Enter Marks : " );

       scanf( "%f", &s.marks );

       fwrite( &s, sizeof( s ), 1, fp );

       fclose( fp ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MK.jpg)

______________  ****  ______________

Program No. - 488 :

Program to read structure variable from File using fread() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "rb" );

       fread( &s, sizeof( s ), 1, fp );

       printf( "Roll No.    : %d\n", s.rno );

       printf( "Enter Name  : %s\n", s.name );

       printf( "Enter Marks : %.2f\n", s.marks );

       fclose( fp ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MM.jpg)

______________  ****  ______________

Program No. - 489 :

Program to write structure variable to File using fprintf() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "w" );

       printf( "Enter Roll No. : " );

       scanf( "%d", &s.rno );

       printf( "Enter Name : " );

       fflush( stdin );

       gets( s.name );

       printf( "Enter Marks : " );

       scanf( "%f", &s.marks );

       fprintf( fp, "%d %s %f\n", s.rno, s.name, s.marks );

       fclose( fp ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MN.jpg)

______________  ****  ______________

Program No. - 490 :

Program to read structure variable from File using fscanf() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "r" );

       fscanf( fp, "%d %s %f", &s.rno, s.name, &s.marks );

       printf( "Roll No.: %d\n", s.rno );

       printf( "Name  : %s\n", s.name );

       printf( "Marks : %.2f\n", s.marks );

       fclose( fp ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MP.jpg)

______________  ****  ______________

Program No. - 491 :

Program to write structure variables to File using fprintf() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       char another = 'Y';

       struct student s;

       system( "cls" );

       fp = fopen( "students", "w" ) ;

       while( another == 'Y' || another == 'y' )

       {

              printf( "Enter Roll No, Name & Marks : " );

              scanf( "%d %s %f", &s.rno, s.name, &s.marks );

              fprintf( fp, "%d %s %f\n", s.rno, s.name, s.marks );

              printf( "Add another record (Y/N) : " );       

              fflush( stdin );

              another = getche( );

              printf( "\n" );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MR.jpg)

______________  ****  ______________

Program No. - 492 :

Program to read structure variables from File using fscanf() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "r" );

       while( fscanf( fp, "%d %s %f", &s.rno, s.name, ​&s.marks ) != EOF )

       {

              printf( "\nRoll No.    : %d\n", s.rno );

              printf( "Enter Name  : %s\n", s.name );

              printf( "Enter Marks : %.2f\n", s.marks );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MS.jpg)

______________  ****  ______________

Program No. - 493 :

Program to write structure variables to File using fwrite() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main()

{

       FILE *fp;

       char another = 'Y';

       struct student s;

       system( "cls" );

       fp = fopen( "students", "wb" ) ;

       while( another == 'Y' || another == 'y' )

       {

              printf( "Enter Roll No, Name & Marks : " );

              scanf( "%d %s %f", &s.rno, s.name, &s.marks );

              fwrite( &s, sizeof( s ), 1, fp );

              printf( "Add another record (Y/N) : " );

              fflush( stdin );

              another = getche( );

              printf( "\n" );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MT.jpg)

______________  ****  ______________

Program No. - 494 :

Program to read structure variables from File using fread() function.

Code :

#include <stdio.h>

struct  student

{

       int rno;

       char name[50];

       float marks;

};

int  main( )

{

       FILE *fp;

       struct student s;

       system( "cls" );

       fp = fopen( "students", "rb" );

       while( fread( &s, sizeof( s ), 1, fp ) == 1 )

       {

              printf( "\nRoll No.: %d\n", s.rno );

              printf( "Name  : %s\n", s.name );

              printf( "Marks : %.2f\n", s.marks );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MU.jpg)

______________  ****  ______________

Program No. - 495 :

Program to use Error Handling function fopen().

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       int n;

       system( "cls" );

       fp = fopen( "demo1", "r" );

       if( fp == NULL )

       {

              printf( "File can not open.\n" );

       }

       else

       {

              printf( "File is opened.\n" );

       }

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MV.jpg)

______________  ****  ______________

Program No. - 496 :

Program to use Error-handling function fopen( ) to check whether the given file is open or not.

Code :

#include <stdio.h>

#include <process.h>

int  main()

{

       FILE  *fp ;

       system( "cls" );

       fp = fopen( "text.txt", "r" ) ;

       if ( fp == NULL )

       {

              puts( "Unable to Open File." ) ;

              system( "pause" );

              exit( 1 ) ;

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MW.jpg)

______________  ****  ______________

Program No. - 497 :

Program to use Error-handling functions feof( ) and ferror( ) while reading data from file.

Code :

#include <stdio.h>

int  main()

{

       FILE  *fp ;

       char  ch ;

       system( "cls" ) ;

       fp = fopen( "demo", "r" ) ;

       while( !feof ( fp ) )

       {

              ch = fgetc( fp ) ;

              if( ferror( fp ) )

              {

                     printf( "Error in Reading File.\n" ) ;

                     break ;

              }

              else

                      printf( "%c", ch ) ;

       }

       fclose( fp ) ;

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MX.jpg)

______________  ****  ______________

Program No. - 498 :

Program to use Random access function fseek( ), ftell( ) and rewind( ) function.

Code :

#include <stdio.h>

int  main()

{

       FILE *fp;

       char ch;

       long n;

       system( "cls" );

       fp = fopen( "demo", "w" );

       printf( "Enter String ( ctrl+z to end ) : " );

       ch = getchar();

       while( ch != EOF )

       {

              putc( ch, fp );

              ch = getchar();

       }

       fclose( fp );

       fp = fopen( "demo", "r" );

       printf( "\nChar - Pos" );

       n = 0L;

       while( feof( fp ) == 0 )

       {

              fseek( fp, n, 0 );

              printf( "\n%3c - %2d", fgetc( fp ), ftell( fp ) );

              n = n + 1L;

       }

       rewind( fp );

       printf( "\nString : " );

       ch = fgetc( fp );

       while( ch != EOF )

       {

              printf( "%c", ch );

              ch = fgetc( fp );

       }

       printf( "\n" );

       fclose( fp );

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MY.jpg)

______________  ****  ______________

Program No. - 499 :

Program to show the use of Command-line arguments.

Code :

#include <stdio.h>

int  main( int argc, char *argv[ ] )

{

       int i;

       system( "cls" );

       printf( "Program Name: %s\n", argv[0] );

       for( i=1 ; i<argc ; i++ )

       {

              printf( "Argument %d : %s\n", i, argv[ i ] );

       }

       system( "pause" );

       return 0;

}

Output :

![](image_rsrc48MZ.jpg)

Command to run on Command Prompt :

![](image_rsrc48N0.jpg)![](image_rsrc48N1.jpg)

______________  ****  ______________

Program No. - 500 :

Program to use command line argument to copy the content of source file to target file.

Code :

#include <stdio.h>

#include <stdlib.h>​​/*  #include <process.h>  */

int  main( int  argc, char  *argv[ ] )

{

       FILE  *fs, *ft;

       char  ch;

       system( “cls” );

       if( argc != 3 )

       {

              puts( "Improper Number of Arguments." );

              exit( 1 );

       }

       fs = fopen( argv[1], "r" );

       if( fs == NULL )

       {

              puts( "Unable to Open Source File." );

              exit( 1 ) ;

       }

       ft = fopen( argv[2], "w" );

       if( ft == NULL )

       {

              puts( "Unable to Open Target File." );

              fclose( fs );

              exit( 1 );

       }

       while( 1 )

       {

              ch = fgetc( fs );

              if( ch == EOF )

                     break;

              else

                     fputc( ch, ft ) ;

       }

       fclose( fs ) ;

       fclose( ft ) ;

       system( “pause” );

       return 0;

}

Output :

![](image_rsrc48N2.jpg)

Command to run on Command Prompt :

![](image_rsrc48N3.jpg)![](image_rsrc48N4.jpg)

Source File (test1.txt) :

![](image_rsrc48N5.jpg)

Target File (test2.txt) :

![](image_rsrc48N6.jpg)

______________  ****  ______________

______________  ****  ______________

We  Wish  You  All  The  Best  ! ! !

______________  ****  ______________

![](image_rsrc48N7.jpg)
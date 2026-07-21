![](cover.jpeg)

KOTLIN AND C

CODING

EXAMPLES

PROGRAMMING FOR BEGINNERS

J KING

[Basic Programs in Kotlin](#text00003.html__Toc68614608)

[Kotlin program to perform arithmetic operations on two numbers](#text00003.html__Toc68614609)

[Program to perform simple calculation](#text00004.html__Toc68614610)

[Program to input numbers (integer, float, double) at run time](#text00005.html__Toc68614611)

[Kotlin program to find largest of three numbers](#text00006.html__Toc68614612)

[Kotlin program to swap two numbers](#text00007.html__Toc68614613)

[Kotlin program to check whether a number is EVEN or ODD](#text00008.html__Toc68614614)

[Kotlin program to print the Multiplication table](#text00009.html__Toc68614615)

[Program to calculate and display student grades](#text00010.html__Toc68614616)

[Kotlin program to convert temperature](#text00011.html__Toc68614617)

[Kotlin program to display Fibonacci series](#text00012.html__Toc68614618)

[Kotlin program to find area of circle](#text00013.html__Toc68614619)

[Kotlin program to find area of Square](#text00014.html__Toc68614620)

[Program to find area of a cylinder](#text00015.html__Toc68614621)

[Kotlin program to generate 4 digits OTP](#text00016.html__Toc68614622)

[Kotlin program to find area of Pentagon](#text00017.html__Toc68614623)

[Kotlin program to find prime numbers](#text00018.html__Toc68614624)

[Kotlin program to convert decimal to binary](#text00019.html__Toc68614625)

[C program to find SUM and AVERAGE of two numbers.](#text00021.html__Toc68614626)

[C program to print ASCII value of a character](#text00022.html__Toc68614627)

[C program to print all numbers from 1 to N using goto statement](#text00023.html__Toc68614628)

[Program to print numbers from 1 to N using while loop](#text00024.html__Toc68614629)

[Program to print Square, Cube and Square Root](#text00025.html__Toc68614630)

[Program to print table of a given number](#text00026.html__Toc68614631)

[Program for Largest Number among three numbers](#text00027.html__Toc68614632)

[Area of rectangle program in c](#text00028.html__Toc68614633)

[C program - Convert Feet to Inches](#text00029.html__Toc68614634)

[Program to create a text file using file handling](#text00030.html__Toc68614635)

[C program to find factorial of a number](#text00031.html__Toc68614636)

[Program to swap two bits of a byte](#text00032.html__Toc68614637)

[Program to swap two numbers using four different methods](#text00033.html__Toc68614638)

[Age Calculator (C program to calculate age)](#text00034.html__Toc68614639)

[C program to design a digital clock](#text00035.html__Toc68614640)

[Program to calculate compound interest](#text00036.html__Toc68614641)

[Program to check whether number is Perfect Square or not](#text00037.html__Toc68614642)

[Program to print message without using any semicolon in program](#text00038.html__Toc68614643)

[Sum of Series Programs / Examples using C](#text00039.html__Toc68614644)

KOTLIN CODING

EXAMPLES

PROGRAMMING FOR BEGINNERS

J KING

# Basic Programs in Kotlin

# Kotlin program to perform arithmetic operations on two numbers

Example:

    Input:

    a = 13

    b = 5

    Output:

    a + b = 18

    a - b = 8

    a * b = 65

    a / b = 2

    a % b = 3

### PROGRAM

##### // Main Method Entry Point of Program

##### fun main(args:Array<String>){

#####     val a = 13

#####     val b = 5

#####     val sum  = a + b  // Perform Addition

#####     val sub  = a - b  // Perform Subtraction

#####     val muti = a * b  // Perform Multiplication

#####     val div  = a / b  // Perform Division

#####     val rem  = a % b  // Perform remainder

#####     // Print  on Console

#####     println("Addison of $a and $b is       : $sum")

#####     println("Subtraction of $a and $b is   : $sub")

#####     println("Multiplication of $a and $b is: $muti")

#####     println("Division of $a and $b is      : $div")

#####     println("Remainder of $a and $b is     : $rem")

##### }

Output

Addison of 13 and 5 is       : 18

Subtraction of 13 and 5 is   : 8

Multiplication of 13 and 5 is: 65

Division of 13 and 5 is      : 2

Remainder of 13 and 5 is     : 3

# Program to perform simple calculation

Example:

    Input:

    first = 30

    second = 15

    choice = '+'

    Output:

    30 + 15 = 45

### PROGRAM

##### /**

##### * Kotlin Program to Perform Simple Calculation on Two integer numbers

##### * User have to  ( +, -, *, /, % ) put any choice to perform operation

##### */

##### package com.includehelp.basic

##### import java.util.*

##### // Main Method Entry Point of Program

##### fun main(args: Array<String>) {

#####     // InputStream to get Input

#####     val reader = Scanner(System.`in`)

#####     //Input First Integer Value

#####     print("Enter Integer Value : ")

#####     var first = reader.nextInt()

#####     //Input Second Integer Value

#####     print("Enter Integer Value : ")

#####     var second = reader.nextInt()

#####     //Input Any Character as Choice

#####     print("Enter any Action( +, -, *, /, % ) :  ")

#####     val choice = reader.next()[0]

#####     try{

#####         var result = when(choice){

#####             '+' -> first+second

#####             '-' -> first-second

#####             '*' -> first*second

#####             '/' -> first/second

#####             '%' -> first%second

#####             else -> {

#####                 System.err.println("Not a Valid Operation choice")

#####                 return

#####             }

#####         }

#####         //Print Result

#####         println("Result is : $result")

#####     }catch (E:Exception){

#####         System.err.println("Exception  : ${E.toString()}")

#####     }

##### }

Output

RUN 1:

Enter Integer Value : 35

Enter Integer Value : 8

Enter any Action( +, -, *, /, % ) :  %

Result is : 3

---

RUN 2:

Enter Integer Value : 456

Enter Integer Value : 67

Enter any Action( +, -, *, /, % ) :  /

Result is : 6

# Program to input numbers (integer, float, double) at run time

### PROGRAM

import java.util.*

// Main Method Entry Point of Program

fun main(args: Array<String>) {

    // InputStream to get Input

    var reader = Scanner(System.`in`)

    // Input Integer Value

    println("Enter Integer Value : ")

    val intValue = reader.nextInt()

    println("Integer Number is : $intValue")

    // Input Long Value

    println("Enter Long Value : ")

    val longValue = reader.nextLong()

    println("Long Number is : $longValue")

    // Input Float Value

    println("Enter Float Value : ")

    val floatValue = reader.nextFloat()

    println("Float Number is : $floatValue")

    // Input Double Value

    println("Enter Double Value : ")

    val doubleValue = reader.nextDouble()

    println("Double Number is : $doubleValue")

}

Output

Run 1:

Enter Integer Value :

123

Integer Number is : 123

Enter Long Value :

34355566

Long Number is : 34355566

Enter Float Value :

45.34

Float Number is : 45.34

Enter Double Value :

456.78

Double Number is : 456.78

# Kotlin program to find largest of three numbers

Example:

    Input:

    First number: 10

    Second number: 20

    Third number: 30

    Output:

    Largest number: 30

### PROGRAM

##### package com.includehelp.basic

##### import java.util.*

##### // Main Method Entry Point of Program

##### fun main(args: Array<String>) {

#####     // InputStream to get Input

#####     val reader = Scanner(System.`in`)

#####     // Input Integer values

#####     println("Enter First Value : ")

#####     var first = reader.nextInt()

#####     println("Enter Second Value : ")

#####     var second = reader.nextInt()

#####     println("Enter Third Value : ")

#####     var third = reader.nextInt();

#####     // condition to find largest of three numbers

#####     val largest =   if(first>second && first>third)

#####                         first

#####                     else if(second>third)

#####                         second

#####                     else

#####                         third

#####     println("Largest Number is: $largest")

##### }

Output

Enter First Value :

23

Enter Second Value :

45

Enter Third Value :

89

Largest Number is: 89

# Kotlin program to swap two numbers

Example:

    Input:

    First number: 10

    Second number: 20

    Output:

    First number: 20

    Second number: 10

### PROGRAM

##### import java.util.*

##### // Main Method Entry Point of Program

##### fun main(arg: Array<String>) {

#####     // InputStream to get Input

#####     var reader = Scanner(System.`in`)

#####     // Input two values

#####     println("Enter First Value : ")

#####     var first = reader.nextInt();

#####     println("Enter Second Value : ")

#####     var second = reader.nextInt();   

#####     println("Numbers Before Swap : \n first = $first \n second = $second ")

#####     //Code for Swap Numbers

#####     var temp = first

#####     first=second

#####     second=temp

#####     println("Numbers After  Swap : \n first = $first \n second = $second ")

##### }

Output

##### Run 1:

##### Enter First Value :

##### 45

##### Enter Second Value :

##### 12

##### Numbers Before Swap :

##### first = 45

##### second = 12

##### Numbers After  Swap :

##### first = 12

##### second = 45

# Kotlin program to check whether a number is EVEN or ODD

Example:

    Input:

    N = 13

    Output:

    "ODD"

    Input:

    N = 24

    Output:

    "EVEN"

### PROGRAM

/*

    * Kotlin program to Input Integer

    * Numbers and check Number is Even or ODD

*/

import java.util.*

// Main Method Entry Point of Program

fun main(args: Array<String>) {

    // InputStream to get Input

    val reader = Scanner(System.`in`)

    //Input Integer Value

    println("Enter Integer Value : ")

    var number = reader.nextInt();

    val str = if(number%2==0) "EVEN" else "ODD"

    println("Number is $str")

}

Output

RUN 1:

Enter Integer Value :

34

Number is EVEN

---

Run 2:

Enter Integer Value :

15

Number is ODD

# Kotlin program to print the Multiplication table

### PROGRAM

##### import java.util.*

##### // Main function entry point of program

##### fun main(args: Array<String>) {

#####     val sc = Scanner(System.`in`)

#####     println("Enter Number: ")

#####     val num: Int = sc.nextInt()

#####     // for loop to print multiplication table of given number

#####     for (i in 1..10) {

#####         val result = num * i

#####         println("$num*$i = $result")

#####     }

##### }

Output

Enter Number:

5

5*1 = 5

5*2 = 10

5*3 = 15

5*4 = 20

5*5 = 25

5*6 = 30

5*7 = 35

5*8 = 40

5*9 = 45

5*10 = 50

# Program to calculate and display student grades

    Percentage >=80 -> A

    Percentage >=60 -> B

    Percentage r>=40 -> C

    else D

    Note: Maximum Marks 100 in Each Subject

Example:

    Input:

    English = 98

    Physics = 34

    Chemistry = 67

    Maths = 90

    Output:

    Total Marks = 356.0

    Percentage = 71.2

    Grade = B

### PROGRAM

import java.util.*

//Main Function , Entry point of Program

fun main(args: Array<String>) {

    //array of subjects Names

    val subjectName = arrayOf<String>("English","Physics","Chemistry","Maths")

    //Input Stream

    val scanner = Scanner(System.`in`)

    //Declare Array to Contain Subjects marks

    val marksArray = DoubleArray(5)

    //Start Input Subjects Marks

    println("Input Marks->")

    for(i in marksArray.indices){

        print("${subjectName[i]} : ")

        marksArray[i] = scanner.nextDouble()

    }

    //Calculate Total Marks in All Subjects

    val total = marksArray.sum()

    //Calculate Percentage

    val percentage = marksArray.average()

    //Print Total and Percentage

    println("Total of All subjects Marks : $total")

    println("Percentage : $percentage")

    //To find out Grade based on Percentage

    when{

        percentage>80 -> println("Grade : A")

        percentage>60 -> println("Grade : B")

        percentage>40 -> println("Grade : C")

        else -> println("Grade : D")

    }

}

Output

Run 1:

English : 98

Physics : 42

Chemistry : 67

Maths : 90

Total of All subjects Marks : 297

Percentage : 74.25

Grade : B

# Kotlin program to convert temperature

Example:

    Input:

    Fahrenheit = 67

    Output:

    Celsius = 19.444444444444443

### PROGRAM

##### package com.includehelp

##### import java.util.*

##### //Main Function , Entry point of Program

##### fun main(args: Array<String>) {

#####     //Input Stream

#####     val scanner = Scanner(System.`in`)

#####     //Input temperature in Fahrenheit

#####     print("Enter temperature into Fahrenheit : ")

#####     val fahrenheit = scanner.nextDouble()

#####     //Convert  Fahrenheit to Celsius

#####     val celsius =( (fahrenheit  -  32  ) *  5)/9

#####     //Print temperature in Celsius

#####     println("Temperature in Fahrenheit ($fahrenheit) = Celsius ($celsius)")

##### }

Output

Output will be:

Run 1:

Enter temperature into Fahrenheit : 67

Temperature in Fahrenheit (67.0) = Celsius (19.444444444444443)

---

Run 2:

Enter temperature into Fahrenheit : 78

Temperature in Fahrenheit (78.0) = Celsius (25.555555555555557)

# Kotlin program to display Fibonacci series

Example:

    Input:

    term1 = 0

    term2 = 1

    N = 10

    Output:

    Fibonacci series: 0 1 1 2 3 5 8 13 21 34

    Input:

    term1 = 0

    term2 = 1

    N = 5

    Output:

    Fibonacci series: 0 1 1 2 3

### PROGRAM

##### /**

##### * Display Fibonacci Series up to a Given number of terms

##### * e.g.  0 1 1 2 3 5 8 13....n

##### */

##### import java.util.*

##### //Main Function entry Point of Program

##### fun main(args: Array<String>) {

##### // Input Stream

##### val scanner = Scanner(System.`in`)

##### // input total number of terms

##### println("Enter terms  : ")

##### val n: Int = scanner.nextInt()

##### var term1 = 0

##### var term2 = 1

##### var count = 1

##### // Iterate Loop to print fibonacci Series upto given terms

##### while (count <= n){

##### print("$term1 ")

##### val s = term1+term2

##### term1 = term2;

##### term2 = s

##### count++

##### }

##### }

Output

RUN 1:

Enter terms  :

10

0 1 1 2 3 5 8 13 21 34

---

Run 2:

Enter terms  :

5

0 1 1 2 3

# Kotlin program to find area of circle

Example:

    Input:

    Radius: 3

    Output:

    Area of circle: 28.259999999999998

### PROGRAM

##### import java.util.*

##### // PI Constant Value

##### val PI = 3.14

##### /* function to calculate area of circle of given radius */

##### fun getAreaOfCirlce(radius: Double): Double {

#####     return PI * radius * radius

##### }

##### // Main Method Entry Point of Program

##### fun main(args:Array<String>){

#####     val sc = Scanner(System.`in`)

#####     // Input Radius

#####     println("Enter Circle Radius  : ")

#####     val radius = sc.nextDouble()

#####     // Call function to get Area of Circle

#####     val areaOfCircle = getAreaOfCirlce(radius)

#####     // Print Area of Circle

#####     println("Area of Circle : $areaOfCircle")

##### }

Output

Run 1:

Enter Circle Radius  :

3

Area of Circle : 28.259999999999998

-----

Run 2:

Enter Circle Radius  :

8

Area of Circle : 200.96

# Kotlin program to find area of Square

Example:

    Input:

    side = 6

    Output:

    area = 36.0

### PROGRAM

##### import java.util.*

##### //Main Function , Entry point of Program

##### fun main(args: Array<String>) {

#####     //Input Stream

#####     val scanner = Scanner(System.`in`)

#####     //Input Side of Square

#####     print("Enter Side of Square : ")

#####     val side = scanner.nextDouble()

#####     //Calculate Area of square

#####     val squareArea = side*side;

#####     //Print Area

#####     println("Area of Square is : $squareArea")

##### }

Output

Run 1:

Enter Side of Square : 6

Area of Square is : 36.0

---

Run 2:

Enter Side of Square : 4.5

Area of Square is : 20.25

# Program to find area of a cylinder

Example:

    Input:

    Radius = 5

    Height = 7

    Output:

    Surface Area of Cylinder is :75.39822368615503

### PROGRAM

##### package com.includehelp

##### import java.util.*

##### //Main Function , Entry point of Program

##### fun main(args: Array<String>) {

#####     //Input Stream

#####     val scanner = Scanner(System.`in`)

#####     //Input Radius

#####     print("Enter Radius of Cylinder : ")

#####     val radius = scanner.nextDouble()

#####     //Input Height

#####     print("Enter Height of Cylinder : ")

#####     val height = scanner.nextDouble()

#####     //Cylinder Surface Area

#####     val areaCylinder = 2*Math.PI*(radius+height)

#####     //Print Area

#####     println("Surface Area of Cylinder is :$areaCylinder")

##### }

Output

Run 1:

Enter Radius of Cylinder : 5

Enter Height of Cylinder : 7

Surface Area of Cylinder is :75.39822368615503

---

Run 2:

Enter Radius of Cylinder : 29

Enter Height of Cylinder : 4

Surface Area of Cylinder is :207.34511513692635

# Kotlin program to generate 4 digits OTP

### PROGRAM

##### /**

#####     * Kotlin Program to Generate 4 digit OTP

##### */

##### /**

#####     * Function for Generate 4 digit OTP String

#####     * @return

##### */

##### fun generateOTP(): String {

#####     val randomPin = (Math.random() * 9000).toInt() + 1000

#####     return randomPin.toString()

##### }

##### // Main Method Entry Point of Program

##### fun main(args: Array<String>) {

#####     // Call function for Generate OTP

#####     val otp1 = generateOTP()

#####     // Print OTP

#####     println("OTP : $otp1")

##### }

Output

Run 1:

OTP : 7997

-----

Run 2:

OTP : 7682

-----

Run 3:

OTP : 6934

-----

Run 4:

OTP : 4189

# Kotlin program to find area of Pentagon

Formula to find area of Pentagon:  = (5/2)sa , where

s  - Side of Pentagon

a  - Apothem of Pentagon

Example:

    Input:

    side= 5

    apothem = 6

    Output:

    area = 75.0

### PROGRAM

##### import java.util.*

##### //Main Function , Entry point of Program

##### fun main(args: Array<String>) {

#####     //Input Stream

#####     val scanner = Scanner(System.`in`)

#####     //Input Side

#####     print("Enter Side of Pentagon : ")

#####     val s = scanner.nextDouble()

#####     //Input Apothem

#####     print("Enter Apothem of Pentagon : ")

#####     val a = scanner.nextDouble()

#####     //Area of Pentagon

#####     val areaPentagon = (5.0/2.0)*s*a

#####     //Print Area

#####     println("Pentagon Area is :$areaPentagon")

##### }

Output

Run 1:

Run 1:

Enter Side of Pentagon : 5

Enter Apothem of Pentagon : 6

Pentagon Area is :75.0

---

Run 2:

Enter Side of Pentagon : 8

Enter Apothem of Pentagon : 6

Pentagon Area is :120.0

# Kotlin program to find prime numbers

Example:

    Input:

    start = 1

    end = 100

    Output:

    [2, 3, 5, 7, 11, 13, 17, 19, 23, 29,

    31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]

### PROGRAM

##### /**

##### * Kotlin Program to find out Prime Numbers between

##### * given Range(include START and END)

##### * A prime number is a whole number greater than 1

##### * whose only factors are 1 and itself.

##### * e.g 7, 11, 13, 17

##### */

##### import java.util.*

##### //Function to check Prime Number

##### fun findPrimeNo(number: Long): Boolean {

#####     if(number<2) return false

#####     for (i in 2.toLong()..number/2) {

#####         if (number % i == 0.toLong()) {

#####             return false

#####         }

#####     }

#####     return true

##### }

##### //Main Function, Entry Point of Program

##### fun main(arg: Array<String>) {

#####     //Input Stream

#####     val sc = Scanner(System.`in`)

#####     //Input Start of Range

#####     print("Enter Start of Range  : ")

#####     val start: Long = sc.nextLong()

#####     //Input End of Range

#####     print("Enter End of Range  : ")

#####     val end: Long = sc.nextLong()

#####     //Declare Mutable List to hold factors

#####     val list: MutableList<Long> = ArrayList()

#####     //iterate through loop start to end to find Prime  number in Range

#####     for (i in start..end) {

#####         if (findPrimeNo(i)) {

#####             list.add(i)

#####         }

#####     }

#####     println("Prime Numbers from $start to $end  : $list")

##### }

# Kotlin program to convert decimal to binary

Example:

    Input:

    Decimal number = 12

    Recursive division:

|     Number | Quotient | Remainder |
| 12 | 6 | 0 |
| 6 | 3 | 0 |
| 3 | 1 | 1 |
| 1 | 0 | 1 |

Read the remainders in reverse order

1100 is the binary conversion for 12 .

### PROGRAM

##### import java.util.*

##### /* function to convert given decimal number into Binary */

##### fun getBinaryNumber(decimalNumber: Int): String {

#####     var decimalNumber = decimalNumber

#####     val binaryStr = StringBuilder()

#####     while (decimalNumber > 0) {

#####         val r = decimalNumber % 2

#####         decimalNumber /= 2

#####         binaryStr.append(r)

#####     }

#####     return binaryStr.reverse().toString()

##### }

##### // Main Method Entry Point of Program

##### fun main(arg: Array<String>) {

#####     val sc = Scanner(System.`in`)

#####     println("Enter Decimal Number  : ")

#####     //Input Decimal Number

#####     val decimalNumber: Int = sc.nextInt()

#####     // Call function to Convert Decimal into binary

#####     val binaryNumber = getBinaryNumber(decimalNumber)

#####     // Print Binary Number

#####     println("Binary Number : $binaryNumber")

##### }

Output

Run 1:

Enter Decimal Number  :

15

Binary Number : 1111

-----

Run 2:

Enter Decimal Number  :

12345

Binary Number : 11000000111001

----

Run 3:

Enter Decimal Number  :

545654

Binary Number : 10000101001101110110

C PROGRAMMING

EXAMPLES

PROGRAMMING FOR BEGINNERS

J KING

# C program to find SUM and AVERAGE of two numbers.

### Sum and Average of two numbers

### PROGRAM

##### /* c program find sum and average of two numbers*/

##### #include <stdio.h>

##### int main()

##### {

#####     int a,b,sum;

#####     float avg;

#####     printf("Enter first number :");

#####     scanf("%d",&a);

#####     printf("Enter second number :");

#####     scanf("%d",&b);

#####     sum=a+b;

#####     avg= (float)(a+b)/2;

#####     printf("\nSum of %d and %d is = %d",a,b,sum);

#####     printf("\nAverage of %d and %d is = %f",a,b,avg);

#####     return 0;

##### }

Output

    Enter first number :10

    Enter second number :15

    Sum of 10 and 15 is = 25

    Average of 10 and 15 is = 12.500000

# C program to print ASCII value of a character

### PROGRAM

##### #include <stdio.h>

##### int main()

##### {

##### char ch;

##### //input character

##### printf("Enter the character: ");

##### scanf("%c",&ch);

##### printf("ASCII is = %d\n", ch);

##### return 0;

##### }

Output

First run:

Enter the character: a

ASCII is = 97

Second run:

Enter the character: A

ASCII is = 65

# C program to print all numbers from 1 to N using goto statement

### PROGRAM

##### #include <stdio.h>

##### int main()

##### {

##### int count,n;

##### //read value of N

##### printf("Enter value of n: ");

##### scanf("%d",&n);

##### //initialize count with 1

##### count =1;

##### start: //label

##### printf("%d ",count);

##### count++;

##### if(count<=n)

##### goto start;

##### return 0;

##### }

Output

Enter value of n: 10

1 2 3 4 5 6 7 8 9 10

# Program to print numbers from 1 to N using while loop

### PROGRAM

##### #include <stdio.h>

##### int main()

##### {

##### //loop counter declaration

##### int number;

##### //variable to store limit /N

##### int n;

##### //assign initial value

##### //from where we want to print the numbers

##### number =1;

##### //input value of N

##### printf("Enter the value of N: ");

##### scanf("%d",&n);

##### //print statement

##### printf("Numbers from 1 to %d: \n",n);

##### //while loop, that will print numbers

##### //from 1 to n

##### while(number <= n)

##### {

##### //printing the numbers

##### printf("%d ",number);

##### //increasing loop counter by 1

##### number++;

##### }

##### return 0;

##### }

Output

Enter the value of N: 25

Numbers from 1 to 25:

1 2 3 4 5 6 7 8 9 10 11 12 13 14 15

16 17 18 19 20 21 22 23 24 25

# Program to print Square, Cube and Square Root

### PROGRAM

##### /*C program to print square, cube and square root of all numbers from 1 to N.*/

##### #include <stdio.h>

##### #include <math.h>

##### int main()

##### {

#####     int i,n;

#####     printf("Enter the value of N: ");

#####     scanf("%d",&n);

#####     printf("No     Square   Cube    Square Root\n",n);

#####     for(i=1;i<=n;i++)

#####     {

#####         printf("%d \t %ld \t %ld \t %.2f\n",i,(i*i),(i*i*i),sqrt((double)i));

#####     }

#####     return 0;

##### }

![](OEBPS/Image00000.jpg)

# Program to print table of a given number

### PROGRAM

##### #include<stdio.h>

##### int main()

##### {

##### //declare variable

##### int count,t,r;

##### //Read value of t

##### printf("Enter number: ");

##### scanf("%d",&t);

##### count=1;

##### start:

##### if(count<=10)

##### {

##### //Formula of table

##### r=t*count;

##### printf("%d*%d=%d\n",t,count,r);

##### count++;

##### goto start;

##### }

##### return 0;

##### }

Output

Enter number: 10

10*1=10

10*2=20

10*3=30

10*4=40

10*5=50

10*6=60

10*7=70

10*8=80

10*9=90

10*10=100

# Program for Largest Number among three numbers

### PROGRAM

##### /* c program to find largest number among 3 numbers*/

##### #include <stdio.h>

##### int main()

##### {

#####     int a,b,c;

#####     int largest;

#####     printf("Enter three numbers (separated by space):");

#####     scanf("%d%d%d",&a,&b,&c);

#####     if(a>b && a>c)       

#####         largest=a;

#####     else if(b>a && b>c)      

#####         largest=b;

#####     else

#####         largest=c;

#####     printf("Largest number is = %d",largest);

#####     return 0;

##### }

Output

First Run:

Enter three numbers (separated by space): 10 20 30

Largest number is = 30

Second Run:

Enter three numbers (separated by space):10 30 20

Largest number is = 30

Third Run:

Enter three numbers (separated by space):30 10 20

Largest number is = 30

Fourth Run:

Enter three numbers (separated by space):30 30 30

Largest number is = 30

# Area of rectangle program in c

### PROGRAM

##### /*C program to find area of a rectangle.*/

##### #include <stdio.h>

##### int main()

##### {

#####     float l,b,area;

#####     printf("Enter the value of length: ");

#####     scanf("%f",&l);

#####     printf("Enter the value of breadth: ");

#####     scanf("%f",&b);

#####     area=l*b;

#####     printf("Area of rectangle: %f\n",area);

#####     return 0;

##### }

Output

    Enter the value of length: 1.25

    Enter the value of breadth: 3.15

    Area of rectangle: 3.937500

# C program - Convert Feet to Inches

### PROGRAM

##### #include<stdio.h>

##### int main()

##### {

##### int feet,inches;

##### printf("Enter the value of feet: ");

##### scanf("%d",&feet);

##### //converting into inches

##### inches=feet*12;

##### printf("Total inches will be: %d\n",inches);

##### return 0;

##### }

Output

    Enter the value of feet: 15

    Total inches will be: 180

# Program to create a text file using file handling

### PROGRAM

##### #include< stdio.h >

##### int main()

##### {

#####     FILE *fp;   /* file pointer*/

#####     char fName[20];

#####     printf("Enter file name to create :");

#####     scanf("%s",fName);

#####     /*creating (open) a file, in “w”: write mode*/

#####     fp=fopen(fName,"w");

#####     /*check file created or not*/

#####     if(fp==NULL)

#####     {

#####         printf("File does not created!!!");

#####         exit(0); /*exit from program*/

#####     }

#####     printf("File created successfully.");

#####     return 0;

##### }

Output

    Run 1:

    Enter file name to create : file1.txt

    File created successfully.

    Run 2:

    Enter file name to create : d:/file1.txt

    File created successfully.

    “file will be created in d: drive”.

    Run 3:

    Run 1:

    Enter file name to create : h:/file1.txt

    File does not created!!!

# C program to find factorial of a number

Factorial is an integer product, with all of it below integer till 1\. Represent factorial in mathematical by ! Sign.

Example:
Factorial 5 is:
5! = 120 [That is equivalent to 5*4*3*2*1 =120]

### Simple program

##### /*C program to find factorial of a number.*/

##### #include <stdio.h>

##### int main()

##### {

#####     int num,i;

#####     long int fact;

#####     printf("Enter an integer number: ");

#####     scanf("%d",&num);

#####     /*product of numbers from num to 1*/

#####     fact=1;

#####     for(i=num; i>=1; i--)

#####         fact=fact*i;

#####     printf("\nFactorial of %d is = %ld",num,fact);

#####     return 0;

##### }

Output

Enter an integer number: 7

Factorial of 7 is = 5040

### User Define Function

/*Using Function: C program to find factorial of a number.*/

#include <stdio.h>

/* function : factorial, to find factorial of a given number*/

long int factorial(int n)

{

    int i;

    long int fact=1;

    if(n==1) return fact;

    for(i=n;i>=1;i--)

        fact= fact * i;

    return fact;

}

int main()

{

    int num;

    printf("Enter an integer number :");

    scanf("%d",&num);

    printf("\nFactorial of %d is = %ld",num,factorial(num));

    return 0;

}

# Program to swap two bits of a byte

Example:

Input number:  0x0A (Hexadecimal)

Binary of input number: 0000 1010

After swapping of bit 1 and 2

Binary will be: 0000 1100

Output number will be: 0x0C (Hexadecimal)

### PROGRAM

##### #include <stdio.h>

##### /*

##### Program to swap 1st and 2nd bit of hexadecimal value stored in data variable

##### */

##### int main()

##### {

#####     unsigned char data = 0xA; // Assiging hexadecimal value

#####     // Get 1st bit from data

#####     unsigned char bit_1 = (data >> 1) & 1;

#####     // Get 2nd bit from data

#####     unsigned char bit_2 = (data >> 2) & 1;

#####     // Get XOR of bit_1 and bit_2

#####     unsigned char xor_of_bit = bit_1 ^ bit_2;

#####     printf("After swapping the bits, data value is: %2X", data ^ (xor_of_bit << 1 | xor_of_bit << 2));

#####     return 0;

##### }

Output

After swapping the bits, data value is:  C

# Program to swap two numbers using four different methods

### METHODS

1.  Using third variable
2.  Without using third variable
3.  Using X-OR operator
4.  Using simple statement

### PROGRAM

##### //C program to swap two numbers using four different methods.

##### #include <stdio.h>

##### int main()

##### {

#####     int a,b,t;

#####     printf(" Enter value of A ?  ");

#####     scanf("%d",&a);

#####     printf(" Enter value of B ?  ");

#####     scanf("%d",&b);

#####     printf("\n Before swapping : A= %d, B= %d",a,b);

#####     /****first method using third variable*/

#####     t=a;

#####     a=b;

#####     b=t;

#####     printf("\n After swapping (First method) : A= %d, B= %d\n",a,b);

#####     /****second method without using third variable*/

#####     a=a+b;

#####     b=a-b;

#####     a=a-b;

#####     printf("\n After swapping (second method): A= %d, B= %d\n",a,b);

#####     /****Third method  using X-Or */

#####     a^=b;

#####     b^=a;

#####     a^=b;

#####     printf("\n After swapping (third method) : A= %d, B= %d\n",a,b);

#####     /****fourth method  (single statement)*/

#####     a=a+b-(b=a);

#####     printf("\n After swapping (fourth method): A= %d, B= %d\n",a,b);

#####     return 0;

##### }

Output

Enter value of A ?  100

Enter value of B ?  200

Before swapping : A= 100, B= 200

After swapping (First method) : A= 200, B= 100

After swapping (second method): A= 100, B= 200

After swapping (third method) : A= 200, B= 100

After swapping (fourth method): A= 100, B= 200

# Age Calculator (C program to calculate age)

### PROGRAM

##### /*Age Calculator (C program to calculate age).*/

##### #include <stdio.h>

##### #include <time.h>

##### /*check given year is leap year or not*/

##### int isLeapYear(int year, int mon)

##### {

#####     int flag = 0;

#####     if (year % 100 == 0)

#####     {

#####             if (year % 400 == 0)

#####             {

#####                     if (mon == 2)

#####                     {

#####                             flag = 1;

#####                     }

#####             }

#####     }

#####     else if (year % 4 == 0)

#####     {

#####             if (mon == 2)

#####             {

#####                     flag = 1;

#####             }

#####     }

#####     return (flag);

##### }

##### int main()

##### {

#####     int DaysInMon[] = {31, 28, 31, 30, 31, 30,

#####                        31, 31, 30, 31, 30, 31};

#####     int days, month, year;

#####     char dob[100];

#####     time_t ts;

#####     struct tm *ct;

#####     /* enter date of birth */

#####     printf("Enter your date of birth (DD/MM/YYYY): ");

#####     scanf("%d/%d/%d",&days,&month, &year);

#####     /*get current date.*/

#####     ts = time(NULL);

#####     ct = localtime(&ts);

#####     printf("Current Date: %d/%d/%d\n",

#####             ct->tm_mday, ct->tm_mon + 1, ct->tm_year + 1900);

#####     days = DaysInMon[month - 1] - days + 1;

#####     /* leap year checking*/

#####     if (isLeapYear(year, month))

#####     {

#####             days = days + 1;

#####     }

#####     /* calculating age in no of days, years and months */

#####     days = days + ct->tm_mday;

#####     month = (12 - month) + (ct->tm_mon);

#####     year = (ct->tm_year + 1900) - year - 1;

#####     /* checking for leap year feb - 29 days */

#####     if (isLeapYear((ct->tm_year + 1900), (ct->tm_mon + 1)))

#####     {

#####             if (days >= (DaysInMon[ct->tm_mon] + 1))

#####             {

#####                     days = days - (DaysInMon[ct->tm_mon] + 1);

#####                     month = month + 1;

#####             }

#####     }

#####     else if (days >= DaysInMon[ct->tm_mon])

#####     {

#####             days = days - (DaysInMon[ct->tm_mon]);

#####             month = month + 1;

#####     }

#####     if (month >= 12)

#####     {

#####             year = year + 1;

#####             month = month - 12;

#####     }

#####     /* print age */

#####     printf("\n## Hey you are  %d years %d months and %d days old. ##\n", year, month, days);

#####     return 0;

##### }

# C program to design a digital clock

### PROGRAM

##### /*C program to design a digital clock.*/

##### #include <stdio.h>

##### #include <time.h> //for sleep() function

##### #include <unistd.h>

##### #include <stdlib.h>

##### int main()

##### {

#####     int hour, minute, second;

#####     hour=minute=second=0;

#####     while(1)

#####     {

#####         //clear output screen

#####         system("clear");

#####         //print time in HH : MM : SS format

#####         printf("%02d : %02d : %02d ",hour,minute,second);

#####          //clear output buffer in gcc

#####         fflush(stdout);

#####          //increase second

#####         second++;

#####         //update hour, minute and second

#####         if(second==60){

#####             minute+=1;

#####             second=0;

#####         }

#####         if(minute==60){

#####             hour+=1;

#####             minute=0;

#####         }

#####         if(hour==24){

#####             hour=0;

#####             minute=0;

#####             second=0;

#####         }

#####         sleep(1);   //wait till 1 second

#####     }

#####     return 0;

##### }

# Program to calculate compound interest

### PROGRAM

/*C program to calculate compound interest.*/

#include <stdio.h>

#include <math.h>

in t main()

{

    floa t principal, rate, year, ci;

    printf("Enter principal: ");

    scanf("%f", &principal);

    printf("Enter rate: ");

    scanf("%f", &rate);   

    printf("Enter time in years: ");

    scanf("%f", &year);

    //calculate compound interest

    ci=principal*((pow((1+rate/100),year)-1));

    printf("Compound interest is: %f\n",ci);

    retur n 0;

}

Output

    Enter principal: 10000

    Enter rate: 10.25

    Enter time in years: 5

    Compound interest is: 6288.943359

# Program to check whether number is Perfect Square or not

### PROGRAM

##### /*C program to check number is perfect square or not.*/

##### #include <stdio.h>

##### #include <math.h>

##### int main()

##### {

#####     int num;

#####     int iVar;

#####     float fVar;

#####     printf("Enter an integer number: ");

#####     scanf("%d",&num);

#####     fVar=sqrt((double)num);

#####     iVar=fVar;

#####     if(iVar==fVar)

#####         printf("%d is a perfect square.",num);

#####     else

#####         printf("%d is not a perfect square.",num);

#####     return 0;

##### }

### BY User Define Function

##### /*C program to check number is perfect square or not.*/

##### #include <stdio.h>

##### #include <math.h>

##### /*function definition*/

##### int isPerfectSquare(int number)

##### {

#####     int iVar;

#####     float fVar;

#####     fVar=sqrt((double)number);

#####     iVar=fVar;

#####     if(iVar==fVar)

#####         return 1;

#####     else

#####         return 0;

##### }

##### int main()

##### {

#####     int num;

#####     printf("Enter an integer number: ");

#####     scanf("%d",&num);

#####     if(isPerfectSquare(num))

#####         printf("%d is a perfect square.",num);

#####     else

#####         printf("%d is not a perfect square.",num);

#####     return 0;

##### }

Output

    First Run:

    Enter an integer number: 16

    16 is a perfect square.

    Second Run:

    Enter an integer number: 26

    26 is not a perfect square.

# Program to print message without using any semicolon in program

### PROGRAM

##### /*Program to print "Hello C" using if and else

##### statement both.*/

##### #include <stdio.h>

##### int main()

##### {

#####     if(!printf("Hello "))

#####         ;

#####     else

#####         printf("C\n");

#####     return 0;

##### }

#### OUTPUT

  Hello C

# Sum of Series Programs / Examples using C

1.  1+2+3+4+..N<

### PROGRAM

##### /*This program will print the sum of all natural numbers from 1 to N.*/

##### #include<stdio.h>

##### int main()

##### {

#####     int i,N,sum;

#####     /*read value of N*/

#####     printf("Enter the value of N: ");

#####     scanf("%d",&N);

#####     /*set sum by 0*/

#####     sum=0;

#####     /*calculate sum of the series*/

#####     for(i=1;i<=N;i++)

#####         sum= sum+ i;

#####     /*print the sum*/

#####     printf("Sum of the series is: %d\n",sum);

#####     return 0;

##### }

Enter the value of N: 100

    Sum of the series is: 5050
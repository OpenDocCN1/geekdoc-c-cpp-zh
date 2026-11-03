
### 1.85 Determine the value of each of the following logical expressions if a = 5, b = 10 and c = -6
- (a) a > b && a < c
- (b) a < b && a > c
- (c) a == c || b > a
- (d) b > 15 && c < 0 || a > 0
- (e) (a/2.0 == 0.0 && b/2.0 != 0.0) || c < 0.0

### 1.86 What is the output of the following program?
```
main ()
{
    char x;
    int y;
    x = 100;
    y = 125;
    printf ("%c\n", x) ;
    printf ("%c\n", y) ;
    printf ("%d\n", x) ;
}
```

### 1.87 Find the output of the following program?
```
main ()
{
    int x = 100;
    printf("%d\n", 10 + x++);
    printf("%d\n", 10 + x++);
}
```

### 1.88 What is printed by the following program?
```
main ()
{
    int x = 5, y = 10, z = 10 ;
    x = y == z;
    printf("%d", x) ;
}
```

### 1.89 What is the output of the following program?
```
main ()
{
    int x = 100, y = 200;
    printf ("%d", (x > y) ? x : y);
}
```

### 1.90 What is the output of the following program?
```
main ()
{
    unsigned x = 1 ;
    signed char y = -1 ;
    if(x > y)
        printf("x > y");
    else
        printf("x<= y") ;
}
```
Did you expect this output? Explain.

### 1.91 What is the output of the following program? Explain the output.
```
main ()
{
    int x = 10 ;
    if(x == 20) printf("TRUE") ;
    else printf("FALSE") ;
}
```

### 1.92 What is the error in each of the following statements?
- (a) if (m == 1 && n != 0)
  printf("OK");
- (b) if (x <= 5)
  printf("Jump");

### 1.93 What is the error, if any, in the following segment?
```
int x = 10 ;
float y = 4.25 ;
x = y % x ;
```

### 1.94 What is printed when the following is executed?
```
for (m = 0; m < 3; m++)
    printf("%d\n", (m%2) ? m : m+2);
```

### 1.95 What is the output of the following segment when executed?
```
int m = -14, n = 3;
printf("%d\n", m * n * 10) ;
n = -n;
printf("%d\n", m * n * 10);
```

## Programming Exercises

### 1.1 Write a program that will print your mailing address in the following form:
- First line : Name
- Second line : Door No, Street
- Third line : City, Pin code

### 1.2 Modify the above program to provide border lines to the address.

### 1.3 Write a program using one print statement to print the pattern of asterisks as shown below:

### 1.4 Write a program that will print the following figure using suitable characters.
*
 * *
 * * *
 * * * *

![](img/fe6da5f61b1e2c77309bbee135b45e35_149_0.png)

### 1.5 Given the radius of a circle, write a program to compute and display its area. Use a symbolic constant to define the p value and assume a suitable value for radius.

### 1.6 Write a program to output the following multiplication table:
5 × 1 = 5
5 × 2 = 10
5 × 3 = 15
. . .
. . .
5 × 10 = 50

### 1.7 Given two integers 20 and 10, write a program that uses a function add( ) to add these two numbers and sub( ) to find the difference of these two numbers and then display the sum and difference in the following form:
20 + 10 = 30
20 − 10 = 10

### 1.8 Given the values of three variables a, b and c, write a program to compute and display the value of x, where
x = a / (b − c)
Execute your program for the following values:
(a) a = 250, b = 85, c = 25
(b) a = 300, b = 70, c = 70
Comment on the output in each case.

### 1.9 Relationship between Celsius and Fahrenheit is governed by the formula
F = 9C/5 + 32
Write a program to convert the temperature
(a) from Celsius to Fahrenheit and
(b) from Fahrenheit to Celsius.

### 1.10 Area of a triangle is given by the formula
A = √[S(S − a)(S − b)(S − c)]
Where a, b and c are sides of the triangle and 2S = a + b + c. Write a program to compute the area of the triangle given the values of a, b and c.

### 1.11 Distance between two points (x₁, y₁) and (x₂, y₂) is governed by the formula
D² = (x₂ − x₁)² + (y₂ − y₁)²
Write a program to compute D given the coordinates of the points.

### 1.12 A point on the circumference of a circle whose center is (0, 0) is (4,5). Write a program to compute radius and area of the circle. (Hint: use the formula given in Ex. 1.11)

### 1.13 The line joining the points (2,2) and (5,6) which lie on the circumference of a circle is the diameter of the circle. Write a program to compute the area of the circle.

### 1.14 Write a program to display the equation of a line in the form
ax + by = c
for a = 5, b = 8 and c = 18.

### 1.15 Write a program to display the following simple arithmetic calculator
x = [ ]   y = [ ]
sum = [ ]   Difference = [ ]
Product = [ ]   Division = [ ]

### 1.16 Write a program to determine and print the sum of the following harmonic series for a given value of n:
1 + 1/2 + 1/3 + ... + 1/n
The value of n should be given interactively through the terminal.

### 1.17 Write a program to read the price of an item in decimal form (like 15.95) and print the output in paise (like 1595 paise).

### 1.18 Write a program that prints the even numbers from 1 to 100.

### 1.19 Write a program that requests two float type numbers from the user and then divides the first number by the second and display the result along with the numbers.

### 1.20 The price of one kg of rice is Rs. 16.75 and one kg of sugar is Rs. 15. Write a program to get these values from the user and display the prices as follows:
*** LIST OF ITEMS ***
Item Price
Rice Rs 16.75
Sugar Rs 15.00

### 1.21 Write program to count and print the number of negative and positive numbers in a given set of numbers. Test your program with a suitable set of numbers. Use scanf to read the numbers. Reading should be terminated when the value 0 is encountered.

### 1.22 Write a program to do the following:
(a) Declare x and y as integer variables and z as a short integer variable.
(b) Assign two 6 digit numbers to x and y
(c) Assign the sum of x and y to z
(d) Output the values of x, y and z
Comment on the output.

### 1.23 Write a program to read two floating point numbers using a scanf statement, assign their sum to an integer variable and then output the values of all the three variables.

### 1.24 Write a program to illustrate the use of typedef declaration in a program.

### 1.25 Write a program to illustrate the use of symbolic constants in a real-life application.

### 1.26 Given the string "WORDPROCESSING", write a program to read the string from the terminal and display the same in the following formats:
(a) WORD PROCESSING
(b) WORD
PROCESSING
(c) W.P.

### 1.27 Write a program to read the values of x and y and print the results of the following expressions in one line:
(a) (x+y)/(x-y)
(b) (x+y)/2
(c) (x+y)(x-y)

### 1.28 Write a program to read the following numbers, round them off to the nearest integers and print out the results in integer form:
35.7 50.21 -23.73 -46.45

### 1.29 Write a program that reads 4 floating point values in the range, 0.0 to 20.0, and prints a horizontal bar chart to represent these values using the character * as the fill character. For the purpose of the chart, the values may be rounded off to the nearest integer. For example, the value 4.36 should be represented as follows.
* * * * *
* * * * 4.36
* * * *
Note that the actual values are shown at the end of each bar.

### 1.30 Write an interactive program to demonstrate the process of multiplication. The program should ask the user to enter two two-digit integers and print the product of integers as shown below.
45
37
7 × 45 is 315
3 × 45 is 135
Add them 1665

### 1.31 Write a program to read three integers from the keyboard using one scanf statement and output them on one line using:
(a) three printf statements,
(b) only one printf with conversion specifiers, and
(c) only one printf without conversion specifiers.

### 1.32 Write a program that prints the value 10.45678 in exponential format with the following specifications:
(a) correct to two decimal places;
(b) correct to four decimal places; and
(c) correct to eight decimal places.

### 1.33 Write a program to print the value 345.6789 in fixed-point format with the following specifications:
(a) correct to two decimal places;

### 1.46 Write a program to read a four digit integer and print the sum of its digits.
Hint: Use / and % operators.

### 1.47 Write a program to print the size of various data types in C.

### 1.48 Given three values, write a program to read three values from keyboard and print out the largest of them without using if statement.

### 1.49 Write a program to read two integer values m and n and to decide and print whether m is a multiple of n.

### 1.50 Write a program to read three values using scanf statement and print the following results:
- (a) Sum of the values
- (b) Average of the three values
- (c) Largest of the three
- (d) Smallest of the three

### 1.51 The cost of one type of mobile service is Rs. 250 plus Rs. 1.25 for each call made over and above 100 calls. Write a program to read customer codes and calls made and print the bill for each customer.

### 1.52 Write a program to print a table of sin and cos functions for the interval from 0 to 180 degrees in increments of 15 as shown below.

| x (degrees) | sin (x) | cos (x) |
|---|---|---|
| 0 | ...... | ...... |
| 15 | ...... | ...... |
| ... |  |  |
| 180 | ...... | ...... |

### 1.53 Write a program to compute the values of square-roots and squares of the numbers 0 to 100 in steps 10 and print the output in a tabular form as shown below.

| Number | Square-root | Square |
|---|---|---|
| 0 | 0 | 0 |
| 100 | 10 | 10000 |

### 1.54 Write a program that determines whether a given integer is odd or even and displays the number and description on the same line.

### 1.55 Write a program to illustrate the use of cast operator in a real life situation.

## Key Terms
- **Computer:** It is an electronic device that takes data and instructions as input from the user, processes the data, and generates useful information as an output.
- **Vacuum tube:** It was used in the first generation computers for developing the circuitry. It comprised of glass and filaments.
- **Transistor:** It is a solid state device used in the second generation computers. It replaced vacuum tubes.
- **IC:** It is a silicon chip that embeds an electronic circuit comprising of several components, such as transistors, diodes, and resistors. It is used in third generation computers.
- **Microprocessor:** It is a processor chip used in fourth generation computers. It integrates thousands of components on a single chip.
- **LAN:** It is a network, where multiple computers in a local area, such as home, office, or small group of buildings, are connected and allowed to communicate among them.
- **WAN:** It is a network, which facilitates connection and communication of hundreds of computers located across multiple locations.
- **MAN:** It is a network that is used to connect the computers over a large geographical area, such as district or city.
- **GUI:** It is a user-friendly interface that provides icons and menus to interact with the various computer applications.
- **Microcomputer:** It is defined as a computer that has a microprocessor as its CPU.
- **Minicomputer:** It is a medium-sized computer that is designed to serve multiple users simultaneously.
- **Mainframe computer:** It is a computer, which helps in handling the information processing of various organizations like banks, insurance companies, hospitals and railways.

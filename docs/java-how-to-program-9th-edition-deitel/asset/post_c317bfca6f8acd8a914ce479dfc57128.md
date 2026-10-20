
2.5 Write declarations, statements or comments that accomplish each of the following tasks:
a) State that a program will calculate the product of three integers.
b) Create a Scanner called input that reads values from the standard input.
c) Declare the variables x, y, z and result to be of type int.
d) Prompt the user to enter the first integer.
e) Read the first integer from the user and store it in the variable x.
f) Prompt the user to enter the second integer.
g) Read the second integer from the user and store it in the variable y.
h) Prompt the user to enter the third integer.
i) Read the third integer from the user and store it in the variable z.
j) Compute the product of the three integers contained in variables x, y and z, and assign the result to the variable result.
k) Display the message "Product is" followed by the value of the variable result.

2.6 Using the statements you wrote in Exercise 2.5, write a complete program that calculates and prints the product of three integers.

## Answers to Self-Review Exercises

2.1 a) left brace ({), right brace (}). b) if. c) // . d) Space characters, newlines and tabs. e) Keywords. f) main. g) System.out.print, System.out.println and System.out.printf.

2.2 a) False. Comments do not cause any action to be performed when the program executes. They're used to document programs and improve their readability.
b) True.
c) False. Java is case sensitive, so these variables are distinct.
d) False. The remainder operator can also be used with noninteger operands in Java.
e) False. The operators *, / and % are higher precedence than operators + and -.

2.3 a) int c, thisIsAVariable, q76354, number;
or
int c;
int thisIsAVariable;
int q76354;
int number;

System.out.print( "Enter an integer: " );

value = input.nextInt();

System.out.println( "This is a Java program" );

2.4 a) Error: Semicolon after the right parenthesis of the condition ( c < 7 ) in the if. Correction: Remove the semicolon after the right parenthesis. [Note: As a result, the output statement will execute regardless of whether the condition in the if is true.] b) Error: The relational operator => is incorrect. Correction: Change => to >=.

2.5 a) // Calculate the product of three integers
b) Scanner input = new Scanner( System.in );
c) int x, y, z, result;
or
int x;
int y;
int z;
int result;
d) System.out.print( "Enter first integer: " );
e) x = input.nextInt();
f) System.out.print( "Enter second integer: " );
g) y = input.nextInt();
h) System.out.print( "Enter third integer: " );
i) z = input.nextInt();
j) result = x * y * z;
k) System.out.printf( "Product is %d\n", result );

### 2.6 The solution to Self-Review Exercise 2.6 is as follows:

```
// Ex. 2.6: Product.java
// Calculate the product of three integers.
import java.util.Scanner; // program uses Scanner

public class Product
{
    public static void main( String[] args )
    {
        // create Scanner to obtain input from command window
        Scanner input = new Scanner( System.in );

        int x; // first number input by user
        int y; // second number input by user
        int z; // third number input by user
        int result; // product of numbers

        System.out.print( "Enter first integer: " ); // prompt for input
        x = input.nextInt(); // read first integer

        System.out.print( "Enter second integer: " ); // prompt for input
        y = input.nextInt(); // read second integer

        System.out.print( "Enter third integer: " ); // prompt for input
        z = input.nextInt(); // read third integer

        result = x * y * z; // calculate product of numbers

        System.out.printf( "Product is %d\n", result );
    } // end method main
} // end class Product
```

Enter first integer: 10
Enter second integer: 20
Enter third integer: 30
Product is 6000

## Exercises

2.7 Fill in the blanks in each of the following statements:
- a) ______ are used to document a program and improve its readability.
- b) A decision can be made in a Java program with a(n) ______.

## Exercises

2.16 (Comparing Integers) Write an application that asks the user to enter two integers, obtains them from the user and displays the larger number followed by the words "is larger". If the numbers are equal, print the message "These numbers are equal". Use the techniques shown in Fig. 2.15.

2.17 (Arithmetic, Smallest and Largest) Write an application that inputs three integers from the user and displays the sum, average, product, smallest and largest of the numbers. Use the techniques shown in Fig. 2.15. [Note: The calculation of the average in this exercise should result in an integer representation of the average. So, if the sum of the values is 7, the average should be 2, not 2.3333...]

![](img/009e962758dcc71dbc43a493362e6dc0_104_0.png)

2.19 What does the following code print?

System.out.println( "**\n**\n**\n**\n****" );

System.out.println( "**\n**\n**\n**\n****" );

2.20 What does the following code print?

System.out.println( "**" );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );

2.21 What does the following code print?

System.out.println( " " );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );

2.22 What does the following code print?

System.out.println( " " );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );
System.out.println( "*****" );

2.23 What does the following code print?

System.out.printf( "%5s\n%s\n%s\n%s\n%s\n", "**", "*****", "*****", "*****", "*****" );

2.24 (Largest and Smallest Integers) Write an application that reads five integers and determines and prints the largest and smallest integers in the group. Use only the programming techniques you learned in this chapter.

2.25 (Odd or Even) Write an application that reads an integer and determines and prints whether it's odd or even. [Hint: Use the remainder operator. An even number is a multiple of 2. Any multiple of 2 leaves a remainder of 0 when divided by 2.]

2.26 (Multiples) Write an application that reads two integers, determines whether the first is a multiple of the second and prints the result. [Hint: Use the remainder operator.]

2.27 (Checkerboard Pattern of Asterisks) Write an application that displays a checkerboard pattern, as follows:

* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *

2.28 (Diameter, Circumference and Area of a Circle) Here’s a peek ahead. In this chapter, you learned about integers and the type int. Java can also represent floating-point numbers that contain decimal points, such as 3.14159. Write an application that inputs from the user the radius of a circle as an integer and prints the circle’s diameter, circumference and area using the floating-point value 3.14159 for π. Use the techniques shown in Fig. 2.7. [Note: You may also use the predefined constant Math.PI for the value of π. This constant is more precise than the value 3.14159. Class Math is defined in package java.lang. Classes in that package are imported automatically, so you do not need to import class Math to use it.] Use the following formulas (r is the radius):

diameter = 2r
circumference = 2πr
area = πr²

Do not store the results of each calculation in a variable. Rather, specify each calculation as the value that will be output in a System.out.printf statement. The values produced by the circumference and area calculations are floating-point numbers. Such values can be output with the format specifier %f in a System.out.printf statement. You’ll learn more about floating-point numbers in Chapter 3.

2.29 (Integer Value of a Character) Here’s another peek ahead. In this chapter, you learned about integers and the type int. Java can also represent uppercase letters, lowercase letters and a considerable variety of special symbols. Every character has a corresponding integer representation. The set of characters a computer uses together with the corresponding integer representations for those characters is called that computer’s character set. You can indicate a character value in a program simply by enclosing that character in single quotes, as in 'A'.

You can determine a character’s integer equivalent by preceding that character with (int), as in
(int) 'A'

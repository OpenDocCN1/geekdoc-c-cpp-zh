![](images/00002.jpeg)

Book 1

C++ Programming Professional Made Easy

BY SAM KEY

&

Book 2

Rails Programming Professional Made Easy

BY SAM KEY

Book 1

C++ Programming Professional Made Easy

BY SAM KEY

Expert C++ Programming Language Success in a Day for Any Computer User!

Copyright 2015 by  Sam Key - All rights reserved.

In no way is it legal to reproduce, duplicate, or transmit any part of this document in either electronic means or in printed format. Recording of this publication is strictly prohibited and any storage of this document is not allowed unless with written permission from the publisher. All rights reserved.

Table Of Contents

Introduction

Chapter 1 - Introduction to C++

Chapter 2 - C++ Variables and Operators

Chapter 3 - All About User Input

Chapter 4 - Using Flow Control Statements

Conclusion

Preview Of ‘Android Programming’

Check Out My Other Books

Introduction

I want to thank you and congratulate you for downloading the book, “Professional C++ Programming Made Easy”.

This book contains proven steps and strategies on how to learn the C++ programming language as well as its applications.

There’s no need to be a professional developer to code quick and simple C++ programs. With this book, anyone with basic computer knowledge can explore and enjoy the power of the C++ Programming Language. Included are the following fundamental topics for any beginner to start coding today:

*   The basic C++ terms
*   Understanding the C++ Program Structure
*   Working with Variables, Expressions, and Operators
*   Using the Input and Output Stream for User Interaction
*   Creating Logical Comparisons
*   Creating Loops and Using Condition Statements
*   And Many More!

Thanks again for downloading this book, I hope you enjoy it!

Chapter 1 – Introduction to C++

What You Will Learn:

**A Brief History of the C++ Language

**C++ Basic Terminology

**C++ Program Structure

C++ is one of the most popular programming languages that people are using today. More specifically, C++ is a library of “commands” that tell your computer what to do and how to do it. These commands make up the C++ source code.

Take note that C++ is different from the C programming language that came before it. In fact, it is supposedly better version of the C language when Bjarne Stroustrup created it back in 1983\.

Even today, the C++ language serves as the “starting point” for many experts in the world of programming. Although it is particularly easy to learn and apply, the ceiling for C++ mastery is incredibly high.

C++ Basic Terminology

Of course, the first step in learning the C++ programming language is to understand the basic terms. To prevent any unnecessary confusion at any point as you read this book, this section explains the most commonly used terms in the C++ program syntax. Just like the entire programming language itself, most terms in C++ are easy to remember and understand.

Compiler

Before anything else, take note that a compiler is needed to run the codes you’ve written with C++. Think of compilers as “translators” that convert programming language into machine language – the language that a computer understands. The machine language consists of only two characters (1s and 0s), which is why it is also called as binary language. If you’re learning C++ at school, then you shouldn’t worry about getting a compiler for C++ or an Integrated Development Environment for that matter.

Integrated Development Environment

An Integrated Development Environment (IDE) is essentially the software you’re using to write C++ programs. It only makes sense for IDEs to come with compilers needed to run your codes. If you have no experience with C++ programming and attempting to learn it on your own, you can opt for a free C++ IDE such as Code::Blocks. A good choice for complete beginners is to opt for a simple C++ IDE such as Quincy 2005 since there is very little setup required.

Variables and Parameters

Variables are individual blocks in the program’s memory that contains a given value. A value may be set as a constant, determined by the value of other variables using operators, or set/changed through user input. Variables are denoted by variable names or identifiers. In programming with C++, you can use any variable name you desire as long as all characters are valid.  Remember that only alphanumeric characters and “underscores” (_) can be used in identifiers. Punctuation marks and other symbols are not allowed.

Keep in mind that variables always need to be declared first before they can be used. Declaring variables are different from deciding their actual values; meaning both processes are done in two different codes. These processes will be explained in the next chapter.

“Parameters” work the same way as regular variables. In fact, they are even written in the same syntax. However, parameters and variables are initialized in different ways. Parameters are specifically included in functions to allow arguments to be passed to a separate location from which the functions are called.

Statements

Every program written with C++ consists of different lines of code that performs tasks such as setting variables, calling functions, and other expressions. These lines are statements. Each individual statement always ends with a semicolon (;). More importantly, statements in a function are executed chronologically based on which comes first. Of course, this order can be altered using flow control statements such as “if statements” and “loops”.

Functions

Functions are blocks in a C++ program structured to complete a single task. You can call upon functions at any point whilst the program is running. Curly brackets or braces ({}) enclose the statements or “body” in each function. Aside from a function name, functions are also set with corresponding “types” which refer to the requested form of returned value. You can also use and set parameters at the beginning of each function. They are enclosed in parentheses “()” and separated using commas (,).

In C++, the following is the most used syntax when creating functions:

“type” “name” ( parameter 1, parameter 2, parameter 3, …)

{
              “statements”;
}

Comments

When working on particularly bigger projects, most experienced programmers use “comments” that can be used as descriptions for specific sections in a C++ program. Comments are completely ignored by a compiler and can therefore ignore proper coding syntax. Comments are preceded either by a two slashes (//) or a slash-asterisk (/*). You will find comments in the examples throughout this book to help you understand them. A quick example would be the “Hello World!” program below. Of course, you can also use comments in your future projects for reference and debugging purposes.

The C++ Program Structure

The program structure of C++ is very easy to understand. The compiler reads every line of code from top to bottom. This is why the first part of a C++ program usually starts with preprocessor directives and the declaration of variables and their values. The best way to illustrate this structure is to use the most popular example in the world of C++ -- the “Hello World!”  program. Take note of the lines of code as well as the comments below:

#include <iostream> // this is a preprocessor directive

int main() // this line initiates the function named main, which should be found in every C++ program

{

std::cout << “Hello World!”; // the statements found between the curly braces make up the main function’s body

return 0; // the return 0; statement is required to tell the program that the function ran correctly. However, some compilers do not require this line in the main function

}

The topmost line (“#include <iostream>”) is a preprocessor directive that defines a section of the standard C++ programming library known as the Input/Output Stream or simply iostream. This section handles the input and output operations in C++ programs. Remember that this is important if you wish to use “std::cout” in the main function’s body.

The first line “int main ()” initializes the main function. Remember that the “int” refers to the integer data type and he “main” refers to the function’s name. There are other data types aside from int. But you should focus on the integer data type for now. Since the “Hello World!” program does not need a parameter, it leaves the space between the parentheses succeeding the function name blank. Also, bear in mind that you should NOT place a semicolon (;) after initializing functions.

Next is the function’s body, denoted by the open curly brace. This particular part (“std::cout”) of the program refers to the standard character output device, which is the computer’s display device. Next comes the insertion operator (<<) from the input/output stream which means the rest of the line is to be outputted (excluding quotations). Lastly, the statement is closed with a semicolon (;).

The last line in the function’s body is the return statement (“return = 0;”). Remember that the return expression (in this example, “0”) depends on the data type specified upon initialization of the function. However, it is possible to create functions without the need for return statements using the “void” function type. For example; void main ().

An alternate way to do this is to include the line “using namespace std;” under the preprocessor line so you no longer need to write “std::” each time you use it. If you opt for this method, the code would look like:

#include <iostream>

using namespace std;

int main()

{

              cout << “Hello World!”;

              return 0;

}

Chapter 2 – C++ Variables and Operators

What You Will Learn:

**Introduction to C++ Operators and How to Use Them

**Declaring and Determining the Value of Variables

**Creating New Lines in the Program Output

In a C++ program, variables and constants are controlled or “operated” using Operators. Take note that the basic operators in the C++ programming language are essentially the same as arithmetic operator. This includes the equal sign (=) for assigning expressions, the plus sign (+) for addition, the minus sign (-) for subtraction, the asterisk (*) for multiplication, the forward slash (/) for division, and the percentage sign (%) for obtaining the remainder from any expression.

C++ also uses other operators to fulfill additional tasks other than basic arithmetic operations. As mentioned in the previous chapter, the iostream header allowed you to use the insertion operator (<<) for processing output. There are also different operators accessible even without the #include directive. These “basic” operators can be categorized under increment/decrement operators, comparison operators, compound assignment operators, and logical operators.

Declaring Variables

Before using variables in C++ operations, you must first declare them and determine their values. Again, declaring variables and giving their values are two separate processes. The syntax for declaring variables are as follows:

“type” “variable”;

Just like when initializing functions, you need to specify the data type to be used for a given variable. For example; say you want to declare “x” as an integer variable. The initialization should look like this:

int x;

After the declaration of x, you can give it a value using the assign operator (=). For example; to assign the value “99” to variable x, use the following line:

x = 99;

Make sure to declare a variable first before you assign a value to it. Alternatively, you can declare a variable and assign a value to it using a single line. This can be done using:

int x = 99;

Aside from setting these expressions as you write the program, you can also use operations and user input to determine their values as the program runs. But first, you need to learn about the other operators in C++.

Increment and Decrement Operators

The increment operator consists of two plus signs (++) while the decrement operator consists of two minus signs (--). The main purpose of increment and decrement operators is to shorten the expression of adding and subtracting 1 from any given variable. For example; if x = 2, then ++x should equal 3 while –x should equal 1\.

If being used to determine the values of two or more variables, increment and decrement operators can be included as either a prefix or suffix. When used as a suffix (x++ or x--), it denotes the original value of x before adding or subtracting 1\. When run on their own, both ++x and x++ have the same meaning. But when used in setting other variables, the difference is made obvious. Here is a simple example to illustrate the difference:

X = 5;

Y = ++x;

In this example, the value of y is determined after increasing the value of x. In other words, the value of y in this example is equal to 6.

X = 5;

Y = x++;

In this example, the value of y is determined before increasing the value of x. In other words, the value of y in this example is equal to 6.

Compound Assignment Operators

Aside from basic arithmetic operators and the standard assignment operator (=), compound assignment operators can also be used to perform an operation before a value is assigned. Compound assignment operators are basically shortened versions of normal expressions that use basic arithmetic operators.

Here are some examples of compound assignment operators:

x -= 1;              // this is the same as the expression x = x – 1;

x *= y;              // this is the same as the expression x = x * y;

x += 1;              // this is the same as the expression x = x + 1;

x /= y;                // this is the same as the expression x = x / y;

Comparison Operators

Variables and other expressions can be compared using relational or comparison operators. These operators are used to check whether a value is greater than, less than, or equal to another. Here are the comparison operators used in C++ and their description:

==               -              checks if the values are equal

<              -              checks if the first value is less than the second

>              -              checks if the first value is greater than the second

<=              -              checks if the first value is less than or equal to the second

>=              -               checks if the first value is greater than or equal to the second

!=              -              checks if the values are NOT equal

Comparison operators are commonly used in creating condition statements. They can also be used to evaluate an expression and return a Boolean value (“true” or “false”).  Using the comparison operators listed above; here are some example expressions and their corresponding Boolean value:

(8 == 1) // this line evaluates to “false”

(8 > 1)  // this line evaluates to “true”

(8 != 1) // this line evaluates to “true”

(8 <= 1) // this line evaluates to “false”

Also take note that the Boolean value “false” is equivalent to “0” while “true” is equivalent to other non-zero integers.

Aside from numerical values, the value of variables can also be checked when using comparison operators. Simply use a variable’s identifier when creating the expression. Of course, the variable must be declared and given an identified value first before a valid comparison can be made. Here is an example scenario

#include <iostream>
using namespace std;

int main ()

{
 int a = 3;              // the values of a and b are set first
 int b = 4;
              cout << “Comparison a < b = “ << (a < b);
              return 0;
}

The output for this code is as follows:

Comparison a < b = true

Take note that the insertion operator (<<) is used to insert the value of the expression “a < b” in the output statement, which is denoted in the 7th line (“cout << “Comparison a < b = “…). Don’t forget that you need an output statement in order to see if your code works. The following code will produce no errors, but it won’t produce an output either:

#include <iostream>

int main (

{
              int a = 3;
              int b = 4;
              (a < b);
              return 0;
}

In this code, it is also true that a < b. However, no output will be produced since the lines necessary for the program output are omitted.

Logical Operators

There are also other logical operators in C++ that can determine the values of Boolean data. They are the NOT (!), AND (&&), and OR (||) operators. Here are specific examples on how they are used:

!(6 > 2) // the NOT operator (!) completely reverses any relational expressions and produces the opposite result. This expression is false because 6 > 2 is correct

(6 > 2 && 5 < 10) // the AND (&&) operator only produces true if both expressions correct. This expression is true because both 6 > 2 && 5 < 10 are correct

(6 = 2 || 5 < 10) // the OR (||) operator produces true if one of the expressions are correct. This expression is true because the 5 < 10 is correct although 6 = 2 is false.

You can also use the NOT operator in addition to the other two logical operators. For example:

!(6 = 2 || 5 < 10) // this expression is false

!(6 > 2 && 5 < 10) // this expression is also false

!(6 < 2 && 5 < 10) // this expression is true

Creating New Lines

From this point on in this book, you will be introduced to simple C++ programs that produce output with multiple lines. To create new lines when producing output, all you need to do is to use the new line character (\n). Alternatively, you can use the “endl;” manipulator to create new lines when using the “cout” code. The main difference is that the internal buffer for the output stream is “flushed” whenever you use the “endl;” manipulator with “cout”. Here are examples on how to use both:

cout << “Sentence number one \nSentence number two”;

The example above uses the new line character.

cout << “Sentence number one” << endl;
cout << “Sentence number two”;

The example above uses “endl;”.

Of course, the first code (using \n) is relatively simpler and easier for general output purposes. Both will produce the following output:

Sentence number one

Sentence number two

Chapter 3 – All About User Input

What You Will Learn:

**Utilizing the Input Stream

**Using Input to Determine or Modify Values

**How to Input and Output Strings

Up to this point, you’ve learned how to make a C++ program that can perform arithmetic operations, comparisons, and can produce output as well. This time, you will learn how to code one of the most important aspects of computer programs – user input.

As stated earlier, user input can be utilized to determine or modify the values of certain variables. C++ programs use abstractions known as streams to handle input and output. Since you already know about the syntax for output (“cout”), it’s time to learn about the syntax for input (“cin”).

The Extraction Operator

The input syntax “cin” is used with the extraction operator (>>) for formatted input.  This combination along with the keyboard is the standard input for most program environments. Remember that you still need to declare a variable first before input can be made. Here is a simple example:

int x; // this line declares the variable identifier x. Take note of the data type “int” which means that only an integer value is accepted

cin >> x;               // this line extracts input from the cin syntax and stores it to x

User input can also be requested for multiple variables in a single line. For example; say you want to store integer values for variables x and y. This should look like:

int x, y;              // this line declares the two variables

cin >> x >> y;              // this line extracts user input for variables x and y

Take note that the program will automatically require the user to input two values for the two variables. Which comes first depends on the order of the variables in the line (in this case, input for variable “x” is requested first).

Here is an example of a program that extracts user input and produces an output:

#include <iostream> // again, this is essential for input and output
using namespace std;

int main ()

{
              int x;
              cout << “Insert a random number \n”;
cin >> x; // this is where user input is extracted
              cout << “You inserted: “ << x;
              return 0;

}

Bear in mind that the value extracted from the input stream overwrites any initial value of a variable. For example, if the variable was declared as “int x = 2;” but was later followed by the statement “cin >> x;”, the new value will then replace the original value until the program/function restarts or if an assignment statement is introduced.

Strings

Keep in mind that there are other types you can assign to variables in C++. Aside from integers, another fundamental type is the string. A string is basically a variable type that can store sets of characters in a specific sequence. In other words, this is how you can assign words or sentences as values for certain variables.

First of all, you need to add the preprocessor directive “#include <string>” before you can use strings in your program. Next, you need to declare a string before it can receive assignments. For example; if you want to declare a string for “Name” and assign a value for it, you can use the code:

#include <string>
using namespace std;

int main ()

{
   string name;
name =  “Insert your name here”; // including quotations

}

Creating output using strings is basically the same as with integers. You only need to use “cout” and insert the string to the line. The correct syntax is as follows:

string name;

Name = “Your Name Here”;

cout << “My name is: “ << name;

Without any changes, the output for the above code is:

Your Name Here

Inputting Strings

To allow user input values for strings, you need to use the function “getline” in addition to the standard input stream “cin”. The syntax for this is “getline (cin, [string]);”. Below is an example program that puts string input into application.

#include <iostream>
#include <string>
using namespace std;

int main ()

{
              string name;
              cout << “Greetings! What is your name?\n”;
getline (cin, name); // this is the extraction syntax
              cout << “Welcome “ << name;
              return 0;

}

Take note that strings have “blank” values by default. This means nothing will be printed if no value is assigned or if there is no user input.

Chapter 4 – Using Flow Control Statements

What You Will Learn:

**If and Else Selection Statements

**Creating Choices

**Creating Iterating/Looping Statements

Remember that statements are the basic building blocks of a program written using C++. Each and every line that contains expressions such as a variable declaration, an operation, or an input extraction is a statement.

However, these statements are linear without some form of flow control that can establish the “sense” or “logic” behind a C++ program. This is why you should learn how to utilize flow control statements such as selection statements and looping statements. 

If and Else Statements

If and else statements are the most basic form of logic in a C++ program. Basically, the main purpose of an “if” statement is to allow the execution of a specific line or “block” of multiple statements only if a specified condition is fulfilled.

Next is the “else” statement which allows you to specify what would occur in case the conditions aren’t met. Without an “else” statement, everything inside the “if” statement will be completely ignored. Here the syntax for an “if” and “else” statement:

if (age >= 18)
              cout << “You are allowed to drink.”;
else
              cout << “You are not yet allowed to drink.”;

Remember that conditions can only be set using comparison operators and logical operators (refer to Chapter 2). Take note that you can also execute multiple statements using if/else conditions by enclosing the lines in curly braces. It is also possible to use composite conditions using logical operators such as AND (&&) and OR (||).

Finally, you can use another “if” statement after an “else” statement for even more possibilities. Of course, you also need to specify conditions for every “if” statement you use. Here is a good example that demonstrates what you can do using “if” and “else” statements in addition to user input:

#include <iostream>
using namespace std;

int main()

{
              int number;
              cout << “Enter a number from 1-3\n”;
              cin >> number;
              if (number == 1 || number == 2)
                            cout << “You have entered either 1 or 2.”;
              else if (number == 3)
                            cout << “You have entered 3.”;
              else
              {
                            cout << “Please follow the instructions\n”;
                            cout << “Please Try Again.”;
              }
              return 0;
}

There are 3 possible outcomes in the program above. The first outcome is achieved if the user entered any of the numbers 1 or 2\. The second outcome is achieved if the user entered the number 3\. Lastly, the third outcome is achieved if the user entered a different number other the ones specified.

Creating Choices (Yes or No)

Another way to utilize if/else statements is to create “Yes or No” choices. For this, you need to make use of the variable type “char” which can hold a character from the 8-bit character set (you can use char16_t, char32_t, or wchar_t for larger character sets; but this is not usually necessary). Just like all other variables, a “char” variable needs to be declared before it can be used.

Of course, you want the user to make the choice, which is why you need to use the “cin” function to extract user input. Here is a simple program that asks for the user’s gender:

#include <iostream>
using namespace std;

int main()

{
char gender; // this is the char variable declaration
              cout << “Male or Female? (M/F)”;
cin >> gender; // user input is stored to gender
              if (gender == ‘m’ || gender == ‘M’)
                            cout << “You have selected Male.”;
              else if (gender == ‘f’ || gender == ‘F’)
                            cout << “You have selected Female.”;
              else
                            cout << “Please follow the instructions.”;
              return 0;

}

Take note that you should use single quotation marks (‘) when pinpointing “char” values. In C++, “char” values are always called inside single quotation marks. Additionally, remember that “char” values are case-sensitive, which is why the example above used the OR (||) operator in the conditions to accept both lowercase and uppercase answers. You can see that the program above checked if the user entered ‘m’, ‘M’, ‘f’, or ‘F’.

Looping Statements

Lastly, using “loops” allow statements to be executed for a set number of times or until a condition is met. By incorporating other statements in loops, you can do far more than just create pointless repetitions. But first, you need to be familiar with the different types of loops.

There are 3 types of loops in C++ -- while, do, and for.

While Loop

The “while loop” is regarded as the simplest form of loop in the C++. Basically, it repeats the statement(s) as long as the given condition is true. Keep in mind that your code should be structured to eventually fulfill the condition; otherwise you might create an “infinite loop”.

Here is an example of a while loop:

int x = 100;

while (x >= 0) // the condition for the loop is set
              {
              cout << x;
--x; // the value of x is decreased
              }

In this example, the loop executes as long as the value of x is greater than or equal to 0\. Take note of the decrement operator (--) in the statement “--x;”. This makes sure that the value of x is continually decreased until the condition is met and the loop ends.

Do-While Loop

The next type of loop is the “do-while loop”. The do-while loop is essentially the same as the while loop. The main difference is that the do-while loop allows the execution of the statement(s) at least once before the condition is checked. Whereas in the while loop, the condition is checked first.

Here is an example of a do-while loop:

int x = 100;
int y;

do
              {
              cout << “The value is “ << x << “\n”;
              cout << “Enter a value to subtract.”;
              cin >> y;
              x -= y;
              }
while (x > 0); // in the do-while loop, the condition is checked last

In the example above, the statements are executed at least once before the value of x is checked. Whereas in a while loop, there is a possibility that the statement(s) will not be executed at all.

For Loop

The third type of loop is the “for loop” which has specific areas for the initialization, condition, and increase. These three sections are sequentially executed throughout the life cycle of the loop. By structure, for loops are created to run a certain number of times because increment or decrement operators are usually used in the “increase” section.

Here is the syntax for this loop to help you understand it better:

for (int x = 10; x > 0; x--)

Notice the three expressions inside the parentheses (int x = 10; x > 0; x--) are separated in semicolons. These parameters denote the three sections of the loop. You may also use multiple expressions for each section using a comma (,). Here is the syntax for this:

for ( int x = 10, y = 0; x != y; --x, ++y )
              {
              cout << “X and Y is different\n”;
              }

In this example, the loop is executed as long as x is not equal to y. And in order for the loop to end, the values of x and y are adjusted until the value of x equals the value of y. Based on the parameters above, the statement “X and Y is different” will run a total of 5 times before the loop is ended.

Conclusion

Thank you again for downloading this book! 

I hope this book was able to help you to learn and understand the C++ programming language!

The next step is to start from where you are now and try to learn something new. Keep in mind that you’ve only scratched the surface of all the things you can do in the world of C++!

Finally, if you enjoyed this book, please take the time to share your thoughts and post a review on Amazon. We do our best to reach out to readers and provide the best value we can. Your positive review will help us achieve that.  It’d be greatly appreciated!

Thank you and good luck!

![thank-you](images/00001.jpeg)

[Click here to leave a review on amazon.com](https://www.amazon.com/review/create-review?ie=UTF8&asin=B00S776K5M&channel=reviews-product&nodeID=&ref_=cm_cr_pr_wr_but_top)

Preview Of ‘Android Programming in a Day! The Power Guide for Beginners in Android App Programming

Chapter 1: Preparation

Android application development is not easy. You must have some decent background in program development. It is a plus if you know Visual Basic and Java. And it will be definitely a great advantage if you are familiar or have already used Eclipse’s IDE (Integrated Development Environment). Also, being familiar with XML will help you.

You will need a couple of things before you can start developing apps.

First, you will need a high-end computer. It is common that other programming development kits do not need a powerful computer in order to create applications. However, creating programs for Android is a bit different. You will need more computing power for you to run Android emulators, which are programs that can allow you to test your programs in your computer.

Using a weak computer without a decent processor and a good amount of RAM will only make it difficult for you to run those emulators. If you were able to run it, it will run slowly.

Second, you will need an Android device. That device will be your beta tester. With it, you will know how your program will behave in an Android device. When choosing the test device, make sure that it is at par with the devices of the market you are targeting for your app. If you are targeting tablet users, use a tablet. If you are targeting smartphones, then use a smartphone.

Third, you will need the Android SDK (Software Development Kit) from Google. The SDK is a set of files and programs that can allow you to create and compile your program’s code. As of this writing, the latest Android SDK’s file size is around 350mb. It will take you 15 – 30 minutes to download it. If you uncompressed the Android SDK file, it will take up around 450mb of your computer’s disk space. The link to the download page is: http://developer.android.com/sdk/index.html

The SDK can run on Windows XP, Windows 7, Mac OSX 10.8.5 (or higher), and Linux distros that can run 32bit applications and has glibc (GNU C library) 2.11 or higher.

Once you have unpacked the contents of the file you downloaded, open the SDK Manager. That program is the development kit’s update tool. To make sure you have the latest versions of the kit’s components, run the manager once in a while and download those updates. Also, you can use the SDK Manager to download older versions of SDK. You must do that in case you want to make programs with devices with dated Android operating systems.

[Click here to check out the rest of Android Programming in a Day on Amazon.](http://www.amazon.com/Android-Programming-Power-Beginners-Development-ebook/dp/B00QMK9MRO)

Check Out My Other Books

Below you’ll find some of my other popular books that are popular on Amazon and Kindle as well.  Simply click on the links below to check them out.  Alternatively, you can visit my author page on Amazon to see other work done by me.

[Click here to check out C Programming Success in a Day on Amazon.](http://www.amazon.com/Programming-Success-Day-programming-Developers-ebook/dp/B00Q3Y55PM)

[Click here to check out Android Programming in a Day on Amazon.](http://www.amazon.com/Android-Programming-Power-Beginners-Development-ebook/dp/B00QMK9MRO)

[Click here to check out Python Programming in a Day on Amazon.](http://www.amazon.com/Python-Programming-Day-Beginners-beginners-ebook/dp/B00R1WXCD2)

[ ](http://www.amazon.com/Python-Programming-Day-Beginners-beginners-ebook/dp/B00R1WXCD2)

[Click here to check out PHP Programming Professional Made Easy on Amazon.](http://www.amazon.com/PHP-Programming-Professional-Made-Easy-ebook/dp/B00RES3EWC)

[Click here to check out CSS Programming Professional Made Easy on Amazon.](http://www.amazon.com/CSS-Programming-Professional-Made-Easy-ebook/dp/B00RET2L2U)

[Click here to check out C Programming Professional Made Easy on Amazon.](http://www.amazon.com/Programming-Professional-Made-Easy-programming-ebook)

[Click here to check out HTML Professional Programming Made Easy on Amazon](http://www.amazon.com/HTML-Programming-Professional-Made-Easy-ebook/dp/B00SGGKHSU)             

[Click here to check out JavaScript Programming Made Easy on Amazon](http://www.amazon.com/JavaScript-Professional-Programming-Made-Easy-ebook/dp/B00SDM365S)

[Click here to check out Windows 8 Tips for Beginners on Amazon.](http://www.amazon.com/Windows-Tips-Beginners-Networking-Technology-ebook/dp/B00RW2E6JA)

If the links do not work, for whatever reason, you can simply search for these titles on the Amazon website to find them.

Book 2

Rails Programming Professional Made Easy

BY SAM KEY

Expert Rails Programming Success In A Day For Any Computer User!

Copyright 2015 by  Sam Key - All rights reserved.

In no way is it legal to reproduce, duplicate, or transmit any part of this document in either electronic means or in printed format. Recording of this publication is strictly prohibited and any storage of this document is not allowed unless with written permission from the publisher. All rights reserved.

Table Of Contents

Chapter 1 Why Rails Matters

Chapter 2 Getting Started

Chapter 3Create Your First Project

Chapter 4 Say “Hello There!”

Chapter 5 Let’s Do Something More

Chapter 6 Creating Article Title

Chapter 7 Creating the Form

Chapter 8 Save Your Data

Chapter 9 Make Your Articles Neat

Chapter 10 Create Some Rules, Too

Chapter 11 Update Articles

Chapter 12 Destroy Some Data

Preview of "C Programming Success In a Day"

Check out My Other Books

Introduction

I want to thank you and congratulate you for downloading the book, “insert book title here Professional Rails Programming Made Easy: Expert Rails Programming Success In A Day For Any Computer User!”

This book contains proven steps and strategies on how to learn the program Ruby on Rails and immediately create an application by applying the rudiments of this platform.

Rails is one of the newest and most popular platforms. Thanks to the growth of Internet, this platform has been targeting audiences that are quite interested in creating stable web designs. If your work involves the Internet and you want to implement ideas that would help you launch projects online, you would definitely want to learn how to code using this program. Within this book are everything that you need to learn from installing the platform, getting the basics and making sure that you are ready to rock any programmer’s boat.

Thanks again for downloading this book. I hope you enjoy it!

# Chapter 1 Why Rails Matters

If you are a computer programmer, the Ruby on Rails platform would probably the next program that you have to learn how to use. It is also worth looking into if your work is largely based on design, and you want to try something current to make websites easy to manipulate and beautiful. It could also be the platform that would launch your career or create leverage for yourself at the office. Yes, this platform could be your trump card to your next promotion, or that awesome site that you have in mind.

What Rails Can Do For You

If you are wondering what good this program can do for most computer users, then here are the awesome things that you can get out of the platform.

1\. Get to Code

Coding is not rocket science, and if you are using Ruby, you probably would not even feel that you are using a programming language. You would want to learn to code to retain what you are going to experience with the platform, so take the time to study anyway.

If you are getting into Rails, you do not need to be a Computer Science major. If you are a businessman who has a great idea for a web app and you want to try coding it yourself, then this platform may be your best bet.

2\. Get to Code Better

Sometimes it is not about arguing what is the best platform out there and get drunk arguing which is the best among Python, Java, PHP, or Ruby. If you already know other programming languages, you would need to still keep up with the times and learn some new tricks. Ruby on Rails provides that opportunity.

3\. Get to Code Faster

RoR is a beautiful platform that allows you to write shorter codes, and it has a great set of features for exception handling which makes it really easy to spot and handle possible errors. You also would not need to still maintain the usual reference counts in your extension libraries. You also get awesome support using Ruby from C, which gives you better handle when you want to write C extensions.

RoR makes any programmer productive because it is opinionated and it gives guesses on how you can probably code something in the best way possible. The Don’t Repeat Yourself (DRY) Principle of RoR also makes you skip the usual coding process of writing something again and again, which often makes the code long, complex, and difficult to debug. That means that at the end of the project, you get to look at your code and have a better grasp of what happened there.

4\. Understand How Twitter Works

Yes, Twitter is created using RoR, and if you are an SEO specialist, a web designer, or simply a tech geek, knowing how this social media platform is done would definitely help you out. You would also discover that a lot of the hot new websites today are built on this platform.

5\. Learn a Platform with a Great Community

RoR is relatively young compared to other programming languages, and for that reason, it has a very active and collaborative community. You definitely would get to hang out with several other developers and would probably build something together. Doing that is always good for your résumé.

6\. It works with all operating systems and offers threading that is independent from the operating system. That means that is also very portable, and would even work on a computer that runs on Windows 95.

If these perks sound great, then it’s time to get started with a Rails project!

# Chapter 2 Getting Started

If you want to learn how to use Rails, then you would need to first have the following:

1\. Ruby – choose the language version that is 1.9.3, or later. You can download it by visiting ruby-lang.org.

2\. RubyGems packaging system – it is typically installed with Ruby that has versions 1.9 or newer.

3\. Installed SQLite3 Database

Rails, as you probably figured out, is a framework dedicated to web application development written in the language of Ruby. That means that you would want to learn a little bit of Ruby coding in order to eliminate any difficulty in jumping into Rails. If you have a browser open, you can get great help in practicing Ruby codes by logging in to tryruby.org, which features a great interactive web tutorial. Try it out first to get the hang out of coding with Ruby.

If you do not have any working SQLite 3 yet, you can find it at sqlite.org. You can also get installation instructions there.

Installing Rails

1\. Run the Rails installer (for Windows and Mac users) or the Tokaido (Mac OS X users)

2\. Check out the version of the installed Ruby on your computer by running the Run command on Start menu and then typing cmd on the prompt (Windows). If you are running on Mac OS X, launch Terminal.app.

Key in “$ ruby –v” (no captions). After you hit Enter, you will see the Ruby version installed

3\. Check out the version of SQLite3 installed by typing “$ sqlite3 –version”.

4\. After Rails installation, type in “$ rails –version” on Terminal.app or at the command prompt. If it says something similar to Rails 4.2.0, then you are good to go.

A Note on the $ sign

The $ sign would be used here in this book to look like the terminal prompt where you would type your code after. If you are using Windows for the Rails platform, you would see something like this: c:\source_code> .

Chapter 3 Create Your First Project

Here’s something that most web developers are raving about Rails: it comes with generators, or scripts that are made to make development a lot easier by making all things that you need to get started on a particular project. Among these scripts is the new application generator, which gives you the foundation you need for a new Rails app so you do not have to write one yourself. Now that allows you to jump right into your code!

Since you are most likely to build a website or an API (application program interface), you would want to start coding a blog application. To start, launch a terminal and go to any directory where you can create files. On the prompt, type “$ rails new blog.”

After you hit Enter, Rails will start making an application called Blog in the directory. It will also start making gem dependencies that you already have in your Gemfile bundle install.

Now, go to where your blog app is by typing in “$ cd blog”.

What’s in There?

Once you get into the directory, you will find a number of files that Rails have already installed by default. If you are not quite sure about what these files are for, here’s a quick rundown of the file or folder functions:

1\. app/ - this has the models, helpers, mailers, assets, and controllers for the app you just created. You’ll be looking more at this folder later.

2\. bin/ - this has the script that you will use to run the app. Also, this has other scripts that you will be using to deploy, setup, or run the application you are going to create.

3\. config/ - this allows you to tweak the app’s database, routes, etc.

4\. config.ru – this is the configuration that will be used by Rack-based servers to run the app.

5\. db/ - this would contain your database and database migrations

6\. Gemfile, Gemfile.lock – these would allow you to tell the program what sort of gem dependencies you are going to need for the app you’re building.

7\. lib/ - contains the extended modules needed for the app

8\. lib – contains the app’s log files

9\. public/ – this would be the sole folder that other people could see. It would be containing all your compiled assets and created static files.

10\. Rakefile – this would be the one file that would locate and load tasks that can be set to run from the command line. You can add tasks that you would prefer to use later on by adding the files needed to the lib/tasks directory

11\. README.rdoc – just like readme’s function, this would be a brief document that would tell other people how your app works, how to set it up, etc.

12\. test/ - these would contain all your unit tests and all the things that you are going to need for testing.

13\. tmp/ - this would hold all temporary files

14\. vendor/ - this would contain all your third-party codes and would also contain all vendored gems.

Now, if you are seeing all these in the app directory you just made, then you are ready to create little bits and pieces that you would be adding up later to make a real blog app!

Firing Up the Web Server

Since you already have the barebones of your blog application, you would want to set up how the app is going to be launched on the internet. To start a web server go to the directory where blog is located, and then type “$ bin/rails server”.

Important note:

You would need to have a JavaScript runtime available in your computer if you want to use asset compression for JavaScript or if you want to compile a CoffeeScript. Otherwise, you would expect to see an execjs error when you attempt to compile these assets. If you want to look at all the supported runtimes, you can go to github.com/sstephenson/execjs#readme.

If you are successful, what you just did would launch WEBrick, which is the server that Ruby apps use by default. You can see what’s happening so far in your app by firing up a web browser and typing http://localhost:3000\. Now, since you have done nothing much, you would be seeing the Rails default page. It will tell you that you are currently in development mode. You also do not need to constantly require the server to look at the changes that you have made – any changes will be automatically picked up and seen. Also keep in mind that if you managed to see this “Welcome Aboard” thing, you are sure that you created an app that is configured correctly. If you want to find out the app’s environment, click on “About your application’s environment” link.

Got everything right so far? Let’s move on to making something other people can read.

# Chapter 4 Say “Hello There!”

If you want to make Rails learn how to say Hi to other people, you would need the following:

1\. A controller

The purpose of a controller is to allow your program to receive any requests. When you route, you enable Rails to decide which of the controllers you set up will receive which types of requests. That may also mean that there would be different routes leading to the controller, which would be triggered by specific actions. An action is required in order to collect any information needed in order to send it to a view

2\. A view

This thing’s main purpose is to enable Rails to display the information made available to the action and display it in a format that other people can read. There are different view templates that are already available and coded using eRuby, which can be used in request cycles before it the information is sent to anyone who wants to look at this information.

Got it? Good. Now, to setup your welcome page, you need to generate a controller and then name it “welcome” using an action named “index”. Your code will look like this:

$ bin/rails generate controller welcome index

Now, Rails will be creating a bunch of files plus a route for you to use. When Rails is done with that, you will see this:

create  app/controllers/welcome_controller.rb

route  get 'welcome/index'

invoke  erb

create    app/views/welcome

create    app/views/welcome/index.html.erb

invoke  test_unit

create    test/controllers/welcome_controller_test.rb

invoke  helper

create    app/helpers/welcome_helper.rb

invoke  assets

invoke    coffee

create      app/assets/javascripts/welcome.js.coffee

invoke    scss

create      app/assets/stylesheets/welcome.css.scss

If you want to view where the course of your controller is, go to app/controllers/welcome_controller.rb. If you want to look at the view, you can find it at app/views/welcome/index.html.erb.

Here comes the fun part. Pull up a text editor and open app/views/welcome/index.html.erb there. Clear all the codes you see there, and replace it with this:

              <h1>Hello Rails!</h1>

After doing so, you have successfully informed Rails that you want “Hello Rails!” to appear. That means that it is also the greeting that you want to see when you go to [http://localhost:3000](http://localhost:3000), which is still displaying “Welcome aboard”.

Create the App’s Home Page

The next thing that you need to do is to tell Rails where the home page is. To do that, pull up your text editor again and open config/routes.rb. You should see something like this:

              Rails.application.routes.draw do

  get 'welcome/index'

  # The priority is based upon order of creation:

  # first created -> highest priority.

  #

  # You can have the root of your site routed with "root"

  # root 'welcome#index'

  #

  # ...

Those lines represent the routing file which tells Rails how to link requests to specific actions and controllers. Now, find the line “root 'welcome#index'” and uncomment it. When you get back to [http://localhost:3000](http://localhost:3000), you will see that it now displays Hello Rails!

# Chapter 5 Let’s Do Something More

Now that you have figured out how to make a controller, a view, and an action, it’s time to create a new resource. A resource is something that groups together similar objects the same way you group people, plants, and animals. To make items for resources, you use the CRUD method (create, read, update, destroy).

Rails make it easy for you to build websites because it already comes with a method for resources that it can use for making a REST resource. REST, or Representational State Transfer is known as the web’s architectural structure which is used to design all applications that use a network, and instead of using rather complex operations to link two machines, you can use HTTP to make machines communicate. That means that in a lot of ways, the Internet is based on a RESTful design.

Now, following the project you are creating, pull up config/routes.rb and make sure it’s going to look like this:

Rails.application.routes.draw do

  resources :articles

  root 'welcome#index'

end

If you are going to look at the rake routes, you will notice that Rails has already made routes for all actions involving REST. It is going to look like this:

$ bin/rake routes

      Prefix Verb   URI Pattern                  Controller#Action

    articles GET    /articles(.:format)          articles#index

             POST   /articles(.:format)          articles#create

new_article GET    /articles/new(.:format)      articles#new

edit_article GET    /articles/:id/edit(.:format) articles#edit

     article GET    /articles/:id(.:format)      articles#show

             PATCH  /articles/:id(.:format)      articles#update

             PUT    /articles/:id(.:format)      articles#update

             DELETE /articles/:id(.:format)      articles#destroy

        root GET    /                            welcome#index

#  Chaper 6 Creating Article Title

This part would be the creating and reading part of CRUD, where you would put in a location where you would be placing articles for the blog you’re building. In order to do so, you can create an ArticlesController by running this code:

$ bin/rails g controller articles

Now, you need to manually place an action inside the controller that you just created. Go to app/controllers/articles_controller.rb and pull up the class ArticlesController. Edit it to look like this:

class ArticlesController < ApplicationController

  def new

  end

end

You now have to create a template that Rails would be able to view. In order to create a title for the article that you want to display, pull up app/views/articles/new.html.erb and make a new file there. Type the following:

<h1>New Article</h1>

What did just happen? Check out http://localhost:3000/articles/new and you will see that the page now has a title! You will now want to create a template that will look like a form that you can fill up to write your articles in online.

#  Chapter 7 Creating the Form

Pull up app/views/articles/new.html.erb and then add this code:

              <%= form_for :article do |f| %>

  <p>

    <%= f.label :title %><br>

    <%= f.text_field :title %>

  </p>

  <p>

    <%= f.label :text %><br>

    <%= f.text_area :text %>

  </p>

  <p>

    <%= f.submit %>

  </p>

<% end %>

You will see that you have just created a form that has a space for the article title text, submit button, and it comes with boxes too! That is the function of the code form_for. You will realize that when you submit an article you are going to create, it needs to be done in another URL and then the entire text should then go somewhere else. Edit app/views/articles/new.html.erb by finding the form_for line and make it look like this:

<%= form_for :article, url: articles_path do |f| %>

In Rails, the action “create” does the job of making new forms for submissions, and therefore, your form should be working towards this action. You would notice that when you try to submit an article, you would see an error there. In order to make it work, you need to make a “create action” within the ArticlesController.

Create the Article

In order to get rid of this error, you need to edit the ArticlesController class found in app/controllers/articles_controller.rb. It should look like this:

class ArticlesController < ApplicationController

def new

end

def create

end

end

Once that is done, the controller should now be able to save the article to the database. Now, you would need to set the parameters of actions done by controllers. Now, make the ending of the above lines to look like this instead:

def create

  render plain: params[:article].inspect

end

Now that should make the error go away. Try refreshing the page to see what happened.

Make the Model

Rails already provide a generator that would be used by your project to launch a model. To order Rails to start generating one, run this on the terminal:

$ bin/rails generate model Article title:string text:text

What just happened is that you told Rails that you are requiring an Article model that has a title and a text that are attributed to separate strings. You would see that the platform made up a lot of files, but you would be most interested in db/migrate/20140120191729_create_articles.rb which contains your blog’s database.

Now, you would want to run a migration, which you can do with a single line of code:

$ bin/rake db:migrate

What Rails would do is that it would be executing this command which means that it made the Articles Table:

==  CreateArticles: migrating ==================================================

-- create_table(:articles)

   -> 0.0019s

==  CreateArticles: migrated (0.0020s) =========================================

Chapter 8 Save Your Data

Pull up app/controllers/articles_controller.rb and edit the “create” action into this:

def create

  @article = Article.new(params[:article])

  @article.save

  redirect_to @article

end

You’re almost able to create an article! However, when you refresh the page, you would see a Forbidden Attributes Error, and would point you at the line @article – Article.new(params[:article]). The reason Rails is giving you a hard time is because it wants you to tell what parameters should be in your controller actions. That allows your program to be secure once you run it, and prevent it from assigning wrong controller parameters which can make your entire coded program crash.

To fix this, edit out the highlighted line in the error you just saw and change it into:

@article = Article.new(params.require(:article).permit(:title, :text))

Show Your Work

In order to make the page display your article, you can make use of the “show” action by adding it to app/controllers/articles_controller.rb. Add these following lines:

class  ArticlesController < ApplicationController

  def  show

    @article  = Article.find(params[:id])

  end

  def  new

  end

Now let’s add some style. Create a new file named app/views/articles/show.html.erb and put in the following lines:

<p>

  <strong>Title:</strong>

  <%= @article.title %>

</p>

<p>

  <strong>Text:</strong>

  <%= @article.text %>

</p>

Refresh [http://localhost:3000/articles/new](http://localhost:3000/articles/new) and then you will see that you can create articles and display them!

#  Chapter 9 Make Your Articles Neat

Find a way to list all the articles that you are going to create in order to have an organized database. To do that, pull up app/controllers/articles_controller.rb and add the following lines to create a control.

class ArticlesController < ApplicationController

  def index

    @articles = Article.all

  end

  def show

    @article = Article.find(params[:id])

  end

  def new

  end

Now, to add a view, pull up app/views/articles/index.html.erb and then add the following lines:

<h1>Article List</h1>

<table>

  <tr>

    <th>Title</th>

    <th>Text</th>

  </tr>

  <% @articles.each do |article| %>

    <tr>

      <td><%= article.title %></td>

      <td><%= article.text %></td>

    </tr>

  <% end %>

</table>

Head over to [http://localhost:3000/articles](http://localhost:3000/articles) and you will see all the articles that you have made so far.

Tidy Up Some More with Links

You definitely need to create links for the articles that you have created so your readers can pull them up easily. To add links, open app/views/welcome/index.html.erb and then change it to look like this:

<h1>Hello, Rails!</h1>

<%= link_to 'My Blog', controller: 'articles' %>

Now, what if you want to add a link that would allow you to write a new article right away? All you need to do is to add the following lines to app/views/articles/index.html.erb to have a New Article link:

%= link_to 'New article', new_article_path %>

If you want to create a link to go back to where you were previously, add the following lines to the same file:

<%= form_for :article, url: articles_path do |f| %>

  ...

<% end %>

<%= link_to 'Back', articles_path %>

#  Chapter 10 Create Some Rules, Too

When you are creating a blog program, you do not want your users to accidentally submit a blank page, and then just land right back where they were without knowing what they did. Rails can help you make sure that doesn’t happen by editing the app/models/article.rb file to look like this:

class Article < ActiveRecord::Base

  validates :title, presence: true,

                    length: { minimum: 5 }

end

That means that the title should be at least 5 characters in order for the article to go through, otherwise it would not be saved. Now that this rule for your blog is in place, you need to show the blog user that something went wrong and that the form should be filled up properly. To do that, tweak the “create” and “new” actions in app/controllers/articles_controller.rb in order to look like this:

def new

  @article = Article.new

end

def create

  @article = Article.new(article_params)

  if @article.save

    redirect_to @article

  else

    render 'new'

  end

end

private

  def article_params

    params.require(:article).permit(:title, :text)

  end

What just happened is that you told Rails that if the user did not type in 5 characters in the Title field, it should show the blank form again to the user. That doesn’t offer much help. In order to tell the user what went wrong, edit the app/controllers/articles_controller.rb file again and to cater the following changes:

def create

  @article = Article.new(article_params)

  if @article.save

    redirect_to @article

  else

    render 'new'

  end

end

def update

  @article = Article.find(params[:id])

  if @article.update(article_params)

    redirect_to @article

  else

    render 'edit'

  end

end

private

  def article_params

    params.require(:article).permit(:title, :text)

  end

Now, to show this to the user, tweak the app/views/articles/index.html.erb file and add the following lines:

<table>

  <tr>

    <th>Title</th>

    <th>Text</th>

    <th colspan="2"></th>

  </tr>

  <% @articles.each do |article| %>

    <tr>

      <td><%= article.title %></td>

      <td><%= article.text %></td>

      <td><%= link_to 'Show', article_path(article) %></td>

      <td><%= link_to 'Edit', edit_article_path(article) %></td>

    </tr>

  <% end %>

</table>

#  Chapter 11 Update Articles

You would expect your users to change their minds about the article that they just wrote and make some changes. This would involve the Update action in CRUD, which would prompt you to add an edit action in the ArticlesController and add this function between the “create” and “new” actions. It should look like this:

def new

  @article = Article.new

end

def edit

  @article = Article.find(params[:id])

end

def create

  @article = Article.new(article_params)

  if @article.save

    redirect_to @article

  else

    render 'new'

  end

end

To allow a view for this, create a file and name it app/views/articles/edit.html.erb and then put in the following lines:

<h1>Editing article</h1>

<%= form_for :article, url: article_path(@article), method: :patch do |f| %>

  <% if @article.errors.any? %>

    <div id="error_explanation">

      <h2>

        <%= pluralize(@article.errors.count, "error") %> prohibited

        this article from being saved:

      </h2>

      <ul>

        <% @article.errors.full_messages.each do |msg| %>

          <li><%= msg %></li>

        <% end %>

      </ul>

    </div>

  <% end %>

  <p>

    <%= f.label :title %><br>

    <%= f.text_field :title %>

  </p>

  <p>

    <%= f.label :text %><br>

    <%= f.text_area :text %>

  </p>

  <p>

    <%= f.submit %>

  </p>

<% end %>

<%= link_to 'Back', articles_path %>

Now, you would need to create the “update” action in app/controllers/articles_controller.rb. Edit the file to look like this:

def create

  @article = Article.new(article_params)

  if @article.save

    redirect_to @article

  else

    render 'new'

  end

end

def update

  @article = Article.find(params[:id])

  if @article.update(article_params)

    redirect_to @article

  else

    render 'edit'

  end

end

private

  def article_params

    params.require(:article).permit(:title, :text)

  end

In order to show a link for Edit, you can edit app/views/articles/index.html.erb to make the link appear after the Show link.

<table>

  <tr>

    <th>Title</th>

    <th>Text</th>

    <th colspan="2"></th>

  </tr>

  <% @articles.each do |article| %>

    <tr>

      <td><%= article.title %></td>

      <td><%= article.text %></td>

      <td><%= link_to 'Show', article_path(article) %></td>

      <td><%= link_to 'Edit', edit_article_path(article) %></td>

    </tr>

  <% end %>

</table>

Now, to give chance for the user to Edit his work, add these lines to the template app/views/articles/show.html.erb:

...

<%= link_to 'Back', articles_path %> |

<%= link_to 'Edit', edit_article_path(@article) %>

#  Chapter 12 Destroy Some Data

No, it does not mean that you have to ruin the entire program you built. At this point, you would need to make provisions for the user to delete some of the articles that he wrote. Since you are creating a RESTful program, you would need to use the following route:

DELETE /articles/:id(.:format)      articles#destroy

This route makes it easy for Rails to destroy resources and you would need to make sure that it is placed before the protected or private methods. Let’s add this action to the app/controllers/articles_controller.rb file:

def destroy

  @article = Article.find(params[:id])

  @article.destroy

  redirect_to articles_path

end

After doing so, you would notice that the ArticlesController in app/controllers/articles_controller.rb will now appear this way:

class ArticlesController < ApplicationController

  def index

    @articles = Article.all

  end

  def show

    @article = Article.find(params[:id])

  end

  def new

    @article = Article.new

  end

  def edit

    @article = Article.find(params[:id])

  end

  def create

    @article = Article.new(article_params)

    if @article.save

      redirect_to @article

    else

      render 'new'

    end

  end

  def update

    @article = Article.find(params[:id])

    if @article.update(article_params)

      redirect_to @article

    else

      render 'edit'

    end

  end

  def destroy

    @article = Article.find(params[:id])

    @article.destroy

    redirect_to articles_path

  end

  private

    def article_params

      params.require(:article).permit(:title, :text)

    end

end

Now, it’s time for you to let the user know that they have this option. Pull up the app/views/articles/index.html.erb file and add the following lines:

<h1>Listing Articles</h1>

<%= link_to 'New article', new_article_path %>

<table>

  <tr>

    <th>Title</th>

    <th>Text</th>

    <th colspan="3"></th>

  </tr>

  <% @articles.each do |article| %>

    <tr>

      <td><%= article.title %></td>

      <td><%= article.text %></td>

      <td><%= link_to 'Show', article_path(article) %></td>

      <td><%= link_to 'Edit', edit_article_path(article) %></td>

      <td><%= link_to 'Delete', article_path(article),

              method: :delete,

              data: { confirm: 'Are you sure?' } %></td>

    </tr>

  <% end %>

</table>

You would notice that you also added up a feature to make the user confirm whether he really would want to delete the submitted article. Now, in order to make the confirmation box appear, you need to make sure that you have the file jquery_ujs in your machine.

# Conclusion

Thank you again for downloading this book! 

I hope this book was able to help you to grasp the basics of Ruby on Rails and allow you to create a webpage based on the codes and processes discussed in this book.

The next step is to discover other applications of the platform and learn other Rails techniques that would improve your program design and integration.

Finally, if you enjoyed this book, please take the time to share your thoughts and post a review on Amazon. We do our best to reach out to readers and provide the best value we can. Your positive review will help us achieve that.  It’d be greatly appreciated!

Thank you and good luck!

![thank-you](images/00001.jpeg)

Click here to leave a review on amazon.com

Preview Of ‘C Programming Success in a Day: Beginners’ Guide To Fast, Easy And Efficient Learning Of C Programming’

’

# Chapter 1: Hello World – the Basics

When coding a C program, you must start your code with the function ‘main’. By the way, a function is a collection of action that aims to achieve one or more goals. For example, a vegetable peeler has one function, which is to remove a skin of a vegetable. The peeler is composed of parts (such as the blade and handle) that will aid you to perform its function. A C function is also composed of such components and they are the lines of codes within it.

Also, take note that in order to make your coding life easier, you will need to include some prebuilt headers or functions from your compiler.

To give you an idea on what C code looks like, check the sample below:

#include <stdio.h>

int main()

{

printf( "Hello World!\n" );

getchar();

return 0;

}

As you can see in the first line, the code used the #include directive to include the stdio.h in the program. In this case, the stdio.h will provide you with access to functions such as printf and getchar.

## Main Declaration

After that, the second line contains int main(). This line tells the compiler that there exist a function named main. The int in the line indicates that the function main will return an integer or number.

## Curly Braces

The next line contains a curly brace. In C programming, curly braces indicate the start and end of a code block or a function. A code block is a series of codes joined together in a series. When a function is called by the program, all the line of codes inside it will be executed.

## Printf()

The printf function, which follows the opening curly brace is the first line of code in your main function or code block. Like the function main, the printf also have a code block within it, which is already created and included since you included <stdio.h> in your program. The function of printf is to print text into your program’s display window.

Beside printf is the value or text that you want to print. It should be enclosed in parentheses to abide standard practice. The value that the code want to print is Hello World!. To make sure that printf to recognize that you want to print a string and display the text properly, it should be enclosed inside double quotation marks.

By the way, in programming, a single character is called a character while a sequence of characters is called a string.

[Click here to check out the rest of C Programming Success in a Day on Amazon.](http://www.amazon.com/Programming-Success-Day-programming-Developers-ebook/dp/B00Q3Y55PM)

Check Out My Other Books

Below you’ll find some of my other popular books that are popular on Amazon and Kindle as well.  Simply click on the links below to check them out.  Alternatively, you can visit my author page on Amazon to see other work done by me.

[Click here to check out C Programming Success in a Day on Amazon.](http://www.amazon.com/Programming-Success-Day-programming-Developers-ebook/dp/B00Q3Y55PM)

[Click here to check out Python Programming Success in a Day on Amazon.](http://www.amazon.com/Python-Programming-Day-Beginners-beginners-ebook/dp/B00R1WXCD2)

[Click here to check out PHP Programming Professional Made Easy on Amazon.](http://www.amazon.com/PHP-Programming-Professional-Made-Easy-ebook/dp/B00RES3EWC)

[Click here to check out HTML Professional Programming Made Easy on Amazon](http://www.amazon.com/HTML-Programming-Professional-Made-Easy-ebook/dp/B00SGGKHSU)             

[Click here to check out CSS Programming Professional Made Easy on Amazon.](http://www.amazon.com/CSS-Programming-Professional-Made-Easy-ebook/dp/B00RET2L2U)

[Click here to check out Windows 8 Tips for Beginners on Amazon.](http://www.amazon.com/Windows-Tips-Beginners-Networking-Technology-ebook/dp/B00RW2E6JA)

[Click here to check out C Programming Professional Made Easy on Amazon.](http://www.amazon.com/Programming-Professional-Made-Easy-programming-ebook)

[Click here to check out JavaScript Programming Made Easy on Amazon](http://www.amazon.com/JavaScript-Professional-Programming-Made-Easy-ebook/dp/B00SDM365S)

[Click here to check out C ++ Programming Success in a Day on Amazon.](http://www.amazon.com/Programming-Professional-Made-Easy-programming-ebook/dp/B00S776K5M)

If the links do not work, for whatever reason, you can simply search for these titles on the Amazon website to find them.
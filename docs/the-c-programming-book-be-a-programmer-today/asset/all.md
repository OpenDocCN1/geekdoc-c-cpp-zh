![](cover.jpeg)

|  
### AUTHOR:-  MURTUZA CHAWALA

 |

![](images/00002.jpeg) ![](images/00001.jpeg)

PROGRAMMING IN   C

PREFACE

As you know that we live in a world of computers. Knowing how to use a computer is not enough,as the actual interaction with computers happens with programming. This book will make you a programmer by teaching you programming in c language which is one of the oldest,basic and most preferred, programming language in one day.

This book is customized for beginners (no knowledge in programming concepts) .

GO AHEAD WITH PATIENCE AND BE A programmer

 -MURTUZA CHAWALA

CONTENTS

1)INTRODUCTION

2)INPUT/OUTPUT OPERATIONS

3)DECISION MAKING AND LOOPING

4)FUNCTIONS

5)POINTERS

6)ARRAYS

7)STRINGS

8)USER DEFINED DATA TYPE

9) C PROGRAMS

Introduction

C is a general purpose

Programming language which was created by Denis Ritchie at At’t bell laboratory in 1972 in USA.

C is one of the most earliest,popular,powerful and easiest programming language.

The computer(digital system) cannot understand

normal English language ,it only understands machine language(binary code) that is (1s and 0s). thus c is used to tell the computer what exactly is to be performed.

All software,application are written in some programming language(C,C++,Java ) etc

The Linux(Unix) operating system was totally written on c language.

C is also used to make compilers,kernels of an OS(operating system).

C is a programming language , whatever task we carry out on our mobiles,laptops etc is actually done through programming(which is inbuilt) {unknown to end users}

Eg:-whenever a button is pressed its equivalent code is generated,that generated code is then compiled by a compiler .

Compiler(transforms programming code into binary code(1s,0s) this binary code is sent to the CPU and data processed there(in binary) ,it is sent back from the CPU to the monitor and binary code is again converted to output form(audio,decimal,photo etc)

This is the working of a programming language

Q) Benefits of c?

A) 1) c is one of the basic and easiest programming language ie it the first step towards becoming a programmer.

2)c is machine independent ie [(code)](XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX)

can be run on any computer.

3)as it is a structured and procedure oriented language,it gives step by step knowledge

4)Many operation can be performed using c ,also it is flexible(different methods to solve one problem).

5)It has high level language(java) features along with low level language features.

Need to learn programming

Writing the perfect code isn't enough as it is in English language which is not understood by the computer,thus we need to write the codes in an application which will facilitate translation of code into binary .

Compilers are available online (turbo c)

Its suggested that you download the compiler and execute your code concurrently with this book

 C program

Q) C program to print hello world?

A)

   #include<stdio.h>

Void main()

{

Printf(“hello world”);

}

C concepts(explanation)

1) #include is a preprocessor directive(to be studied later)

<stdio.h>  it is a header file which will allow you to perform some in built functions(printf) .

2) void main()

  Every c program starts with main() . void means that the function main does not return any value.

3)printf :

This is an inbuilt function from header file <stdio.h> which will print anything which is written inside print statement .

5) ;

This (semicolon) is used to denote end of line .each statement in main() function [barring few like loops] , which have an ; at the end

NOTE:-

Every c program will have header file

#include<stdio.h> compulsorily as without that printf(printing output) and scanf(taking input) functions cannot be performed.

Main() can be written as void main()

Or int main() and then return 0(null) at end.

Algorithm :Actual logic of program without syntax.

BEFORE STARTING WITH PROGRAMMING WE WILL FIRST GO THROUGH ALL BASIC CONCEPTS IN C

1) Variables :

They are identifiers, a symbolic name given to some value.

Eg:- int a;

Here variable is “a” which is an integer(number) and which may store some value.

2) Constant:

It is also an identifier.

The value of constant is fixed(unlike variable) and cannot be changed during programming.

Eg:-int a=5;

Here a is a constant holding value 5.

3)Keywords

These are reserved words used in programming and cannot be used as an variable or constant EG:- int,char(datatypes) ,void,for,while etc.

4)Data types

They are keywords .

They are used for assigning a type to a variable .

The basic data types.

1)int: It specifies that the variable associated with it holds a number

Eg:- int  a;

It means  a  will be holding some number .

NOTE

:-FORMAT SPECIFIER

If we want to print some integer value as we cannot directly write variable name in printf statement, we use %d

In “ ”

And then ,write the variable name

Eg:- main()

{

int a=5;

Printf(“%d”,a)

}

Thus the compiler will know that it has to print an integer (a) [when %d used]

2)char:it specifies that the variable associated with it holds a single character

Eg:- char  a;

It means a will be holding some character.

FORMAT SPECIFIER

%c.

3)float:it specifies that the variable associated with it holds a floating value (in decimals ) Eg:-4.32

Eg:- float  a;

A will be holding a float value.

FORMAT SPECIFIER

%f

4)void:-

It tells that the variable,function does not hold any value.[mostly used in main() function]

THERE ARE OTHER DATA TYPES TOO

Long int (4bytes) (%ld) [larger number]

Unsigned int(2 bytes) (%u) [positive number ,mostly used for pointers]

Double(8 bytes) (%lf) [ large float value]

Long double(16 bytes) (%Lf)

Above bytes size ie 2,4 etc indicate amount of memory taken by each number,char etc.

NOTE:-

Variable declaration means to declare variable without assigning any value

Eg:- int a;

Variable definition means to declare variable along with its fixed value

Eg:- int a=5;

Local Variable:which are declared inside main() function

Global variable:which are declared outside(before) main() function

OPERATORS

Operators are symbols which operate a value or variable.

They represent an operation.

Eg: +,-,*,>,<  etc

Types of operators

An operator is a symbol that tells the compiler to perform specific mathematical or logical functions. C language is rich in built-in operators and provides the following types of operators −

*   Arithmetic Operators
*   Relational Operators
*   Logical Operators
*   Bitwise Operators
*   Assignment Operators
*   Misc Operators

## Arithmetic Operators

The following table shows all the arithmetic operators supported by the C language. Assume variable A holds 10 and variable B holds 20 then −

[Show Examples](https://www.tutorialspoint.com/cprogramming/c_arithmetic_operators.htm)

| Operator | Description | Example |
| + | Adds two operands. | A + B = 30 |
| − | Subtracts second operand from the first. | A − B = -10 |
| * | Multiplies both operands. | A * B = 200 |
| / | Divides numerator by de-numerator. | B / A = 2 |
| % | Modulus Operator and remainder of after an integer division. | B % A = 0 |
| ++ | Increment operator increases the integer value by one. | A++ = 11 |
| -- | Decrement operator decreases the integer value by one. | A-- = 9 |

## Relational Operators

The following table shows all the relational operators supported by C. Assume variable A holds 10 and variable B holds 20 then −

[Show Examples](https://www.tutorialspoint.com/cprogramming/c_relational_operators.htm)

| Operator | Description | Example |
| == | Checks if the values of two operands are equal or not. If yes, then the condition becomes true. | (A == B) is not true. |
| != | Checks if the values of two operands are equal or not. If the values are not equal, then the condition becomes true. | (A != B) is true. |
| > | Checks if the value of left operand is greater than the value of right operand. If yes, then the condition becomes true. | (A > B) is not true. |
| < | Checks if the value of left operand is less than the value of right operand. If yes, then the condition becomes true. | (A < B) is true. |
| >= | Checks if the value of left operand is greater than or equal to the value of right operand. If yes, then the condition becomes true. | (A >= B) is not true. |
| <= | Checks if the value of left operand is less than or equal to the value of right operand. If yes, then the condition becomes true. | (A <= B) is true. |

## Logical Operators

Following table shows all the logical operators supported by C language. Assume variable A holds 1 and variable B holds 0, then −

[Show Examples](https://www.tutorialspoint.com/cprogramming/c_logical_operators.htm)

| Operator | Description | Example |
| && | Called Logical AND operator. If both the operands are non-zero, then the condition becomes true. | (A && B) is false. |
| &#124;&#124; | Called Logical OR Operator. If any of the two operands is non-zero, then the condition becomes true. | (A &#124;&#124; B) is true. |
| ! | Called Logical NOT Operator. It is used to reverse the logical state of its operand. If a condition is true, then Logical NOT operator will make it false. | !(A && B) is true. |

## Assignment Operators

The following table lists the assignment operators supported by the C language −

[Show Examples](https://www.tutorialspoint.com/cprogramming/c_assignment_operators.htm)

| Operator | Description | Example |
| = | Simple assignment operator. Assigns values from right side operands to left side operand | C = A + B will assign the value of A + B to C |
| += | Add AND assignment operator. It adds the right operand to the left operand and assign the result to the left operand. | C += A is equivalent to C = C + A |
| -= | Subtract AND assignment operator. It subtracts the right operand from the left operand and assigns the result to the left operand. | C -= A is equivalent to C = C - A |
| *= | Multiply AND assignment operator. It multiplies the right operand with the left operand and assigns the result to the left operand. | C *= A is equivalent to C = C * A |
| /= | Divide AND assignment operator. It divides the left operand with the right operand and assigns the result to the left operand. | C /= A is equivalent to C = C / A |
| %= | Modulus AND assignment operator. It takes modulus using two operands and assigns the result to the left operand. | C %= A is equivalent to C = C % A |
| <<= | Left shift AND assignment operator. | C <<= 2 is same as C = C << 2 |
| >>= | Right shift AND assignment operator. | C >>= 2 is same as C = C >> 2 |
| &= | Bitwise AND assignment operator. | C &= 2 is same as C = C & 2 |
| ^= | Bitwise exclusive OR and assignment operator. | C ^= 2 is same as C = C ^ 2 |
| &#124;= | Bitwise inclusive OR and assignment operator. | C &#124;= 2 is same as C = C &#124; 2 |

## Other Operators ↦ sizeof & ternary

Besides the operators discussed above, there are a few other important operators including sizeof and ? : supported by the C Language.

[Show Examples](https://www.tutorialspoint.com/cprogramming/c_sizeof_operator.htm)

| Operator | Description | Example |
| sizeof() | Returns the size of a variable. | sizeof(a), where a is integer, will return 4. |
| & | Returns the address of a variable. | &a; returns the actual address of the variable. |
| * | Pointer to a variable. | *a; |
| ? : | Conditional Expression. | If Condition is true ? then value X : otherwise value Y |

## Operators Precedence in C

Operator precedence determines the grouping of terms in an expression and decides how an expression is evaluated. Certain operators have higher precedence than others; for example, the multiplication operator has a higher precedence than the addition operator.

For example, x = 7 + 3 * 2; here, x is assigned 13, not 20 because operator * has a higher precedence than +, so it first gets multiplied with 3*2 and then adds into 7.

OPERANDS

They are the variable(or constant) on which operation are performed

Eg:- a+b;

a and b are operands and + is an operator.

Expression

An expression is an combination of operators,operands

Eg: a*b+c;

Is an expression

Simple c program to add two numbers

#include<stdio.h>

Void main()

{

int a=10,b=20,c;

c=a+b;

printf(“%d”,c);

}

NOTE:- // means comment which means that line of code will not get executed [used for self understanding purposes]

Explanation

#include<stdio.h>

// [ to include header file stdio.h which will allow us to use the printf statement.]

Void main()

//[function which contains source code and returns nothing]

{

// [to start source code]

Int a=20,b=10,c;

//[ a and b are integer constant having values 20,10

c is an integer variable whose value is undefined .]

C=a+b;

//[operation now c=30]

Printf(“%d”,c);S

//[

Print “%d”, that is an integer c]

OUTPUT:

30.

CH :- 2

 INPUT/OUTPUT OPERATION

Every computer has one primary goal that is to take data as input ,process it and give the required output to user.

Similarly if we want to execute a c program we need to input some values,give some processing information(add two numbers) and then write an output statement.

I/O operations are broadly classified in two groups:-

1)Console I/O function:

Function to receive input from keyboard and print output.(eg:- printf,scanf)

2)File I/O function:

Function to perform I/O operation on floppy or disk

NOTE:- MAJORITY of C  I/O functions are performed by console(printf,scanf) function.

CONSOLE BASED I/O Function

1)printf() function

As mentioned earlier printf is an inbuilt function (whose code we do not have to write) under the header file <stdio.h>

The work of printf function is to print output during execution of program.

Eg:- printf(“hello”); will print

Hello.

If we want to print value of some variable then we use format specifier of that variable (data type)

Eg:- in a=4;

Printf(“%d”,a);

Output: 4

NOTE:- %d is format specifier of int .

2)scanf() function:

To read(accept) data from user we use scanf() function.

If we want to store value of a variable say x as 4 then we use scanf statement which will accept x as 4;

In scanf () we use format specifier of variable and later(after comma,)use &(ampersand) operator which will store x and its value in the memeory.

EG:-

int a;

Printf(“enter value for a”);

Scanf(“%d”,&a);

Q) c program to accept two integers and add them?

A)

   #include<stdio.h>

   Void main()

   {

     Int a,b,c;

     Printf(“enter number 1”);

     Scanf(“%d”,&a);

Printf(“enter number 2”);

Scanf(“%d”,&b);

C=a+b;

Printf(“%d”,c);

}

Other I/o functions

## The getchar() and putchar() Functions

The int getchar(void) function reads the next available character from the screen and returns it as an integer. This function reads only single character at a time. You can use this method in the loop in case you want to read more than one character from the screen.

The int putchar(int c) function puts the passed character on the screen and returns the same character. This function puts only single character at a time. You can use this method in the loop in case you want to display more than one character on the screen. Check the following example −

#include  <stdio.h>int main(  )  {

 int c;

   printf(  "Enter a value :");

c = getchar(  );

   printf(  "\nYou entered: ");

   putchar( c );

 return  0;}

When the above code is compiled and executed, it waits for you to input some text. When you enter a text and press enter, then the program proceeds and reads only a single character and displays it as follows −

$./a.outEnter a value : this is testYou entered: t

## The gets() and puts() Functions

The char *gets(char *s) function reads a line from stdin into the buffer pointed to by s until either a terminating newline or EOF (End of File).

The int puts(const char *s) function writes the string 's' and 'a' trailing newline to stdout.

#include  <stdio.h>int main(  )  {

 char str[100];

   printf(  "Enter a value :");

   gets( str );

   printf(  "\nYou entered: ");

   puts( str );

 return  0;}

When the above code is compiled and executed, it waits for you to input some text. When you enter a text and press enter, then the program proceeds and reads the complete line till end, and displays it as follows −

$./a.outEnter a value : this is testYou entered: this is test

CHAPTER 3:

DECISION MAKING

Decision making statements are one of the most fundamental concepts in c language.

A wide variety of programs(tasks) can be executed by decision making statement.

These statements can help us to check multiple conditions(possibilities)

And print the desired condition

They are also called as selection or conditional statements..

CONDITIONAL STATEMENTS:

1) If statement

It is a conditional statement used in c to check condition or control execution of statements.

It is very simple to use.

Syntax

If(condition)

{

Statements

}

In the above syntax the condition is checked first if it is true then the program control flow goes inside braces and executes block of statements.

If condition is false the statements do not get executed

NOTE:-

WE DO NOT ISSUE A SEMICOLEN; FOR AN IF STATEMENT.

EG:-

Int a =5;

If(a==5)      //[NO ;]

{

Printf(“condition is true”);

}

OUTPUT:

Condition is true.

2) if-else statement

This statement is also very useful ,

And unlike if statement it can check two conditions

SYNTAX:-

If(condition)

{

Statement(true);

}

else

{

  Statement(false);             

}             

EG:-

Int a =4;

If(a==3)

{

Printf(“condition is true”);

}

Else

{

Printf(“condition is false”);

}

OUTPUT:-

Condition is false.

Nested if statement

Nested if-else statement

3) Switch statement

Switch statement is a multiple decision making statement.

When if-else condition is used to check statement more than one condition the complexity of program increases.

Thus to overcome this problem c provides switch statement.

It is used to check multiple conditions efficiently.

![switch_statement](images/00003.jpeg)

SYNTAX:

Switch(expression)

{

Case 1:

Statements;

Break;

  Case 2:Statements;

Break;

  Case 3:Statements;

Break;

Case n:Statements;

Break;

}

#include  <stdio.h>

int main ()  {

 /* local variable definition */

 char grade =  'B';

 switch(grade)  {

 case  'A'  :

         printf("Excellent!\n"  );

 break;

 case  'B'  :

 case  'C'  :

         printf("Well done\n"  );

 break;

 case  'D'  :

         printf("You passed\n"  );

 break;

 case  'F'  :

         printf("Better try again\n"  );

 break;

 default  :

         printf("Invalid grade\n"  );

 }

   printf("Your grade is  %c\n", grade );

 return  0;}

When the above code is compiled and executed, it produces the following result −

Well done

Your grade is B

Note: the case label should be an integer or character.

Each statement of switch must have a break to exit from case ,else after executing the correct case,control will go to next case and execute that too;

There are other conditional statements too like nested if..else,nested switch etc

Chapter 4

 LOOP

Looping is also one of the important  concepts in programming .

Loops are used for executing a set of statements again and again.

The data inside loops keeps on executing until condition is false.

It is used for writing condition.

A loop execution can be done by

Starting a loop with a terminating condition

Initialize a variable and start a loop

Execution of statements inside loop

Increment or decrement of variable(till condition)

Types of looping statement

1)entry controlled loop:

also called as pre tested loop

Here,the condition is checked first and then statements inside are evaluated

While and for are entry controlled loops, and are widely used.

A) while loop

It is an entry controlled loop which is used to repeat a block of statement until condition becomes true.

Syntax:-

While(condition)

{

Statement;

Increment/decrement;

}

ALGORITHM :

Eg:-

A=3,b=5;

While(a<b)

Print a;

A++;

Output 3 4

B) For loop

It is more efficient and useful than while loop .

One of the most important actions of for loop is that three action can be taken at a time ie

A)variable initialization

B)Condition checking

C)Increment/decrement of a variable.

Syntax:-

For(initialization;condition;incr/decr)

{

Statements;

}

Eg:-

A=3,I;

For(i=1;i<a;i++)

{

Print(i)

}

Output:-

1 2 3

Here after I is printed for the first time the control goes back to the loop increments I to 2, checks whether I<a(3) if yes than again print …..

Else

Control will come out of loop.

2) Exit controlled loop

A}do-while loop

It is the only exit controlled loop

Here the statements are first executed then the condition is checked.

It is guaranteed that the statement will be executed at least once.

Though it is rarely used ,it is quite popular for menu driven programs(switch case)

Syntax:-

Do

{

Statements

}while(condition);

JUMP STATEMENTS

These statements are used to transfer flow of statements from one process to another.

1)Goto

2)Break

3)Continue

4)Exit

1)Goto

This statement transfers the control of the program from one point to another.

Syntax:-

Goto label:

Here label can be any identifier,it need not be declare,

It should be pointing to some other line

Label:statements;

Eg:-

N=4;

For(i=0;i<N;i++)

{

Print i;

If(i==2)

Goto here:

}

Here:printf(yippeee)

In the above algorithm variable (I) should have been printed 5 times but because of goto statement, I after printing twice will because of jump statement goto ,

Jump to here: and print yippeee

Output:- 0 1 yippeee

2)Break

It is one of the useful jump statements in loops and switch cases

It is used to transfer control out of loop(exit from loop or switch cases)

It causes loop termination,(which is sometimes necessary when some condition is satisfied.

Syntax:-

If(condition)

Break;

3)Continue

This statement is used when it is required to skip a part of the body under some condition.

If condition is true and continue statement is used then control does not go to print or other statement in a loop it will directly go to start of loop.

Syntax:- continue;

It does not cause loop termination

And just like break it is also used with if (conditional) statement.

4)Exit():-

This is a simple jump statement which terminates program completely if statement is called.

If exit is used control does not go ahead [till getch()] and directly stops compiling.

Syntax:-exit();

NOTE:- unlike conditional(if..,,)

And looping (for,..) statements, jump statements are used only for reference and for small tasks and jump statements work on conditional and looping statement.

Chapter 5:

    FUNCTIONS

A number of statements grouped into one logical unit is called function

As mentioned earlier there are two types of types

1)Inbuilt function:

whose code need not be written,(who come under some header file) eg:- printf(<stdio.h>)

2)User defined functions:

These are set of statements that are defined by user to achieve some specific tasks.

Functions are set of instruction in a logical sequence which performs specified task

Advantages of function:

1)Easy and simple to use.

2)Function divides a large block of code into small parts which can be easily understood.

3)Debugging(removing errors) becomes easier.

4)Useful in case of large problems.

How to use a function

There are three parts while using a function .

1) Function declaration

2) Function call

3) Function definition

1) Function declaration

If any user defined function has to used,it has to be declared first[before main() is better]

Syntax:-

datatype function_name(parameter)

Eg:- int sum(int a,int b)

NOTE:-  HERE DATAYPE MEANS WHAT VALUE FUNCTION WILL BE RECEIVING

PARAMETER MEANS WHAT VARIABLE(VALUES) THE MAIN PROGRAM WILL BE SENDING .

2) Function call

This statement transfers the control from the main() part to the actual function outside main()

{basically calls the function}

Syntax:-

Function_name(parameters)

Eg:-sum(a,b)

(its ok if datatype not used with parameters when calling function)

3) Function definition

This is the main part of the function

It contains all codes that are to be performed.

It may take zero,one or more inputs and may or may not give back some output but performs processing of data.

It contains a header which contains of the function name(earlier declared) and body which consist of steps.

Syntax_                          Return datatype  function_name(parameters)

{

Statements/……

}

NOTE:- here return datatype means value(int,char) to be returned to main program.

If return type is void then no value is returned.

Function declaration and call are used for declare and call of function.

Function defintion is for processing of data,

Program.

#include<stdio.h> 
void main() 
{ 
       int a,b; 
       clrscr(); 
       printf("Enter Two Number : "); 
       scanf("%d%d",&a,&b); 
       sum(a,b); 
       getch(); 
} 
      sum(int x,int y) 
  { 
       int z; 
       z=x+y; 
       printf("Sum of Two Number is : %d",z); 
       return 0; 
} 
Output : 
Enter Two Number : 10 20 
Sum of Two Number is : 30 

FUNCTION Can be called in two ways

1) Call by value

2)Call by reference

| Difference between call by value and call by reference |  |
| call by value | call by reference |  |
| In call by value, a copy of actual arguments is passed to formal arguments of the called function and any change made to the formal arguments in the called function have no effect on the values of actual arguments in the calling function. | In call by reference, the location (address) of actual arguments is passed to formal arguments of the called function. This means by accessing the addresses of actual arguments we can alter them within from the called function. |  |
| In call by value, actual arguments will remain safe, they cannot be modified accidentally. | In call by reference, alteration to actual arguments is possible within from called function; therefore the code must handle arguments carefully else you get unexpected results. |  |
|  |  |  |

Function categories.

1)Function with no return value and no parameter

2)Function with no return value and a parameter

3)Function with a return value and a no parameter

4)Function with a return value and a  parameter

Storage classes :

It refers to scope of variable and memory allocated to store that variable.

In other words it tells us what extra features are given to the variable.

There are 4 storage class.

1) AUTO

2) REGISTER

3) STATIC

4) EXTERNAL

## The auto Storage Class

The auto storage class is the default storage class for all local variables.

{

 int mount;

 auto  int month;}

The example above defines two variables with in the same storage class. 'auto' can only be used within functions, i.e., local variables.

## The register Storage Class

The register storage class is used to define local variables that should be stored in a register instead of RAM. This means that the variable has a maximum size equal to the register size (usually one word) and can't have the unary '&' operator applied to it (as it does not have a memory location).

{

 register  int  miles;}

The register should only be used for variables that require quick access such as counters. It should also be noted that defining 'register' does not mean that the variable will be stored in a register. It means that it MIGHT be stored in a register depending on hardware and implementation restrictions.

## The static Storage Class

The static storage class instructs the compiler to keep a local variable in existence during the life-time of the program instead of creating and destroying it each time it comes into and goes out of scope. Therefore, making local variables static allows them to maintain their values between function calls.

The static modifier may also be applied to global variables. When this is done, it causes that variable's scope to be restricted to the file in which it is declared.

In C programming, when static is used on a class data member, it causes only one copy of that member to be shared by all the objects of its class.

## The extern Storage Class

The extern storage class is used to give a reference of a global variable that is visible to ALL the program files. When you use 'extern', the variable cannot be initialized however, it points the variable name at a storage location that has been previously defined.

When you have multiple files and you define a global variable or function, which will also be used in other files, then extern will be used in another file to provide the reference of defined variable or function. Just for understanding, extern is used to declare a global variable or function in another file.

The extern modifier is most commonly used when there are two or more files sharing the same global variables or functions as explained below.

Recursion:

It is a programming technique,

where a function calls itself again and again.

The C programming language supports recursion, i.e., a function to call itself. But while using recursion, programmers need to be careful to define an exit condition from the function, otherwise it will go into an infinite loop.

Recursive functions are very useful to solve many mathematical problems, such as calculating the factorial of a number, generating Fibonacci series, etc.

## Example: Factorial of a Number Using Recursion

#include  <stdio.h>long  int multiplyNumbers(int n);

int main(){

 int n;

    printf("Enter a positive integer: ");

    scanf("%d", &n);

    printf("Factorial of %d = %ld", n, multiplyNumbers(n));

 return  0;}long  int multiplyNumbers(int n){

 if (n >= 1)

 return n*multiplyNumbers(n-1);

 else

 return  1;}

Output

Enter a positive integer: 6

Factorial of 6 = 720

Suppose the user entered 6.

Initially, the multiplyNumbers() is called from the main() function with 6 passed as an argument.

Then, 5 is passed to the multiplyNumbers() function from the same function (recursive call). In each recursive call, the value of argument n is decreased by 1.

When the value of n is less than 1, there is no recursive call.

Chapter 6:

Pointers

INTRODUCTION:

Pointer is a variable that stores memory address of another variable.

Pointer enhances dynamic handling of data.

A pointer is a variable whose value is the address of another variable, i.e., direct address of the memory location. Like any variable or constant, you must declare a pointer before using it to store any variable address. The general form of a pointer variable declaration is −

type *var-name;

Here, type is the pointer's base type; it must be a valid C data type and var-name is the name of the pointer variable. The asterisk * used to declare a pointer is the same asterisk used for multiplication. However, in this statement the asterisk is being used to designate a variable as a pointer. Take a look at some of the valid pointer declarations −

## How to Use Pointers?

#include  <stdio.h>

int main ()  {

 int var  =  20; /* actual variable declaration */

 int *ip; /* pointer variable declaration */

ip =  &var; /* store address of var in pointer variable*/

   printf("Address of var variable: %x\n",  &var );

 /* address stored in pointer variable */

   printf("Address stored in ip variable: %x\n", ip );

 /* access the value using the pointer */

   printf("Value of *ip variable: %d\n",  *ip );

 return  0;}

When the above code is compiled and executed, it produces the following result −

Address of var variable: bffd8b3c

Address stored in ip variable: bffd8b3c

Value of *ip variable: 20

Passing pointer to function

C programming allows passing a pointer to a function. To do so, simply declare the function parameter as a pointer type.

Following is a simple example where we pass an unsigned long pointer to a function and change the value inside the function which reflects back in the calling function −

#include  <stdio.h>#include  <time.h>

void getSeconds(unsigned  long  *par);

int main ()  {

 unsigned  long sec;

   getSeconds(  &sec );

 /* print the actual value */

   printf("Number of seconds: %ld\n", sec );

 return  0;}

void getSeconds(unsigned  long  *par)  {

 /* get the current number of seconds */

 *par = time( NULL );

 return;}

When the above code is compiled and executed, it produces the following result −

Number of seconds :1294450468

DYNAMIC MEMORY ALLOCATION

It is the process of allocating memory at run time.

In C, the exact size of array is unknown until compile time, i.e., the time when a compiler compiles your code into a computer understandable language. So, sometimes the size of the array can be insufficient or more than required.

Dynamic memory allocation allows your program to obtain more memory space while running, or to release it if it's not required.

In simple terms, Dynamic memory allocation allows you to manually handle memory space for your program.

Although, C language inherently does not have any technique to allocate memory dynamically, there are 4 [library functions](http://www.programiz.com/c-programming/library-function) under "stdlib.h" for dynamic memory allocation.

| Function | Use of Function |
| --- | --- |
| [malloc()](http://www.programiz.com/c-programming/c-dynamic-memory-allocation#malloc) | Allocates requested size of bytes and returns a pointer first byte of allocated space |
| [calloc()](http://www.programiz.com/c-programming/c-dynamic-memory-allocation#calloc) | Allocates space for an array elements, initializes to zero and then returns a pointer to memory |
| [free()](http://www.programiz.com/c-programming/c-dynamic-memory-allocation#free) | deallocate the previously allocated space |
| [realloc()](http://www.programiz.com/c-programming/c-dynamic-memory-allocation#realloc) | Change the size of previously allocated space |

##  malloc()

The name malloc stands for "memory allocation".

The function malloc() reserves a block of memory of specified size and return a [pointer](http://www.programiz.com/c-programming/c-pointers) of type void which can be casted into pointer of any form.

### Syntax of malloc()

ptr = (cast-type*) malloc(byte-size)

Here, ptr is pointer of cast-type. The malloc() function returns a pointer to an area of memory with size of byte size. If the space is insufficient, allocation fails and returns NULL pointer.

ptr = (int*) malloc(100 * sizeof(int));

This statement will allocate either 200 or 400 according to size of int 2 or 4 bytes respectively and the pointer points to the address of first byte of memory.

## calloc()

The name calloc stands for "contiguous allocation".

The only difference between malloc() and calloc() is that, malloc() allocates single block of memory whereas calloc() allocates multiple blocks of memory each of same size and sets all bytes to zero.

### Syntax of calloc()

ptr = (cast-type*)calloc(n, element-size);

This statement will allocate contiguous space in memory for an array of n elements. For example:

ptr = (float*) calloc(25, sizeof(float));

This statement allocates contiguous space in memory for an array of 25 elements each of size of float, i.e, 4 bytes.

##  free()

Dynamically allocated memory created with either calloc() or malloc() doesn't get freed on its own. You must explicitly use free() to release the space.

### syntax of free()

free(ptr);

This statement frees the space allocated in the memory pointed by ptr.

## C realloc()

If the previously allocated memory is insufficient or more than required, you can change the previously allocated memory size using realloc().

### Syntax of realloc()

ptr = realloc(ptr, newsize);

Here, ptr is reallocated with size of newsize.

Write a C program to find sum of n elements entered by user. To perform this program, allocate memory dynamically using malloc() function.

#include  <stdio.h>#include  <stdlib.h>

int main(){

 int num, i, *ptr, sum = 0;

    printf("Enter number of elements: ");

    scanf("%d", &num);

    ptr = (int*) malloc(num * sizeof(int)); //memory allocated using malloc

 if(ptr == NULL)                    

    {

        printf("Error! memory not allocated.");

 exit(0);

    }

    printf("Enter elements of array: ");

 for(i = 0; i < num; ++i)

    {

        scanf("%d", ptr + i);

        sum += *(ptr + i);

    }

    printf("Sum = %d", sum);

    free(ptr);

 return  0;}

Chapter 7:

Array and String.

Array is a data structure which contains group of elements under a single name.

A very useful technique that reduces time and helps in looping statements

Instead of declaring individual variables, such as number0, number1, ..., and number99, you declare one array variable such as numbers and use numbers[0], numbers[1], and ..., numbers[99] to represent individual variables. A specific element in an array is accessed by an index.

All arrays consist of contiguous memory locations. The lowest address corresponds to the first element and the highest address to the last element.

![](images/00008.jpeg)

Instead of scanning(accepting) 5 numbers, we can store all the 5 numbers in a variable. This technique is called as an array.

Declaration of array

Int a[5];

It means that variable a will store 5 numbers ,each element in array can be accessed using index . a[0],a[1],a[2] and so on.

Type of array

1 dimensional

2 dimensional

Multi dimensional

Program : Addition of All Elements of the Array

| 123456789101112131415161718192021222324252627 | #include<stdio.h>int  main()  { int  i,  arr[50],  sum,  num; printf("\nEnter no of elements :"); scanf("%d", &num); //Reading values into Array printf("\nEnter the values :"); for  (i = 0;  i < num;  i++)      scanf("%d", &arr[i]); //Computation of total sum = 0; for  (i = 0;  i < num;  i++)      sum = sum + arr[i]; //Printing of all elements of array for  (i = 0;  i < num;  i++)      printf("\na[%d]=%d",  i,  arr[i]); //Printing of total printf("\nSum=%d",  sum); return  (0);} |

## Output :

| 123456 | Enter no of elements : 3Enter the values : 11  22  33a[0]=11a[1]=22a[2]=33Sum=66 |

Program : Find Smallest Element in Array in C Programming

| 123456789101112131415161718192 | #include<stdio.h>int  main()  { int  a[30],  i,  num,  smallest; printf("\nEnter no of elements :"); scanf("%d", &num); //Read n elements in an array for  (i = 0;  i < num;  i++)      scanf("%d", &a[i]); //Consider first element as smallest smallest = a[0]; for  (i = 0;  i < num;  i++)  {      if  (a[i] < smallest)  { smallest = a[i];      } } // Print out the Result printf("\nSmallest Element : %d",  smallest); return  (0);} |

## Output :

| 123 | Enter no of elements : 511  44  22  55  99Smallest Element : 11 |

## C Program to Search an element in Array

| 1234567891011121314151617181920212223242526272829303132 | #include<stdio.h>int  main()  { int  a[30],  ele,  num,  i; printf("\nEnter no of elements :"); scanf("%d", &num); printf("\nEnter the values :"); for  (i = 0;  i < num;  i++)  {      scanf("%d", &a[i]); } //Read the element to be searched printf("\nEnter the elements to be searched :"); scanf("%d", &ele); //Search starts from the zeroth location i = 0; while  (i < num && ele != a[i])  {      i++; } //If i < num then Match found if  (i < num)  {      printf("Number found at the location = %d",  i + 1); }  else  {      printf("Number not found"); } return  (0);} |

## Output :

| 1234 | Enter no of elements : 511  22  33  44  55Enter the elements to  be searched : 44Number found at the location = 4 |

STRINGS

Strings are basically an array of characters.

Strings are actually one-dimensional array of characters terminated by a nullcharacter '\0'. Thus a null-terminated string contains the characters that comprise the string followed by a null.

The following declaration and initialization create a string consisting of the word "Hello". To hold the null character at the end of the array, the size of the character array containing the string is one more than the number of characters in the word "Hello."

char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};

If you follow the rule of array initialization then you can write the above statement as follows −

char greeting[] = "Hello";

Following is the memory presentation of the above defined string in C/C++ −

![](images/00004.jpeg)

Actually, you do not place the null character at the end of a string constant. The C compiler automatically places the '\0' at the end of the string when it initializes the array. Let us try to print the above mentioned string −

#include  <stdio.h>

int main ()  {

 char greeting[6]  =  {'H',  'e',  'l',  'l',  'o',  '\0'};

   printf("Greeting message: %s\n", greeting );

 return  0;}

When the above code is compiled and executed, it produces the following result −

Greeting message: Hello

C supports a wide range of functions that manipulate null-terminated strings −

C supports a wide range of functions that manipulate null-terminated strings −

| S.N. | Function & Purpose |
| 1 | strcpy(s1, s2);Copies string s2 into string s1. |
| 2 | strcat(s1, s2);Concatenates string s2 onto the end of string s1. |
| 3 | strlen(s1);Returns the length of string s1. |
| 4 | strcmp(s1, s2);Returns 0 if s1 and s2 are the same; less than 0 if s1<s2; greater than 0 if s1>s2. |
| 5 | strchr(s1, ch);Returns a pointer to the first occurrence of character ch in string s1. |
| 6 | strstr(s1, s2);Returns a pointer to the first occurrence of string s2 in string s1. |

All these function can be accessed using standard header file <string.h>

## Example: Calculate Length of String without Using strlen() Function

#include  <stdio.h>int main(){

 char s[1000], i;

    printf("Enter a string: ");

    scanf("%s", s);

 for(i = 0; s[i] != '\0'; ++i);

    printf("Length of string: %d", i);

 return  0;}

Output

Enter a string: Programiz

Length of string: 9

## C Program to Search occurrence of Character in String

| #include<stdio.h>#include<conio.h>int  main()  { char  str[20],  ch; int  count = 0,  i; printf("\nEnter a string : "); scanf("%s", &str); printf("\nEnter the character to be searched : "); scanf("%c", &ch); for  (i = 0;  str[i] != '\0';  i++)  {      if  (str[i] == ch) count++; } if  (count == 0)      printf("\nCharacter '%c'is not present",  ch); else      printf("\nOccurence of character '%c' : %d",  ch,  count); return  (0);} |

* * *

Output :

| 123456789 | <strong>First Run :</strong>Enter  a  string : c4learn.blogspot.comEnter the character to  be searched : oOccurence of character  'o' : 3<strong>Second Run :</strong>Enter  a  string : c4learn.blogspot.comEnter the character to  be searched : xCharacter  'x'is  not  present |

Chapter 8:

User defined datatype.

STRUCTURE

Arrays allow to define type of variables that can hold several data items of the same kind. Similarly structure is another user defined data type available in C that allows to combine data items of different kinds.

Structures are used to represent a record. Suppose you want to keep track of your books in a library. You might want to track the following attributes about each book −

*   Title
*   Author
*   Subject
*   Book ID

## Defining a Structure

To define a structure, you must use the struct statement. The struct statement defines a new data type, with more than one member. The format of the struct statement is as follows −

Struct name

{

Datatype member_name;

Datatype member_name;

};

Eg:- struct student

   {

Int data;

Char name[10];

};

## Accessing Structure Members

To access any member of a structure, we use the member access operator (.). The member access operator is coded as a period between the structure variable name and the structure member that we wish to access. You would use the keyword struct to define variables of structure type. The following example shows how to use a structure in a program −

Eg:-

struct student

   {

Int data;

Char name[10];

}s;

S.data;

S.name;

## Example: Store Information in Structure and Display it

#include  <stdio.h>struct student{

 char name[50];

 int roll;

 float marks;} s[10];

int main(){

 int i;

    printf("Enter information of students:\n");

 // storing information

 for(i=0; i<10; ++i)

    {

        s[i].roll = i+1;

        printf("\nFor roll number%d,\n",s[i].roll);

        printf("Enter name: ");

        scanf("%s",s[i].name);

        printf("Enter marks: ");

        scanf("%f",&s[i].marks);

        printf("\n");

    }

    printf("Displaying Information:\n\n");

 // displaying information

 for(i=0; i<10; ++i)

    {

        printf("\nRoll number: %d\n",i+1)

printf("Name: ");

        puts(s[i].name);

        printf("Marks: %.1f",s[i].marks);

        printf("\n");

    }

 return  0;}

Output

Enter information of students:

For roll number1,

Enter name: Tom

Enter marks: 98

For roll number2,

Enter name: Jerry

Enter marks: 89

.

.

.

Displaying Information:

Roll number: 1

Name: Tom

Marks: 98

.

.

.

In C, [structure](http://www.programiz.com/c-programming/c-structures) can be passed to [functions](http://www.programiz.com/c-programming/c-functions) by two methods:

1.  [Passing by value (passing actual value as argument)](http://www.programiz.com/c-programming/c-user-defined-functions)
2.  [Passing by reference (passing address of an argument)](http://www.programiz.com/c-programming/c-pointer-functions)

### Passing structure by value

A structure variable can be passed to the function as an argument as a normal variable.

If structure is passed by value, changes made to the structure variable inside the function definition does not reflect in the originally passed structure variable.

C program to create a structure student, containing name and roll and display the information.

#include  <stdio.h>struct student{

 char name[50];

 int roll;};

void display(struct student stu);// function prototype should be below to the structure declaration otherwise compiler shows error

int main(){

 struct student stud;

    printf("Enter student's name: ");

    scanf("%s", &stud.name);

    printf("Enter roll number:");

    scanf("%d", &stud.roll);

display(stud); // passing structure variable stud as argument

 return  0;}void display(struct student stu){

  printf("Output\nName: %s",stu.name);

  printf("\nRoll: %d",stu.roll);}

### Passing structure by reference

The memory address of a structure variable is passed to function while passing it by reference.

If structure is passed by reference, changes made to the structure variable inside function definition reflects in the originally passed structure variable.

C program to add two distances (feet-inch system) and display the result without the return statement.

#include  <stdio.h>struct distance{

 int feet;

 float inch;};void add(struct distance d1,struct distance d2, struct distance *d3);

int main(){

 struct distance dist1, dist2, dist3;

    printf("First distance\n");

    printf("Enter feet: ");

    scanf("%d", &dist1.feet);

    printf("Enter inch: ");

    scanf("%f", &dist1.inch);

    printf("Second distance\n");

    printf("Enter feet: ");

    scanf("%d", &dist2.feet);

    printf("Enter inch: ");

    scanf("%f", &dist2.inch);

    add(dist1, dist2, &dist3);

 //passing structure variables dist1 and dist2 by value whereas passing structure variable dist3 by reference

    printf("\nSum of distances = %d\'-%.1f\"", dist3.feet, dist3.inch);

 return  0;}void add(struct distance d1,struct distance d2, struct distance *d3) {

 //Adding distances d1 and d2 and storing it in d3

  d3->feet = d1.feet + d2.feet;

     d3->inch = d1.inch + d2.inch;

 if (d3->inch >= 12) { /* if inch is greater or equal to 12, converting it to feet. */

d3->inch -= 12;

         ++d3->feet;

    }}

UNION

A union is a special data type available in C that allows to store different data types in the same memory location. You can define a union with many members, but only one member can contain a value at any given time. Unions provide an efficient way of using the same memory location for multiple-purpose.

## Defining a Union

To define a union, you must use the union statement in the same way as you did while defining a structure. The union statement defines a new data type with more than one member for your program. The format of the union statement is as follows −

Union name

{

Datatype name;

Datatype name;

};

Union and structure are same just that members of union use same memory,unlike structure members whose each member will occupy seperate space.

The difference between structure and union is,
1\. The amount of memory required to store a structure variable is the sum of the size of all the members.
On the other hand, in case of unions, the amount of memory required is always equal to that required by its largest member.

2\. In case of structure, each member have their own memory space but In union, one block is used by all the member of the union.

Detailed Example:

| 123456 | struct stu{ char c; int l; float p;}; |

| 123456 | union emp{ char c; int l; float p;}; |

In the above example size of the structure stu is 7 and size of union emp is 4.

Chapter 9:

C programs

## Program to Multiply Two Numbers

#include  <stdio.h>int main(){

 double firstNumber, secondNumber, productOfTwoNumbers;

    printf("Enter two numbers: ");

 // Stores two floating point numbers in variable firstNumber and secondNumber respectively

    scanf("%lf %lf", &firstNumber, &secondNumber); 

 // Performs multiplication and stores the result in variable productOfTwoNumbers

    productOfTwoNumbers = firstNumber * secondNumber; 

 // Result up to 2 decimal point is displayed using %.2lf

    printf("Product = %.2lf", productofTwoNumbers);

 return  0;}

Output

Enter two numbers: 2.4

1.12

Product = 2.69

## Program to Check Even or Odd

#include  <stdio.h>int main(){

 int number;

    printf("Enter an integer: ");

    scanf("%d", &number);

 // True if the number is perfectly divisible by 2

 if(number % 2 == 0)

        printf("%d is even.", number);

 else

        printf("%d is odd.", number);

 return  0;}

Output

Enter an integer: -7

-7 is odd.

## Program to Print ASCII Value

#include  <stdio.h>int main(){

 char c;

    printf("Enter a character: ");

 // Reads character input from the user

    scanf("%c", &c); 

 // %d displays the integer value of a character

 // %c displays the actual character

    printf("ASCII value of %c = %d", c, c);

 return  0;}

Output

Enter a character: G

ASCII value of G = 71

## Program to Check Prime Number

#include  <stdio.h>int main(){

 int n, i, flag = 0;

    printf("Enter a positive integer: ");

    scanf("%d",&n);

 for(i=2; i<=n/2; ++i)

    {

 // condition for nonprime number

 if(n%i==0)

        {

            flag=1;

 break;

        }

    }

 if (flag==0)

        printf("%d is a prime number.",n);

 else

        printf("%d is not a prime number.",n);

 return  0;}

Output

Enter a positive integer: 29

29 is a prime number.

## Example: Program to Check Leap Year

#include  <stdio.h>

int main(){

 int year;

    printf("Enter a year: ");

    scanf("%d",&year);

 if(year%4 == 0)

    {

 if( year%100 == 0)

        {

 // year is divisible by 400, hence the year is a leap year

 if ( year%400 == 0)

                printf("%d is a leap year.", year);

 else

                printf("%d is not a leap year.", year);

        }

 else

            printf("%d is a leap year.", year );

    }

 else

        printf("%d is not a leap year.", year);

 return  0;}

Output 1

Enter a year: 1900

1900 is not a leap year.

Output 2

Enter a year: 2012

2012 is a leap year.
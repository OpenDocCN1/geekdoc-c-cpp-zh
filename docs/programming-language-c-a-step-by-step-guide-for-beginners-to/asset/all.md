![](Image00000.jpg)

programming language csusanta bourisusanta bouriContents[Title Page](#text00001.html_a77N)[                                        ABOUT THE BOOK](#text00003.html_a79C)[What is c?](#text00005.html_a764)[Programming Basics](#text00007.html_a754)[Data Types](#text00008.html_a756)[Decision control instruction](#text00009.html_a758)[Use of logical operator in C](#text00010.html_a75A)[Loop control statements](#text00011.html_a75C)[Case control statements](#text00012.html_a75E)[Storage Class](#text00013.html_a75G)[Function,   ](#text00014.html_a75J)[Pointer](#text00015.html_a75M)[Array](#text00016.html_a75P)[String](#text00017.html_a75S)[Structure](#text00018.html_a75U)[printf and scanf](#text00019.html_a75W)[Preprocessor directives](#text00020.html_a75Y)[File Handling](#text00021.html_a760)[C – Typedef, C – Union](#text00022.html_a762)[About The Author](#text00023.html_a79S)                                        ABOUT THE BOOKC Programming Language introduces you to the most commonly used programming language, one that has been the basis for many other versions over the years. It is a great book, not just for beginning programmers, but also for computer users who would want to have an idea what is happening behind the scenes as they work with various computer programs.
In this book, you are going to learn what the C programming language entails, how to write conditions, expressions, statements and even commands, for the language to perform its functions efficiently. You will learn too how to organize relevant expressions so that after compilation and execution, the computer returns useful results and not error messages. Additionally, this book details the data types that you need for the C language and how to present it as well.
Simply put, this is a book for programmers, learners taking other computer courses, and other computer users who would like to be versed with the workings of the most popular computer language,  CTopies are as shown below:_What is cProgramming BasicsData typesTokens and keywordsDecision control instructionUse of logical operator in CLoop control statementsCase control statementsStorage ClassFunction,PointerArrayStringStructurePre-processor directivesFile HandlingTypeset, – UnionINTRODUCTIONC Programming Language introduces you to the most commonly used programming language, one that has been the basis for many other versions over the years. It is a great book, not just for beginning programmers, but also for computer users who would want to have an idea what is happening behind the scenes as they work with various computer programs.
In this book, you are going to learn what the C programming language entails, how to write conditions, expressions, statements and even commands, for the language to perform its functions efficiently. You will learn too how to organize relevant expressions so that after compilation and execution, the computer returns useful results and not error messages. Additionally, this book details the data types that you need for the C language and how to present it as well.
Simply put, this is a book for programmers, learners taking other computer courses, and other computer users who would like to be versed with the workings of the most popular computer language,  CWhat is cProgramming BasicsData typesTokens and keywordsDecision control instructionUse of logical operator in CLoop control statementsCase control statementsStorage ClassFunction,PointerArrayStringStructurePre-processor directivesFile HandlingTypeset, – UnionWhat is c?C is a programming language developed at AT & T’s Bell laboratories of USA in 1972.it was designed and written by a man named Dennis Ritchie..Possible why c seems so popular is because it is reliable, simple and easy to use. Moreover, in an industry where newer languages, tools and technologies emerge and vanish day in and day out, a language that has survived for more than three decades has to be really good.An opinion that is often heard  today is – ‘c has been already superseded by language like   c++ ,and java, so why bother to learn c today”,Getting started with cCommunicating with a computer involves speaking the language the computer understands, which immediately rules out English as the language of communication with computer. However ,there is a close analogy between learning English language is to first learn the alphabets used in the language, then learn to combine these alphabets ti form words, which in turn are combined to form sentences and sentences are combined to form paragraphs. Learning  c is similar and easier. Instead of straight-away learning how to write programs, we must first know what alphabets, numbers and special symbols are used in c.Then how using them, constants, variables and keywords are constructed, and finally, how are these combined to form a an instruction. A group of instruction would be combined later on to form a program.The c character setA character denotes any alphabets, digits or special symbol used to represent information.

| Alphabets ..........................................A,B,C,........................X,Y,Z,Digits ................................................0,1,2,3,4,5,6,7,8,9Special symbols.................................=,-;(,),%,&,!,#,@,{,},+,-,*,/,<,>,?, |

Constants, variables and keywordsA constant is an entity that does not change, whereas, a variable is an entity that may change.Types of c constantsa)        Primary constants :-    integer constants ,real constants, character constantsb)        Secondary constants:-  array, pointer, structure, union, enum, etcTYPES OF C CONSTANT

1.  Integer constants
2.  Real or Floating point constants
3.  Octal & Hexadecimal constants
4.  Character constants
5.  String constants
6.  Backslash character constants

| Constant type | data type (Example) |
| Integer constants | int (53, 762, -478 etc ) unsigned int (5000u, 1000U etc)
long int, long long int
(483,647 2,147,483,680) |
| Real or Floating point constants | float (10.456789) doule (600.123456789) |
| Octal constant | int (Example: 013 /*starts with 0 */) |
| Hexadecimal constant | int (Example: 0x90 /*starts with 0x*/) |
| character constants | char (Example: ‘A’, ‘B’, ‘C’) |
| string constants | char (Example: “ABCD”, “Hai”) |
|  |  |

RULES FOR CONSTRUCTING C CONSTANT:1\. INTEGER CONSTANTS IN C:

*   An integer constant must have at least one digit.
*   It must not have a decimal point.
*   It can either be positive or negative.
*   No commas or blanks are allowed within an integer constant.
*   If no sign precedes an integer constant, it is assumed to be positive.
*   The allowable range for integer constants is -32768 to 32767.

2. REAL CONSTANTS IN C:

*   A real constant must have at least one digit
*   It must have a decimal point
*   It could be either positive or negative
*   If no sign precedes an integer constant, it is assumed to be positive.
*   No commas or blanks are allowed within a real constant.

3. CHARACTER AND STRING CONSTANTS IN C:

*   A character constant is a single alphabet, a single digit or a single special symbol enclosed within single quotes.
*   The maximum length of a character constant is 1 character.
*   String constants are  enclosed within double quotes.

4. BACKSLASH CHARACTER CONSTANTS IN C:

*   There are some characters which have special meaning in C language.
*   They should be preceded by backslash symbol to make use of special function of them.
*   Given below is the list of special characters and their purpose.

| Backslash _ character | Meaning |
| \b | Backspace |
| \f | Form feed |
| \n | New line |
| \r | Carriage return |
| \t | Horizontal tab |
| \” | Double quote |
| \’ | Single quote |
| \\ | Backslash |
| \v | Vertical tab |
| \a | Alert or bell |
| \? | Question mark |
| \N | Octal constant (N is an octal constant) |
| \XN | Hexadecimal constant (N – hex.dcml cnst) |

HOW TO USE CONSTANTS IN A C PROGRAM?We can define constants in a C program in the following ways.

1.  By “const” keyword

2.  By “#define” preprocessor directive

Please note that when you try to change constant values after defining in C program, it will through error.EXAMPLE PROGRAM USING CONST KEYWORD IN C:

| 234567891011121314 | #include <stdio.h>void main(){const int height = 100; /*int constant*/const float number = 3.14; /*Real constant*/const char letter = 'A'; /*char constant*/const char letter_sequence[10] = "ABC"; /*string constant*/const char backslash_char = '\?'; /*special char cnst*/printf("value of height :%d \n", height );printf("value of number : %f \n", number );printf("value of letter : %c \n", letter );printf("value of letter_sequence : %s \n", letter_sequence);printf("value of backslash_char : %c \n", backslash_char);} |

OUTPUT:

| value of height : 100 value of number : 3.140000
value of letter : A
value of letter_sequence : ABC
value of backslash_char : ?   |

EXAMPLE PROGRAM USING #DEFINE PREPROCESSOR DIRECTIVE IN C:

| 1234567891011121314 | #include <stdio.h>#define height 100#define number 3.14#define letter 'A'#define letter_sequence "ABC"#define backslash_char '\?'void main(){printf("value of height : %d \n", height );printf("value of number : %f \n", number );printf("value of letter : %c \n", letter );printf("value of letter_sequence : %s \n",letter_sequence);printf("value of backslash_char : %c \n",backslash_char);} |

OUTPUT:

| value of height : 100 value of number : 3.140000
value of letter : A
value of letter_sequence : ABC
value of backslash_char : ? |

Rules for constructing integer constantsa)        An integer constant must have at least one digits.b)        It must not have a decimal point.c)         It can be either positive or negative.d)        If no sign precedes an integer constant, it is assumed to be positive.e)        No commas or blanks are allowed within an integer constant.f)          The allowable range for integer constant is -2147483648 to + 2147483647Ex- 426, +782, -8000, -7605Rules for constructing real constantsReal constant are often called floating point constants. The real constants could be written in two formsFractional form , and Exponential forma)        A real constant must have at least one digits.b)        It must have a decimal point.c)         It could be either positive or negative.d)        Default sign is positive.e)        No commas or blanks are allowed within a real constant.Ex:- +325.34, 426.0, -48.5789Rules for constructing character constantsa)        A character constant is a single alphabet, a single digits or a single special symbol enclosed within single inverted commas. Both the inverted commas should point to the left. for example a is a valid character constant whereas a is not.b)         The maximum length of a character constant can be 1 character.Ex:- A,T,STypes of c variablesAn entity that may vary during program execution is called a variable. Variable   names are given to location  in memory. These locations can contain integer, real or character constant. In any language the types of variables that it can support depends on the types of constant that it can handle. This is because a particular type of variable can hold only an integer constant, a real variable can hold only a real constant and a character variable can hold only a character constant.Three types of C variables    : _ a) integer   x ,y, z ;     b) float   z;          c) char st- name[20] :Rules for constructing variable namesa)       A variable name is any combination of 1 to  30 alphabets, digits or underscores. Some compilers allow variable names whose length could be up to 247 character. Still it would be safer to stick to the rule of 31 character. Do not create unnecessarily long variable names as it adds to your typing effort.b)        The first character in the variable name must be an alphabet or underscore.c)         No commas or blanks are allowed within a variable name.d)        No special symbol other than an underscore.Ex:- si...int,  m-hra, pop-e-78THERE ARE THREE TYPES OF VARIABLES IN C PROGRAM THEY ARE,

1.  Local variable

2.  Global variable

3.  Environment variable

1. EXAMPLE PROGRAM FOR LOCAL VARIABLE IN C:

*   The scope of local variables will be within the function only.
*   These variables are declared within the function and can’t be accessed outside the function.
*   In the below example, m and n variables are having scope within the main function only. These are not visible to test function.
*   Like wise, a and b variables are having scope within the test function only. These are not visible to main function.

| #include<stdio.h>void test();int main(){int m = 22, n = 44;// m, n are local variables of main function/*m and n variables are having scopewithin this main function only.These are not visible to test funtion.*//* If you try to access a and b in this function,you will get 'a' undeclared and 'b' undeclared error */printf("\nvalues : m = %d and n = %d", m, n);test();}void test(){int a = 50, b = 80;// a, b are local variables of test function/*a and b variables are having scopewithin this test function only.These are not visible to main function.*//* If you try to access m and n in this function,you will get 'm' undeclared and 'n' undeclarederror */printf("\nvalues : a = %d and b = %d", a, b);} |

OUTPUT:

| values : m = 22 and n = 44values : a = 50 and b = 80 |

EXAMPLE PROGRAM FOR GLOBAL VARIABLE IN C:

*   The scope of global variables will be throughout the program. These variables can be accessed from anywhere in the program.
*   This variable is defined outside the main function. So that, this variable is visible to main function and all other sub functions.

| 1234567891011121314151617 | #include<stdio.h>void test();int m = 22, n = 44;int a = 50, b = 80;int main(){printf("All variables are accessed from main function");printf("\nvalues: m=%d:n=%d:a=%d:b=%d", m,n,a,b);test();}void test(){printf("\n\nAll variables are accessed from" \" test function");printf("\nvalues: m=%d:n=%d:a=%d:b=%d", m,n,a,b);} |

OUTPUT:

| All variables are accessed from main function values : m = 22 : n = 44 : a = 50 : b = 80
All variables are accessed from test function
values : m = 22 : n = 44 : a = 50 : b = 80 |

ENVIRONMENT VARIABLES IN C:

*   Environment variable is a variable that will be available for all C  applications and C programs.
*   We can access these variables from anywhere in a C program without declaring and initializing in an application or C program.
*   The inbuilt functions which are used to access, modify and set these environment variables are called environment functions.

*   There are 3 functions which are used to access, modify and assign an environment variable in C. They are,

EXAMPLE PROGRAM FOR GETENV() FUNCTION IN C:This function gets the current value of the environment variable. Let us assume that environment variable DIR is assigned to “/usr/bin/test/”.

| 12345678 | #include <stdio.h>#include <stdlib.h>int main(){printf("Directory = %s\n",getenv("DIR"));return 0;} |

OUTPUT:

| /usr/bin/test/ |

EXAMPLE PROGRAM FOR SETENV() FUNCTION IN C:This function sets the value for environment variable. Let us assume that environment variable “FILE” is to be assigned “/usr/bin/example.c”

| 123456789 | #include <stdio.h>#include <stdlib.h>int main(){setenv("FILE", "/usr/bin/example.c",50);printf("File = %s\n", getenv("FILE"));return 0;} |

OUTPUT:

| File = /usr/bin/example.c |

EXAMPLE PROGRAM FOR PUTENV() FUNCTION IN C:This function modifies the value for environment variable. Below example program shows that how to modify an existing environment variable value.

| 12345678910111213 | #include <stdio.h>#include <stdlib.h>int main(){setenv("DIR", "/usr/bin/example/",50);printf("Directory name before modifying = " \"%s\n", getenv("DIR"));putenv("DIR=/usr/home/");printf("Directory name after modifying = " \"%s\n", getenv("DIR"));return 0;} |

OUTPUT:

| Directory name before modifying = /usr/bin/example/ Directory name after modifying = /usr/home/ |

DIFFERENCE BETWEEN VARIABLE DECLARATION & DEFINITION IN C:

| Variable declaration | Variable definition   |
| Declaration tells the compiler about data type and size of the variable. | Definition allocates memory for the variable. |
| Variable can be declared many times in a program. | It can happen only one time for a variable in a program. |
| The assignment of properties and identification to a variable. | Assignments of storage space to a variable. |

C   keywordsThe keywords cannot be used as variable names because if we do so , we are trying to assign a new meaning to the keyword, which is not allowed by the computer. Some c compilers allow you to construct variable names that exactly resemble the keywords. However, it would be safer not to mix up the variable names and the keywords. The keywords are also called reserved words.  There are only 32 keywords available in c.

| Auto                                                                                                            doubleBreak                                                                                                            elseCase                                                                                                           enumChar                                                                                                            extermConst                                                                                                            float          Continue                                                                                                            for Default                                                                                                          gotodo                                                                                                                 if |
| Int                                                    structLong                                                switchRegister                                                  typedefReturn                                                      unionShort                                                  unsignedSigned                                                       void      Sizeof                                                volatilestatic                                                             while |

The first C programa)        Each instruction in a c program is written as a separate statement. Therefore a complete c program would comprise a series of statement.b)        The statements in a program must appear in the same order in which we wish them to be executed, unless of course the logic of the problems demands a deliberate jump, or transfer of control to a statements to a statement, which is out of sequence.c)        Blank spaces may be inserted between two words to improve the readability of the statement. However, no blank spaces are allowed within a variable, constant or keyword.d)         All statements are entered in small case letters.e)        C has no specific rules for the position at which a statement is to be written. That’s why it is often called a free form language.f)           Every c statement must end with a; thus ; acts as a statement terminator.#include<stdio.h>main(){​ int total;​ printf("\n enter total marks in exam");​ scanf("%d",&total);​ if (total>=100)​ printf("\n passed");​ else​ printf("\n failed")}The output of this program are as belowEnter total marks in exam  :- 200passedabove program explanationa)        it is necessary to use  #include<stdio.h> at the beginning of the program.#include is a pre-processor directive.b)       Main() is a function. A function is nothing but a set of statements .in a  c  program there can be multiple functions. To begin with, we would concentrate only one function. The name of this function has to be main(), it cannot be anything else. All statements that belong to main() are enclosed within a pair of braces {} as shown belowInt main(){Statement 1Statement  2Statement   3}C) Output in C can be achieved using  printf() functionThe general form of printf() function is%f for printing real values%d  for printing integer values%c  for  printing  character valuesD)Inputs in C can be achieved using scanf() functionThe general form of scanf() function isFormat string                                      variable%d                                                     int%f                                                       float%c                                                      charWe can write a program to used printf()  &  scanf()  are as below#include<stdio.h>main(){​ float f,c;​ printf ("enter celcius temp");​ scanf( "%f", &c);​ f=(9*c)/5+32;​ printf("%f",f);}Out put of this programEnter celcius temp  2068.000000C InstructionsThere are basically three types of instruction in C :A)        Type declaration instruction     -   this instruction is used to declare the types of variables used in a C program.B)        Arithmetic instruction    : - this instruction is used to perform arithmetic operations on constants and variables.C)        Control instruction     :-    this instruction is used to control the sequence of execution of various statements in a c  program.Programming BasicsThis C programming basics section explains a simple “Hello World” C program. Also, it covers below basic topics as well, which are to be known by any C programmer before writing a C program.C PROGRAMMING BASICS TO WRITE A C PROGRAM:Below are few commands and syntax used in C programming to write a simple C program. Let’s see all the sections of a simple C program line by line.

| C Basic commands | Explanation |
| #include <stdio.h>:- | This is a preprocessor command that includes standard input output header file(stdio.h) from the C library before compiling a C program |
| int main() :- | This is the main function from where execution of any C program begins. |
| {:- | This indicates the beginning of the main function. |
| /*_some_comments_*/ | whatever is given inside the command “/*   */” in any C program, won’t be considered for compilation and execution. |
| printf(“Hello_World! “):_ | printf command prints the output onto the screen. |
| getch():- | This command waits for any character input from keyboard. |
| return 0;- | This command terminates C program (main function) and returns 0. |
| }:- | This indicates the end of the main function. |

A SIMPLE C PROGRAM:Below C program is a very simple and basic program in C programming language. This C program displays “Hello World!” in the output window. And, all syntax and commands in C programming are case sensitive. Also, each statement should be ended with semicolon (;) which is a statement terminator.A)

| #include <stdio.h>int main(){/* Our first simple C basic program */printf("Hello World! ");getch();return 0;} |

OUTPUT:

| Hello World! |

STEPS TO WRITE C PROGRAMS AND GET THE OUTPUT:Below are the steps to be followed for any C program to create and get the output. This is common to all C program and there is no exception whether its a very small C program or very large C program.

1.  Create
2.  Compile
3.  Execute or Run
4.  Get the Output

CREATION, COMPILATION AND EXECUTION OF A C PROGRAM:Prerequisite:

*   If  you want to create, compile and execute C programs by your own, you have to install C compiler in your machine. Then, you can start to execute your own C programs in your machine.
*   You can refer below link for how to install C compiler and compile and execute C programs in your machine.
*   Once C compiler is installed in your machine, you can create, compile and execute C programs as shown in below link.
*   If you don’t want to install C/C++ compilers in your machine, you can refer online compilers which will compile and execute C/C++ and many other programming languages online and display outputs on the screen. Please search for online C/C++ compilers in Google for more details.

BASIC STRUCTURE OF A C PROGRAM:Structure of C program is defined by set of rules called protocol, to be followed by programmer while writing C program. All C programs are having sections/parts which are mentioned  below.

1.  Documentation section
2.  Link Section
3.  Definition Section
4.  Global declaration section
5.  Function prototype declaration section
6.  Main function
7.  User defined function definition section

EXAMPLE C PROGRAM TO COMPARE ALL THE SECTIONS:You can compare all the sections of a C program with the below C program.

|  | #include <stdio.h>  int total = 0;      int sum (int, int);  int main ()          {printf ("This is a C basic program \n");total = sum (1, 1);printf ("Sum of two numbers : %d \n", total);return 0;}int sum (int a, int b){  return a + b;      } |

OUTPUT:

| This is a C basic program Sum of two numbers : 2 |

DESCRIPTION FOR EACH SECTION OF THE C PROGRAM:

*   Let us see about each section of a C basic program in detail below.
*   Please note that a C program mayn’t have all below mentioned sections except main function and link sections.
*   Also, a C program structure mayn’t be in below mentioned order.

| Sections | Description |
| Documentation section | We can give comments about the program, creation or modified date, author name etc in this section. The characters or words or anything which are given between “/*” and “*/”, won’t be considered by C compiler for compilation process. These will be ignored by C compiler during compilation.   |
| Link Section | Header files that are required to execute a C program are included in this section |
| Definition Section | In this section, variables are defined and values are set to these variables. |
| Global declaration section | Global variables are defined in this section. When a variable is to be used throughout the program, can be defined in this section. |
| Function prototype declaration section | Function prototype gives many information about a function like return type, parameter names used inside the function. |
| Main function | Every C program is started from main function and this function contains two major sections called declaration section and executable section. |
| User defined function section | User can define their own functions in this section which perform particular task as per the user requirement. |

KEY POINTS TO REMEMBER IN C PROGRAMMING BASICS:

1.  C programming is a case sensitive programming language.

2.  Each C programming statement is ended with semicolon (;) which are referred as statement terminator.

3.  printf() command is used to print the output onto the screen

4.  C programs are compiled using C compilers and displays output when executed.

Data TypesC data types are defined as the data storage format that a variable can store a data to perform a specific operation.Data types are used to define a variable before to use in a program.Size of variable, constant and array are determined by data types.C – DATA TYPES:There are four data types in C language. They are,

| Types | Data Types |
| Basic data types | int, char, float, double |
| Enumeration data type | enum |
| Derived data type | pointer, array, structure, union |
| Void data type | void |

BASIC DATA TYPES IN C LANGUAGE:1.1.      INTEGER DATA TYPE:

*   Integer data type allows a variable to store numeric values.
*   “int” keyword is used to refer integer data type.
*   The storage size of int data type is 2 or 4 or 8 byte.
*   It varies depend upon the processor in the CPU that we use.  If we are using 16 bit processor, 2 byte  (16 bit) of memory will be allocated for int data type.
*   Like wise, 4 byte (32 bit) of memory for 32 bit processor and 8 byte (64 bit) of memory for 64 bit processor is allocated for int datatype.
*   int (2 byte) can store values from -32,768 to +32,767
*   int (4 byte) can store values from -2,147,483,648 to +2,147,483,647.
*   If you want to use the integer value that crosses the above limit, you can go for “long int” and “long long int” for which the limits are very high.

Note:

*   We can’t store decimal values using int data type.
*   If we use int data type to store decimal values, decimal values will be truncated and we will get only whole number.
*   In this case, float data type can be used to store decimal values in a variable.
*   CHARACTER DATA TYPE:

*   Character data type allows a variable to store only one character.
*   Storage size of character data type is 1\. We can store only one character using character data type.
*   “char” keyword is used to refer character data type.
*   For example, ‘A’ can be stored using char data type. You can’t store more than one character using char data type.
*   Please refer  [C – Strings](http://fresh2refresh.com/c/c-strings/)  topic to know how to store more than one characters in a variable.

1.3\. FLOATING POINT DATA TYPE:Floating point data type consists of 2 types. They are,

1.  float
2.  double

1.  FLOAT:

*   Float data type allows a variable to store decimal values.
*   Storage size of float data type is 4. This also varies depend upon the processor in the CPU as “int” data type.
*   We can use up-to 6 digits after decimal using float data type.
*   For example, 10.456789 can be stored in a variable using float data type.

2.  DOUBLE:

*   Double data type is also same as float data type which allows up-to 10 digits after decimal.
*   The range for double datatype is from 1E–37 to 1E+37.

SIZEOF() FUNCTION IN C LANGUAGE:sizeof() function is used to find the memory space allocated for each C data types.

| 1234567891011121314 | #include <stdio.h>#include <limits.h>int main(){int a;char b;float c;double d;printf("Storage size for int data type:%d \n",sizeof(a));printf("Storage size for char data type:%d \n",sizeof(b));printf("Storage size for float data type:%d \n",sizeof(c));printf("Storage size for double data type:%d\n",sizeof(d));return 0;} |

OUTPUT:

| Storage size for int data type:4 Storage size for char data type:1
Storage size for float data type:4
Storage size for double data type:8 |

MODIFIERS IN C LANGUAGE:

*   The amount of memory space to be allocated for a variable is derived by modifiers.
*   Modifiers are prefixed with basic data types to modify (either increase or decrease) the amount of storage space allocated to a variable.
*   For example, storage space for int data type is 4 byte for 32 bit processor. We can increase the range by using long int which is 8 byte. We can decrease the range by using short int which is 2 byte.

*   There are 5 modifiers available in C language. They are,

1.  short
2.  long
3.  signed
4.  unsigned
5.  long long

Below table gives the detail about the storage size of each C basic data type in 16 bit processor. Please keep in mind that storage size and range for int and float datatype will vary depend on the CPU processor (8,16, 32 and 64 bit)

| C Data types / storage Size | Range |
| char / 1 | –127 to 127 |
| int / 2 | –32,767 to 32,767 |
| float / 4 | 1E–37 to 1E+37 with six digits of precision |
| double / 8 | 1E–37 to 1E+37 with ten digits of precision |
| long double / 10 | 1E–37 to 1E+37 with ten digits of precision |
| long int / 4 | –2,147,483,647 to 2,147,483,647 |
| short int / 2 | –32,767 to 32,767 |
| unsigned short int / 2 | 0 to 65,535 |
| signed short int / 2 | –32,767 to 32,767 |
| long long int / 8 | –(2power(63) –1) to 2(power)63 –1 |
| signed long int / 4 | –2,147,483,647 to 2,147,483,647 |
| unsigned long int / 4 | 0 to 4,294,967,295 |
| unsigned long long int / 8 | 2(power)64 –1 |

ENUM EXAMPLE PROGRAM:

| 123456789101112 | #include <stdio.h>int main(){enum MONTH { Jan = 0, Feb, Mar };enum MONTH month = Mar;if(month == 0)printf("Value of Jan");else if(month == 1)printf("Month is Feb");if(month == 2)printf("Month is Mar");} |

OUTPUT:

| Month is March |

DERIVED DATA TYPE IN C LANGUAGE:

*   Array, pointer, structure and union are called derived data type in C language.
*   To know more about derived data types, please v isit “ [C – Array](http://fresh2refresh.com/c/c-array/) ” , “ [C – Pointer](http://fresh2refresh.com/c/c-pointer/) ” , “ [C – Structure](http://fresh2refresh.com/c/c-structures/) ” and “ [C – Union](http://fresh2refresh.com/c/c-union/) ” topics in this  tutorial.

. VOID DATA TYPE IN C LANGUAGE:

*   Void is an empty data type that has no value.
*   This can be used in functions and pointers.
*   Please  visit “ [C – Function](http://fresh2refresh.com/c/c-function/) ” to pic to know how to use void data type in function with simple call by value and call by reference example programs.

Tokens and keywordsC tokens, Identifiers and Keywords are the basics in a C program. All are explained in this page with definition and simple example programs.C TOKENS:

*   C tokens   are the basic buildings blocks in C language which are constructed together to write a C program.
*   Each and every smallest individual units in a C program are known as C tokens.

C tokens are of six types. They are,TOKENS EXAMPLE PROGRAM:

| 1234567 | #include<stdio.h>int main(){int x, y, total;x = 10, y = 20;total = x + y;printf ("Total = %d \n", total)} |

where,

3.  IDENTIFIERS IN C LANGUAGE:

*   Each program elements in a C program are given a name called identifiers.
*   Names given to identify Variables, functions and arrays are examples for identifiers. eg. x is a name given to integer variable in above program.

RULES FOR CONSTRUCTING IDENTIFIER NAME IN C:

1.  First character should be an alphabet or underscore.

2.  Succeeding characters might be digits or letter.

3.  Punctuation and special characters aren’t allowed except underscore.

4.  Identifiers should not be keywords.

4.  KEYWORDS IN C LANGUAGE:

*   Keywords are pre-defined words in a C compiler.
*   Each keyword is meant to perform a specific function in a C program.
*   Since keywords are referred names for compiler, they can’t be used as variable name.

Decision control instructionBy default the instruction in a program are executed sequentially. However , in  serious programming situations, seldom do we want the instructions to be executed sequentially. Many a time ,we want a set of instructions to be executed in one situation, and an entirely different set of instructions to be executed in another situation. This kind of situation is dealt with in c programs using a decision control instruction. As mentioned earlier, a decision control instruction can be implemented in c usingC has major three decision control instructiona)         The if  statementb)         The if –else statementc)          The  conditional operatorsThe  if  statementLike most languages, c  uses the keyword if  to implement the decision control instruction. The keyword if tells the compiler that what follows is a decision control instruction. If the condition whatever it is ,is true, then the statement is not executed, instead the program skips past it. But how do we express the condition itself in c? And how do we evaluate its truth or falsity? As a general rule, we express a condition using c’s relational operators. The relational operators allow us to compare two values to see whether they are equal to each other, unequal, or whether one is greather than the other. Here is how they look and how they are evaluated in C.

| This expression                                                                                                               is true ifX==y                                                                                                      x is equal to yX!=y                                                                                                     x is not equal to yX<y                                                                                                      x is less than yx>y                                                                                                       x is greater than yx <=y                                                                                                     x is less than or equal to y    x>=y                                                                                                       x is greater than or equal to y |

The relational operators should be familiar to you except for the equality operators ==and the in equality operators  != Note that = is used for assignment, whereas, == is used for comparison of two quantities.Here is a simple program, which demonstrates the use of if and the relational operators.a)#include<stdio.h>main(){​ int a,b,c,big;​ printf("enter the value of a,b and c");​ scanf("%d%d%d",&a,&b,&c);​ big=a;​ if(b>big)​ big=b;​ if(c>big)​ big=c;​ printf("largest number=%d",big);}Output of this program are as belowenter the value of a,b and c 100200500Largest number = 500On execution of this program , if you type enter the value of a,b and c  , you get a message on the screen through printf(). The largest number..To make you comfortable with the decision control instruction, one more example has been given below.Study it carefully  before reading further.b)#include<stdio.h>main(){​ int a,b,c,small;​ printf("Enter the value of a,b and c");​ scanf("%d%d%d",&a,&b,&c);​ small=a;​ if(b<small)​ small=b;​ if(c<small)​ small=c;​ printf("smallest no=%d",small);}Output of this program are as follow belowEnter the value of a,b and c50100150Smallest no = 50On execution of this program , if you type enter the value of a,b and c  , you get a message on the screen through printf(). The smallest number.The  if – else statementThe if statement by itself will execute a single statement, or a group of statement, when the expression following if evaluates to true. It does nothing when the expression evaluates to false. Can we execute one group of statements if the expression evaluates to true and another group of statement if the expression evaluates to  false? Of course!This is what is the purpose of the else statement that is demonstrated in the following example:A)#include<stdio.h>main(){​ int  total;​ float percentage;​ printf("\n enter the total marks in exam");​ scanf("%d",& total);​ percentage= total/8;​ printf(" percentage =%f",percentage);​ if(percentage>=90)​ printf("\n1st divisioin ");​ if( percentage>=70)​ printf("\n 2nd division");​ if ( percentage>=50)​ printf( " \n third division");​ else​ printf( "\n failed");}Output of this program are as follows belowenter the total marks in exam580Percentage = 72.000002nd divisionB)#include<stdio.h>main(){​ int total;​ printf("\n enter total marks in exam");​ scanf("%d",&total);​ if (total>=100)​ printf("\n passed");​ else​ printf("\n failed");}Output of this programenter total marks in exam:500passedA few points worth nothingA)       The group of statements after the if upto and not including the else is called an if block, similarly, the statements after the else form the else block.B)       Notice that the else is written exactly below the if. Ihe statements in the if block and those in the else block have been indented to the right. This formatting convention is  followed the book to enable you to understand the working of the  program better.C)       Had there been only one statement to be executed in the if block and one statement in the else block we could have dropped the pair of braces.D)       As with the if statement, the default, the default scope of else is also the statement immediately after the else. To override this default scope, a pair of braes, as shown in the above example, must be used.Nested if – elsesIt is perfectly all right if we write an entire if-else construct within either the body of the if statement or thebody of an else statement. This is called nesting of ifs. This is shown in the following program:a)#include <stdio.h>Int main(){Int i ;Printf(“ enter either 1 or 2 “);Scanf(“%d”, &i);If (i==1)Printf(“ you would go to heaven \n”);Else{If (i==2);Printf(“\n hell was created with you in mind “);ElsePrintf(“\n how was mother earth”);}Return 0;}Note that :_the second if- else construct is nested in the first else statement. If the condition in the first if statement is false, then the condition in the second if statement checked. If  it is false as well, then final else statement is executed.  You can see in the program how each time a if –else construct is nested within another if- else construct, it is also indented to add clarity to the program. Inculcate this habit of indentation, otherwise, you would end up writing programs which nobody can understand easily at a later date. Note that whether we indent or do not indent the program, it does not alter the flow of execution of instructions in the program.Use of logical operator in CThese operators are used to perform logical operation on the given expressionC allows usage of three logical operators, namely, &&,  ||,and. !, These are to be read as AND , OR  and NOT respectively.

| Operators | Example/ description |
| && (logical AND) | ( X>5)&&(Y<5)IT RETURNS TRUE WHEN BOTH CONDITION ARE TRUE |
| &#124;&#124; ( logical OR) | (X>=10)&#124;&#124;(Y>=10)IT RETURNS TRUE WHEN AT LEAST ONE OF THECONDITION IN TRUE |
| ! (  logical NOT) | !((X>5)&&(Y<5))IT REVERSES THE STATE OF THE OPERAND“((X>5)&&(Y<5))”  IF “((X>5)&&(Y<5))” IS TRUE,LOGICAL,  NOT, OPERATOR MAKES IS FALSE |

A)         Write a program to find  year ia a leap year or not.#include<stdio.h>main(){​ int n;​ printf("Enter any year");​ scanf("%d",&n);​ if(((n%100==0)&&(n%400==0))||((n%100!=0)&&(n%4==0)))​ printf("year is a leap year");​ else​ printf("yearis not a leap year");}Output of this program :Enter any year2000Year is a leap yearARITHMETIC OPERATORS IN CC arithmetic operators are used to perform mathematical calculations like    addition,  subtraction,  multiplication, division, and modulus in c program.

| Arithmetic operators/ operation | Example |
| +( addition) | A+B |
| -( subtraction) | A-B |
| *( multiplication) | A*B |
| /( division) | A/B |
| %( modulus) | A%B |

A)        WRITE A PROGRAM TO ADDITION A NUMBER#include<stdio.h>main(){​ int a,b,c,add;​ printf( "\nEnter three number",a,b,c);​ scanf("%d %d %d",&a, &b, &c);​ add=(a+b+c);​ printf("\n =%d",add);}C ASSIGNMENT OPERATORSIn c program , values for the variables are assigned using assignment operators.A)        For example, if the value   10, is to be assigned for the variable  sum,  it can be assigned as  , sum=10;B)        There are 2 categories of assignment operators in c  language, they areC)        Simple assignment operators ( example : =)D)        Compound assignment operators ( example : +=,-=,*=,/=,%=,&=,^=)

| operators | Example/ description |
| = | Sum=10; 10 is assigned to variable sum |
| += | Sum+=10; this is same as sum = sum +10 |
| -= | Sum-=10; this is same as sum = sum -10 |
| *= | Sum *=10; this is same as sum = sum *10 |
| /= | Sum/=10; this is same as sum = sum /10 |
| %= | Sum %=10; this is same as sum = sum%10 |
| &= | Sum&=10; this is same as sum = sum &10 |
| ^= | Sum^=10; this is same as sum = sum ^10 |

a)       In this program, values from o-9, are summed up and total ,45, is displayed as output.b)       Assignment operators such as =,  +=, are used in this program to assign the values and to sum up the values.a)#include<stdio.h>int main (){​ int total=0,i;​ for (i=0;i<10;i++)​ {​ total+=i;//this is same as total = total +i​ }​ printf("\ntotal=%d,total");}OutputTotal=45C  relational operatorsRelational operators are used to find the relation between two variables, i.e  to  compare the values of  two variables in a c  program.

| Operators | Example/ description |
| > | x>y, ( x is greater than y) |
| < | X<y, ( x is less than y) |
| >= | X>=y, ( x is greater than or equal to y). |
| <= | X<=y, ( x is less than or equal to y ) |
| == | X==y, ( x is equal to y) |
| != | X !=y, ( x is not equal to y) |

Example program for C  relational operatorsa)       In this program relational operators (==) is used to compare 2 values whether they are equal are not.b)       If both values are equal, output is displayed as , values are equal,  else, output is displayed as , values are not equal,.c)         Note:-  double equal sign (==) should be used to compare 2 values. We should not  single equal sign (=).a)#include<stdio.h>int main (){​ int m=40,n=20;​ if ( m==n)​ {​ printf("\n m and n are equal");​ }​ {​ printf("\n m and n are not equal");​ }}OutputM and n are not equalBit wise operatorsThese  operators are used to perform bit operations. Decimal values are converted into binary values which are the sequence of bits and and bit wise operators work on these bits.Bit wise operators in c language are & ( bitwise AND),| ( bitwise OR), ^(XOR), <<(left shift) and >>( right shift)Truth table for bit wise operation & bitwise  operators

| x | y | x/y | X&y | X^y |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 | 0 |

Below are the bit wise operators and their name in c languagea)         &-   bitwise ANDb)         |-   bitwise  ORc)          - - bitwise NOTd)         ^-  XORe)         << -  left shiftf)           >> -  right shiftConsider x=40, and y=80\. Binary form of these values are given belowX=00101000Y=01010000All bit wise operations for x and y are given belowA)        X&y= 00000000( binary)=0(decimal)B)        X|y= 01111000(binary)=120(decimal)C)        –x= 111111111111111111111111111111111111111111111111111=-41(decimal)D)        X^y= 01111000(binary)=120(decimal)E)        X<<1= 01010000(binary)= 80( decimal)F)        X>>1= 00010100( binary) = 20 ( decimal)Note :- value of 40 in binary is 000000000000000000000000000000000000000000000000000000,so all 0’s are converted into in bit wise NOT operation.Bitwise left shift and right shift :-  in left shift operation,  x<<1,  1 means that the bits will be left shifted by one place. If we ised it as , x<<2 then it means that the bits will be shifted by 2 places.,Example program for bit wise operations in c.#include<stdio.h>main(){​ int m =40, n=80, AND_opr, OR_opr, XOR_opr, NOT_opr;​ AND_opr=(m&n);​ OR_opr =(m|n);​ NOT_opr =(-m);​ XOR_opr =(m^n);​ printf("\n AND_opr value= %d\n", AND_opr);​ printf("\n OR_opr value= %d\n", OR_opr); ​ printf("\n NOT_opr value= %d\n", NOT_opr);​ printf("\n XOR_opr value= %d\n", XOR_opr);​ printf("\n left_shift value= %d\n", m<<1);​ printf("\n right_shift value= %d\n", m>>1);}OutputAND_opr value = 0OR_opr value =120NOT_opr value= -41XOR_opr value = 120left_shift value = 80right_shift  value = 20conditional operators in cconditional operators return one value if condition is true and returns another value is condition is false.This operators is also called as ternary operators.Syntax : ( condition?true_ value:false_ value);Example : ( a> 100 ? 0:1);In above example, if a is greater than 100, 0 is returned else 1 is returned. This is equal to if else conditional statements.Example program for conditional / ternary operators in c#include<stdio.h>int main(){​ int x=1,y;​ y= ( x==1 ? 2:0);​   printf("\n  x value is %d ",x);​   printf("\n  y  value is %d ",y);​ }OutputX value is 1Y value is 2C  increment/ decrement operatorsIncrement operators are used to increase the value of the variable of the by one and decrement operators are used to decrease the value of the variable by one in c peograms.Syntax :-increment operators : ++var_name;(or) var_name++;decrement operators:-  --var_name;(or)var_name--;example :_increment operators :-    ++i; i++;decrement operators :-   --i;  i--;example program for increment operators in cin this program, value of , i,  is increment one by one from i upto 9 using ,i++, operators and output id displayed as , 123456789a)         Example for increment operators#include<stdio.h>int main (){​ int i=1;​ while (i<=10)​ {​ printf("\n %d",i);​ i++;​ }}Output123456789b)         Example  for decrement operators#include<stdio.h>int main (){​ int i=20;​ while (i>10)​ {​ printf("\n %d",i);​ i--;​ }}Output209 18 17 16 15 14 13 12 11C)Example program for pre – increment operators in c#include<stdio.h>int main (){​ int i=0;​ while (++i<5)​ {​ printf("\n %d",i);​ }​ return 0;}Output1234Step 1: in above program, value of ,i , is incremented from 0 to 1 using pre – increment operators.Step 2: this incremented value ,1, is compared with 5 in while expression.Step 3: then this incremented value ,1, is assigned to the variable ,i,Above 3 steps are continued until while expression becomes false and output is displayed as , 1234D) Example program for pre – Decrement operators in c#include<stdio.h>int main(){​ int i=10;​ while( --i>5)​ {​ printf("\n %d",i);​ }​ return 0;}Output9 87 6Step 1:  in above program, the value of ,i, is decremented from 10 to 9 using pre – decrement operators.Step 2: this decremented value ,9, is compared with 5 in while expression.Step 3: then this decremented value ,9,  is assigned to the variables ,i,.Above 3 steps are continued until while expression becomes false and output id displayed as 9,8,7,6Special operators in cBelow are some of the special operators that the c programming language offers.

| operators | Description |
| & | This is used to get the address of the variableExample: &a will give address of a |
| * | This is used as pointer to a variableExample: *a where, * is pointer to the variable a |
| Sizeof() | This gives the size of the variable.Example: size of (char) will give us 1 |

a)Example program for & AND * operators in c#include<stdio.h>int  main(){​ int *ptr,q;​ q=50;ptr=&q;​ printf("\n %d,"* ptr );​ return 0;}Output50b)Example program for sizeof() operators in c#include<stdio.h>#include<limits.h>int main(){​ int a;​ char b;​ float c;​ double d;​ printf ("\n storage size for int data type : %d ", sizeof(a));printf ("\n storage size for char data type : %c ", sizeof(b));printf ("\n storage size for float data type : %f ", sizeof(c));printf ("\n storage size for double data type : %f ", sizeof(d));​ return 0;​ }Output :storage size for int data type:4,  storage size for char data type:1 ,  storage size for float data type,:4, storage size for double data type : 8 ,Loop control statementsLoop control statements in C are used to perform looping operations until the given condition is true. Control comes out of the loop statements once condition becomes false.TYPES OF LOOP CONTROL STATEMENTS IN C:There are 3 types of loop control statements in C language. They are,

1.  for
2.  while
3.  do-while

THE FOR LOOPThe for loop allows us to specify three things about a loop in a single line.

*   Setting a loop counter to an initial value
*   Testing the loop counter to determine whether its value has reached the number of repetitions desired.
*   Increasing the value of loop counter each time the program segment within the loop has been executed.

Syntax :_for( initialise counter; test counter ; increment counter){Do this;And this;And this;}THE WHILE LOOPIt is often the case in programming that you want to do something a fixed number of times.Syntax :_  Initialise loop counter;While( test loop counter using a condition){Do this;And this;Increment loop counter;}The DO –WHILE LOOPIt is used to ensure that the statements within the loop are executed at least once.Syntax:_  Do{this;and this;and this;and this;} while( this condition is true); A)EXAMPLE PROGRAM (FOR LOOP) IN C:In for loop control statement, loop is executed until condition becomes false.#include <stdio.h>int main(){int i;for(i=0;i<10;i++){printf("%d ",i);}    }OUTPUT:

| 0 1 2 3 4 5 6 7 8 9 |
|  |

B)EXAMPLE PROGRAM (WHILE LOOP) IN C:In while loop control statement, loop is executed until condition becomes false.#include <stdio.h>int main(){int i=3;while(i<10){printf("%d\n",i);i++;}    }OUTPUT:

| 3 4 5 6 7 8 9 |

EXAMPLE PROGRAM (DO WHILE LOOP) IN C:In do..while loop control statement, while loop is executed irrespective of the condition for first time. Then 2 nd  time onwards, loop is executed until condition becomes false.C)#include <stdio.h>int main(){int i=1;do{  printf("Value of i is %d\n",i);i++;}while(i<=4 && i>=2);    }OUTPUT:

| Value of i is 1 Value of i is 2
Value of i is 3
Value of i is 4 |

Case control statementsThe statements which are used to execute only specific block of statements in a series of blocks are called case control statements.There are 4 types of case control statements in C language. They are,

1.  switch
2.  break
3.  continue
4.  goto

1.  SWITCH CASE STATEMENT IN C:

the control statement that allows us to make a decision from the number of choices is called a switch, or more correctly a switch case default, since these three keyword go together to make up the control statement.syntex :_switch ( integer expression){case constant 1;do this;case constant 2;do this;case constant 3;do this;default;do this;}1)EXAMPLE PROGRAM FOR SWITCH..CASE STATEMENT IN C:

| 12345678910111213141516171819202122232425262728 | #include <stdio.h>int main (){int value = 3;switch(value){case 1:printf(“Value is 1 \n” );break;case 2:printf(“Value is 2 \n” );break;case 3:printf(“Value is 3 \n” );break;case 4:printf(“Value is 4 \n” );break;default :printf(“Value is other than 1,2,3,4 \n” );}return 0;} |

OUTPUT:

| Value is 3 |

2.  BREAK STATEMENT IN C:

we often come across situation ehere we want to jump out of a loop instantly, without waiting to get back to the conditional test. the break allows us to do this. when break is encountered inside any loop, control automatically passes to the first statement after the loop. a break is usually associated with an if.2)EXAMPLE PROGRAM FOR BREAK STATEMENT IN C:

| #include <stdio.h>int main(){int i;for(i=0;i<10;i++){if(i==5){printf("\nComing out of for loop when i = 5");break;}printf("%d ",i);}} |

OUTPUT:

| 0 1 2 3 4 Coming out of for loop when i = 5 |

3.  CONTINUE STATEMENT IN C:

in some programming situation, we want to take the control to the beginning of the loop, bypassing the statements inside the loop, which have not yet been executed. the keyword continue allows us to do this. when continue is encountered inside any loop control automatically passes to the beginning of the loop.EXAMPLE PROGRAM FOR CONTINUE STATEMENT IN C:

| #include <stdio.h>int main(){int i;for(i=0;i<10;i++){if(i==5 &#124;&#124; i==6){printf("\nSkipping %d from display using " \"continue statement \n",i);continue;}printf("%d ",i);}} |

OUTPUT:

| 0 1 2 3 4Skipping 5 from display using continue statement Skipping 6 from display using continue statement
7 8 9 |

4. GOTO STATEMENT IN C:In a difficult programming situation, it seems so easy to use a goto to take the control where you want. However, almost always, there is a more elegant way of writing the same program using if. For, while, and switch. These constructs are far more logical and easy to understand.EXAMPLE PROGRAM FOR GOTO STATEMENT IN C:

| #include <stdio.h>int main(){int i;for(i=0;i<10;i++){if(i==5){printf("\nWe are using goto statement when i = 5");goto HAI;}printf("%d ",i);}HAI : printf("\nNow, we are inside label name \"hai\" \n");} |

OUTPUT:

| 0 1 2 3 4 We are using goto statement when i = 5
Now, we are inside label name “hai” |

Storage ClassA variable’s storage class tells us:A)   Where the variable would be stored.•                                             B) What will be the initial value of the variable, if initial value is not     specifically assigned( i.e the default initial value)•           •                                                    C)  What is the scope of the variable;i.e in which function the value of the variablrs would be available.•           D)  What is the life of the variable, i.e how long would the variable   exist.TYPES OF STORAGE CLASS SPECIFIERS IN C:There are 4 storage class specifies available in C language. They are,1)          Automatic storage class2)          Register   storage class3)          Static       storage   class4)          External   storage  classAutomatic storage class:Storage :_ memoryDefault initial value :_   an un predictable value, which is often called a garbage value.Scope :_             local to the block in which the variables is defined.Life  :_       till the control remains within the block in which the variable is defined.Register storage class:Storage:_ CPU registersDefault initial value :_ garbage valueScope:_ local to the block in which the variable is definedLife:_ till the control remains within the block in which the variable is defined.Static storage class:Storage:_ memoryDefault initial value :_ zeroScope:_ local to the block in which the variable is definedLife:_ value of the variables persists between different function calls.External storage class:Storage:- memoryDefault initial value :_  zeroScope:_ globalLife:- as long as the program’s execution does not come to an end.1.        EXAMPLE PROGRAM FOR AUTOmatic VARIABLE IN C:The scope of this auto variable is within the function only. It is equivalent to local variable. All local variables are auto variables by default.

| #include<stdio.h>void increment(void);int main(){increment();increment();increment();increment();return 0;}void increment(void){auto int i = 0 ;printf ( "%d ", i ) ;i++;} |

OUTPUT:

| 0 0 0 0 |

EXAMPLE PROGRAM FOR STATIC VARIABLE IN C:Static variables retain the value of the variable between different function calls.

| 1234567891011121314151617 | //C static example#include<stdio.h>void increment(void);int main(){increment();increment();increment();increment();return 0;}void increment(void){static int i = 0 ;printf ( "%d ", i ) ;i++;} |

OUTPUT:

| 0 1 2 3 |
|  |

EXAMPLE PROGRAM FOR EXTERNal VARIABLE IN C:The scope of this extern variable is throughout the main program. It is equivalent to global variable. Definition for extern variable might be anywhere in the C program.

| 1234567891011 | #include<stdio.h>int x = 10 ;int main( ){extern int y;printf("The value of x is %d \n",x);printf("The value of y is %d",y);return 0;}int y=50; |

OUTPUT:

| The value of x is 10 The value of y is 50 |

EXAMPLE PROGRAM FOR REGISTER VARIABLE IN C:

| 1234567891011121314151617 | #include <stdio.h>int main(){register int i;int arr[5];// declaring arrayarr[0] = 10;// Initializing arrayarr[1] = 20;arr[2] = 30;arr[3] = 40;arr[4] = 50;for (i=0;i<5;i++){// Accessing each variableprintf("value of arr[%d] is %d \n", i, arr[i]);}return 0;} |

OUTPUT:

| value of arr[0] is 10 value of arr[1] is 20
value of arr[2] is 30
value of arr[3] is 40
value of arr[4] is 50 |

Function,   C functions are basic building blocks in a program. All C programs are written using functions to improve re-usability, understand ability and to keep track on them. You can learn below concepts of C functions in this section in detail.1\. WHAT IS C FUNCTION?A large C program is divided into basic building blocks called C function. C function contains set of instructions enclosed by “{  }” which performs specific operation in a C program. Actually, Collection of these functions creates a C program.2\. USES OF C FUNCTIONS:

*   C functions are used to avoid rewriting same logic/code again and again in a program.
*   There is no limit in calling C functions to make use of same functionality wherever required.
*   We can call functions any number of times in a program and from any place in a program.
*   A large C program can easily be tracked when it is divided into functions.
*   The core concept of C functions are, re-usability, dividing a big task into small pieces to achieve the functionality and to improve understand ability of very large C programs.

3\. C FUNCTION DECLARATION, FUNCTION CALL AND FUNCTION DEFINITION:A)        a function gets called when the function name is followed by a semicolon . for exampleInt main (){Argentina();}B)        a function is defined when function name is followed by a pair of braces in which one or more statements may be present. for exampleVoid argentina(){Statements 1;Statements 2;Statements 3;}C)        any function can be called from any other function. even main() can be called from other function. for example#include<stdio.h>Void message()Int main (){Message();Return0;}Void message(){Printf(“\n can not imagine without c”);Main();}D)A function can be called any number of times. For example:#include<stdio.h>Void message(){Message();Message();Return0;}Void message(){Printf(“\n jewel thief”);}E)there are basically two types of functions;Library function :_ printf(), scanf(); etcUser-defined function :- argentina(), brazil(), etcSIMPLE EXAMPLE PROGRAM FOR C FUNCTION:

*   As you know, functions should be declared and defined before calling in a C program.
*   In the below program, function “square” is called from main function.
*   The value of “m” is passed as argument to the function “square”. This value is multiplied by itself in this function and multiplied value “p” is returned to main function from function “square”.

| #include<stdio.h>// function prototype, also called function declarationfloat square ( float x );                              // main function, program starts from hereint main( )              {float m, n ;printf ( "\nEnter some number for finding square \n");scanf ( "%f", &m ) ;// function calln = square ( m ) ;                      printf ( "\nSquare of the given number %f is %f",m,n );}float square ( float x )   // function definition{float p ;p = x * x ;return ( p ) ;} |

OUTPUT:

| Enter some number for finding square2Square of the given number 2.000000 is 4.000000 |

using library function:Example:-#include<stdio.h>#include<math.h>Int main(){Float a=0.5;Float  w, x y,z;W=sin(a);X=cos(a);Y=tan(a);Z=pow(a,2);Printf(“\n%f%f%f%f”,w,x,y,z);Return0;}advanced features of function:a)        Return type of functionb)        Calling function by value or by referencec)        RecursionReturn type of function:_#include<stdio.h>Float square (float);Int main(){Float a,b;Printf(“\n enter any number”);Scanf(“\n%f”,&a);B= square(a);Printf(“\n square of %f is %f”, a,b);Return 0;}Float square (float x){Float y;Y= x*x;Return(y);}Output:-Enter any number  3Square of 3 is 9.000000Enter any number 1\. 5Square of 1.5 is  2.250000Enter any number    2.5Square of 2.5 is 6.250000CALL BY VALUE:

*   In call by value method, the value of the variable is passed to the function as parameter.
*   The value of the actual parameter can not be modified by formal parameter.
*   Different Memory is allocated for both actual and formal parameters. Because, value of actual parameter is copied to formal parameter.

Note:

*   Actual parameter – This is the argument which is used in function call.
*   Formal parameter – This is the argument which is used in function definition

EXAMPLE PROGRAM FOR C FUNCTIONS (USING CALL BY VALUE):

*   In this program, the values of the variables “m” and “n” are passed to the function “swap”.
*   These values are copied to formal parameters “a” and “b” in swap function and used.

| #include<stdio.h>// function prototype, also called function declarationvoid swap(int a, int b);          int main(){int m = 22, n = 44;// calling swap function by valueprintf(" values before swap  m = %d \nand n = %d", m, n);swap(m, n);                        }void swap(int a, int b){int tmp;tmp = a;a = b;b = tmp;printf(" \nvalues after swap m = %d\n and n = %d", a, b);} |

OUTPUT:

| values before swap m = 22 and n = 44
values after swap m = 44
and n = 22 |

2\. CALL BY REFERENCE:

*   In call by reference method, the address of the variable is passed to the function as parameter.
*   The value of the actual parameter can be modified by formal parameter.
*   Same memory is used for both actual and formal parameters since only address is used by both parameters.

EXAMPLE PROGRAM FOR C FUNCTION (USING CALL BY REFERENCE):

*   In this program, the address of the variables “m” and “n” are passed to the function “swap”.
*   These values are not copied to formal parameters “a” and “b” in swap function.
*   Because, they are just holding the address of those variables.
*   This address is used to access and change the values of the variables.

| #include<stdio.h>// function prototype, also called function declarationvoid swap(int *a, int *b);int main(){int m = 22, n = 44;//  calling swap function by referenceprintf("values before swap m = %d \n and n = %d",m,n);swap(&m, &n);        }void swap(int *a, int *b){int tmp;tmp = *a;*a = *b;*b = tmp;printf("\n values after swap a = %d \nand b = %d", *a, *b);} |

OUTPUT:

| values before swap m = 22 and n = 44 values after swap a = 44
and b = 22 |

Recursion :In, c  it is possible for the functions to call themselves. A function is called recursive, if a statements within the body of a function calls the same function. Sometimes called circular definition, recursion is thus the process of  defining something in terms of itself.Following are the recursive version of the functions to calculate the factorial value.#include<stdio.h>Int rec (int){Int a,fact;Printf(“\ enter any value”};Scanf(“%d”,a);Fact=rec(a);Printf(“\n factorial value= %d”,fact);Return0;}Int rec (int x){Int f;If(x==1)Return(1);ElseF=x*rec(x-1);Return (f);}Output:Enter any number1Factorial value =1Enter any number 2Factorial value =2Enter any number 3Factorial value =3Enter any number 5Factorial value = 120Argument, return valueAll C functions can be called either with arguments or without arguments in a C program. These functions may or may not return values to the calling function. Now, we will see simple example C programs for each one of the below.

1.  C function with arguments (parameters) and with return value.
2.  C function with arguments (parameters) and without return value.
3.  C function without arguments (parameters) and without return value.
4.  C function without arguments (parameters) and with return value.

| C functions aspects | syntax |
| 1\. With arguments and with return values | function declaration: int function ( int );function call: function ( a );function definition:       
int function( int a )
{
statements;
return a;
} |
| 2\. With arguments and without return values | function declaration: void function ( int );function call: function( a );function definition:
void function( int a )
{
statements;
} |
| 3\. Without arguments and without return values | function declaration: void function();function call: function();function definition:
void function()
{
statements;
} |
| 4\. Without arguments and with return values | function declaration: int function ( );function call: function ( );function definition:
int function( )
{
statements;
return a;
} |

NOTE:

*   If the return data type of a function is “void”, then, it can’t return any values to the calling function.
*   If the return data type of the function is other than void such as “int, float, double etc”, then, it can return values to the calling function.

a)      EXAMPLE PROGRAM FOR WITH ARGUMENTS & WITH RETURN VALUE:In this program, integer, array and string are passed as arguments to the function. The return type of this function is “int” and value of the variable “a” is returned from the function. The values for array and string are modified inside the function itself.

| #include<stdio.h>#include<string.h>int function(int, int[], char[]);int main(){int i, a = 20;int arr[5] = {10,20,30,40,50};  char str[30] = "\"fresh2refresh\"";printf("    ***values before modification***\n");  printf("value of a is %d\n",a);  for (i=0;i<5;i++){// Accessing each variableprintf("value of arr[%d] is %d\n",i,arr[i]);  }printf("value of str is %s\n",str);printf("\n    ***values after modification***\n");a= function(a, &arr[0], &str[0]);printf("value of a is %d\n",a);  for (i=0;i<5;i++){// Accessing each variableprintf("value of arr[%d] is %d\n",i,arr[i]);  }printf("value of str is %s\n",str);return 0;}int function(int a, int *arr, char *str){int i;a = a+20;arr[0] = arr[0]+50;arr[1] = arr[1]+50;arr[2] = arr[2]+50;arr[3] = arr[3]+50;arr[4] = arr[4]+50;strcpy(str,"\"modified string\"");return a;} |

OUTPUT:

| ***values before modification*** value of a is 20
value of arr[0] is 10
value of arr[1] is 20
value of arr[2] is 30
value of arr[3] is 40
value of arr[4] is 50
value of str is “fresh2refresh”***values after modification***
value of a is 40
value of arr[0] is 60
value of arr[1] is 70
value of arr[2] is 80
value of arr[3] is 90
value of arr[4] is 100
value of str is “modified string” |

b)      EXAMPLE PROGRAM FOR WITH ARGUMENTS & WITHOUT RETURN VALUE:In this program, integer, array and string are passed as arguments to the function. The return type of this function is “void” and no values can be returned from the function. All the values of integer, array and string are manipulated and displayed inside the function itself.

| #include<stdio.h>void function(int, int[], char[]);int main(){int a = 20;int arr[5] = {10,20,30,40,50};  char str[30] = "\"fresh2refresh\"";function(a, &arr[0], &str[0]);return 0;}void function(int a, int *arr, char *str){int i;printf("value of a is %d\n\n",a);  for (i=0;i<5;i++){// Accessing each variableprintf("value of arr[%d] is %d\n",i,arr[i]);  }printf("\nvalue of str is %s\n",str);  } |

OUTPUT:

| value of a is 20value of arr[0] is 10 value of arr[1] is 20
value of arr[2] is 30
value of arr[3] is 40
value of arr[4] is 50value of str is “fresh2refresh” |

3\. EXAMPLE PROGRAM FOR WITHOUT ARGUMENTS & WITHOUT RETURN VALUE:In this program, no values are passed to the function “test” and no values are returned from this function to main function.

| #include<stdio.h>void test();          int main(){test();                        return 0;}void test()  {int a = 50, b = 80;  printf("\nvalues : a = %d and b = %d", a, b);} |

OUTPUT:

| values : a = 50 and b = 80 |

c)        EXAMPLE PROGRAM FOR WITHOUT ARGUMENTS & WITH RETURN VALUE:In this program, no arguments are passed to the function “sum”. But, values are returned from this function to main function. Values of the variable a and b are summed up in the function “sum” and the sum of these value is returned to the main function.

| #include<stdio.h>int sum();          int main(){int addition;addition = sum();                  printf("\nSum of two given values = %d", addition);return 0;}int sum()  {int a = 50, b = 80, sum;  sum = a + b;return sum;      } |

OUTPUT:

| Sum of two given values = 130 |

DO YOU KNOW HOW MANY VALUES CAN BE RETURN FROM C FUNCTIONS?

*   Always, Only one value can be returned from a function.
*   If you try to return more than one values from a function, only one value will be returned that appears at the right most place of the return statement.
*   For example, if you use “return a,b,c” in your function, value for c only will be returned and values a, b won’t be returned to the program.
*   In case, if you want to return more than one values, pointers can be used to directly change the values in address instead of returning those values to the function.

Library functions

*   Library functions in C language are inbuilt functions which are grouped together and placed in a common place called library.
*   Each library function in C performs specific operation.
*   We can make use of these library functions to get the pre-defined output instead of writing our own code to get those outputs.
*   These library functions are created by the persons who designed and created C compilers.
*   All C standard library functions are declared in many header files which are saved as file_name.h.
*   Actually, function declaration, definition for macros are given in all header files.
*   We are including these header files in our C program using “#include<file_name.h>” command to make use of the functions those are declared in the header files.
*   When we include header files in our C program using “#include<filename.h>” command, all C code of the header files are included in C program. Then, this C program is compiled by compiler and executed.

*   If you want to check source code for all header files, you can check inside “include” directory after C compiler is installed in your machine.
*   For example, if you install DevC++ compiler in C directory in your machine, “C:\Dev-Cpp\include” is the path where all header files will be available.

LIST OF MOST USED HEADER FILES IN C PROGRAMMING LANGUAGE:

| Header file | Description |
| stdio.h | This is standard input/output header file in which Input/Output functions are declared |
| conio.h | This is console input/output header file |
| string.h | All string related functions are defined in this header file |
| stdlib.h | This header file contains general functions used in C programs |
| math.h | All maths related functions are defined in this header file |
| time.h | This header file contains time and clock related functions |
| ctype.h | All character handling functions are defined in this header file |
| stdarg.h | Variable argument functions are declared in this header file |
| signal.h | Signal handling functions are declared in this file |
| setjmp.h | This file contains all jump functions |
| locale.h | This file contains locale functions |
| errno.h | Error handling functions are given in this file |
| assert.h | This contains diagnostics functions |

Creating library functionsSER DEFINED FUNCTIONS IN C:As you know, there are 2 types of functions in C. They are, library functions and user defined functions

*   Library functions are inbuilt functions which are available in common place called C library. Where as, User defined functions are the functions which are written by us for our own requirement.

ADDING USER DEFINED FUNCTIONS IN C LIBRARY:

*   Do you know that we can add our own user defined functions in C library?
*   Yes. It is possible to add, delete, modify and access our own user defined function to or from C library.
*   The advantage of adding user defined function in C library is, this function will be available for all C programs once added to the C library.
*   We can use this function in any C program as we use other C library functions.
*   In latest version of GCC compilers, compilation time can be saved since these functions are available in library in the compiled form.
*   Normal header files are saved as “file_name.h” in which all library functions are available. These header files contain source code and this source code is added in main C program file where we add this header file using “#include <file_name.h>” command.
*   Where as, precompiled version of header files are saved as “file_name.gch”.

| # include <stdio.h>// Including our user defined function.# include “c:\\addition.h”    int main (){int total;// calling function from librarytotal = addition (10, 20);printf ("Total = %d \n", total);} |

OUTPUT:

| Total = 30 |

Command line argumentsWhere,Argc=5                 
argv[0]    =”test   “         
argv[1]      =”this  “       
argv[2]      =”is  “     
argv[3]       =”a “
argv[4]        =”program”
argv[5]         =     “  Null”EXAMPLE PROGRAM FOR ARGC() AND ARGV() FUNCTIONS IN C:

| #include <stdio.h>#include <stdlib.h>int main(int argc, char *argv[])   //  command line arguments{if(argc!=5){printf("Arguments passed through command line " \"not equal to 5");return 1;}printf("\n Program name  : %s \n", argv[0]);printf("1st arg  : %s \n", argv[1]);printf("2nd arg  : %s \n", argv[2]);printf("3rd arg  : %s \n", argv[3]);printf("4th arg  : %s \n", argv[4]);printf("5th arg  : %s \n", argv[5]);return 0;} |

OUTPUT:

| Program name : test 1st arg : this
2nd arg : is
3rd arg : a
4th arg : program
5th arg : (null) |

Variable length argument

*   Variable length arguments is an advanced concept in C language offered by c99 standard. In c89 standard, fixed arguments only can be passed to the functions.
*   When a function gets number of arguments that changes at run time, we can go for variable length arguments.
*   It is denoted as … (3 dots)
*   stdarg.h header file should be included to make use of variable length argument functions.

EXAMPLE PROGRAM FOR VARIABLE LENGTH ARGUMENTS IN C:

| 12345678910111213141516171819202122232425262728293031323334353637 | #include <stdio.h>#include <stdarg.h>int add(int num,...);int main(){printf("The value from first function call = " \"%d\n", add(2,2,3));printf("The value from second function call= " \"%d \n", add(4,2,3,4,5));/*Note - In function add(2,2,3),first 2 is total number of arguments2,3 are variable length argumentsIn function add(4,2,3,4,5),4 is total number of arguments2,3,4,5 are variable length arguments*/return 0;}int add(int num,...){va_list valist;int sum = 0;int i;va_start(valist, num);for (i = 0; i < num; i++){sum += va_arg(valist, int);}va_end(valist);return sum;} |

OUTPUT:

| The value from first function call = 5 The value from second function call= 14 |

In the above program, function “add” is called twice. But, number of arguments passed to the function gets varies for each. So, 3 dots (…) are mentioned for function ‘add” that indicates that this function will get any number of arguments at run time.PointerPointers in C language is a variable that stores/points the address of another variable. A Pointer in C is used to allocate memory dynamically i.e. at run time. The pointer variable might be belonging to any of the data type such as int, float, char, double, short etc.

*   Pointer Syntax : data_type *var_name; Example : int *p;  char *p;

*   Where, * is used to denote that “p” is pointer variable and not a normal variable.

KEY POINTS TO REMEMBER ABOUT POINTERS IN C:

*   Normal variable stores the value whereas pointer variable stores the address of the variable.

*   The content of the C pointer always be a whole number i.e. address.
*   Always C pointer is initialized to null, i.e. int *p = null.
*   The value of null pointer is 0.

*   & symbol is used to get the address of the variable.
*   * symbol is used to get the value of the variable that the pointer is pointing to.
*   If a pointer in C is assigned to NULL, it means it is pointing to nothing.
*   Two pointers can be subtracted to know how many elements are available between these two pointers.

*   But, Pointer addition, multiplication, division are not allowed.
*   The size of any pointer is 2 byte (for 16 bit compiler).

EXAMPLE PROGRAM FOR POINTERS IN C:

| 1234567891011 | #include <stdio.h>int main(){int *ptr, q;q = 50;/* address of q is assigned to ptr */ptr = &q;/* display q's value using ptr variable */printf("%d", *ptr);return 0;} |

OUTPUT:

| 50 |

Thus the following operations can be performed on a pointer:_a)       Addition of a number to a pointerInt i=4,j,k;J=&i;J=j+1;J=j+9;K=j+3;b)       Subtraction of a number from a pointer:-c)Subtraction of one pointer from another:-#include<stdio.h>Int main(){Int arr[ []= { 10,20,30,45,67,56,74}Int * i*,j;I=&arr[1];J=&arr[5];Printf(“\n %d%d”,j-i,*j-i*);Return 0;}d)comparison of two pointer variables:_#include<stdio.h>Int main(){Int arr[]= {10,20,36,72,45,36};Int *j,*k;J=&arr[4];K=(arr+4);If(j==k)Printf(“\n the two pointer point to the same location”);ElsePrintf(“\n the two pointer  do not point to the same location”0;Return 0;}ArrayC Array is a collection of variables belongings to the same data type. You can store group of data of same data type in an array.example of array#include<stdio.h>Int main (){Int x;X=5;X=10;Printf(“\n%d =x”,x);Return 0;}A)Array declaration:-Int marks [30]B)Entering data into  an array :-for(i=0;i<=29;i++){Printf(“\n enter marks”);Scanf(“%d”,&marks[i]);}C)Reading data from an array:-For(i=0;i<=29;i++)Sum=sum+marks[i]);Avg=sum/30;Printf(“\n average marks =%d”, avg);D)Array initialisation:_    Int num[6]={2,4,12,6,45,5,};Int n[]={ 2,4,12,5;45,};Float press[]={12.3,34.2,-23.4,-11.3};E)Bounds checking:_  in c, there is no check to see if the sub-script used for an array exceeds the size of the array.#include<stdio.h>Int main(){Int num [40],i;For(i=0;i<=100;++i)Num[i]=iReturn 0;}We have learnt about arrays:_a)       An array is a collection of similar elementsb)      The first element in the array is numbered 0, so the last element is 1 less than the size of the array.c)        An array is also known as a sub –scripted variable.d)       Before using an array, its type and dimension must be declared.e)      However big an array, its element are always stored in contiguous memory locations.TYPES OF C ARRAYS:There are 2 types of C arrays. They are,

1.  One dimensional array
2.  Multi dimensional array
    *   Two dimensional array
    *   Three dimensional array
    *   four dimensional array etc…

1\. ONE DIMENSIONAL ARRAY IN C:Syntax : data-type arr_name[array_size];

|  |  |
|  |  |

EXAMPLE PROGRAM FOR ONE DIMENSIONAL ARRAY IN C:

| #include<stdio.h>int main(){int i;int arr[5] = {10,20,30,40,50};// declaring and Initializing array in C//To initialize all array elements to 0, use int arr[5]={0};/* Above array can be initialized as below alsoarr[0] = 10;arr[1] = 20;arr[2] = 30;arr[3] = 40;arr[4] = 50; */for (i=0;i<5;i++){// Accessing each variableprintf("value of arr[%d] is %d \n", i, arr[i]);}} |

OUTPUT:

| value of arr[0] is 10value of arr[1] is 20value of arr[2] is 30value of arr[3] is 40value of arr[4] is 50 |

2. TWO DIMENSIONAL ARRAY IN C:

*   syntax : data_type array_name[num_of_rows][num_of_column];

EXAMPLE PROGRAM FOR TWO DIMENSIONAL ARRAY IN C:

| 123456789101112131415161718192021 | #include<stdio.h>int main(){int i,j;// declaring and Initializing arrayint arr[2][2] = {10,20,30,40};/* Above array can be initialized as below alsoarr[0][0] = 10; // Initializing arrayarr[0][1] = 20;arr[1][0] = 30;arr[1][1] = 40; */for (i=0;i<2;i++){for (j=0;j<2;j++){// Accessing variablesprintf("value of arr[%d] [%d] : %d\n",i,j,arr[i][j]);}}} |

OUTPUT:

| value of arr[0] [0] is 10value of arr[0] [1] is 20value of arr[1] [0] is 30value of arr[1] [1] is 40 |

StringWhat are string?The way a group of integers can be  stored in an integer array, similarly a group of characters can be stored in a character array. Character arrys are many a time also called string.
A string constant is a one-dimensional array of characters terminated by a null('\0'). for example char name()= {'h',a','e','l','r','\0',}.
note:- The terminating null ('\0') is important, because it is the only way the function that work with a string can know where the  string ends.in fact by a '\0' is not really a string but merely a collection of character.
EXAMPLE PROGRAM FOR C STRING:

| #include <stdio.h>int main (){char string[] = “klinsman;int i=0;while (i<=7){Printf(“\n”%c”,name[i]);I++}Printf(“\n”);return 0;} |

OUTPUT:

| The string is : klinsman |

the %s used in printf() is a format specification for printing out a string. the same specification can be used to receive a string feom the keyword, as shown below# include<stdio.h>int name(){char name[25];printf(”\n enter your name”);scanf(“%s”,name);printf(“ hello  %s !\n”, name);return 0;}Out putEnter your name  DebnathHello DebnathNote :-     while entering the string using scanf() ,we must be cautious about two things.A)       The length of the string should  not exceed the dimension of the character array. This is because  the c compiler does not perform bounds checking on character arrays.B)       Scanf() is not capable of receiving multi word strings. Therefore, names such as  ‘Debnath’ would be un-acceptable. The way to get around this limition is by using the function ‘gets()’.The usage of functions  gets() and its counterpart   puts() is shown below#include <stdio.h>int main (){Char name[25];Printf(”\n enter your full name “);Gets( name);Puts(“hello”);Puts(name)Return 0;}Output                    Enter your full name    Deb nath RoyHello !Debnath RoyPointers to stringsWhereas we can assign  a char pointer to another char pointerExample:-#include<stdio.h>int main(){char str[]= “hello”;char str2[10];char *s=”good morning”;char *2;str2=str1;/*error*\q=s;/*works*/return 0;}Standard library string functionWith every c compiler, a large set of useful string handling  library function are provided. Lists the more commonly used function along with their purpose.Function                                                                       use                                                                Strlen​ ​ finds length of a string​ ​                                                                                                                                                                                                                                                                                        Strlwr                                                                        converts a string to lowercaseStrupr​ ​ converting a string to uppercaseStrcat                                                                          appends one string at the end of anotherStrcpy                                                                        copies a string into anotherStrcmp                                                                        compares two strings            Strrv                                                                           reverses string                                       ​                                                                                                                                                                                       .......................................................................................................................................................................................................                           strcat() functionThis function concatenates the source string at the end of the target string. For , exampleEXAMPLE PROGRAM FOR STRCAT() FUNCTION IN C:

| #include <stdio.h>#include <string.h>int main( ){char source[ ] = " fresh2refresh" ;char target[ ]= " C tutorial" ;printf ( "\nSource string = %s", source ) ;printf ( "\nTarget string = %s", target ) ;strcat ( target, source ) ;printf ( "\nTarget string after strcat( ) = %s", target ) ;} |

OUTPUT:

| Source string                       = fresh2refresh Target string                        = C tutorial
Target string after strcat( ) = C tutorial fresh2refresh |

:strcmp() functionThis is a function which compares two strings to find out whether they are same or different. The two strings are compared character by character until there is a mis match or end of one of the strings is reached, whichever occurs first. If the two strings are identical, strcmp() returns a value zero. If they are not, it returns the numeric difference between the ASCII values of the first non-matching pair of character.EXAMPLE PROGRAM FOR STRNCAT( ) FUNCTION IN C:

| #include <stdio.h>#include <string.h>int main( ){char string 1[ ] = " jerry”;char string 2[ ]= "ferry" ;int i,j,k;i= strcmp(string1,”jerry”);j= strcmp(string 1,string2);k=strcmp(string 1,”jerry boy”);printf(“\n %d %d %d \n,” i,j,k);return 0;} |

OUTPUT:

| 04-32 |

strcpy() functionThis function copies the contents of one string into another. The base addresses of the source and target strings should be supplied to this functionEXAMPLE PROGRAM FOR STRCPY( ) FUNCTION IN C:

| #include <stdio.h>#include <string.h>int main( ){char source[ ] = " sayonara" ;char target[20];strcpy(target,source);printf ( "\nsource string = %s", source ) ;printf ( "\ntarget string = %s", target ) ;printf ( "\ntarget string after strcpy( ) = %s", target ) ;return 0;} |

OUTPUT:

| source string = sayonara target string = sayonara
  |

strlen() functionThis function counts the number of characters present in a string.EXAMPLE PROGRAM FOR STRLEN() FUNCTION IN C:

| #include <stdio.h>#include <string.h>int main( ){char arr[]=”bamboozled”,int  len1, len2;len1=strlen(arr);len2=strlen(“humpty dumpty”);printf(“\n string=%s length=%d\n”,arr, len1);printf(“\n string=%s length=%d\n”, humpty dumpty”,len2);return 0;} |

OUTPUT:

| String= bamboozled length=10String=humpty dumpty length=13 |

StructureC Structure is a collection of different data types which are grouped together and each element in a C structure is called member.

*   If you want to access structure members in C, structure variable should be declared.
*   Many structure variables can be declared for same structure and memory will be allocated for each separately.
*   It is a best practice to initialize a structure to null while declaring, if we don’t assign any values to structure members.

DIFFERENCE BETWEEN C VARIABLE, C ARRAY AND C STRUCTURE:

*   A normal C variable can hold only one data of one data type at a time.
*   An array can hold group of data of same data type.
*   A structure can hold group of data of different data types and Data types can be int, char, float, double and long double etc.

C Structure:

| Syntax | struct student {
int a;
char b[10];
} |
| Example | a = 10; b = “Hello”; |

C Variable:

| int | Syntax: int a; Example: a = 20; |
| char | Syntax: char b; Example: b=’Z’; |

C Array:

| int | Syntax: int a[3]; Example:
a[0] = 10;
a[1] = 20;
a[2] = 30;
a[3] = ‘\0’; |
| char | Syntax: char b[10]; Example:
b=”Hello”; |

a)Declaring a structure:-ExampleStruct book{Char name;Float price;Int pages;}Note :_while declaring a structure typea)      The closing brace in the structure type declaration must be followed by a semicolon.b)      It is important to understand that a structure type declaration does not tell the compiler to reserve any space in memory. all a structure declaration does is, it defines the form of the structure.c)       Usually structure type declaration appears at the top of the source code file, before any variables or functions are defined.d)      If a structure variables  is initiated to a value {0}, then all its elements are set to value 0,. This is a handy way of initializing structure variables.B)      Accessing structure elements:Having declared the structure type and the structure variables, let us see how the elements of the structure can be accessed.They use a dot (.) operator. So to refer pages of the structure defined in our sample program, we have to useB1.pagesSimilarly, to refer to price, we would useB1.pricec)how structure elements are stored:_example#include<stdio.h>Int main(){Struct book{Char name;Float price;Int pages;};Struck book b1={‘B’,130.00,550];Printf(“\n address of name=%u”,&b1.name);Printf(“\n address of price =%u”, & b1.price);Printf(“\n address of pages =%u”,&b1.pages);Return 0;}OutputAddress of name =65518Address of price=65519Address of pages =65523The structure elements are stored in memory as shown in belowB1.name​ ​ b1.price ​ ​ b1.pages‘b’ ​ ​ 130.00​ ​    55065518​ ​ 65519​ ​ 65523Array of structureExample#include<stdio.h>void link float();int main (){struct book{char name;float price;int pages;};struct book b[100];int i;for(i=0;i<=99;i++){printf (“\n enter names, price, and pages”);fflush(stdin);scanf(“ %c%f%d”,&b[i].name,&b[i].price,&b[i].pages);}for(i=0;i<=99;i++)printf(“\n %C%f%d”,b[i].name;b[i].price,b[i].pages);return 0;}void link float(){float a=0,*b;b=&a;a=*b}Note:- a) how the array of structures is declaredStruct book b[100];These provides space in memory for 100 structures of the types struct book.b)The syntax we use to reference each element of the array b is similar to the syntax used for arrays of ints and chars.c) Even using structures, programming convenience could not be achieved, because a lot of variables(b1 to b100 foe storing data about hundred books) needed to be handled. Therefore he allowed us to to create an array of structure.d)In an array of structures, all elements of the array are stored in adjacent memory locations.e) What is the function linkfloat() doing here?It forces linking of the floating-point emulator into an application. There is no need to call this function, just define it anywhere in your program.Additional feature of structure:_➢       The value of a structure variables can be assigned to another structure variables of the same type using assignment operators.A)Assignment operators to piece-meal copeing#include<stdio.h>#include<string.h>int main(){struct employee{char name[10];int age;float salary;};struct employee e1={“sanjay”,30,5500.50};struct employee  e2=,e3;/*Piece-meal copeing*/strcpy(e2.name,e1.name);    /*e2.name=e1.name is wrong*/e2.age=e1.age;e2\. salary=e1.salary;/*copy all elements at one go*/e3=e2;printf(“\n %s %d %f”, e1.name,e1.age,e1.salary);printf(“\n %s %d %f “, e2.name,e2.age,e2.salary);printf(“\n %s %d %f “, e3.name,e3.age,e3.salary);return 0;}OutputSanjay 305500.500000Sanjay 305500.500000Sanjay 305500.500000b)Nested structure#include<stdio.h>int main(){struct address{char phone[15];char city[25];Int pin;};struct emp{char name[25];struct address a;};struct emp e= {“jeru”, “5311046”,”nagpur”,10);printf(“name=%s phone=%s \n”,e.name,e.a.phone);printf(“\n city=%s pin=%d\n”,e.a.city,e.a.pin);return 0;}OutputName=jeru phone=531046City=Nagpur pin =10c) structure variables passed to a function#include<stdio.h>void display( char*,char*,int);int main(){struct book{char name[25];char author[25];Int callno;};struct book b1=(“let us c”, “YPK”,101); display(“\nb1.name.b1.author,b1.callno);return 0;}void display( char*s, char*t,int n){printf(“%s %s %d \n”, s, t, n);}OutputLet us C YPK 101d)     Pointer to function#include<stdio.h>struct emp{int a;char ch;float s;};int main(){struct emp e;printf(“\n %u %u %u \n “, &e.h,&e.ch,&e.s);return 0;}OutputUsing TC/TC++ compiler we get the address as:65518       65520       65521Using Visual stdio compiler then the output turns to be:1242044            1245048             1245052printf and scanfa)     printf() :_printf() can not only print values of variables, it can also print the result of an expression. An expression is nothing but a valid combination of constant, variables and operators. Thus , 3, 3+2, c and a+b*c-d all are valid expression. The result of these expression can be printed as shown below.Printf(“\n %d%d%d%d”, 3,3+2,c,a+b*c-d);A) EXAMPLE PROGRAM FOR C PRINTF() FUNCTION:

| 1234567891011121314151617 | #include <stdio.h>int main(){char ch = 'A';char str[20] =   float flt = 10.234;int no = 150;double dbl = 20.123456;printf("Character is %c \n", ch);printf("String is %s \n" , str);printf("Float value is %f \n", flt);printf("Integer value is %d\n" , no);printf("Double value is %lf \n", dbl);printf("Octal value is %o \n", no);printf("Hexadecimal value is %x \n", no);return 0;} |

OUTPUT:

| Character is A Float value is 10.234000
Integer value is 150
Double value is 20.123456
Octal value is 226
Hexadecimal value is 96 |

You can see the output with the same data which are placed within the double quotes of printf statement in the program exceptb)     Scanf ():_To make the program general, the program itself should ask the user to supply the values of p, n, r, through the keyboard during execution. This can be achived using a function called scanf()B)EXAMPLE PROGRAM FOR C PRINTF AND SCANF FUNCTIONS IN C PROGRAMMING LANGUAGE:

| 123456789101112 | #include <stdio.h>int main(){char ch;char str[100];printf("Enter any character \n");scanf("%c", &ch);printf("Entered character is %c \n", ch);printf("Enter any string ( upto 100 character ) \n");scanf("%s", &str);printf("Entered string is %s \n", str);} |

OUTPUT :   

| Enter any character a
Entered character is a
Enter any string ( upto 100 character )
hai
Entered string is hai |

Note :_

*   The format specifier %d is used in scanf() statement. So that, the value entered is received as an integer and %s for string.
*   Ampersand is used before variable name “ch” in scanf() statement as &ch.
*   It is just like in a pointer which is used to point to the variable. For more information about how pointer works,
*   printf() is used to display the output and scanf() is used to read the inputs.

1.  printf() and scanf() functions are declared in “stdio.h” header file in C library.

2.  All syntax in C language including printf() and scanf() functions are case sensitive

Preprocessor directivesC PREPROCESSOR DIRECTIVES:

*   Before a C program is compiled in a compiler, source code is processed by a program called preprocessor. This process is called preprocessing.
*   Commands used in preprocessor are called preprocessor directives and they begin with “#” symbol.

| Features of c pre-processor:a )macro expansionb)file inclusionc)conditional compilationd)miscellaneous directive |  |
|  |  |
|  |  |

There are 4 regions of memory which are created by a compiled C program. They are,

1.  First region  – This is the memory region which holds the executable code of the program.

2.  2 nd  region   – In this memory region, global variables are stored.

3.  3 rd region    – stack

4.  4 th region    – heap

DO YOU KNOW DIFFERENCE BETWEEN STACK & HEAP MEMORY IN C LANGUAGE?

| Stack | Heap |
| Stack is a memory region where “local variables”, “return addresses of function calls” and “arguments to functions” are hold while C program is executed. | Heap is a memory region which is used by dynamic memory allocation functions at run time. |
| CPU’s current state is saved in stack memory | Linked list is an example which uses heap memory. |

DO YOU KNOW DIFFERENCE BETWEEN COMPILERS VS INTERPRETERS IN C LANGUAGE?

| Compilers | Interpreters |
| Compiler reads the entire source code of the program and converts it into binary code. This process is called compilation.Binary code is also referred as machine code, executable, and object code. | Interpreter reads the program source code one line at a time and executing that line. This process is called interpretation. |
| Program speed is fast. | Program speed is slow. |
| One time execution. Example: C, C++ | Interpretation occurs at every line of the program. Example: BASIC |

macro expansion:examplee:#include<stdio.h># define upper 25int main((){int i;for(i=1;i<=UPPER;i++)printf(“%d\n”);return 0;}# define upper 25This statement is called macro definition or more commonly, just a macro’, what purpose does it serve? during preprocessing replaces every occurrence of UPPER in the program with 25.macros with arguments:the macros that we have used so far are called simple macros. macros can have arguments, just as functioncan. here is an example#include<stdio.h>#define AREA(x) (3.14*x*x)int main(){float ri =6025,r2=2.5,a;a=AREA(r1);printf(“AREA of circle=%f\n”,a);a=AREA(r2);printf(“ AREA of circle=%f\n”,a);return 0;]OUTPUT:Area of circle=1220656250Area of circle= 19.625000NOTE:A) Be careful not to leave a blank between the macro template and its argument while definning the macroexample: there should be no blank between area and (x) in the definition ,#define AREA(x) (3.14*x*x)b ) The entire macro expansion should be enclosed within parentheses.C)Macros can be split into multiple lines, with a ‘\’(back slash) present at the end of each line.D)If for any reason, you are unable to debug a macro, then you should view the expanded code of the program to see how the macros are getting expanded.FILE INCLUSIONthe second preprocessor directive we will explore in this chapter is file inclusion. this directives causes one file to be included in another.#include”filename”when and why this feature is used? it can be used in two cases:A) It is a good programming practice to keep diffrent sections of a large program separate. these files are #includedat the beginningof main program file.b) There are some functionsand some macro definitions that we need almost in all programs that we write.these commonly needed functions and macro definitions can be stored in a file,and that can be included in every program we write.C) When creating our own library of functions which we wish to distribute to others. in this situation the functions are defined in a” .c” file and their corresponding prototype declarations and macros are declared in a “.h” fileConditional CompilationEXAMPLE PROGRAM FOR #DEFINE, #INCLUDE PREPROCESSORS IN C LANGUAGE:

*   #define  –  This macro defines constant value and can be any of the basic data types.
*   #include <file_name>  –  The source code of the file “file_name” is included in the main C program where “#include <file_name>” is mentioned.

| #include <stdio.h>#define height 100#define number 3.14#define letter 'A'#define letter_sequence "ABC"#define backslash_char '\?'void main(){printf("value of height    : %d \n", height );printf("value of number : %f \n", number );printf("value of letter : %c \n", letter );printf("value of letter_sequence : %s \n", letter_sequence);printf("value of backslash_char  : %c \n", backslash_char);} |

OUTPUT:

| value of height : 100value of number : 3.140000value of letter : Avalue of letter_sequence : ABCvalue of backslash_char : ? |

EXAMPLE PROGRAM FOR CONDITIONAL COMPILATION DIRECTIVES:A) EXAMPLE PROGRAM FOR #IFDEF, #ELSE AND #ENDIF IN C:

*   “#ifdef” directive checks whether particular macro is defined or not. If it is defined, “If” clause statements are included in source file.
*   Otherwise, “else” clause statements are included in source file for compilation and execution.

| #include <stdio.h>#define RAJU 100int main(){#ifdef RAJUprintf("RAJU is defined. So, this line will be added in " \"this C file\n");#elseprintf("RAJU is not defined\n");#endifreturn 0;} |

OUTPUT:

| RAJU is defined. So, this line will be added in this C file |

EXAMPLE PROGRAM FOR #IFNDEF AND #ENDIF IN C:

*   #ifndef exactly acts as reverse as #ifdef directive. If particular macro is not defined, “If” clause statements are included in source file.
*   Otherwise, else clause statements are included in source file for compilation and execution.

| #include <stdio.h>#define ROHIT 100int main(){#ifndef SELVA{printf("SELVA is not defined. So, now we are going to " \"define here\n");#define SELVA 300}#elseprintf("SELVA is already defined in the program”);#endifreturn 0;} |

OUTPUT:

| SELVA is not defined. So, now we are going to define here |

EXAMPLE PROGRAM FOR #IF, #ELSE AND #ENDIF IN C:

*   “If” clause statement is included in source file if given condition is true.
*   Otherwise, else clause statement is included in source file for compilation and execution.

| 12345678910111213 | #include <stdio.h>#define a 100int main(){#if (a==100)printf("This line will be added in this C file since " \"a \= 100\n");#elseprintf("This line will be added in this C file since " \"a is not equal to 100\n");#endifreturn 0;} |

OUTPUT:

| This line will be added in this C file since a = 100 |

Miscellaneous Directive:A)# undefb)#pragma#undef directives:On some occasions, it may be desirable to cause a defined name to become ‘undefined’.This can be accomplished bt means of the #undef directive. In orther to define a macro that has been earlier #defined, the directive,EXAMPLE PROGRAM FOR UNDEF IN C LANGUAGE:This directive undefines existing macro in the program.

| 12345678910 | #include <stdio.h>#define height 100void main(){printf("First defined value for height    : %d\n",height);#undef height          // undefining variable#define height 600     // redefining the same for new valueprintf("value of height after undef \& redefine:%d",height);} |

OUTPUT:

| First defined value for height : 100value of height after undef & redefine : 600 |

#pragma directive:This directive is another special purpose directive that you can use to turn on  or off certain features.Pragmas vary from one compiler to another.a)#pragma startup and #pragma exit:These directives allow us to specify functions that are called upon program startup ( before main()  )     or   program exit ( just before the program terminates).B) #pragma warn:on compilation the compiler reports errors and warning in the programEXAMPLE PROGRAM FOR PRAGMA IN C LANGUAGE:Pragma is used to call a function before and after main function in a C program.

| 123456789101112131415161718192021222324 | #include <stdio.h>void function1( );void function2( );#pragma startup function1#pragma exit function2int main( ){printf ( "\n Now we are in main function" ) ;return 0;}void function1( ){printf("\nFunction1 is called before main function call");}void function2( ){printf ( "\nFunction2 is called just before end of " \"main function" ) ;"} |

OUTPUT:

| Function1 is called before main function callNow we are in main functionFunction2 is called just before end of main function |

File HandlingWHAT IS FILE?File is a collection of bytes that is stored on secondary storage devices like disk. There are two kinds of files in a system. They are,

1.  Text files (ASCII)
2.  Binary files

*   Text files contain ASCII codes of digits, alphabetic and symbols.
*   Binary file contains collection of bytes (0’s and 1’s). Binary files are compiled version of text files .

BASIC FILE OPERATIONS IN C PROGRAMMING:There are 4 basic operations that can be performed on any files in C programming language. They are,

1.  Opening/Creating a file
2.  Closing a file
3.  Reading a file
4.  Writing in a file

MODE OF OPERATIONS PERFORMED ON A FILE IN C LANGUAGE:There are many modes in opening a file. Based on the mode of file, it can be opened for reading or writing or appending the texts. They are listed below.EXAMPLE PROGRAM FOR FILE OPEN, FILE WRITE AND FILE CLOSE IN C LANGUAGE:

| 789101112131415161718192021222324252627282930 | / * Open, write and close a file : */# include <stdio.h># include <string.h>int main( ){FILE *fp ;char data[50];// opening an existing fileprintf( "Opening the file test.c in write mode" ) ;fp = fopen("test.c", "w") ;if ( fp == NULL ){printf( "Could not open file test.c" ) ;return 1;}printf( "\n Enter some text from keyboard” \“ to write in the file test.c" ) ;// getting input from userwhile ( strlen ( gets( data ) ) > 0 ){// writing in the filefputs(data, fp) ;  fputs("\n", fp) ;}// closing the fileprintf("Closing the file test.c") ;fclose(fp) ;return 0;        } |

OUTPUT:

| Opening the file test.c in write modeEnter some text from keyboard to write in the file test.c Hai, How are you?
Closing the file test.c |

EXAMPLE PROGRAM FOR FILE OPEN, FILE READ AND FILE CLOSE IN C LANGUAGE:This file handling C program illustrates how to read the contents of a file. Assume that, a file called “test.c” contains the following data “Hai, How are you?”. Let’s read this data using following C program .

| 123456789101112131415161718192021 | /* Open, Read and close a file: reading string by string */# include <stdio.h>int main( ){FILE *fp ;char data[50] ;printf( "Opening the file test.c in read mode" ) ;fp = fopen( "test.c", "r" ) ;if ( fp == NULL ){printf( "Could not open file test.c" ) ;return 1;}printf( "Reading the file test.c" ) ;while( fgets ( data, 50, fp ) != NULL )printf( "%s" , data ) ;printf("Closing the file test.c") ;fclose(fp) ;return 0;} |

OUTPUT:

| Opening the file test.c in read modeReading the file test.cHai, How are you?Closing the file test.c |

EXAMPLE PROGRAM FOR FOPEN(), FCLOSE(), GETS() AND FPUTS() FUNCTIONS IN C PROGRAMMING LANGUAGE:

| 123456789101112131415161718192021222324252627282930 | / * Open, write and close a file : */# include <stdio.h># include <string.h>int main( ){FILE *fp ;char data[50];// opening an existing fileprintf( "Opening the file test.c in write mode" ) ;fp = fopen("test.c", "w") ;if ( fp == NULL ){printf( "Could not open file test.c" ) ;return 1;}printf( "\n Enter some text from keyboard” \“ to write in the file test.c" ) ;// getting input from userwhile ( strlen ( gets( data ) ) > 0 ){// writing in the filefputs(data, fp) ;  fputs("\n", fp) ;}// closing the fileprintf("Closing the file test.c") ;fclose(fp) ;return 0;        } |

OUTPUT:

| Opening the file test.c in write modeEnter some text from keyboard to write in the file test.c Hai, How are you?
Closing the file test.c |

EXAMPLE PROGRAM FOR PUTW(), GETW() FUNCTION IN C PROGRAMMING LANGUAGE:This file handling C program illustrates how to write into a file using putw() function and how to read the same file using getw() function.

| 1234567891011121314151617181920212223 | #include <stdio.h>int main (){FILE *fp;int i=1, j=2, k=3, num;fp = fopen ("test.c","w");putw(i,fp);putw(j,fp);putw(k,fp);fclose(fp);fp = fopen ("test.c","r");while(getw(fp)!=EOF){num= getw(fp);printf(“Data in test.c file is %d \n”, num);}fclose(fp);return 0;} |

OUTPUT:

| Data in test.c file is 1
2
3 |

EXAMPLE PROGRAM FOR FGETC() FUNCTION IN C PROGRAMMING LANGUAGE:This file handling C program illustrates how to read the contents of a file. Assume that, a file called “test.c” contains the following data “Hi, How are you?”. Let’s read this data using following C program using fgetc() function .

| 1234567891011121314151617181920212223242526 | /* Open, Read and close a file: Reading char by char */# include <stdio.h>int main( ){FILE *fp ;char c ;printf( "Opening the file test.c in read mode" ) ;fp = fopen ( "test.c", "r" ) ; // opening an existing fileif ( fp == NULL ){printf ( "Could not open file test.c" ) ;return 1;}printf( "Reading the file test.c" ) ;while ( 1 ){c = fgetc ( fp ) ; // reading the fileif ( c == EOF )break ;printf ( "%c", c ) ;}printf("Closing the file test.c") ;fclose ( fp ) ; // Closing the filereturn 0;} |

OUTPUT:

| Opening the file test.c in read modeReading the file test.cHi, How are you?Closing the file test.c |

OTHER INBUILT FILE HANDLING FUNCTIONS IN C PROGRAMMING LANGUAGE:C programming language offers many other inbuilt functions for handling files. They are given below. Please click on each function name below to know more details, example programs, output for the respective file handling function.C – Typedef, C – UnionEXAMPLE PROGRAM FOR C TYPEDEF:

| 1234567891011121314151617181920212223 | // Structure using typedef:#include <stdio.h>#include <string.h>typedef struct student{int id;char name[20];float percentage;} status;int main(){status record;record.id=1;strcpy(record.name, "Binod");record.percentage = 86.5;printf(" Id is: %d \n", record.id);printf(" Name is: %s \n", record.name);printf(" Percentage is: %f \n", record.percentage);return 0;} |

OUTPUT:

| Id is: 1 Name is: Binod
Percentage is: 86.500000 |

*   Typedef can be used to simplify the real commands as per our need.
*   For example, consider below statement.

typedef long long int LLI;

*   In above statement, LLI is the type definition for the real C command “long long int”. We can use type definition LLI instead of using full command “long long int” in a C program once it is defined.

ANOTHER EXAMPLE PROGRAM FOR C TYPEDEF :

| 123456789101112 | #include <stdio.h>#include <limits.h>int main(){typedef long long int LLI;printf("Storage size for long long int data " \"type  : %ld \n", sizeof(LLI));return 0;} |

OUTPUT:

| Storage size for long long int data type : 8 |

C – Union

*   Union and structure in C  are same in concepts, except allocating memory for their members.
*   Structure allocates storage space for all its members separately.
*   Whereas, Union allocates one common storage space for all its members

*   We can access only one member of union at a time. We can’t access all member values at the same time in union. But, structure can access all member values at the same time. This is because, Union allocates one common storage space for all its members. Wher e  as Structure allocates storage space for all its members separately.
*   Many union variables can be created in a program and memory will be allocated for each union variable separately.

*   Below table will help you how to form a C union, declare a union, initializing and accessing the members of the union.

EXAMPLE PROGRAM FOR C UNION:

| 12345678910111213141516171819202122232425262728293031323334353637 | #include <stdio.h>#include <string.h>union student{char name[20];char subject[20];float percentage;};int main(){union student record1;union student record2;// assigning values to record1 union variablestrcpy(record1.name, "Amir");strcpy(record1.subject, "Maths");record1.percentage = 86.50;printf("Union record1 values example\n");printf(" Name       : %s \n", record1.name);printf(" Subject    : %s \n", record1.subject);printf(" Percentage : %f \n\n", record1.percentage);// assigning values to record2 union variableprintf("Union record2 values example\n");strcpy(record2.name, "Mani");printf(" Name       : %s \n", record2.name);strcpy(record2.subject, "Physics");printf(" Subject    : %s \n", record2.subject);record2.percentage = 99.50;printf(" Percentage : %f \n", record2.percentage);return 0;} |

OUTPUT:

| Union record1 values example Name : Amir
Subject : Maths
Percentage : 86.500000;
Union record2 values example
Name : Mani
Subject : Physics
Percentage : 99.500000 |

EXPLANATION FOR ABOVE C UNION PROGRAM:Record1 union variable:

*   “Amir” is assigned to union member “record1.name” . The memory location name is “record1.name” and the value stored in this location is “Amir”.
*   Then, “Maths” is assigned to union member “record1.subject”. Now, memory location name is changed to “record1.subject” with the value “Maths” (Union can hold only one member at a time).
*   Then, “86.50” is assigned to union member “record1.percentage”. Now, memory location name is changed to “record1.percentage” with value “86.50”.
*   Like this, name and value of union member is replaced every time on the common storage space.
*   So, we can always access only one union member for which value is assigned at last. We can’t access other member values.
*   So, only “record1.percentage” value is displayed in output. “record1.name” and “record1.percentage” are empty.

*   If we want to access all member values using union, we have to access the member before assigning values to other members as shown in record2 union variable in this program.
*   Each union members are accessed in record2 example immediately after assigning values to them.
*   If we don’t access them before assigning values to other member, member name and value will be over written by other member as all members are using same memory.
*   We can’t access all members in union at same time but structure can do that.

EXAMPLE PROGRAM – ANOTHER WAY OF DECLARING C UNION:

| #include <stdio.h>#include <string.h>union student{char name[20];char subject[20];float percentage;}record;int main(){strcpy(record.name, "Rajib");strcpy(record.subject, "Maths");record.percentage = 86.50;printf(" Name       : %s \n", record.name);printf(" Subject    : %s \n", record.subject);printf(" Percentage : %f \n", record.percentage);return 0;} |

OUTPUT:

| Name :Rajib Subject :Maths
Percentage : 86.500000 |

NOTE:

*   We can access only one member of union at a time. We can’t access all member values at the same time in union.
*   But, structure can access all member values at the same time. This is because, Union allocates one common storage space for all its members. Wher e  as Structure allocates storage space for all its members separately.

DIFFERENCE BETWEEN STRUCTURE AND UNION IN C:

| C Structure | C Union |
| Structure allocates storage space for all its members separately. | Union allocates one common storage space for all its members. Union finds that which of its member needs high storage space over other members and allocates that much space |
| Structure occupies higher memory space. | Union occupies lower memory space over structure. |
| We can access all members of structure at a time. | We can access only one member of union at a time. |
| Structure example: struct student
{
int mark;
char name[6];
double average;
}; | Union example: union student
{
int mark;
char name[6];
double average;
}; |
| For above structure, memory allocation will be like below. int mark – 2B
char name[6] – 6B
double average – 8B 
Total memory allocation = 2+6+8 = 16 Bytes | For above union, only 8 bytes of memory will be allocated since double data type will occupy maximum space of memory over other data types.  Total memory allocation = 8 |

About The AuthorSusanta BouriM.Tech in computer science
Maulana Abul Kalam Azad University Of Technology,
west Bengal,(India)
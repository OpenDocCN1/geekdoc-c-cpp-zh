![](Images/cover00133.jpeg)

C++ Programming Examples

Basic Syntax

HelloWorld.cpp ——————————> p.  5

DataTypes.cpp ———————————> p.  6

Variables.cpp ———————————> p.  7

Constant.cpp ————————————> p.  8

TypeCast.cpp ————————————> p.  9

ArithmeticOps.cpp ———————> p. 10

RelationalOps.cpp ———————> p. 11

AssignmentOps.cpp ———————> p. 12

MiscOps.cpp —————————————> p. 13

IfStatement.cpp —————————> p. 14

TernaryOperator.cpp —————> p. 15

LogicalOps.cpp ——————————> p. 16

Switch.cpp ——————————————> p. 17

ForLoop.cpp —————————————> p. 18

NestedFor.cpp ———————————> p. 19

WhileLoop.cpp ———————————> p. 20

Array.cpp ———————————————> p. 21

ArrayTwo.cpp ————————————> p. 23

String.cpp ——————————————> p. 24

StringArray.cpp —————————> p. 25

Functions.cpp ———————————> p. 26

Recursion.cpp ———————————> p. 27

Scope.cpp ———————————————> p. 28

Structs.cpp —————————————> p. 29

StructArray.cpp —————————> p. 30

Typedef.cpp —————————————> p. 31

CIN.cpp —————————————————> p. 32

Object Oriented

Classes.cpp —————————————> p. 33

Constructor.cpp —————————> p. 34

Inheritance.cpp —————————> p. 36

AccessModifiers.cpp —————> p. 38

FunctionOverloading.cpp -> p. 40

Polymorphism.cpp ————————> p. 41

Pointers

Pointer.cpp —————————————> p. 43

PointerToNull.cpp ———————> p. 44

PointerToVoid.cpp ———————> p. 45

ConstantPointer.cpp —————> p. 46

MultiplePointers.cpp ————> p. 47

PointerToArray.cpp ——————> p. 48

ReturnArrayFromFun.cpp ——> p. 49

PointerToStruct.cpp —————> p. 50

PointerToFunction.cpp ———> p. 51

PointerToAClass.cpp —————> p. 52

Sample Programs

TempConverter.cpp ———————> p. 53

ChemElement.h ———————————> p. 54

PeriodicTable.cpp ———————> p. 55

Average.cpp —————————————> p. 56

CoinFlip.cpp ————————————> p. 57

GuessThePassWord.cpp ————> p. 58

FibRecursion.cpp ————————> p. 60

Advanced

IO.cpp ——————————————————> p. 61

FileIO.cpp ——————————————> p. 62

ErrorHandling.cpp ———————> p. 64

MyHeader.h ——————————————> p. 65

Header.cpp ——————————————> p. 66

CommandLine.cpp —————————> p. 67

MemoryManagement.cpp ————> p. 68

DynamicIntArray.cpp —————> p. 69

DynamicString.cpp ———————> p. 70

ArrayAnalysis.cpp  ——————> p. 72

TicTacToe.h —————————————> p. 75

TicTacToeGame.cpp ———————> p. 76

Pieces.h ————————————————> p. 77

Moves.h —————————————————> p. 78

Game.cpp ————————————————> p. 79

Author’s Note

Thank you very much for your purchase, and your interest in learning a wonderful programming language. “C++ Examples” contains over 50 examples that are fully functional, easy to use, and unique. Previous programming knowledge is not required, however previous knowledge can do nothing but help. The only requirement is patience, dedication, and a passion for learning. However, as to not deter you from learning C++ I am going to explain how to create, compile, and run a “.cpp” source file.

In order to create an editable “.cpp” source file you first need to choose a text editor, I am going to use emacs. So to create a “.cpp” source file type the following command into your

command line:

emacs SourceFile.cpp

Then to compile, use the following command:

g++ SourceFile.c -o SourceFile

Then to run your file, use:

./SourceFile

New topics are presented in this book in an easy to understand way, then programs are made using the new topic as well as previously discussed topics in order to review and learn new material simultaneously. This helps you maximize learning a new language. There is much to learn and practice makes perfect. So let us

begin.

Thank You

HelloWorld.cpp

#include <iostream>//instead of <stdio.h> although that would work

using namespace std;//tells compiler to use std namespace

/*

Author | Email | Date

Basic syntax, and environment set up of a C++ program.

We will be using the g++ compiler, so if you do not have

this installed now is the time to install it.

Any legal C program is a legal c++ program

Apple and PC use C++ to write their interfaces

C++ was originally named “C with classes”... Yay classes

We are inside a block comment right now, comments are not ran

when you run a program

*/

//this is a single line comment

//code inside main() will execute when compiled and ran

int main(){

  //huge difference than the printf() function

  cout << "Hello World!\n";

//can use the newline character,\n, or endl

//we can see our c knowledge can be applied here

  printf("--Hello World--\n");

  return 0;

}

OutPut:

Hello World!

--Hello World—

DataTypes.cpp

#include <iostream>

#include <limits.h>//since we are basically writing c we can do this

using namespace std; //this is new

/*

Author | Email | Date

Primitive Types: bool, char, int, float, double, void

Type modifiers: signed, unsigned, short, long

so you can add these modifiers to data types based on what you need.

*/

int main(){

/*

bool: is a true/false statement

char: a single character

int/long: are whole numbers

float/double: are floating point values(decimal numbers)

void: a none type

*/

  cout << sizeof(char) << " bytes in a char\n";

  cout << "Unsigned Data Types range from 0 - MAXSIZE\n";

  cout << "Signed data takes into account negative range.\n";

  cout <<"Short shortens the bytes, while long lengthens the bytes\n";

  cout << "There are 8 bits in a byte\n";

  cout << "A char is 1 byte(8 bits), so the max value is (2^8)-1\n";

  //unsigned char 0 to 255, signed char -128 to +127

  //this can be done with all the data types.

  return 0;

}

OutPut:

1 bytes in a char

Unsigned Data Types range from 0 - MAXSIZE

Signed data takes into account negative range.

Short shortens the bytes, while long lengthens the bytes

There are 8 bits in a byte

A char is 1 byte(8 bits), so the max value is (2^8)-1

Variables.cpp

#include <iostream>

#include <math.h>//a header file with useful math functions

using namespace std;

/*

Author | Email | Date

How to declare and initialize a variable.

You can initialize a variable with a function call.

*/

int main(){

  //type name = value;

  bool b;//declaration

  b = true;//initialization

  cout << "b: " << true<< "\n";

  cout << "range of unsigned bool: 0 to " 

                                      <<pow(2,8*sizeof(bool))-1<<"\n";

  int x = 1000;

  int y = x;

  int z = x+y;

  cout<<"x: "<<x<<" y: "<<y<<" z: "<<z<<"\n";

  //note: multiple declarations of the same line is ok

  return 0;

}

OutPut:

b: 1

range of unsigned bool: 0 to 255

x: 1000 y: 1000 z: 2000

Constant.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

Constant: How to declare a variable a constant.

Once a constant is initialized, it can not

be changed. Different yet similar to #DEFINE

*/

int main(){

  //common practice is to capitalize all

  //letters of a constant

  const int MAX = 100;

  cout<< "MAX: "<<MAX<<"\n";

  //below is an illegal move

  //comment back in to find out what error it throws

  //MAX = 150;//illegal

return 0;

}

Output:

MAX: 100

TypeCast.cpp

#include <iostream>

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

using namespace std;

/*

Author | Email | Date

How to cast a data type to a different data type, watch out for loss of data. When you type cast you temporarily assign a data type to the data type you are casting to. Not all of the above header files are used, I just want to illustrate some useful ones, and all the “.h” files from C are available in C++.

*/

int main(){

  float decimal = 3.14159;

  float e = 2.71828;//Euler’s Number

  cout << "decimal before: " << decimal << “\n”;

  //we are casting a float to an int, temporarily

  cout << "decimal after: " << (int)decimal << "\n";

  cout<<"e before: "<<e<<"\n";

  cout<<"e after: "<<(int)e<<"\n";

  //useful for quick conversions,

  //passing arguments into functions

  //can cast one class to another

  return 0;

}

Output:

decimal before: 3.14159

decimal after: 3

e before: 2.71828

e after: 2

ArithmeticOps.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

What arithmetic operators are: they allow you to perform arithmetic operations on data types.

They include: + - / * ++ -- %

*/

int main(){

  //perform arithmetic operations

  cout<< "1+1: "<<1+1<<"\n";

  //increment operator, -- works the same but subtracts one

  int x= 1;

  x++;

  cout<<"1++: "<<x<<"\n";

  //modulus operator--> returns the remainder of a quotient

  cout<<"5%3: "<<5%3<<"\n";

  return 0;

}

Output:

1+1: 2

1++: 2

5%3: 2

RelationalOps.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

What relational operators are: they perform comparison tests.

They include: >, >=, <, <=, ==, !=

They compare two values.

*/

int main(){

  cout<< "1<2: "<<(1<2)<<"\n";

  cout<<"1>2: "<<(1>2)<<"\n";

  cout<<"5%3 == 2: "<<(5%3 == 2)<<"\n";

  //is 5%3 not equal to 2

  cout<<"5%3 != 2: "<<(5%3 != 2)<<“\n";

  /*

    These operations return a boolean(a true/false statement),

   however that boolean is represented as a 1 or a 0\. 1 is true, 0 is

    false.

   */

  return 0;

}

Output:

1<2: 1

1>2: 0

5%3 == 2: 1

5%3 != 2: 0

AssignmentOps.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

Assignment operators allow you to assign a variable a value,

while also performing an operation on that same variable.

They include: +=, -=, *=, /=, and %=

*/

int main(){

  //using any arithmetic operation

  //you can create an assignment operation

  int awesome = 99;

  cout<<"awesome before: "<<awesome<<"\n";

  awesome += 10;//awesome = awesome+10;//awesome++

  cout<<"awesome after: "<<awesome<<"\n";

  //try some more with all the arithmetic operators

  return 0;

}

Output:

awesome before: 99

awesome after: 109

MiscOps.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

Various other operators we will run across including the sizeof

operator, the dot operator and the arrow operator.

*/

int main(){

  //sizeof() operator

  cout<<"sizeof(int): "<<sizeof(int)<<"\n";

  //comma operator cause a series of operations to be performed

  //useful for parameter lists

  //dot operator (.) allow member access of an object/struct

  //arrow operator (->) allows dereferencing of a pointer to a struct

  //or a pointer to a class

  return 0;

}

Output:

4

IfStatement.cpp

include <iostream>

using namespace std;

/*

Author | Email | Date

If statements control the flow of your program. They control what code is ran, and what code is not ran based off a true/false statement.

*/

int main(){

  //go ahead and try changing this value

  int test = 222;

  if(test<200){

    cout<<"If code executed, all others skipped...\n";

  }

  else if(test==200){

    cout<<"Else If code executed, all others skipped...\n";

  } else {

    cout<<"Else code executed, when none are passed...\n";

  }

  bool condition = true;

  if(!condition){//bang operator, tests the opposite of condition

    //if condition is false

    cout<<"Condition is false...\n";

  }else {

    cout<<"Condition is true...\n";

  }

  return 0;

}

Output:

Else code executed, when none are passed...

Condition is true…

TernaryOperator.cpp

/*

Author | Email | Date

TernaryOperator: A ternary operator is pretty much shorthand

notation for if blocks. They are also called conditional

operators. They are a one line statement that assigns a variable one of two values based off a true/false statement.

*/

int main(){

  int number = 99;//this number can be anything

  int outcome;

  //below is shorthand notation for:

  //if 99%2 equals 0 outcome = 1

  //else outcome = 0

  outcome = (99%2 == 0) ? 1 : 0;

  printf("outcome: %d\n",outcome);

  //this is a test to see if number is

  //odd or even, if number is evenly divisible

  //by two (the remainder is 0) then it is an

  //even number

}

Output:

outcome: 0

LogicalOps.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

Logical Operators: Logical operators allow you to test multiple booleans in an if statement. They include the and operator (&&), the bang operator (!) and the or operator (||)

*/

int main(){

  int test = 222;

  bool condition = true;

  bool bang = !true; //what this means: bang = false

  if(test<200 && condition){

    //if test<200 is true and condition is true

    cout<<"If code executed, all others skipped...\n";

  }

  else if(bang || condition){

    //if bang is true or condition is true

    cout<<"Else If code executed, all others skipped...\n";

  } else {

    cout<<"Else code executed, when none are passed...\n";

  }

  return 0;

}

Output:

Else If code executed, all others skipped...

Switch.cpp

#include <iostream>

/*

Author | Email | Date

Switch: How to use a switch statement. Switch statements are like if blocks. They “switch” off of some variable, usually an int or a char, but any integral type is legal.

*/

int main(){

  //try changing this number

  int number = 7;//this is what we will switch on

  char letter = ‘a’;//try switching on a char

  switch(number){

  case 0://‘a'

    //if number == 0, run this code, and skip the rest

    printf("Number == 0\n");

    break;//optional

  case 1://‘b’

    printf("Number == 1\n");

    break;//optional

  case 2://‘c’

    printf("Number == 2\n");

  case 3:

    printf("Number == 3\n");

    break;//optional

  default : //again optional

    //ran when no cases are met

    printf("No number matched\n");

  }

}

Output:

No number matched

ForLoop.cpp

#include <iostream>

//no using namespaces std because

//we are not using cout in this program

/*                                                                             

Author | Email | Date

ForLoop: How to create and use a for loop,  when you create a for loop you first initialize some sort of counter variable, it is usually an int named “i”. Second, you set some condition to test each pass. Once the condition is false the for loop terminates. Third you set up a step. Usually you increment by one, but you can increment, decrement, multiply, divide, etc.

*/

int main(){

  for(int i =0; i<=10;i++){//initialization, condition, step                                                    

    printf("i : %d \n",i);                                                     

  }                                                                            

    return 0;

}

OutPut:

i : 0

i : 1

i : 2

i : 3

i : 4

i : 5

i : 6

i : 7

i : 8

i : 9

i : 10

NestedFor.cpp

#include <iostream>

/*                                                                             

Author | Email | Date

NestedFor: A nested for loop is a loop within a for loop, a double for loop. Again C code is legal in C++ so we will take advantage of the

printf() function again.

*/

int main(){

  //Multiplication table                                                       

  for(int i=1; i<=12;i++){

    //when i is 1 this second loop will run 12 times,

    //when i is two this second loop will run 12 times…                                                    

    for(int j=1; j<=12; j++){                                                

      printf("%d \t", i*j);//will run 144 times                                                    

    }                                                                          

    printf("\n");                                                              

  }                                                                              

    return 0;

}

Output:

1 2 3 4 5 6 7 8 9 10 11 12

2 4 6 8 10 12 14 16 18 20 22 24

3 6 9 12 15 18 21 24 27 30 33 36

4 8 12 16 20 24 28 32 36 40 44 48

5 10 15 20 25 30 35 40 45 50 55 60

6 12 18 24 30 36 42 48 54 60 66 72

7 14 21 28 35 42 49 56 63 70 77 84

8 16 24 32 40 48 56 64 72 80 88 96

9 18 27 36 45 54 63 72 81 90 99 108

10 20 30 40 50 60 70 80 90 100 110 120

11 22 33 44 55 66 77 88 99 110 121 132

12 24 36 48 60 72 84 96 108 120 132 144

WhileLoop.cpp

#include <iostream>

/*                                                                             

Author | Email | Date

While Loops: How to create and use a while loop, while loops are great when you don’t know how long the loop is going to run for, like taking in user input, or reading from a file.

*/

int main(){                                                                            

  int x = 0;

  while(x<10){

    printf("x : %d \n", x);

    x++;//watch out for infinite loop, comment out to see what

  //happens…, terminate with cntrl+c                                        

  }

    return 0;

}

Output:

x : 0

x : 1

x : 2

x : 3

x : 4

x : 5

x : 6

x : 7

x : 8

x : 9

Array.cpp

#include <iostream>

#include <math.h>

using namespace std;

/*

Author | Email | Date

Array:How to declare an initialize an array. An array is similar to a list of similar data types.

*/

int main(){

  //will create an array just big enough to hold

  int number_list[]={3, 6, 9, 12, 15};//index from 0 to length-1

  cout<<"number_list[2]: "<<number_list[2]<<"\n";

  cout<<"number_list[0] before: "<<number_list[0]<<"\n";

  number_list[0]= 55;//legal

  cout<<"number_list[0] after: "<<number_list[0]<<"\n";

  //or you can initialize an array of known size

  int new_list[10];

  for(int i = 0; i < 10;i++){

    new_list[i]= pow(i,2);//squaring each i

    cout<<"new_list["<<i<<"]: "<<new_list[i]<<"\n";

  }

  //you can use single members of an

  //array to initialize similar data types

  int member = new_list[9];

  cout<<"member: "<<member<<"\n";

  //one way to get size of any array

  //need to know the data type the array holds

  cout<<"size of out new_list[]: “

                              <<sizeof(new_list)/sizeof(int)<<"\n";

  //later we will cover how to pass arrays as arguments to functions

  return 0;

}

Output:

number_list[2]: 9

number_list[0] before: 3

number_list[0] after: 55

new_list[0]: 0

new_list[1]: 1

new_list[2]: 4

new_list[3]: 9

new_list[4]: 16

new_list[5]: 25

new_list[6]: 36

new_list[7]: 49

new_list[8]: 64

new_list[9]: 81

member: 81

size of out new_list[]: 10

ArrayTwo.cpp

#include <iostream>

/*

Author | Email | Date

ArrayTwo: How to declare an initialize a 2-dimensional array. An 2D array is like an array within an array. You can have 3D arrays, 4D arrays although these may be impractical and very complicated to keep track of.

*/

int main(){

    /*

2-D Array, an array within an array. Organized by row, column, notice double for loop. This can be used to iterate

     through a 2-D array or to initialize a 2-D array.

     */

  //initialize with row and column

  int box[4][4]={{0, 1, 2, 3},

     {10, 11, 12, 13},

     {20, 21, 21, 23},

     {30, 31, 32, 33}};

  for(int r = 0; r<4;r++){

    for(int c = 0; c<4; c++){//nested for loop

      printf("box[%d][%d]: %d\t", r, c, box[r][c]);

    }

    printf("\n");

  }

  return 0;

}

Output:

box[0][0]: 0box[0][1]: 1box[0][2]: 2box[0][3]: 3

box[1][0]: 10box[1][1]: 11box[1][2]: 12box[1][3]: 13

box[2][0]: 20box[2][1]: 21box[2][2]: 22box[2][3]: 23

box[3][0]: 30box[3][1]: 31box[3][2]: 32box[3][3]: 33

String.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

String: A string in C++ is a string of chars. A one dimensional array of chars. You can think of a string as a word or a sentence.

*/

int main(){

  //you can initialize these arrays the same way

  //but you need to include the null byte character '\0'

  char name[7]={'D','o','E','a','s','y','\0'};

  cout << "name: " << name <<"\n";

  //or you can use double quotes

  char new_name[]="Frank";

  cout << "new_name: " << new_name <<"\n";

  //the string.h header file has a bunch of

  //useful functions for strings

  //strcat(), strlen(), strcpy just to name a few

  cout << "length of new_name: " << strlen(new_name) <<"\n";

  //for this one^^^ you could use

  //the sizeof technique we used last time

 //C++ also has a new data type named string

  string sentence = “Very easy to initialize.”;

  cout << “Sentence: ”<<sentence<<“\n”;

return 0;

}

Output:

name: DoEasy

new_name: Frank

length of new_name: 5

Sentence: Very easy to initialize.

StringArray.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

StringArray: How to declare and use a string array.

*/

int main(){

  //this is very different from C, but you can have an array

  //of any legal data type within C++

  string names[] = {"Frank","Tom","Pauline"};

  for(int i = 0; i<3; i ++){

    cout<<"names["<<i<<"]: "<<names[i] << "\n";

  }

  return 0;

}

Output:

names[0]: Frank

names[1]: Tom

names[2]: Pauline

Functions.cpp

#include <iostream>

using namespace std;

/*

Author | Email | Date

Functions: How to make your own functions, and how to call user made functions, we have been calling printf for quite some time, printf is a function.

*/

//can be any legal data type

//when an array is a parameter, it is good practice

//to include a size parameter,e.g. (char name[], int size, …){}

//function needs to be declared above main

/*

Step One: Above main declare the function but do not write the body

Step Two: Declare the return type, function name, and then the

parameter list, in that order.

Step Three: Write the function body below the main method

Step Four: Call the function in the main method.

*/

//declaring function

int greatestFunctionEver(char goingToGetConverted);

//to return an array, we first need to talk about pointers

//so put this on hold for a moment

int main(){

  //function needs to be called in main

  cout << "Our Function Returned: "<<greatestFunctionEver('a')<<"\n";

  return 0;

}

//function needs to be defined below main

/*

When you define your own function you first need to declare a return type, the function must return this type. Second define the function name, this is how you call the function. Third, set up a parameter list, this can be as large or small as you need.

*/

int greatestFunctionEver(char goingToGetConverted){

  return goingToGetConverted;

}

Output:

Our Function Returned: 97

Recursion.cpp

#include<stdio.h>

/*

Recursion: A recursive function is a function that calls

itself. Infinite recursion is possible so beware of this.

Also, you must have a proper base case in order to avoid this.

Recursive functions are somewhat easier to read and write

however they do take up more space on the heap so they do take longer to execute. However, for this size program we

will be alright.

*/

//declare the function

int factorial(int n);

int main(){

  int n = factorial(5);//calling the function

                       //you can assign the output to a variable

                       // or since we know the return type of

                       //factorial is an int, we can do with the

                       //anything we can do with an int: pass it into

                       //functions, perform operations on it,

                       //assign it, etc

  printf("5!: %d\n",n);

  printf("6!: %d\n", factorial(6));

  return 0;

}

/*

Calculates the factorial of n.

Factorial equals n*n-1*n-2*n-3…*1

*/

int factorial(int n){

  //base case

  if (n == 0)

    return 1;

  //recursive step

  else

    return n * factorial(n-1);

}

Output:

5!: 120

6!: 720

Scope.cpp

#include <iostream

using namespace std;

/*

Author | Email | Date

Scope: scope is where and when you can use data and functions based on

where they were declared. Scope can be either global or local.

When you try to use a variable outside of it’s scope you will get an error.

*/

//int i =0;//global scope

int main(){

  //we could declare i out here and it would work

  for(int i = 0;i<10;i++){//i has local scope within the for loop

    cout<<"i: “<<i<<"\n"; //so when you try to use i outside of

                          //the scope of the for loop, an error occurs

  }

  //try adding this line below

  //cout<<"i: "<<i<<"\n";//won't work, will only work

                     //when scope of i is local to main, or is global

  return 0;

}

Output:

i: 0

i: 1

i: 2

i: 3

i: 4

i: 5

i: 6

i: 7

i: 8

i: 9

Struct.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

Struct: How to declare and initialize structs

Structs are data structures, you can think of them

as arrays, but they can hold different data types.

*/

int main(){

  struct Person{

    string name;//kind of useful for easiness,

                //however sometimes it is really useful

                //to know the size of the data you are working with

                //as in knowing the size of a char[]

    int age;

  };//don’t forget this semi-colon

  struct Person doEasy;

  doEasy.name = "Doeasy";

  doEasy.age = 100;//the dot operator we learned about in MiscOps.cpp

  cout<<"Name: "<<doEasy.name <<"\nAge: " <<doEasy.age <<"\n";

  return 0;

}

Output:

Name: Doeasy

Age: 100

StructArray.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

StructArray: How to initialize an array of structs. Just like any

legal data type you can have an array of data structures.

*/

struct Person{

  string name;

  int age;

}Person;

int main(){

  //notice the double curly brackets

  //we are initializing Person structures within the array

  Person contacts[3]={{"Frank",23},{"Lisa",34},{"Bell", 20}};

  struct Person individual;

  individual.name = "DoEasy";

  individual.age = 99;

  struct Person friends[1];

  //just showing you can use all the same techniques you know

  //about arrays

  friends[0] = individual;

  for(int i = 0; i < 3; i++){

    cout<<"Contacts["<<i<<"]"<<"\n";

    cout<<"\t"<<"Name: “<<contacts[i].name<<"\n\tAge:"

                        <<contacts[i].age<<"\n";

  }

  return 0;

}

Output:

Contacts[0]

Name: Frank

Age: 23

Contacts[1]

Name: Lisa

Age: 34

Contacts[2]

Name: Bell

Age: 20

TypeDef.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

Typedef: Explains how to use typedef, a keyword in C++. Typedef renames a data type to a name you choose, they are great for structs.

*/

int main(){

  //typedef is a keyword, so it can't be used anywhere else

  //it is used to give a type a new name

  typedef unsigned char BYTE;

 //we can now call BYTE instead of unsigned char

  BYTE b;//8 bits

  b = (2*2*2*2*2*2*2*2)-1;

  printf("Max value BYTE can hold: %d\n”,b);

  //can have an array as well

  BYTE four[4];//32 bits

  //can also do something like:

  typedef struct Person{

    char name[10];//this is still a string

    int age;

  }Person;//don't forget this

  Person doEasy; //notice no struct when declaring

  strcpy(doEasy.name,"DOEASY");

  doEasy.age = 100;

  printf("Name: %s\nAge: %d\n",doEasy.name, doEasy.age);

  return 0;

}

Output:

Max value BYTE can hold: 255

Name: DOEASY

Age: 100

CIN.cpp

#include<iostream>

using namespace std;

/*

Author | Email | Date

CIN: How to take in standard input using cin.

cin is available in C++, but not in C. cin is a bit easier to use than

scanf()

*/

int main(){

  //you can read in any data type

  //but the variable you store the input in

  //has to correspond

  cout << "Enter an int:\n";

  int x, y;

  cin >> x;

  cout << "Enter another number to add:\n";

  cin >> y;

  string s;

  cout<< "Enter a string:\n";

  cin >> s;

  cout << "Enter a numerator:\n";

  double a, b;

  cin >> a;

  cout << "Enter a denominator:\n";

  cin >> b;

  cout << "The sum is: "<<x+y<<"\n";

  cout << "The string is: "<<s<<"\n";

  cout << "The quotient is: "<<a/b<<"\n";

  return 0;

}

Output:

Enter an int:

100

Enter another number to add:

100

Enter a string:

word

Enter a numerator:

5

Enter a denominator:

4

The sum is: 200

The string is: word

The quotient is: 1.25

Classes.cpp

#include "stduse.h"

using namespace std;

/*

Author | Email | Date

Classes: How to make a class in C++, a class is like a

data structure however they can hold functions,

we will cover how to create and use those functions

for each individual instance of a class. An instance of a class is called an object. Objects are legal data types, they are complex.

*/

//first we will declare all of are data and functions

class Person{

  public:

    string name;

    int age;

    void printPerson();

};//don't forget this, this is the end of the class definition

//How to define a function out side of the Class definition

void Person::printPerson(){

  cout<<"Name: "<<name<<" Age: "<<age<<"\n";

}

int main(){

  Person p1;//p1 is an object, an instance of the Person class

  p1.name = “DoEasy”;

  p1.age = 100;

  //calling the printPerson() method inside

  //the instance of the class, p1

  p1.printPerson();//we are calling the printPerson method

              //from an instance of the Person class

              //we named that instance p1

  return 0;

}

Output:

Name: DoEasy Age: 100

Constructor.cpp

#include <iostream>

#incude <string.h>

using namespace std;

/*

Author | Email | Date

Constructor: You can instantiate a class with a constructor, when you make an instance of a class (a.k.a when you instantiate a class) you have made an object. A constructor is like a special function that creates an object. Constructors initialize the data inside the class.

*/

class Person{

  public:

    string name;

    int age;

    Person();//default constructor has no arguments

    Person(string name_in, int age_in);//constructor with parameters

    void printPerson();

};//don't forget this

//default constructor

//lets start to initialize

Person::Person(){

  name = "No Name Set";//could be anything you like, null…

  age = -1;

}

//constructor with parameters

//person object will have data with values

//we put into this constructor

Person::Person(string name_in, int age_in){

  name = name_in;

  age = age_in;

}

/*

Prints a person object onto the screen

Displays, name: and age.

*/

void Person::printPerson(){

  cout<<"Name: "<<name<<" Age: "<<age<<"\n";

}

int main(){

  Person p1;//call a default constructor just like this

  cout<<"p1:\n\t";

  p1.printPerson();

  Person p2("DoEasy",100);//constructor with parameters

  cout<<"p2:\n\t";

  p2.printPerson();

  return 0;

}

Output:

p1:

Name: No Name Set Age: -1

p2:

Name: DoEasy Age: 100

Inheritance.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

Inheritance: In C++ you can pass down “parent class” genes to another “child class” or a “derived class”. This saves you from writing extra code, and to be able to use your code again.

*/

//parent class

class SpaceBody{

public:

  double mass;

  double radius;

  //we can use methods such as these to access/change our data

  void setMass(double m){

    mass = m;

  }

  double getMass(){

    return mass;

  }

  void setRadius(double r){

    radius = r;

  }

  double getRadius(){

    return radius;

  }

  void print(){

    cout<<"\n\tMass: "<<getMass()<<"\tRadius: "<<getRadius()<<endl;

  }

};

/*

You can define class functions within the class definition as above

it is a bit nicer. We are going to pass along these functions, and

data into another class.

*/

/*

Child class: Will have all data and functions of base class.

You can inherit as many times as you need although this gets messy.

Planet is inheriting SpaceBody, it now has everything contained

within SpaceBody, you can have these two classes in separate files

to reuse base class as much as you want.

*/

class Planet: public SpaceBody{

public:

  string name;

  void setName(string n){

    name = n;

  }

  string getName(){

    return name;

  }

  Planet(string name, double m, double r);

  //this was declared user public

  void print(){

    cout<<"Name: “<<getName();//dont forget to print how the name

 //calling a parent class functions

SpaceBody::print();

  }

//this was declared outside of public: so we need

//to follow this format

Planet::Planet(string n, double m, double r){

  setName(n);

  setMass(m);

  setRadius(r);

}

int main(){

  Planet earth ("Earth", 45555.9, 890.99);

  earth.print();

  /*Please note: we could use getMass() or any function

    inside the class “AstroBody” on a class object of type

    Planet, Planet has all functions within AstroBody*/

}

Output:

Name: Earth

Mass: 45555.9Radius: 890.99

AccessModifiers.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

There are three access modifiers: public, private and protected

-Public: can be accessed anywhere outside the class

-Private: can only be accessed by the class or friend functions

-Protected: Like private except it has one extra quality,

these modifiers can be accessed by child classes(derived classes).

*/

class SpaceBody{

public:

  void setMass(double m){

    mass = m;

  }

  double getMass(){

    return mass;

  }

  void setRadius(double r){

    radius = r;

  }

  double getRadius(){

    return radius;

  }

  void print(){

    cout<<"\n\tMass: "<<getMass()<<"\tRadius: "<<getRadius()<<endl;

  }

protected://could change this to private and it would

          //still work because of polymorphism...

  double mass;

  double radius;

};

class Planet: public SpaceBody{

public:

  void setName(string n){

    name = n;

  }

  string getName(){

    return name;

  }

  Planet(string name, double m, double r);

void print(){

    cout<<"Name: "<<getName();

    SpaceBody::print();

}

//setting an access modifier to private

private :

  string name;

};

Planet::Planet(string n, double m, double r){

  setName(n);

  setMass(m);

  setRadius(r);

}

int main(){

  Planet earth ("Earth", 45555.9, 890.99);

  earth.print();

  //earth.name = "DoEasy";//this wont work,try commenting back in

  //name is private so it can only be accessed by public functions

  //within the Planet class, that is why we made getName() and so on

  earth.setName(“MARS");

  //you need a function from within “Planet class” to change this

  earth.print();

}

Output:

Name: Earth

Mass: 45555.9Radius: 890.99

Name: MARS

Mass: 45555.9Radius: 890.99

FunctionOverloading.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

You can overload a function in C++, overloading a function means:

creating a function of the same name and return type, but of different

parameter lists.

*/

class OutPut{

public:

  void print(int x){

    cout<<"int: "<<x<<endl;

  }

  void print(string s){

    string<<"float: "<<s<<endl;

  }

};

int main(){

  OutPut op;

  op.print(100);

  op.print("DoEasy");

  return 0;

}

Output:

int: 100

float: DoEasy

Polymorphism.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

Polymorphism: Polymorphism is when an object takes on

many forms. Polymorphism occurs after after inheritance,

different objects invoke different data/functions based off of what

data type they are.

*/

class SpaceBody{

public:

  void setMass(double m){

    mass = m;

  }

  double getMass(){

    return mass;

  }

  void setRadius(double r){

    radius = r;

  }

  double getRadius(){

    return radius;

  }

  SpaceBody();

  void test(){

    cout<<"Printed from SpaceBody Class.\n";

  }

  void print(){

    cout<<"\n\tMass: "<<getMass()<<"\tRadius: "<<getRadius()<<endl;

  }

protected:

  double mass;

  double radius;

};

SpaceBody::SpaceBody(){

  setMass(100);

  setRadius(99);

}

class Planet: public SpaceBody{

public:

  void setName(string n){

    name = n;

  }

  string getName(){

    return name;

  }

  Planet(string name, double m, double r);

void test(){

    cout<<"Printed from Planet Class.\n";

  }

  void print(){

    cout<<"Name: "<<getName();

    SpaceBody::print();

  }

private :

  string name;

};

Planet::Planet(string n, double m, double r){

  setName(n);

  setMass(m);

  setRadius(r);

}

int main(){

//mars is of type Planet and SpaceBody

//this is Polymorphism

  SpaceBody mars;

  mars.test();

  Planet earth("Earth", 33, 1);

  earth.test();

  return 0;

}

Output:

Printed from SpaceBody Class.

Printed from Planet Class.

Pointer.cpp

#include <stdio.h>

/*

[Author] | [Email] | [Date]

Pointer: A pointer is a special variable which stores the memory address of a data type. A pointers points to a memory address. When you declare a variable in C++, memory space is allocated to store that variable. A pointer points to the address where the value of that variable is stored, they are useful for creating dynamic programs(which we will cover later), but dynamic programs react and change during run time.

*/

int main(){

  int number = 1;

  int two;

  //to access a memory address use the & symbol

  //next to variable name

  printf("Address of number: %p\n", &number);

  printf("Address of two: %p\n", &two);//placeholder for pointer is %p

  //these two addresses will be separated by 4 bytes, or 32 bits

 //to declare a pointer use the data type (in this case int) then an

  //* next to the name

  int *pointerToInt = &number; //declaring a pointer variable

                               //that points to the address of number

  //just using the pointer will return an address

  printf("Address of where int is stored: %p\n", pointerToInt);

 //to access what the pointer is pointing to use a * on the pointer

  //this is called dereferencing the pointer

  printf("What The Pointer is Pointing to: %d\n", *pointerToInt);

return 0;

}

Output:

Address of number: 0x7fff5f315be8

Address of two: 0x7fff5f315be4

Address of where int is stored: 0x7fff5f315be8

What The Pointer is Pointing to: 1

PointerToNull.cpp

#include <stdio.h>

/*

Author | Email | Date

Pointers to null are legal within C++. Null is a none type similar to void, however they are different. Null is literally nothing, null is used when you don’t know what that value of a variable will be, but you know you want the variable. When a pointer is assigned

to null the pointer does not point to anything, it points to an invalid memory address.Two null pointers will always be equal.

Pointers to null do not point to anything.

They are useful to perform checks.

NULL is a special data type, it is literally nothing.

*/

int main(){

  int *p;

  p = NULL;//we now have a pointer to NULL

  int *cp = NULL;

  printf("p: %p\n",p);//%p is a placeholder for a pointer

  printf("p==cp: %d\n",p==cp);//1 is true, 0 is false

  //can use a pointer to null in an if statement

  //below is equivalent to: p != NULL

  if(p){

    printf("p is not null\n");

  }else {

    printf("p is null\n");

  }

//NULL is nothing, pointers to null are useful in data structures to

//signify the end of the data structure, for example a linked list

return 0;

}

Output:

p: 0x0

p==cp: 1

p is null

PointerToVoid.cpp

#include <stdio.h>

/*

Author | Email | Date

Pointers to void are legal within C++. A pointer to void

can be used to hold a pointer to any data type. Pointers to void

display traits of polymorphism.

*/

int main(){

  //Pointer to void can hold any data type

  int a = 100;

  int *p = &a;//first declare a pointer to an int

  printf("Address of p: %p\n",p);

  printf("sizeof(p): %lu\n", sizeof(p));

  printf("Dereferencing of p: %d\n",*p);

  void *vp;//next declare a pointer to void

  vp = p;//this pointer can hold any data type,

         //useful for function parameters

  /*

    -a pointer to void will have the same representation and memory   

     alignment as a char

    -a ptr to void will never == another ptr, yet two pointers to void

     assigned to NULL will ==

   */

  printf("Address of vp: %p\n",vp);

  printf("sizeof(vp): %lu\n", sizeof(vp));

  return 0;

}

Output:

Address of p: 0x7fff5c39cba8

sizeof(p): 8

Dereferencing of p: 100

Address of vp: 0x7fff5c39cba8

sizeof(vp): 8

ConstantPointer.cpp

#include <stdio.h>

/*

Author | Email | Date

ConstantPointer: Constant pointers are legal within C++. Once a constant pointer is initialized it cannot be changed. Nor can the value the address contains be change.

*/

int main(){

  int x = 100;

  const int *pci = &x;

  printf("Address: %p\n",pci);

  printf("Dereference: %d\n", *pci);

  //this is not legal so it is commented out

  //*pci = 200;//illegal

  //if pci was not a pointer to a constant you could

  //change the value by dereferencing

  return 0;

}

Output:

Address: 0x7fff54958ba8

Dereference: 100

MultiplePointers.cpp

#include <stdio.h>

/*

Author | Email | Date

You can have multiple pointers pointing to the same memory address.

But each of those pointers will have different addresses.

Be careful doing this because memory addresses can become lost

if done improperly. Please note in this example, there is also a reference of a pointer to a pointer.

*/

int main(){

  int x = 1000;

  int *p1 = &x;

  int *p2 = &x;

  //pointers have addresses themselves

  //and can be retrieved using & operator

  printf("Memory address of x: %p\n", p1);

  printf("Memory address of p1: %p\n", &p1);

  printf("Dereference of p1: %d\n", *p1);

  printf("Memory address of x: %p\n", p2);

  printf("Memory address of p1: %p\n", &p2);

  printf("Dereference of p2: %d\n", *p2);

  return 0;

}

Output:

Memory address of x: 0x7fff5bf59ba8

Memory address of p1: 0x7fff5bf59ba0

Dereference of p1: 1000

Memory address of x: 0x7fff5bf59ba8

Memory address of p1: 0x7fff5bf59b98

Dereference of p2: 1000

PointerToArray.cpp

#include <stdio.h>

/*

Author | Email | Date

PointerToArray: When you access array by name, rather than by an

index, an address to the first index will automatically return. You can use the technique below to iterate through an array.

*/

int main(){

  int *p; //declare a pointer before

  int list[]= {777, 222, 100};//initialize array

  //if you use list, instead of list[n], a pointer to the first memory        

  //address in the array therefore, this is like using &list[0]

  p = list;//will give us an address — same as p = &list[0]

  for(int i=0; i<3; i++){

    printf("Memory Address of index %d : %p\n", i, (p+i));

 //this is called pointer arithmetic

    printf("*(p + %d) : %d\n",  i, *(p + i) );

    //same as printing list[i]

    printf("\n");

  }

    return 0;

}

Output:

Memory Address of index 0 : 0x7fff5ec02bbc

*(p + 0) : 777

Memory Address of index 1 : 0x7fff5ec02bc0

*(p + 1) : 222

Memory Address of index 2 : 0x7fff5ec02bc4

*(p + 2) : 100

ReturnArrayFromFun.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

You can return an array from a function, however you have to return a pointer to the first data member in the array. Then you can use

pointer arithmetic to iterate through the array later on.

*/

/*

We will return a pointer to an int.

*/

int* returnArray(int numbers[], int size);

int main(){

  int list[] = {1,2,3};

  int* p = returnArray(list, 3);

  cout << "Returning array: "<<p<<"\n";

  cout<< "We will now dereference each element in array\n";

  for(int i = 0; i < 3; i++){

    cout <<"Array["<<i<<"]: \n"<<"\tMemory Address: “;

    cout << p << " Dereference: “ << *(p+i) << "\n";

  }

  return 0;

}

int* returnArray(int numbers[], int size){

  //this will return the first element in the array

  //we can then dereference this pointer using

  //arithmetic to iterate through the array.

  return numbers;

}

Output:

Returning array: 0x7fff56879b9c

We will now dereference each element in array

Array[0]:

Memory Address: 0x7fff56879b9c Dereference: 1

Array[1]:

Memory Address: 0x7fff56879b9c Dereference: 2

Array[2]:

Memory Address: 0x7fff56879b9c Dereference: 3

PointerToStruct.cpp

#include <stdio.h>

#include <string.h>

/*                                                                             

Author | Email | Date

PointerToStruct: You can have a pointer to a struct just the same way as any other data type. When you declare a pointer the memory address belongs to the first data type in the struct. You can iterate through a struct the same way we learned before.                                           

*/

struct Person{

  char name[20];

  int age;

}; //notice the semi-colon

//the parameter is a pointer to a struct

void printStruct(struct Person *person);

int main(){

  struct Person person;

  printf("Size of Struct: %lu\n\n",sizeof(person));

  strcpy(person.name, "DoEasy Prod.");

  person.age = 1;

  struct Person *p = &person;

  for(int i =0; i<2; i++){

    printf(“address[%d] : %p\n”,i,(p+i));

  }

  printStruct(p);

  return 0;

}

/*

Since we are using a pointer to a struct as a parameter we pass a pointer to a struct into our argument, to see what the pointer is pointing to we must use the -> operator, not the * operator                             

*/

void printStruct(struct Person *person){

  printf("Name: %s\nAge: %d\n", person->name, person->age);

}

Output:

Size of Struct: 24

address[0] : 0x7fff55633bb0

address[1] : 0x7fff55633bc8

Name: DoEasy Prod.

Age: 1

PointerToFunction.cpp

#include <stdio.h>

/*                                                                             

Author | Email | Date                                                         

PointerToFunction: Explains what a pointer to a function is, and how to use them. Once you have a pointer to a function you can use this pointer to call the function. You can call a function from

the pointer.                   

*/

int add(int x, int y);

int main(){

  //when you declare a pointer to a function you have to set

  //it up the same way as you did the original function

  //first declare the return type, then name the pointer, then

  //set the parameter list, and finally set store the address of the

  //original function

  int (*ptrfun)(int, int) = &add;

  int r = (*ptrfun)(10,3);

  printf("r: %d\n",r);

  return 0;

}

int add(int x, int y){

  return x+y;

}

Output:

r: 13

PointerToAClass.cpp

#include <iostream>

#include <string.h>

using namespace std;

/*

Author | Email | Date

You can have a pointer to a class just like you can have a pointer to another data type we have covered. Again use the same techniques we saw in the pointer to a struct example. We use the -> to dereference the pointer and to change the values.

*/

class Person{

  public:

    string name;

    int age;

    Person();

    Person(string name_in, int age_in);

    void printPerson();

};//don't forget this

//default constructor

Person::Person(){

  name = "No Name Set";//could be anything you like null is not bad...

  age = -1;

}

//constructor with parameters

Person::Person(string name_in, int age_in){

  name = name_in;

  age = age_in;

}

/*

*Prints a person object onto the screen

*Displays, name: and age:

*/

void Person::printPerson(){

  cout<<"Name: "<<name<<" Age: "<<age<<"\n";

}

int main(){

  Person p1("DoEasy",100);

  //declare a ptr variable just like any other time

  Person *pp= &p1;

  cout<<"Name: "<<pp->name<<endl;

cout<<"Age: "<<pp->age<<endl; //dereferencing the pointer

  return 0;

}

Output:

Name: DoEasy

Age: 100

TempConverter.cpp

#include<stdio.h>

#include<stdlib.h>

#include<iostream>

/*

Author | Email | Date

Converts a temperature in Fahrenheit to Celsius and Kelvin.

*/

int main(){

  printf("Enter degrees in F:\n");

  double tempF;

  cin >> tempF;

  double tempC = (tempF-32)*(double)5/9;

  double tempK = tempC + 273.15;

  //%.2f formats a decimal number to 2 decimal places

  printf("tempF: %.2f\n",tempF);;

  printf("tempC: %.2f\n",tempC);;

  printf("tempK: %.2f\n",tempK);;

}

Output:

Enter degrees in F:

0

tempF: 0.00

tempC: -17.78

tempK: 255.37

ChemicalElement.h

/*

 ChemicalElemnt: A header file that contains a data structure

that mimics a chemical element.

*/

typedef struct ChemicalElement{

  //names cannot be longer that 19 characters

  char name[20];

  int number;

  double mass;

  //anymore members you can think of?

}ChemicalElement;

PeriodicTable.cpp

#include"ChemicalElement.h"

#include<stdio.h>

#include<string.h>

#include<stdlib.h>

/*

Author | Email | Date

PeriodicTable: A C++ source file where you can save chemical elements,

and maybe start creating molecules.

*/

int main(){

  ChemicalElement hydrogen;

  strcpy(hydrogen.name, "Hydrogen");

  hydrogen.number = 1;

  hydrogen.mass = 1.001;

  ChemicalElement oxygen;

  strcpy(oxygen.name, "Oxygen");

  oxygen.number = 8;

  oxygen.mass = 15.9994;

  ChemicalElement h2o[3];

  h2o[0] = hydrogen;

  h2o[1] = hydrogen;

  h2o[2] = oxygen;

  printf("Printing Water:\n");

  double totalMass=0;

  for(int i = 0; i < 3; i++){

    printf("%s: %.2f\n", h2o[i].name, h2o[i].mass);

    totalMass += h2o[i].mass;

  }

  printf("Total Mass: %.2f\n", totalMass);

  return 0;

}

Output:

Printing Water:

Hydrogen: 1.00

Hydrogen: 1.00

Oxygen: 16.00

Total Mass: 18.00

Average.cpp

#include<stdio.h>

#include<stdlib.h>

#include<time.h>

/*

  Author | Email | Date

  Average: Calculates the average of a random int[]. We cover   

  how to create a random number using rand() the number after

  rand% is the range from [0 to range-1]. Notice the new import

  statements.

*/

int main(){

  srand(time(0));

  int numbers[10];

  int total = 0;

  for(int i = 0; i < 10; i++){

    numbers[i] = rand()%101;// includes [0,100]

    total += numbers[i];

  }

  printf("Array Populated:\n");

  double average = total/10;//ten total number, or use sizeof

  printf("Average: %.2f\n", average);

  return 0;

}

Output:

Array Populated:

Average: 39.00

CoinFlip.cpp

#include<siostream>

#include<stdlib.h>

#include<time.h>

/*

Author | Email | Date

CoinFlip: Simulates a coin toss by random

number generation.

*/

int main(){

  srand(time(0));

  string side = (rand()%2 + 1 == 1) ? “Heads” : “Tails”;

  printf(“%s\n”,side);

return 0;

}

Output 1:

Heads

Output 2:

Heads

Output 3:

tails

GuessThePassPhrase.c

#include<iostream>

#include<stdlib.h>

#include<string.h>

/*

Author | Email | Date

A game to test out while loops, user input and

logic. The game will end when the user guesses our

password.

*/

    /*

    Returns 1 if guess == password

    Otherwise 0 is returned.

   */

int equals(char* guess, char* password);

int main(){

  char PASSWORD[] = "Password";

  char* pp = PASSWORD;

  char guess[15];//guess can be no longer than 15 characters

      //we can use a string however you should practice

           //pointer arithmetic, and understand the equals function

  do{

    printf("Guess the password: \n");

   std::cin >> guess;//std:: needed because we left out using namespace std;

  }while(equals(guess, pp) == 0);

  printf("You win the password was: %s\n",PASSWORD);

  return 0;

}

    /*

    Returns 1 if guess == password

    Otherwise 0 is returned.

   */

  int equals(char* guess, char* password){

    int i = 0;

    while(*(password+i) != '\0'){

      if (*(password+i)!= *(guess+i))

return 0;

      i++;

    }

    return 1;

  }

Output:

Guess the password:

these

Guess the password:

are

Guess the password:

some

Guess the password:

guesses

Guess the password:

Password

You win the password was: Password

FibRecursion.cpp

#include<stdio.h>

/*

Author | Email | Date

FibRecursion: Calculates the fibonacci number up

to the desired place.

*/

int fibonacci(int n);

int main(){

  int fibArray[10];

  printf("Populating Array\n");

  for(int i = 0; i < 10; i++){

    fibArray[i] = fibonacci(i);

    printf("fibArray[%d]: %d\n",i, fibArray[i]);

  }

  return 0;

}

/*

fibonacci: Returns the the nth fibonacci number.

fib[n] = fib[n-1]+fib[n-2]

*/

int fibonacci(int n){

  //base case

  if (n == 0)

    return 0;

  else if (n == 1)

    return 1;

  else

    return fibonacci(n-1) + fibonacci(n-2);

}

Output:

Populating Array

fibArray[0]: 0

fibArray[1]: 1

fibArray[2]: 1

fibArray[3]: 2

fibArray[4]: 3

fibArray[5]: 5

fibArray[6]: 8

fibArray[7]: 13

fibArray[8]: 21

fibArray[9]: 34

IO.cpp

#include <stdio.h>

/*

Author | Email | Date

IO: We’ve been dealing with output all along with the printf() function, now let’s try some input using the scanf() function. We can use CIN, scarf, or getchar().

*/

int main(){

  //we have already been seeing input, but what if you

  //want to get user input from the keyboard?

  /*

    getchar() and putchar()

   */

  char c;

  printf("Enter a value>>> ");

  c = getchar();

  printf("\nChar Entered: ");

  putchar(c);

  printf("\n");

  /*

    scanf() and printf()

   */

  char input[100];

  int i;

  printf("Enter a value>>> ");

  scanf("%s %d", input, &i);//this can be any pattern you like

                            //or you know the user will input

                            //notice the & sign,

                            //scanf  must have a memory addresses,

//of the variables you are using

//input is the first address of the array

  printf("\nInput Entered: ");

  printf("%s %d", input, i);

  printf("\n");

  return 0;

}

Output:

Enter a value>>> s

Char Entered: s

Enter a value>>> string 4

Input Entered: string

FileIO.cpp

#include <stdio.h>

#include <string.h>

/*

  Author | Email | Date

  FileIO: How to read input from a file. We will also discuss how to

  write to a file, when you write to a file make sure to use the

  append option if you don’t want to completely write over the file.

*/

int main(){

  /*

    fgetc(fp) -->reads in a char

    fscanf(fp, char[], sourcefile)—> reads in a pattern

    fgets --> reads in lines

    printf: prints to a document

    fputs: also prints to a file

    Be careful printing to a file as you may delete all the contents,

    make sure you are appending to the file to avoid this.

   */

  FILE *fp;

  char contents[50];//cant be longer than 200

  fp = fopen("tester.txt","r");

  //if fp == NULL {

  fscanf(fp, "%s", contents);

  printf("Word 1: %s\n",contents);

  fscanf(fp, "%s", contents);

  printf("Word 2: %s\n",contents);

  fscanf(fp, "%s", contents);

  printf("Word 3: %s\n",contents);

  for(int i = 0; i<4; i++){

  fgets(contents, 50,  fp);

  printf("Line %d: %s\n", i+1, contents);

  }

  fclose(fp);

  fp = fopen("output.txt","w");

  //doesnt add a new line character

  fprintf(fp,"This will write into file above");

  fputs("This will also fo in the file",fp);

  return 0;

}

//line 1 is empty because we have already scanned that line with

//fscanf() function

Output:

Word 1: This

Word 2: scans

Word 3: words

Line 1:

Line 2: this is another line

Line 3: file input and output

Line 4: can be very useful

ErrorHandling.c

#include <stdio.h>

#include <stdlib.h>

/*

Author | Email | Date

Shows how to deal with errors, what to look for,

and stderr, part of the stdlib

*/

int main(){

  int numerator = 4;

  int denominator = 1;

  int quotient;

  if(denominator == 0){

    fprintf(stderr,"Error: Denominator == 0\nExiting with return status 1.\n");

    return 1;

  }

  quotient = numerator/denominator;

  fprintf(stderr, "Quotient: %d", quotient);

  return 0;

}

Output:

Quotient: 4

MyHeader.h

/*

Author | Email | Date

MyHeader: You can create your own header files within C++. You can later “include” these in other programs. Data structures and classes are a common thing to put in header files.

*/

typedef struct Person{

  char name[10];

  int age;

}Person;

//can put methods in here,

//can put error handling within those methods as well

Header.cpp

#include <stdio.h>

#include <string.h>

#include “MyHeader.h”//notice the include

/*

 Author | Email | Date

Header: Exercises our “MyHeader.h” header file. Shows how to include

user made header files.

*/

int main(){

  Person me;

  strcpy(me.name,"DoEasy");

  me.age = 100;

  printf("Name: %s\nAge: %d\n",me.name, me.age);

  return 0;

}

Output:

Name: DoEasy

Age: 100

CommandLine.cpp

#include <stdio.h>

/*

Author | Email | Date

CommandLine: How to pass in command line arguments.

Please note they are passed as an array of strings

so to accept a different data type takes more work.

Command line arguments are arguments next to the ./SourceFile command.

*/

int main(int argc, char *argv[]){

  if (argc == 1){

    printf("NO COMMAND LINE ARGS\n");

    return 0;

  } else {

    int i =1;

    while(i<argc){

      printf("Command Line Arg[%d]:%s\n", i, argv[i]);

      i++;

    }//end while

  }//end else

  return 0;

}

./CommandLine These Are the Args

Command Line Arg[1]:These

Command Line Arg[2]:Are

Command Line Arg[3]:the

Command Line Arg[4]:Args

MemoryManagement.cpp

#include <stdio.h>

#include <string.h>

#include <stdlib.h>

/*

DoEasy | Email | date

How to take allocate memory dynamically. Dynamic memory allocation means memory changes size, and reacts, during run time.

void *calloc(int num, int size)-->allocates an array of num, elements, each with given size

void free(void *address)-->release a block of memory given by address

void malloc(int num)-->allocates an array of num bytes, which are uninit

void *realloc(void *address, int newsize)-->reallocats memory, extending to size

Dynamic memory allocation is useful when you don't know how much memory space you need

So we can define a pointer to a data type without defining how much memory is required

*/

int main(){

  char name[10];

  char *about_name;

  strcpy(name,"doeasy");

  about_name = malloc(100*sizeof(char));

  printf("sizeof(): %lu\n", sizeof(about_name));

  printf("address: %p\n", &about_name);

  strcpy(about_name,"This string can be as big as the malloc...");

  //so if you wan to make this bigger, like n an error check or

  //based off of some user input you can use realloc()

  //then finally free up the space

  printf("name: %s\n",name);

  printf("about_name: %s\n", about_name);

  free(about_name);

  return 0;

}

Output:

sizeof(): 8

address: 0x7fff5c8e3b90

name: doeasy

about_name: This string can be as big as the malloc…

DynamicString.cpp

/*

Author | Email | Date

DynamicString: How to create a string dynamically.

A dynamic string grows and shrinks as needed.

Most times going into a program you do not know

how long your input is going to be, we will deal with

that right now.

*/

int main(){

  //first declare a char* to hold a string,

  //but set it equal to the size of one char

  //malloc returns a void* so you must cast to the

  //data type we are woking with

  char* input = (char*)malloc(sizeof(char));

  int count = 0;

  //next we will get some user input of unknown length

  printf("Enter a sentence: ");

  char token;

  token = getchar();

  //can only read in one sentence, hit enter from command line

  //to keep program going

  while(token != '\n'){

    //realloc returns a void* so you must cast

    //to the type of pointer you are working with

    input = (char*)realloc(input, sizeof(char)*(count+1));

    input[count] = token;//add to array

    token = getchar();//get the next token

    count++;//increment our size

  }

  printf("You entered: %s\n", input);

  printf("Counted %d tokens.",count);

  return 0;

}

Output:

Enter a sentence: this sentence can be any length

You entered: this sentence can be any length

DynamicIntArray.cpp

#include<stdio.h>

#include<stdlib.h>

/*

Author | Email | Date

DynamicIntArray: A dynamic int array can grow or shrink

during run time. We are going to use much the same approach

as before, but with integers.

*/

int main(){

  int* numbers = (int*)malloc(sizeof(int));

  printf("Enters numbers, press enter to add a number:\n");

  printf("Enter a -1 to exit.\n");

  int input = 0;

  int count = 0;

  while(input != -1){

    scanf("%d", &input);

    numbers = (int*)realloc(numbers, sizeof(int)*(count+1));

    numbers[count] = input;

    count++;

  }

  printf("\nPrinting Numbers:\n");

  for(int i = 0; i<count-1;i++){

    printf("number[%d]: %d\n",i, numbers[i]);

  }

  printf("\nThat was %d numbers.\n",count-1);

  return 0;

}

Output:

Enters numbers, press enter to add a number:

Enter a -1 to exit.

0

22

222

-1

Printing Numbers:

number[0]: 0

number[1]: 22

number[2]: 222

That was 3 numbers.

ArrayAnalysis.cpp

#include<stdio.h>

#include<stdlib.h>

#include<time.h>

/*

  Author | Email | Date

  ArrayAnalysis: Calculates the average, biggest, and smallest number

  of a randomly generated array. We are going to discuss how

  to return an array from a functions, and how to pass an array as a

  parameter.

*/

int* initArray(int size, int range);

double average(int* numbers, int size);

int biggest(int* numbers, int size);

int smallest(int* numbers, int size);

int main(){

  int* pi = initArray(10, 100);

  double ave = average(pi, 10);

  int big = biggest(pi, 10);

  int small = smallest(pi, 10);

  printf("Analyzing Array:\n");

  printf("\tAverage %.2f\n",ave);

  printf("\tBiggest %d\n",big);

  printf("\tSmallest %d\n", small);

  return 0;

}

/*

Creates an array of length size, with

random numbers in between [0, range].

When you return an array you must return

a pointer to an array, which you can later

iterate through.

*/

int* initArray(int size, int range){

  srand(time(0));

  int* num = (int*)malloc(sizeof(int));

  for(int i = 0; i < size; i++){

    num = realloc(num, sizeof(int)*(i+1));

    *(num+i) = rand()%range;

  }

  //this returns a pointer to the first

  //address of numbers

  return num;

}

/*

  average: Calculates the average of our array.

  What we are doing is passing an array into our function.

  More specifically we are passing a pointer to our function

  which we then can use pointer arithmetic on to

  dereference it's members. When you do this it is good practice

  to pass in the size as well.

*/

double average(int* numbers, int size){

  double total = 0;

  for(int i = 0; i < size; i++)

    total += *(numbers+i);

  return total/(double)size;

}

/*

  biggest: finds the largest number in an array.

  We will use the same technique as above.

*/

int biggest(int* numbers, int size){

  int biggest = *numbers;

  //initialize biggest to the first element

  for(int i = 1; i < size; i++){

    if(*(numbers+i) > biggest)

      biggest = *(numbers+i);

  }

  return biggest;

}

/*

  smallest: finds the smallest number in an array.

  We will use the same technique as above.

*/

int smallest(int* numbers, int size){

  int smallest = *numbers;

  //initialize biggest to the first element

  for(int i = 1; i < size; i++){

    if(*(numbers+i) <smallest)

      smallest = *(numbers+i);

  }

  return smallest;

}

Output:

Analyzing Array:

Average 60.30

Biggest 90

Smallest 0

TicTacToe.h

/*

TicTacToe: The beginning to a TicTacToe game, it needs some work, but it is great practice.

*/

char board[3][3];

int player1 = 1;

int player2 = 0;

void initBoard(){

  for(int i = 0; i < 3; i++){

    for(int j = 0; j < 3; j++){

      board[i][j] = ' ';

    }

  }

}

void printBoard(){

  for(int i = 0; i < 3; i++){

    for(int j = 0; j < 3; j++){

      printf("[%c]",board[i][j]);

    }

    printf("\n");

  }

}

/*

Put functions in here to check to see whose turn it is.

And to make moves.

*/

TicTacToeGame.cpp

#include <stdio.h>

#include "TicTacToe.h"

/*

Author | Email | Date

Exercises our TicTacToe.h header file. This file is where

the game is actually played. You can choose to make the game

for one or two players.

*/

int main(){

  initBoard();

  printBoard();

  board[0][1] = 'X';

  printBoard();

}

Output:

[ ][ ][ ]

[ ][ ][ ]

[ ][ ][ ]

[ ][X][ ]

[ ][ ][ ]

[ ][ ][ ]

Pieces.h

/*

Author | Email | Date

Pieces: Contains pieces present in a game of chess.

*/

char *board[8][8];

char pawn = 'p';

char rook = 'r';

char night = 'n';

char bishop = 'b';

char queen = 'q';

char king = 'k';

char block = ' ';

char *lostBlackPieces[16];

char *lostWhitePieces[16];

void initBoard(){

  for(int i = 0; i<8;i++){

    for(int j = 0; j<8; j++){

      if(i==1 || i == 6){

board[i][j] = &pawn;

      }    

      else if (i != 7 || 1 !=0 || i != 1 || i != 6)

      {

        board[i][j]=&block;

      }

    }

  }

  board[7][0]=&rook;

  board[7][1]=&night;

  board[7][2]=&bishop;

  board[7][3]=&queen;

  board[7][4]=&king;

  board[7][5]=&bishop;

  board[7][6]=&night;

  board[7][7]=&rook;

  board[0][0]=&rook;

  board[0][1]=&night;

  board[0][2]=&bishop;

  board[0][3]=&king;

  board[0][4]=&queen;

  board[0][5]=&bishop;

  board[0][6]=&night;

  board[0][7]=&rook;

}

void printBoard(){

  for (int r = 0; r<8; r++){

    for(int c = 0; c<8; c++)

      printf("[%c]", *(board[r][c]));

    printf("\n");

  }

}

Moves.h

/*

Author | Email | Date

Moves: Contains moves present in a game of chess.

*/

int checkPawnMove(char *p, int fromr, int fromc, int tor, int toc){

  if(p != &pawn){

    return 0;

  }

  else if(tor-fromr == 1 || tor - fromr!=-1){

    return 0;

  }

  else if(tor < 0 || tor > 7){

    return 0;

  }

  else if(toc-fromc != 0){

    return 0;

  }

  else{

    return 1;

  }

}

int jumpWithPawn(char *piece, int r, int c, int tor, int toc){

}

void movePawn(char *piece, int r, int c, int tor, int toc){

  if(checkPawnMove(piece, r, c, tor, toc)==1){

    board[tor][toc] = piece; 

    board[r][c] = &block;

  }

}

Game.cpp

#include <stdio.h>

#include "pieces.h"

#include "moves.h"

/*

A game of chess. Here is where you will implement the header files to

actually play a game of Chess. The game is far from complete but it is a nice start. Have fun :)

*/

int main(){

  initBoard();

  printBoard();

  movePawn(board[6][0], 6, 0, 5, 0);

  printBoard();

  movePawn(board[5][0], 5, 0, 4, 0);

  printBoard();

  return 0;

}

Conclusion

In conclusion, we have only scratched the surface with these examples. However, now you have a great base on which to build. So get out there and start building, breaking, and having fun with your own code. Please check out my website for more information:

[tfoss0001.github.io](http://tfoss0001.github.io)

For fun and interactive video tutorials check out my youtube channel:

DoEasy Productions

There are playlists on that channel to help guide you through these examples and to give you ideas for your own programs. Thank you very much.

-Torin Foss
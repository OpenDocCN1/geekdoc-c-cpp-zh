
d) The ______ selection statement is used to execute one action when a condition is true and another action when that condition is false.
e) Several statements grouped together in braces ({ and }) are called a(n) ______.
f) The ______ iteration statement specifies that a statement or group of statements is to be executed repeatedly while some condition remains true.
g) Iteration of a set of instructions a specific number of times is called ______ iteration.
h) When it’s not known in advance how many times a set of statements will be repeated, a(n) ______ value can be used to terminate the iteration.

### 3.2 Write four different C statements that each add 1 to integer variable `x`.

### 3.3 Write a single C statement to accomplish each of the following:

a) Multiply the variable product by 2 using the `*=` operator.

b) Multiply the variable product by 2 using the `=` and `*` operators.

c) Test whether the value of the variable count is greater than 10. If it is, print "Count is greater than 10."

d) Calculate the remainder after q is divided by divisor and assign the result to q. Write this statement two different ways.

e) Print the value 123.4567 with two digits of precision. What value is printed?

f) Print the floating-point value 3.14159 with three digits to the right of the decimal point. What value is printed?

### 3.4 Write a C statement to accomplish each of the following tasks:

a) Define variables sum and x to be of type int.

b) Set variable x to 1.

c) Set variable sum to 0.

d) Add variable x to variable sum and assign the result to variable sum.

e) Print "The sum is: " followed by the value of variable sum.

### 3.5 Combine the statements that you wrote in Exercise 3.4 into a program that calculates the sum of the integers from 1 to 10. Use the `while` statement to loop through the calculation and increment statements. The loop should terminate when the value of `x` becomes 11.

### 3.6 Write single C statements that

a) Input unsigned integer variable x with scanf. Use the conversion specifier `%u`.

b) Input unsigned integer variable y with scanf. Use the conversion specifier `%u`.

c) Set unsigned integer variable i to 1.

d) Set unsigned integer variable power to 1.

e) Multiply unsigned integer variable power by x and assign the result to power.

f) Increment variable i by 1.

g) Test i to see if it’s less than or equal to y in the condition of a while statement.

h) Output unsigned integer variable power with printf. Use the conversion specifier `%u`.

### 3.7 Write a C program that uses the statements in Exercise 3.6 to calculate x raised to the y power. The program should have a while iteration control statement.

### 3.8 Identify and correct the errors in each of the following:

```
a)
while ( c <= 5 ) {
    product *= c;
    ++c;
```

```
b)
scanf( "%.4f", &value );
```

```
c)
if ( gender == 1 )
    puts( "Woman" );
else;
    puts( "Man" );
```

### 3.9 What's wrong with the following while iteration statement (assume z has value 100), which is supposed to calculate the sum of the integers from 100 down to 1?

```c
while ( z >= 0 )
    sum += z;
```

## Answers to Self-Review Exercises

### 3.1
a) Algorithm. b) Program control. c) Sequence, selection, iteration. d) `if...else`. e) Compound statement or block. f) `while`. g) Counter-controlled or definite. h) Sentinel.

### 3.2

```c
x = x + 1;
x += 1;
++x;
x++;
```

### 3.3

a) `product *= 2;`

b) `product = product * 2;`

c) `if ( count > 10 )`
   `puts( "Count is greater than 10." );`

d) `q %= divisor;`
   `q = q % divisor;`

e) `printf( "%.2f", 123.4567 );`
   `123.46 is displayed.`

f) `printf( "%.3f\n", 3.14159 );`
   `3.142 is displayed.`

### 3.4

a) `int sum, x;`

b) `x = 1;`

c) `sum = 0;`

d) `sum += x;` or `sum = sum + x;`

e) `printf( "The sum is: %d\n", sum );`

### 3.5 See below.

```
/* Calculate the sum of the integers from 1 to 10 */
#include <stdio.h>

int main( void )
{
    unsigned int x = 1; // set x
    unsigned int sum = 0; // set sum

    while ( x <= 10 ) { // loop while x is less than or equal to 10
        sum += x; // add x to sum
        ++x; // increment x
    } // end while

    printf( "The sum is: %u\n", sum ); // display sum
} // end main function
```

### 3.6

a) `scanf( "%u", &x );`

b) `scanf( "%u", &y );`

c) `i = 1;`

d) `power = 1;`

e) `power *= x;`

f) `++i;`

g) `while ( i <= y )`
h) `printf( "%u", power );`

### 3.7 See below.

```c
// raise x to the y power
#include <stdio.h>

int main( void )
{
    printf( "%s", "Enter first integer: " );
    unsigned int x;
    scanf( "%u", &x ); // read value for x from user
    printf( "%s", "Enter second integer: " );
    unsigned int y;
    scanf( "%u", &y ); // read value for y from user

    unsigned int i = 1;
    unsigned int power = 1; // set power

    while ( i <= y ) { // loop while i is less than or equal to y
        power *= x; // multiply power by x
        ++i; // increment i
    } // end while

    printf( "%u\n", power ); // display power
} // end main function
```

### 3.8
a) Error: Missing the closing right brace of the `while` body.  
Correction: Add closing right brace after the statement `++c;`.

b) Error: Precision used in a `scanf` conversion specification.  
Correction: Remove `.4` from the conversion specification.

c) Error: Semicolon after the `else` part of the `if...else` statement results in a logic error.  
The second `puts` will always be executed.  
Correction: Remove the semicolon after `else`.

### 3.9
The value of the variable `z` is never changed in the `while` statement. Therefore, an infinite loop is created. To prevent the infinite loop, `z` must be decremented so that it eventually becomes `0`.

## Exercises

### 3.10 Identify and correct the errors in each of the following. [Note: There may be more than one error in each piece of code.]

a) `if ( sales >= 5000 )`  
    `puts( "Sales are greater than or equal to $5000" );`  
   `else`  
    `puts( "Sales are less than $5000" )`

b) `int x = 1, product = 0;`

   `while ( x <= 10 ); {`  
       `product *= x;`  
       `++x;`  
   `}`

c) `while ( x <= 100 )`  
       `total += x;`  
       `++x;`

d) while ( y < 10 ) {
       printf( "%d\n", y );
   }

### 3.11 Fill in the blanks in each of the following:

- a) In _______, statements execute one after the other in the order they are written.
- b) _______ programs help you "think out" a program.
- c) All programs can be written in terms of _______, _______, _______ and _______ control structures.
- d) Flowcharts are drawn using _______, _______, _______ and _______ connected by arrows called flowlines.
- e) Flowlines indicate the _______ in which the actions are performed.
- f) The _______ multiple-selection statement selects one among many options based on the value of an expression.
- g) The _______ operator is C's only ternary operator. It takes three operands, _______ a condition, _______ the value for the conditional expression if the condition is true, and _______ the value for the conditional expression if the condition is false.
- h) The if statement is a _______ structure.

### 3.12 What does the following program print?

```
1  #include <stdio.h>
2
3  int main( void )
4  {
5      int y;
6      int x = 1;
7      int total = 0;
8
9      while ( x <= 10 ) {
10         y = x * x * x;
11         printf( "%d\n", y );
12         total += y;
13         ++x;
14     } // end while
15
16     printf( "The total is %d\n", total );
17 } // end main
```

### 3.13 Write a single pseudocode statement that indicates each of the following:

- a) Display the message "Enter your name:"
- b) Assign the product of variables a, b, c and d to variable p.
- c) The following condition is to be tested in a conditional statement: if x is greater than y, then x is assigned the value 10, otherwise x is assigned the value 20.
- d) Obtain values for variables a, b, c and d from the keyboard.

### 3.14 Formulate a pseudocode algorithm for each of the following:

- a) Obtain three numbers from the keyboard, compute their product and display the result.
- b) Obtain two numbers from the keyboard, and determine and display which (if either) is the smaller of the two numbers.
- c) Obtain a series of positive numbers from the keyboard, and determine and display their average. Assume that the user types the sentinel value -1 to indicate "end of data entry."

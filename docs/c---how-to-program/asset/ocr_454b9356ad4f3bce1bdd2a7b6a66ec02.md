```
    d) while ( y < 10 ) {
           printf( "%d\n", y );
       }
```

3.11 Fill in the blanks in each of the following:

+   - a) In _______, statements execute one after the other in the order they are written.
+   - b) _______ programs help you "think out" a program.
+   - c) All programs can be written in terms of _______, _______, _______ and _______ control structures.
+   - d) Flowcharts are drawn using _______, _______, _______ and _______ connected by arrows called flowlines.
+   - e) Flowlines indicate the _______ in which the actions are performed.
+   - f) The _______ multiple-selection statement selects one among many options based on the value of an expression.
+   - g) The _______ operator is C's only ternary operator. It takes three operands, _______ a condition, _______ the value for the conditional expression if the condition is true, and _______ the value for the conditional expression if the condition is false.
+   - h) The if statement is a _______ structure.

3.12 What does the following program print?

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

3.13 Write a single pseudocode statement that indicates each of the following:

+   - a) Display the message "Enter your name:"
+   - b) Assign the product of variables a, b, c and d to variable p.
+   - c) The following condition is to be tested in a conditional statement: if x is greater than y, then x is assigned the value 10, otherwise x is assigned the value 20.
+   - d) Obtain values for variables a, b, c and d from the keyboard.

3.14 Formulate a pseudocode algorithm for each of the following:

+   - a) Obtain three numbers from the keyboard, compute their product and display the result.
+   - b) Obtain two numbers from the keyboard, and determine and display which (if either) is the smaller of the two numbers.
+   - c) Obtain a series of positive numbers from the keyboard, and determine and display their average. Assume that the user types the sentinel value -1 to indicate "end of data entry."
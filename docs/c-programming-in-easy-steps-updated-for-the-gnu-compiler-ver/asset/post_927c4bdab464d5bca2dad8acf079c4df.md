
...cont'd

- 1 Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](img/d1dfb0563339ba187decb78799155b7f_60_0.png)

- 2 Add a main function that declares and initializes two integer variables

```
int main()
{
    int yes = 1, no = 0;
}
```

- 3 Next, in the main function block, output the result of logic operations performed on the variables

```
printf("AND (no&&no): %d \n", no && no );
printf("AND (yes&&no): %d \n", yes && no );
printf("AND (yes&&yes): %d \n", yes && yes );
printf("OR (no||no): %d \n", no || no );
printf("OR (yes||no): %d \n", yes || no );
printf("OR (yes||yes): %d \n", yes || yes );
printf("NOT (yes !yes): %d %d\n", yes , !yes );
printf("NOT (no !no): %d %d\n", no , !no );
```

- 4 At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

- 5 Save the program file, then compile and execute the program to see the results of the logic operations

![](img/d1dfb0563339ba187decb78799155b7f_60_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_60_2.png)

Notice that 0 && 0 returns 0 (false) -- demonstrating the anecdote “two wrongs don't make a right”.

## Examining conditions

![](img/d1dfb0563339ba187decb78799155b7f_61_0.png)

Possibly the C programmer's favorite test operator is the `?:` conditional operator, also known as the "ternary" operator. This operator first evaluates an expression for a true or false Boolean value, then executes one of two given statements depending on the result of the evaluation.

The conditional operator has this syntax:

```
~~~c
( test-expression ) ? if-true-do-this : if-false-do-this ;
~~~
```

This operator could, for example, be used to evaluate whether a given number is odd or even by examining if there is any remainder after dividing the number by two, then output an appropriate string, like this:

```
~~~c
( 7 % 2 != 0 ) ? printf( "Odd Number" ) : printf( "Even Number" ) ;
~~~
```

In this case, dividing seven by two does not leave a zero remainder – so the expression evaluates as true; therefore the first statement is executed, correctly describing the number as an odd value.

The conditional operator is also useful to ensure correct grammar in output regarding singular and plural items, thus avoiding awkward phrases like "There is 5". The evaluation can simply be made within the `printf()` statement to use the appropriate version:

```
~~~c
printf( "There %s %d" , ( num == 1 ) ? "is" : "are" , num ) ;
~~~
```

In this case, when it's true that the `num` variable has a value of one, the "is" version will be used, otherwise the "are" version will be used.

The conditional operator can also be used to assign an appropriate value to a variable depending on the result of an evaluation. Used in this way its syntax looks like this:

```
~~~c
variable = ( test-expression ) ? if-true-assign-this : if-false-assign-this ;
~~~
```

This operator could, for example, be used to evaluate whether one given number is greater than another then assign the greater number to a variable, like this:

```
~~~c
int num , a = 5 , b = 2 ;
num = ( a > b ) ? a : b ;
~~~
```

In this case, the value of variable `a` is greater than that of variable `b`, so the `num` variable is assigned the greater value of `5`.

![](img/d1dfb0563339ba187decb78799155b7f_61_1.png)

Although the conditional operator is quick and easy to use it can reduce code readability.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions.

```c
#include <stdio.h>
```

- 2. Add a main function that declares and initializes a single integer variable.

```c
int main()
{
    int num = 7;
}
```

- 3. Next, in the main function block, insert a conditional statement to output the variable value’s parity.

```c
(num % 2 != 0) ? printf("%d is odd\n", num) : printf("%d is even\n", num);
```

- 4. Now, insert conditional statements to output a phrase using correct grammar for plurals.

```c
printf("There %s ", (num == 1) ? "is" : "are");
printf("%d %s\n", num, (num == 1) ? "apple" : "apples");
```

- 5. Decrease the variable value then insert conditional statements to output a phrase correct for singularity.

```c
num -= 1;
printf("There %s ", (num == 1) ? "is" : "are");
printf("%d %s\n", num, (num == 1) ? "apple" : "apples");
```

- 6. At the end of the main function block, return a zero integer value, as required by the function declaration.

```c
return 0;
```

- 7. Save the program file, then compile and execute the program to see the results of the conditional operations.

![](img/d1dfb0563339ba187decb78799155b7f_62_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_62_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_62_2.png)

The conditional operator is best used for terse statements that offer just two simple alternatives to implement.

...cont'd

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions `#include <stdio.h>`
- 2. Add a main function that declares and initializes a single integer variable

```c
int main()
{
    int num = 1234567890 ;
}
```

- 3. Next, in the main function block, insert statements to reveal the memory allocated to the int data type (in this implementation) by type name and object name

```c
printf("Size of int data type is %d bytes\n" , sizeof( int ) ) ;
printf("Size of int variable is %d bytes\n" , sizeof( num ) ) ;
```

- 4. Now, insert a statement to reveal that an array allocates the same memory for each one of its elements

```c
printf("Size of an int array is %d bytes\n" , sizeof( int[3]) ) ;
```

- 5. Define a structure comprising one char variable and one int variable then reveal its total memory allocation – including any padding

```c
struct { int score ; char grade ; } result ;
printf("Size of a structure is %d bytes\n" , sizeof( result ) ) ;
```

- 6. At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

- 7. Save the program file, then compile and execute the program to see output from the sizeof operations

![](img/d1dfb0563339ba187decb78799155b7f_64_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_64_1.png)

This example includes code for a struct object, which is a list of different variables. Structures are demonstrated in Chapter 9 but a struct is included here to demonstrate how the sizeof operator can measure its memory size.

![](img/d1dfb0563339ba187decb78799155b7f_64_2.png)

## Comparing bit values

A byte comprises 8 bits that can each contain a 1 or a 0 to store a binary number representing decimal values from 0 to 255. Each bit contributes a decimal component only when that bit contains a 1. Components are designated right-to-left from the “Least Significant Bit” (LSB) to the “Most Significant Bit” (MSB). The binary number in the bit pattern below represents decimal 50.

![](img/d1dfb0563339ba187decb78799155b7f_65_0.png)

Many C programmers never use bitwise operators but it is useful to understand what they are and how they may be used.

| Bit No | 7 MSB | 6 | 5 | 4 | 3 | 2 | 1 | 0 LSB |
|---|---|---|---|---|---|---|---|---|
| Decimal | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Binary | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |

Although the char data type is the basic 1-byte storage unit in C programming, as described on page 62, it is possible to manipulate individual parts of a byte using “bitwise” operators.

| Operator: | Name: | Binary number operation: |
|---|---|---|
| &#124; | OR | Return a 1 in each bit where either of two compared bits is a 1<br>Example: 1010 &#124; 0101 = 1111 |
| &amp; | AND | Return a 1 in each bit where both of two compared bits is a 1<br>Example: 1010 &amp; 1100 = 1000 |
| ~ | NOT | Return a 1 in each bit where the bit is not 1, and return 0 where the bit is 1<br>Example: ~ 1010 = 0101 |
| ^ | XOR | Return a 1 in each bit where only one of two compared bits is a 1<br>Example: 1010 ^ 0100 = 1110 |
| &lt;&lt; | Shift left | Move each bit that is a 1 a specified number of bits to the left<br>Example: 0010 &lt;&lt; 2 = 1000 |
| &gt;&gt; | Shift right | Move each bit that is a 1 a specified number of bits to the right<br>Example: 1000 &gt;&gt; 2 = 0010 |

![](img/d1dfb0563339ba187decb78799155b7f_65_1.png)

Each half of a byte is known as a “nibble” (4 bits). The binary numbers in the examples in the table describe values stored in a nibble.

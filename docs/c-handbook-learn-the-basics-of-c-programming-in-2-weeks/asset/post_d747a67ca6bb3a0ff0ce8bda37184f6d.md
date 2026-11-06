
## Chapter 7: The Operators in C#

Operators determine how logical or mathematical manipulations should be performed. Basically, operators are symbols that can communicate with the C# compiler. This programming language has a powerful collection of pre-installed operators. These operators are divided into six categories, namely:

- Relational Operators
- Assignment Operators
- Arithmetic Operators
- Bitwise Operators
- Logical Operators
- Misc. Operators

Let’s discuss each category in detail:

### The Relational Operators

The table below will show you the relational operators available in the C# language. Let’s use two variables: X = 2; Y = 4.

- “ == ” – This operator tests the equality of the operands. If the values are equal, the operator gives “ true ” as the result. For instance, “ Y == X ” isn’t true.
- “ > ” – This operator checks the value of both operands. If the left operand’s value is higher than that of the right operand, the condition is true. For example: “ Y > X ” is true.
- “ < ” – This operator checks the value of the operands involved. If the right operand’s value is higher than that of the left operand, the condition is true. For instance: “ X < Y ” is true.
- “ != ” – This operator checks the equality of the operands. If the values of the operands are not equal, the condition is true. For example: “ Y != X ” is true.
- “ <= ” – This operator tests whether the left operand’s value is less than or equal to that of the right operand. Here’s an example: “ Y <= X ” isn’t true.
- “ >= ” – This operator tests whether the right operand’s value is less than or equal to that of the left operand. Here’s an example: “ Y >= X ” is true.

### The Assignment Operators

The following list shows the C#-compatible assignment operators:

- “ = ” – This assignment operator can copy the right operand’s value and give it to the left operand. For example: Z = X + Y will assign the value of X + Y to Z.
- “ += ” – This assignment operator is called “Add AND.” It can add the value of the right operand to that of the left operand and give the sum to the left operand. For instance: Z += X is equal to Z = Z + X.
- “ -= ” – This operator is known as “Subtract AND.” It can subtract the value of the right operand from that of the left operand and give the difference to the left operand. For example: Z -= X is equal to Z = Z − X.
- “ *= ” – This operator is called “Multiply AND.” It can multiply the value of the right operand with that of the left operand and give the product to the left operand. For instance: Z *= X is equal to Z = Z * X.
- “ /= ” – This assignment operator is known as “Divide AND.” It can divide the value of the left operand with the value of the right operand and give the value to the left operand. Here’s an example: Z /= X is equal to Z = Z / X.
- “ %= ” – This operator is called “Modulus AND.” It uses two operands to take a modulus and assigns the result to the left operand. For example: (Z %= X) is equal to (Z = Z % X).
- “ <<= ” – This operator is called “Left Shift AND.” It adjusts the value of the left operand to the left based on the number indicated by the right operand. Then, it assigns the value to the left operand. Here’s how it works: Z <<= 3 is equal to Z = Z << 3.
- “ >>= ” – This operator is known as “Right Shift AND.” It adjusts the value of the left operand to the right based on the number indicated by the right operand. Check this example: (X >>= 3) is equal to (X = X >> 3).

### The Arithmetic Operators

The list below shows the available arithmetic operators in the C# language. To help you understand each operator, let's use two variables: X = 2 and Y = 4.

- “ + ” – This operator adds up two operands (e.g. X + Y = 6).
- “ - ” – This operator subtracts the value of the second variable from the first one (e.g. Y – X = 2).
- “ * ” – This operator multiplies the operands (e.g. X * Y = 8).
- “ / ” – This operator uses the denominator to divide the numerator (e.g. Y/X = 2).
- “ ++ ” – This is called the increment operator. It increases the value of a variable by 1 (e.g. X++ = 3).
- “ -- ” – This is known as the decrement operator. It decreases the value of a variable by 1 (e.g. Y-- = 3).

### The Bitwise Operators

You can use bitwise operators to work on bits. With this category, you’ll be able to perform bit-by-bit operations. The image below contains the truth tables for ^, |, and &.

| p | q | p & q | p \| q | p ^ q |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 1 |

For the following examples, let’s assume that X is 60 and Y is 13. Let’s convert them into binary elements:

X = 0011 1100

Y = 0000 1101

Now, let’s perform bit operations on these variables:

X|Y = 0011 1101

X&Y = 0000 1100

~X = 1100 0011

X^Y = 0011 0001

The list below shows the bitwise operators available in the C# language. Let’s use the same values: X = 60; Y = 13.

- “&” – This binary operator is called “AND.” If both operands have the same bit, that bit will be copied to the result. For instance: (X & Y) = 12, i.e. 0000 1100.
- “|” – This operator is called “OR.” It will copy a bit that exists in one of the operands. For example: (X | Y) = 61, i.e. 0011 1101.
- “^” – This binary operator is called XOR. It copies a bit that exists in just one of the operands. Thus, XOR won’t copy bits that exist in both operands. Here’s an example: (X ^ Y) = 49, i.e. 0011 0001.
- “~” – This is a unary operator. It “flips” bits when used in the C# programming language. Here’s an example: (~X) = -61, i.e. 1100 0011.
- “>>” – This is known as the “right shift operator.” It moves the value of the left operand to the right based on the bits indicated by the right operand. Here’s an example: X >> 2 = 15, i.e. 0000 1111.
- “<<” – This is called the left shift operator. It moves the value of the left operand to the left based on the bits indicated by the right operand. For example: X << 2 = 240, i.e. 1111 0000.

### The Logical Operators

The following list will show you the logical operators available in C#. Let’s assign Boolean Values to X and Y. X holds “TRUE” while Y holds “False.”

- “||” – This operator is known as “Logical OR.” If one of the operands is not equal to zero, the condition is true. For example: (X || Y) is true.
- “&&” – This operator is known as “Logical And.” If all of the operands are not equal to zero, the condition is true. For instance: (X && Y) is false.
- “!” – This operator is called “Logical Not.” You should use it to reverse the state of an operand. If the condition is true, this operator will become false. !(X || Y) is false.

### The Misc. Operators

The C# programming language supports other operators. Here are the important ones:

- “ sizeof() ” – This operator can identify the size of any data type. For instance, **sizeof(int)** can give you 4.
- “ typeof() ” – This operator can identify the type of any class. For example: **typeof(StreamReader).**
- “ & ” – You can use this operator to determine the address of any variable. For example: **&x** will give you the address of the variable named “ x. ”
- “ * ” – You can use this operator to create a pointer to any variable. For example: You can use *x to create a pointer, name it as “ x, ” and assign it to any variable.
- “ ?: ” – This operator is called the “ conditional expression. ” It assigns values to any variable based on its conditions. For example, it may assign the value of X to a variable if its condition is true. If the condition is false, however, it will assign the value of Y.
- “ is ” – You can use this operator to determine if an object belongs to a certain type. Here’s an example: **If( Gucci is Bag)** // will check whether an object named Gucci belongs to the class named Bag.

## Chapter 8: The Loops in C#

In some situations, you have to execute a code block several times. Entering the same statements repeatedly, however, is boring and time consuming. That means you should find a way to repeat blocks of codes quickly and easily. If you don’t know how to accomplish that, this chapter can help you greatly.

Important Note: Statements are generally executed in a sequential manner. That means C# executes the first statement first, followed by the next one, etc. You should remember this concept as you read this chapter.

Just like other programming languages, C# provides you with different control structures in terms of execution paths. That means you can access effective structures if you need to work on complex programs.

If you have to execute the same code blocks multiple times, you can streamline your task using a loop statement. The image below will show you the basic form of loop statements in C#:

![](img/4fa8a5f30786d4f308acc92572dd6e8f_42_0.png)

The C# programming language offers different kinds of loops. You can use these loops for your own codes. Check the list below:

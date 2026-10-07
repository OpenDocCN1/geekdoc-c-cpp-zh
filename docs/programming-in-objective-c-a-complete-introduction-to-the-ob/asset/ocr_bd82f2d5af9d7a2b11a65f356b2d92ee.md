# The Comma Operator

At the bottom of the precedence pole, so to speak, is is the comma operator. In Chapter 5, "Program Looping," we pointed out that inside a for statement, you can include more than one expression in any of the fields separating each expression with a comma. For example, the for statement that begins

```
for ( i = 0, j = 100; i != j; ++i, j -= 10 )
...
```

initializes the value of i to 0 and j to 100 before the loop begins, and increments the value of i and subtracts 10 from the value of j after the body of the loop is executed.

Because all operators in Objective-C produce a value, the value of the comma operator is that of the rightmost expression.

# The size Operator

Although you should never make assumptions about the size of a data type in your program, sometimes you need know this information. This might be when performing dynamic memory allocation using library routines like malloc, or when writing or archiving to a file. Objective-C provides an operator called sizeof that you can use to determine the size of a data type or object.The sizeof operator returns the size of the specified item by. The argument to the sizeof operator can be a variable, an array name, a basic data type, an object, the name of a derived data type, or an expression. For example, writing

```
sizeof (int)
```

gives the number of bytes needed to store an integer. On your MacBook Air, this produces a result of 4 (or 32 bits). If x is declared as an array of 100 ints, the expression

```
sizeof (x)
```

would give the amount of storage required to store the 100 integers of x.

Given that myFract is a Fraction object that contains two instance variables (numerator and denominator), the expression

```
sizeof (myFract)
```

produces the value 4 on any system that represents pointers by 4 bytes. In fact, this is the value that sizeof yields for any object because you are asking for the size of the pointer to the object's data. To get the size of the actual data structure to store an instance of a Fraction object, you would instead write the following:

```
sizeof (*myFract)
```

On my MacBook Air, this gives me a value of 12.That's 4 bytes each for the numerator and denominator, plus another 4 bytes for the inherited isa member mentioned in the section "How Things Work," at the end of this chapter.
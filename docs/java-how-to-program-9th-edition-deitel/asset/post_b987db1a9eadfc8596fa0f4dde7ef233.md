
condition is false, the body never executes. The do...while statement tests the loop-continuation condition after executing the loop's body; therefore, the body always executes at least once.

## Section 5.6 switch Multiple-Selection Statement

- The switch statement (p. 164) performs different actions based on the possible values of a constant integral expression (a constant value of type byte, short, int or char, but not long).
- The end-of-file indicator (p. 167) is a system-dependent keystroke combination that terminates user input. On UNIX/Linux/Mac OS X systems, end-of-file is entered by typing the sequence <Ctrl> d on a line by itself. This notation means to simultaneously press both the Ctrl key and the d key. On Windows systems, enter end-of-file by typing <Ctrl> z.
- Scanner method hasNext (p. 167) determines whether there's more data to input. This method returns the boolean value true if there's more data; otherwise, it returns false. As long as the end-of-file indicator has not been typed, method hasNext will return true.
- The switch statement consists of a block that contains a sequence of case labels (p. 168) and an optional default case (p. 168).
- When the flow of control reaches a switch, the program evaluates the switch's controlling expression and compares its value with each case label. If a match occurs, the program executes the statements for that case.
- Listing cases consecutively with no statements between them enables the cases to perform the same set of statements.
- Every value you wish to test in a switch must be listed in a separate case label.
- Each case can have multiple statements, and these need not be placed in braces.
- Without break statements, each time a match occurs in the switch, the statements for that case and subsequent cases execute until a break statement or the end of the switch is encountered.
- If no match occurs between the controlling expression's value and a case label, the optional default case executes. If no match occurs and the switch does not contain a default case, program control simply continues with the first statement after the switch.
- As of Java SE 7, you can use Strings in a switch statement's controlling expression and case labels.

## Section 5.7 break and continue Statements

- The break statement (p. 168), when executed in a while, for, do...while or switch, causes immediate exit from that statement.
- The continue statement (p. 172), when executed in a while, for or do...while, skips the loop's remaining body statements and proceeds with its next iteration. In while and do...while statements, the program evaluates the loop-continuation test immediately. In a for statement, the increment expression executes, then the program evaluates the loop-continuation test.

## Section 5.8 Logical Operators

- Simple conditions are expressed in terms of the relational operators >, <, >= and <= and the equality operators == and !=, and each expression tests only one condition.
- Logical operators (p. 174) enable you to form more complex conditions by combining simple conditions. The logical operators are && (conditional AND), || (conditional OR), & (boolean logical AND), | (boolean logical inclusive OR), ^ (boolean logical exclusive OR) and ! (logical NOT).
- To ensure that two conditions are both true, use the && (conditional AND) operator. If either or both of the simple conditions are false, the entire expression is false.
- To ensure that either or both of two conditions are true, use the || (conditional OR) operator, which evaluates to true if either or both of its simple conditions are true.
- A condition using && or || operators (p. 174) uses short-circuit evaluation (p. 175)—they’re evaluated only until it’s known whether the condition is true or false.
- The & and | operators (p. 175) work identically to the && and || operators, but always evaluate both operands.
- A simple condition containing the boolean logical exclusive OR (^; p. 176) operator is true if and only if one of its operands is true and the other is false. If both operands are true or both are false, the entire condition is false. This operator is also guaranteed to evaluate both of its operands.
- The unary ! (logical NOT; p. 176) operator “reverses” the value of a condition.

## Self-Review Exercises

### 5.1 (Fill in the Blanks)

Fill in the blanks in each of the following statements:

- a) Typically, __________ statements are used for counter-controlled repetition and __________ statements for sentinel-controlled repetition.
- b) The do...while statement tests the loop-continuation condition __________ executing the loop’s body; therefore, the body always executes at least once.
- c) The __________ statement selects among multiple actions based on the possible values of an integer variable or expression.
- d) The __________ statement, when executed in a repetition statement, skips the remaining statements in the loop body and proceeds with the next iteration of the loop.
- e) The __________ operator can be used to ensure that two conditions are both true before choosing a certain path of execution.
- f) If the loop-continuation condition in a for header is initially __________, the program does not execute the for statement’s body.
- g) Methods that perform common tasks and do not require objects are called __________ methods.

### 5.2 (True/False Questions)

State whether each of the following is true or false. If false, explain why.

- a) The default case is required in the switch selection statement.
- b) The break statement is required in the last case of a switch selection statement.
- c) The expression (( x > y ) && ( a < b )) is true if either x > y is true or a < b is true.
- d) An expression containing the || operator is true if either or both of its operands are true.
- e) The comma (,) formatting flag in a format specifier (e.g., %,20.2f) indicates that a value should be output with a thousands separator.
- f) To test for a range of values in a switch statement, use a hyphen (-) between the start and end values of the range in a case label.
- g) Listing cases consecutively with no statements between them enables the cases to perform the same set of statements.

### 5.3 (Write a Statement)

Write a Java statement or a set of Java statements to accomplish each of the following tasks:

- a) Sum the odd integers between 1 and 99, using a for statement. Assume that the integer variables sum and count have been declared.
- b) Calculate the value of 2.5 raised to the power of 3, using the pow method.
- c) Print the integers from 1 to 20, using a while loop and the counter variable i. Assume that the variable i has been declared, but not initialized. Print only five integers per line. [Hint: Use the calculation i % 5. When the value of this expression is 0, print a newline character; otherwise, print a tab character. Assume that this code is an application. Use the System.out.println() method to output the newline character, and use the System.out.print( '\t' ) method to output the tab character.]
- d) Repeat part (c), using a for statement.

### 5.4 (Find the Error)

Find the error in each of the following code segments, and explain how to correct it:

```java
a) i = 1;
while ( i <= 10 );
    ++i;
}
```

```java
b) for ( k = 0.1; k != 1.0; k += 0.1 )
    System.out.println( k );
```

```java
c) switch ( n )
{
    case 1:
        System.out.println( "The number is 1" );
    case 2:
        System.out.println( "The number is 2" );
        break;
    default:
        System.out.println( "The number is not 1 or 2" );
        break;
}
```

d) The following code should print the values 1 to 10:

```java
n = 1;
while ( n < 10 )
    System.out.println( n++ );
```

## Answers to Self-Review Exercises

5.1 a) for, while. b) after. c) switch. d) continue. e) && (conditional AND). f) false. g) static.

5.2 a) False. The default case is optional. If no default action is needed, then there’s no need for a default case. b) False. The break statement is used to exit the switch statement. The break statement is not required for the last case in a switch statement. c) False. Both of the relational expressions must be true for the entire expression to be true when using the && operator. d) True. e) True. f) False. The switch statement does not provide a mechanism for testing ranges of values, so every value that must be tested should be listed in a separate case label. g) True.

5.3 a)

```java
sum = 0;
for ( count = 1; count <= 99; count += 2 )
    sum += count;
```

5.3 b)

```java
double result = Math.pow( 2.5, 3 );
```

5.3 c)

```java
i = 1;
while ( i <= 20 )
{
    System.out.print( i );
    if ( i % 5 == 0 )
        System.out.println();
    else
        System.out.print( '\t' );
    ++i;
}
```

5.3 d)

```java
for ( i = 1; i <= 20; i++ )
{
    System.out.print( i );
```

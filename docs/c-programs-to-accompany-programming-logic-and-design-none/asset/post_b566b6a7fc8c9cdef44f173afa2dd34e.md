
As you can see in Figure 4-2, when parentheses are added, it still takes five steps, but the order of evaluation is changed and the result is also changed.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_63_0.png)

Figure 4-2 Evaluation of expression using relational and logical operators with parentheses

## COMPARING STRINGS

In C++, you may use the same relational operators when you compare string objects that you use to compare numeric data types such as ints and doubles.

The following code shows how to use the equality operator to compare two string objects and also to compare one string object and one string constant:

```cpp
string s1 = "Hello";
string s2 = "World";
// The following test evaluates to false because "Hello" is not the
// same as "World".
if (s1 == s2)
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to true because "Hello" is the same
// as "Hello".
if (s1 == "Hello")
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to false because "Hello" is not the
// same as "hello".
if (s1 == "hello")
    // code written here executes if true
else
    // code written here executes if false
```

> **NOTE** Two strings are equal when their contents are the same.

> **NOTE** C++ is case sensitive, which means that C++ does not consider a lowercase "h" to be equal to an uppercase "H" because their ASCII values are different. Lowercase "h" has an ASCII value of 104 and uppercase "H" has an ASCII value of 72. A table of ASCII values can be found in Appendix C - Understanding Numbering Systems and Computer Codes in *Programming Logic and Design, Fifth Edition*.

The following code shows how to use the other relational operators to compare two `string` objects and also to compare one `string` object and one `string` constant:

```cpp
string s1 = "Hello";
string s2 = "World";
// The following test evaluates to false because "Hello" is not
// greater than "World".
if (s1 > s2)
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to true because "Hello" is the same as
// "Hello".
if (s1 <= "Hello")
    // code written here executes if true
else
    // code written here executes if false
```

When you compare `string`s, C++ compares the ASCII values of the individual characters in the `string` to determine if one `string` is greater than, less than, or equal to another, in terms of alphabetizing the text in the `string`s. As shown in the preceding code, the `string` object s1, whose value is "Hello", is not greater than the `string` object s2, whose value is "World", because World comes after Hello in alphabetical order.

The following code sample shows additional examples of using the relational operators with two `string` objects:

```cpp
string s1 = "whole";
string s2 = "whale";
// The next statement evaluates to true because the contents of
// s1, "whole", are greater than the contents of s2, "whale".
if (s1 > s2)
    // code written here executes if true
else
    // code written here executes if false

// The next statement evaluates to true because the contents of s2,
// "whale", are less than the contents of s1, "whole".
if (s2 < s1)
    // code written here executes if true
else
    // code written here executes if false

// The next statement evaluates to true because the contents of s1,
// "whole", are the same as the string constant, "whole".
if (s1 == "whole")
    // code written here executes if true
else
    // code written here executes if false
```

## DECISION STATEMENTS

Every decision in a program is based on whether an expression evaluates to `true` or `false`. Programmers use decision statements to change the flow of control in a program. **Flow of control** means the order in which statements are executed. Decision statements are also known as **branching statements** because they cause the computer to make a decision, choosing from one or more branches (or paths) in the program.

There are different types of decision statements in C++. We will begin with the `if` statement.

### THE IF STATEMENT

The `if` statement is a single-path decision statement. As you learned in *Programming Logic and Design, Fifth Edition*, `if` statements are also referred to as “single alternative” or “single-sided” statements.

When we use the term “single-path,” we mean that if an expression evaluates to `true`, your program executes one or more statements; but if the expression evaluates to `false`, your program will not execute these statements. There is only one defined path—the path taken if the expression evaluates to `true`. In either case, the statement following the `if` statement is executed.

The syntax, or set of rules, for writing an `if` statement in C++ is as follows:

```cpp
if (expression)
    statementA;
```

Note that when you type the keyword `if` to begin an `if` statement, you follow it with an expression placed within parentheses.

When the compiler encounters an `if` statement, the expression within the parentheses is evaluated. If the expression evaluates to `true`, then the computer executes `statementA`. If the expression in parentheses evaluates to `false`, then the computer will not execute `statementA`. Remember that whether the expression evaluates to `true` and executes `statementA`, or the expression evaluates to `false` and does not execute `statementA`, the statement following the `if` executes next.

Note that a C++ statement, such as an `if` statement, can be either a simple statement or a block statement. A **block** statement is made up of multiple C++ statements. C++ defines a block as statements placed within a pair of curly braces. If you want your program to execute more than one statement as part of an `if` statement, you must enclose the statements in a pair of curly braces or only one statement will execute. The following example illustrates an `if` statement that uses the relational operator `<` to test if the value of the variable `customerAge` is less than 65. You will see the first curly brace in the fourth line and the second curly brace in the third to seventh line.

```cpp
int customerAge = 53;
int discount = 10, numUnder_65 = 0;
if(customerAge < 65)
{
    discount = 0;
    numUnder_65 += 1;
}
cout << "Discount : " << discount << endl;
cout << "Number of customers under 65 is: " << numUnder_65 << endl;
```

In the preceding code, the variable named `customerAge` is initialized to the value 53. Because 53 is less than 65, the expression `customerAge < 65` evaluates to true and the block statement executes. The block statement is made up of the two assignment statements within the curly braces: `discount = 0;` and `numUnder_65 += 1;`. If the expression evaluates to false, the block statement does not execute. In either case, the next statement to execute is the output statement `cout << "Discount : " << discount << endl;`.

Notice that you do not include a semicolon at the end of the line with the `if` and the expression to be tested. Doing so is not a syntax error, but it can create a logic error in your program. A **logic error** causes your program to produce incorrect results. In C++, the semicolon (;) is called the null statement and is considered a legal statement. The **null** statement is a statement that does nothing. Examine the following code:

```cpp
if (customerAge < 65); // semicolon here is not correct
{
    discount = 0;
    numUnder_65 += 1;
}
```

If you write an `if` statement as shown in the preceding code, your program will test the expression `customerAge < 65`. If it evaluates to true, the null statement executes, which means your program does nothing, and then the statement `discount = 0;` executes because this is the next statement following the `if` statement. This does not cause a logic error in your program, but consider what happens when the expression in the `if` statement evaluates to false. If false, the null statement does not execute, but the statement `discount = 0;` will execute because it is the next statement after the `if` statement.

The following code uses an `if` statement to test two string objects for equality:

```cpp
string dentPlan = "Y";
if (dentPlan == "Y")
    grossPay = grossPay - 23.50;
```

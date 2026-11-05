
For debugging, it is often easier to follow and read simple relational comparisons than compound comparisons. You will study this in more detail in a later section in this chapter. With additional thought, most numeric comparisons involving the compound relational operators of <= and >= can be revised. By simply adding or subtracting from the endpoint, the comparison can be written in a simpler form. Consider the following two statements in Example 5-3, which yield exactly the same comparison.

### Example 5-3

```
(examScore >= 90)    // Avoid compounds if you can.
(examScore > 89)     // Better test - does the same as above.
```

Both of the expressions in Example 5-3 return `true` for integer values larger than 89. The first line contains a compound expression (`examScore greater than 90` or `examScore equal to 90`). By simply subtracting 1 from 90, you can write a simpler conditional expression, as shown in Line 2 of Example 5-3.

Develop good style by surrounding operators with a space. This includes arithmetic, logical, and relational symbols. Readability is enhanced if you type a space before and after every operator, for example, x > 5; y == z; aValue = bValue + 3.

Table 5-3 in Example 5-4 presents several conditional expressions. Both relational and equality operators are used. A result of the expression with an explanation is included.

### Example 5-4

For each expression example, use the following declaration of variables:

```csharp
int aValue = 100;
int bValue = 1000;
char cValue = 'A';
string sValue = "CS158";
decimal money = 50.22m;
double dValue = 50.22;
```

**Table 5-3** Results of sample conditional expressions

| Expression | Result | Explanation |
|---|---|---|
| `(money == 100.00)` | Syntax error | Type mismatch. Money is `decimal`, 100.00 is `double`. Receive an error message that says "Operator '==' cannot be applied to `double` and `decimal`." |
| `(money == 50.22m)` | `true` | Must suffix the `decimal` number with M or m. |
| `(money != dValue)` | Syntax error | Type mismatch. Money is `decimal`, dValue is `double`. Receive an error message that says "Operator '!=' cannot be applied to `double` and `decimal`." |
| `(aValue > bValue)` | `false` | 100 is not greater than 1000. |
| `(sValue < "CS")` | Syntax error | < cannot be used with `string` operand. |
| `(aValue > (bValue - 999))` | `true` | 100 is greater than 1. |
| `(aValue > dValue)` | `true` | Integer aValue is converted to `double` and compared correctly. |
| `(aValue < money)` | `false` | Integer aValue is converted to `decimal` and compared correctly. |
| `(cValue = 'F')` | Syntax error | Cannot use single equality symbol (=) for condition comparison. Single equal symbol (=) is used for assignment. |
| `(cValue < 'F')` | `true` | Unicode A has a value of 65; Unicode F has a value of 70. |

In C#, the == and != are defined to work with strings to compare the characters lexicographically. This is not the case for other reference variables. In addition, the relational operators such as <, >, <=, and >= are not defined to work with strings. The relational operators can be used with char data types.

## Logical Operators

Conditional expressions can be combined with logical conditional operators to form complex expressions. The logical operators in C# are &, &&, |, ||, and !. The operands to logical operators must be Boolean expressions. Just as you communicate a compound expression in English, you can combine expressions with AND or OR. C# uses two ampersands && and two pipes || to represent AND and OR, respectively. These two operators are called the conditional logical operators. To add two points to examScore that range between 70 and 90, you might write the following pseudocode:

```
if (examScore > 69 AND examScore < 91)
    examScore = examScore + 2
```

When expressions are combined with AND, both expressions must evaluate to true for the entire compound expression to return true. As shown in Table 5-4, unless both expression operands are true, the compound expression created using the && evaluates to false.

**Table 5-4 Conditional logical AND &&**

| Expression1 | Expression2 | operand1 && operand2 |
|---|---|---|
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

![](img/e33ae760e23d89eac66541252ad65de8_276_0.png)

Table 5-4 is sometimes referred to as a truth table.

When combining logical operators with relational tests, developers often make the mistake of omitting the variable for the second and subsequent conditions being tested. In English, you would probably say, "if examScore is greater than 69 and less than 91." You normally do not repeat the variable being tested. In C#, you must repeat the variable. It is incorrect to write:

```
(examScore > 69 < 91)    //Invalid
```

It is also incorrect to write:

```
(69 < examScore < 91)    //Invalid
```

The correct way to write the expression is:

```
((examScore > 69) && (examScore < 91))    //Correct way
```

![](img/e33ae760e23d89eac66541252ad65de8_277_0.png)

It is not necessary to use the two innermost parentheses. Later in this chapter, in Table 5-7, you will explore the order of operations. The relational operators (< and >) have a higher precedence than the logical && and || operators, meaning the comparisons would be performed prior to the &&. Including the parentheses adds to the readability.

As illustrated in Table 5-5, || only returns a `false` result when both of the operands are `false`. At all other times, when either one of the operands evaluates to `true`, the entire compound expression evaluates to `true`.

**Table 5-5** Conditional logical OR `||`

| Expression1 | Expression2 | operand1 `||` operand2 |
|---|---|---|
| `true` | `true` | `true` |
| `true` | `false` | `true` |
| `false` | `true` | `true` |
| `false` | `false` | `false` |

Compound expressions using the `||` must also have a complete expression on both sides of the logical symbol. The following is invalid:

```
(letterGrade == 'A' || 'B')                         //Invalid
```

The correct way to write the conditional expression is:

```
((letterGrade == 'A') || (letterGrade == 'B'))       //Correct way
```

![](img/e33ae760e23d89eac66541252ad65de8_277_1.png)

Parentheses can be added to conditional expressions to improve readability.

The `!` symbol is the **logical negation operator**. It is a unary operator that negates its operand and is called the **NOT operator**. It returns `true` when operand1 is `false`. It returns `false` when operand1 is `true`.

Given the following declaration:

```
char letterGrade = 'A';
```

When the NOT operator (`!`) is placed in front of the conditional expression, the statement returns `false`, as shown in the following line:

```
(! (letterGrade == 'A'))
```

The conditional expression first yields a `true` result (letterGrade is equal to 'A'). Adding the NOT operator `!` negates that result. Thus, the expression evaluates to `false`.

As illustrated in Table 5-6, the NOT operator `!` returns the logical complement, or negation, of its operand.

**Table 5-6** Logical NOT !

| Expression1 | ! operand1 |
| --- | --- |
| `true` | `false` |
| `false` | `true` |

![](img/e33ae760e23d89eac66541252ad65de8_278_0.png)

As with the logical && and ||, the ! operator can also be difficult to follow. It is easier to debug a program that includes only positive expressions. An extra step is required in problem solving if you have to analyze a result that has been reversed or negated.

This section on compound conditions is included to give you an understanding of reading complex expressions. As you learn in the following sections, you can often avoid writing complex expressions that use logical operators with the use of a multiway or nested selection statement. This might take more thought than just combining a number of conditional expressions with a logical operator. However, because compound conditions can be difficult to debug, you should explore other options whenever possible.

## Short-Circuit Evaluation

In C#, the && and || operators are also called the **short-circuiting logical operators**. These operators enable doing as little as is needed to produce the final result through short-circuit evaluation. With **short-circuit evaluation**, as soon as the value of the entire expression is known, evaluation stops. A conditional expression is evaluated from left to right. With expressions involving &&, if the first evaluates as **false**, there is no need to evaluate the second. The result will be **false**. With expressions involving ||, if the first evaluates as **true**, there is no need to evaluate the second. The result will be **true**. Using the initialized variables, consider the expressions that follow in Example 5-5.

### Example 5-5

```csharp
int examScore = 75;
int homeWkGrade = 100;
double amountOwed = 0;
char status = 'I';
// : added to indicate more lines follow
((examScore > 90) && (homeWkGrade > 80))        // Line 1 - false
((amountOwed == 0) || (status == 'A'))          // Line 2 - true
```

When the first part of the expression (`examScore > 90`) in Line 1 evaluates to **false**, there is no need to evaluate the second. The result of the entire expression is **false**. If the first part of the expression in Line 1 evaluates to **true**, the second expression has to be evaluated. Both must be **true** for the entire expression to evaluate to **true**.

Line 2 is a logical OR; thus, if the first part of the expression evaluates to **true**, there is no need to evaluate the second. The result of the entire expression is **true** as soon as one of

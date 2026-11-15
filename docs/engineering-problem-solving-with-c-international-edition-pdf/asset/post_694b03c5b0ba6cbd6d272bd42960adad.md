
| A | B | A && B | A || B | !A | !B |
|---|---|---|---|---|---|
| False | False | False | False | True | True |
| False | True | False | True | True | False |
| True | False | False | True | False | True |
| True | True | True | True | False | False |

values for a, b, and c, we can evaluate this condition as true or false. For example, if a is equal to 1, b is equal to 5, and c is equal to 8, then the condition is true. If a is equal to -2, b is equal to 9, and c is equal to 2, then the condition is false.

If A and B are conditions, then the logical operators can be used to generate new conditions A && B, A || B, !A, and !B. The condition A && B is true only if both A and B are true. The condition A || B is true if either or both A and B are true. The ! operator changes the value of the condition which it precedes. Thus, the condition !A is true only if A is false, and the condition !B is true only if B is false. These definitions are summarized in Table 3.1.

Table 3.1 provides a truth table for the four conditions

A && B, A || B, !A, and !B.

Truth tables provide the truth values of a condition given the truth values of the boolean operands. In Table 3.1 there are two boolean operands, A and B, there are 2^2 = 4 unique combinations of values these boolean operands can represent. Each additional boolean operand doubles the number of unique combinations. Consider the condition

A && B || B && C.

The truth value of this expression depends on the truth values of the three boolean operands A, B and C, thus there are 2^3 = 8 unique combinations, as illustrated in Table 3.2.

The following program illustrates the use of logical and relational operators to generate the truth table provided in Table 3.2.

| A | B | C | A && B || B && C |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

```cpp
/*--------------------------------------------------------------*/
/* Program chapter3_1 generates a truth table                   */
/* for the condition:                                           */
/* A && B || B && C                                             */
/*--------------------------------------------------------------*/
#include <iostream>
using namespace std;

int main()
{
   //Declare and initialize objects
   bool A(false), B(false), C(false);

   //Print table header
   cout << " TABLE 3.2\n A\tB\tC\tA && B || B && C"
        << endl;
   cout << "------------------------------------------"
        << endl;

   cout << endl;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle C
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle B and C
   B = !B;
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle C
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle A, B and C
   A = !A;
   B = !B;
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Repeat the pattern for B and C.

   //Toggle C
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle B and C
   B = !B;
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;

   //Toggle C
   C = !C;
   cout << A << '\t' << B << '\t' << C << '\t' << '\t'
        << (A && B || B && C) << endl;
   return 0;
}
```

When expressions with logical operators are executed, C++ will only evaluate as much of the expression as necessary to evaluate it. This is known as **short circuiting**. For example, if A is false, then the expression

```
A && B
```

is also false, and there is no need to evaluate B. Similarly, if A is true, then the expression

```
A || B
```

is true, and there is no need to evaluate B. To verify the correctness of Table 3.2, you must be aware that the && operator takes precedence over the || operator. The precedence of operators is discussed in the following section.

- 1. Modify program `chapter3_1` to generate a truth table for the condition A&&B&&C.
- 2. Modify program `chapter3_1` to generate a truth table for the condition A||B||C.
- 3. Modify program `chapter3_1` to generate a truth table for the condition A&&B.

## Precedence and Associativity

A condition can contain several logical operators, as in the following:

```
! (b==c || b==5.5)
```

The hierarchy, from highest to lowest, is !, &&, ||, but parentheses can be used to change the hierarchy. In the previous example, the expressions b==c and b==5.5 are evaluated first. Suppose b is equal to 3 and c is equal to 5. Then neither expression is true, so the expression b==c || b==5.5 is false. We then apply the ! operator to the false condition, which gives a true condition.

A condition can contain both arithmetic operators and relational operators, as well as logical operators. Table 3.3 contains the precedence and the associativity order for the elements in a condition.

| Precedence | Operation | Associativity |
| :--- | :--- | :--- |
| 1 | ( ) | innermost first |
| 2 | ++ -- + - ! (type) | right to left (unary) |
| 3 | * / % | left to right |
| 4 | + - | left to right |
| 5 | < <= > >= | left to right |
| 6 | == != | left to right |
| 7 | && | left to right |
| 8 | || | left to right |
| 9 | = += -= *= /= %= | right to left |

## Practice!

Determine whether the following conditions in problems 1 through 8 are true or false. Assume that the following objects have been declared and initialized as shown:

```
a = 5.5 b = 1.5 k = 3
```

- 1. a < 10.0 + k
- 2. a + b >= 6.5
- 3. k != a - b
- 4. b - k > a
- 5. !(a == 3 * b)
- 6. -k <= k + 6
- 7. a < 10 && a > 5
- 8. fabs(k) > 3 || k < b - a

## 3.4 Selection Statements: if Statement

The if statement allows us to test conditions and then perform statements based on whether the conditions are true or false. C++ contains two forms of if statements—the simple if statement and the if else statement. C++ also contains a switch statement that allows us to test multiple conditions and then execute groups of statements based on whether the conditions are true or false.

### Simple if Statements

The simplest form of an if statement has the following general form:

```
if ( condition )
statement 1;
```

If the condition is true, we execute statement 1; if the condition is false, we skip statement 1.

> The statement within the if statement is indented so that it is easier to visualize the structure of the program from the statements.

If we wish to execute several statements (or a sequence structure) when the condition is true, we use a **statement block** which is composed of a set of statements enclosed in braces. The location of the braces is a matter of style; two common styles are shown:

```
Style 1
if (condition)
{
    statement 1;
    statement 2;
    ...
    statement n;
}

Style 2
if (condition) {
    statement 1;
    statement 2;
    ...
    statement n;
}
```

In the text solutions, we use the first style convention; thus, both braces are on lines by themselves.

> In the text solutions, we use the first style convention; thus, both braces are on lines by themselves. Although this makes the program a little longer, it also makes it easier to notice if a brace has been mistakenly omitted. Figure 3.4 contains flowcharts of the control flow with simple if statements containing either one statement to execute, or a statement block to execute, if the condition is true.

![](img/f2bfa570e453b020c16e048c79a3ea0e_121_0.png)

Figure 3.4 Flowcharts for selection statements.

if Statement: The if statement allows us to test conditions and then perform statements based on whether the conditions are true or false.

### Syntax:

```
if (condition)
    statement;
[else
    statement;]

if (condition) {
    statement block
} else {
    statement block
}
```

### Example:

```
#include <iostream>    //Required for cout
using namespace std;
int main()
{
  int a, count(0), sum(0);
  cin >> a;
  if (a < 50)
  {
    ++count;
    sum += a;
  }
  cout << (double) sum/count;
  return 0;
}
```

If a is less than 50, then count is incremented by 1 and a is added to sum; otherwise, these two statements are skipped.

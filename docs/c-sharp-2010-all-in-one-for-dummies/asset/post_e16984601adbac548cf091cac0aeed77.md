
and reassigns the uppercased character to sb[0]. Finally, it extracts the improved string "Jones" from the StringBuilder.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_96_0.png)

The BuildASentence example presented earlier in this chapter could benefit from using a StringBuilder. I use StringBuilder quite a bit.

The StringCaseChanging and VariousStringTechniques examples on this book's Web site show StringBuilder in action.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_96_1.png)

Book II introduces a C# feature called extension methods. The example there adds several handy methods to the String class. Later in that minibook, we describe how to convert between strings, arrays of char, and arrays of byte. Those are operations you may need to do frequently (and are shown in the StringCaseChanging example on this book's Web site).

## Chapter 4: Smooth Operators

### In This Chapter

- ✔ Performing a little arithmetic
- ✔ Doing some logical arithmetic
- ✔ Complicating matters with compound logical operators

**M**athematicians create variables and manipulate them in various ways, adding them, multiplying them, and — here's a toughie — even integrating them. Chapter 2 of this minibook describes how to declare and define variables. However, it says little about how to use variables to get anything done after you declare them. This chapter looks at the operations you can perform on variables to do some work. Operations require *operators*, such as `+`, `-`, `=`, `<`, and `&`. I cover arithmetic, logical, and other types of operators in this chapter.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_98_0.png)

Writing programs that get things done is good. You'll never make it as a C# programmer if your programs don't do something — unless, of course, you're a consultant.

## Performing Arithmetic

The set of arithmetic operators breaks down into several groups: the simple arithmetic operators, the assignment operators, and a set of special operators unique to programming. After you digest these, you also need to digest a separate set of logical operators. *Bon appétit!*

### Simple operators

You most likely learned in elementary school how to use most of the simple operators. Table 4-1 lists them. **Note:** Computers use an asterisk (\*), not the multiplication sign (×), for multiplication.

**Table 4-1** Simple Operators

| Operator | What It Means |
|---|---|
| - (unary) | Take the negative of |
| * | Multiply |
| / | Divide |
| + | Add |
| - (binary) | Subtract |
| % | Modulo |

Most of these operators in the table are *binary* operators because they operate on two values: one on the left side of the operator and one on the right side. The lone exception is the unary negative. However, it’s just as straightforward as the others, as shown in this example:

```
int n1 = 5;
int n2 = -n1;   // n2 now has the value -5.
```

The value of `-n` is the negative of the value of `n`.

The modulo operator may not be quite as familiar to you as the others. Modulo is similar to the remainder after division. Thus, 5 % 3 is 2 (5 / 3 = 1, remainder 2), and 25 % 3 is 1 (25 / 3 = 8, remainder 1). Read it “five modulo three” or simply “five mod three.” Even numbers mod 2 are 0: 6 % 2 = 0 (6/2 = 3, remainder 0).

The arithmetic operators other than modulo are defined for all numeric types. The modulo operator isn’t defined for floating-point numbers because you have no remainder after the division of floating-point values.

### Operating orders

The value of some expressions may not be clear. Consider, for example, the following expression:

```
int n = 5 * 3 + 2;
```

Does the programmer mean “multiply 5 times 3 and then add 2,” which is 17, or “multiply 5 times the sum of 3 and 2,” which gives you 25?

C# generally executes common operators from left to right. So, the preceding example assigns the value 17 to the variable `n`.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_99_0.png)

The logical comparisons are defined for all numeric types, including float, double, decimal, and char. All the following statements are legal:

```csharp
bool b;
b = 3 > 2;        // true
b = 3.0 > 2.0;    // true
b = 'a' > 'b';    // false -- Alphabetically, later is greater.
b = 'A' < 'a';    // true -- Upper A is less than lower a.
b = 'A' < 'b';    // true -- All upper are less than all lower.
b = 10M > 12M;    // false
```

The comparison operators always produce results of type bool. The comparison operators other than == are not valid for variables of type string. (Not to worry: C# offers other ways to compare strings.)

## Comparing floating-point numbers: Is your float bigger than mine?

Comparing two floating-point values can get dicey, and you need to be careful with these comparisons. Consider the following comparison:

```csharp
float f1;
float f2;
f1 = 10;
f2 = f1 / 3;
bool b1 = (3 * f2) == f1; // b1 is true if (3 * f2) equals f1.
f1 = 9;
f2 = f1 / 3;
bool b2 = (3 * f2) == f1;
```

Notice that both the fifth and eighth lines in the preceding example contain first an assignment operator (=) and then a logical comparison (==). These are different animals, so don't type = when you mean ==. C# does the logical comparison and then assigns the result to the variable on the left.

The only difference between the calculations of b1 and b2 is the original value of f1. So, what are the values of b1 and b2? The value of b2 is clearly true: 9 / 3 is 3; 3 * 3 is 9; and 9 equals 9. Voilà!

The value of b1 isn't obvious: 10 / 3 is 3.333 . . . and 3.333 . . . * 3 is 9.999 . . . , 9.999 . . . equal to 10? That depends on how clever your processor and compiler are. On a Pentium or later processor, C# isn't smart enough to realize that b1 should be true if the calculations are moved away from the comparison.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_103_0.png)

You can use the system absolute value method to compare f1 and f2:

```csharp
Math.Abs(f1 - 3.0 * f2) < .00001; // Use whatever level of accuracy.
```

This calculation returns true for both cases. You can use the constant Double.Epsilon instead of .00001 to produce the maximum level of accuracy. Epsilon is the smallest possible difference between two nonzero double variables.

In this case, C# evaluates boolExpression1 and boolExpression2. It then looks to see whether they both are true before deciding the value of b. However, this may be a wasted effort. If one expression is false, there's no reason to perform the other. Regardless of the value of the second expression, the result will be false. Nevertheless, & goes on to evaluate both expressions.

The && operator avoids evaluating both expressions unnecessarily, as shown in the following example:

```
bool b = (boolExpression1) && (boolExpression2);
```

In this case, C# evaluates boolExpression1. If it's false, then b is set to false and the program continues on its merry way. On the other hand, if boolExpression1 is true, then C# evaluates boolExpression2 and stores the result in b. The && operator uses this short-circuit evaluation because it short-circuits around the second Boolean expression, if necessary.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_105_0.png)

Most programmers use the doubled forms most of the time.

The || operator works the same way, as shown in the following expression:

```
bool b = (boolExpression1) || (boolExpression2);
```

If boolExpression1 is true, there's no point in evaluating boolExpression2 because the result is always true.

You can read these operators as "short-circuit and" and "short-circuit or."

## Matching Expression Types at TrackDownAMate.com

In calculations, an expression's type is just as important as its value. Consider the following expression:

```
int n;
n = (5 * 5) + 7;
```

My calculator says the resulting value of n is 32. However, that expression also has an overall type based on the types of its parts.

Written in "type language," the preceding expression becomes

```
int [=] (int * int) + int;
```

To evaluate the type of an expression, follow the same pattern you use to evaluate the expression's value. Multiplication takes precedence over addi-

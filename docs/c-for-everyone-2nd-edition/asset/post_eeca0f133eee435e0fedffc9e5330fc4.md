
## Programming Tip 3.3

![](img/23fb3582e93ebc95909e1de029c3d388_108_0.png)

### Tabs

Block-structured code has the property that nested statements are indented by one or more levels:

```cpp
int main()
{
   int floor;
   ...
   if (floor > 13)
   {
      floor--;
   }
   ...
   return 0;
}
```

0 1 2 Indentation level

How do you move the cursor from the leftmost column to the appropriate indentation level? A perfectly reasonable strategy is to hit the space bar a sufficient number of times. However, many programmers use the Tab key instead. A tab moves the cursor to the next indentation level.

![](img/23fb3582e93ebc95909e1de029c3d388_108_1.png)

You use the Tab key to move the cursor to the next indentation level.

While the Tab key is nice, some editors use tab characters for alignment, which is not so nice. Tab characters can lead to problems when you send your file to another person or a printer. There is no universal agreement on the width of a tab character, and some software will ignore tabs altogether. It is therefore best to save your files with spaces instead of tabs. Most editors have a setting to automatically convert all tabs to spaces. Look at the documentation of your development environment to find out how to activate this useful setting.

## Special Topic 3.1

![](img/23fb3582e93ebc95909e1de029c3d388_108_2.png)

### The Selection Operator

C++ has a selection operator of the form

```cpp
condition ? value1 : value2
```

The value of that expression is either value1 if the test passes or value2 if it fails. For example, we can compute the actual floor number as

```cpp
actual_floor = floor > 13 ? floor - 1 : floor;
```

which is equivalent to

```cpp
if (floor > 13)
{
   actual_floor = floor - 1;
}
else
{
   actual_floor = floor;
}
```

You can use the selection operator anywhere that a value is expected, for example:

```cpp
cout << "Actual floor: " << (floor > 13 ? floor - 1 : floor);
```

We don't use the selection operator in this book, but it is a convenient construct that you will find in many C++ programs.

## Programming Tip 3.4

### Avoid Duplication in Branches

![](img/23fb3582e93ebc95909e1de029c3d388_109_0.png)

Look to see whether you *duplicate code* in each branch. If so, move it out of the if statement. Here is an example of such duplication:

```cpp
if (floor > 13)
{
   actual_floor = floor - 1;
   cout << "Actual floor: " << actual_floor << endl;
}
else
{
   actual_floor = floor;
   cout << "Actual floor: " << actual_floor << endl;
}
```

The output statement is exactly the same in both branches. This is not an error—the program will run correctly. However, you can simplify the program by moving the duplicated statement, like this:

```cpp
if (floor > 13)
{
   actual_floor = floor - 1;
}
else
{
   actual_floor = floor;
}
cout << "Actual floor: " << actual_floor << endl;
```

Removing duplication is particularly important when programs are maintained for a long time. When there are two sets of statements with the same effect, it can easily happen that a programmer modifies one set but not the other.

## 3.2 Comparing Numbers and Strings

Relational operators (< > <= >= == !=) are used to compare numbers and strings.

Every if statement contains a condition. In many cases, the condition involves comparing two values. For example, in the previous examples we tested floor > 13. The comparison > is called a relational operator. C++ has six relational operators (see Table 1).

Table 1. Relational Operators

| C++ | Math Notation | Description |
|---|---|---|
| `>` | `>` | Greater than |
| `>=` | `≥` | Greater than or equal |
| `<` | `<` | Less than |
| `<=` | `≤` | Less than or equal |
| `==` | `=` | Equal |
| `!=` | `≠` | Not equal |

As you can see, only two C++ relational operators (< and >) look as you would expect from the mathematical notation. Computer keyboards do not have keys for ≤, ≥, or ≠, but the <=, >=, and != operators are easy to remember because they look similar. The == operator is initially confusing to most newcomers to C++. In C++, = already has a meaning, namely assignment.

![](img/23fb3582e93ebc95909e1de029c3d388_109_1.png)

In C++, you use a relational operator to check whether one value is greater than another.

The `==` operator denotes equality testing:

```cpp
floor = 13; // Assign 13 to floor
if (floor == 13)  // Test whether floor equals 13
```

You must remember to use `==` inside tests and to use `=` outside tests. (See Common Error 3.2 on page 85 for more information.)

You can compare strings as well:

```cpp
if (input == "Quit") ...
```

Use `!=` to check whether two strings are different. In C++, letter case matters. For example, "Quit" and "quit" are not the same string.

### Syntax 3.2 — Comparisons

![](img/23fb3582e93ebc95909e1de029c3d388_110_0.png)

Table 2 Relational Operator Examples

| Expression | Value | Comment |
| :--- | :--- | :--- |
| 3 <= 4 | true | 3 is less than 4; <= tests for "less than or equal". |
| 3 =< 4 | Error | The "less than or equal" operator is <=, not =<. The "less than" symbol comes first. |
| 3 > 4 | false | > is the opposite of <=. |
| 4 < 4 | false | The left-hand side must be strictly smaller than the right-hand side. |
| 4 <= 4 | true | Both sides are equal; <= tests for "less than or equal". |
| 3 == 5 - 2 | true | == tests for equality. |
| 3 != 5 - 1 | true | != tests for inequality. It is true that 3 is not 5 - 1. |
| 3 = 6 / 2 | Error | Use == to test for equality. |
| 1.0 / 3.0 == 0.33333333 | false | Although the values are very close to one another, they are not exactly equal. See Common Error 3.3 on page 86. |
| "10" > 5 | Error | You cannot compare a string to a number. |

Table 2 summarizes how to use relational operators in C++.

![](img/23fb3582e93ebc95909e1de029c3d388_111_0.png)

- 6. Which of the following conditions are true, provided a is 3 and b is 4?
  - a. a + 1 <= b
  - b. a + 1 >= b
  - c. a + 1 != b
- 7. Give the opposite of the condition

  `floor > 13`
- 8. What is the error in this statement?

  ```cpp
  if (score_a = score_b)
  {
      cout << "Tie" << endl;
  }
  ```
- 9. Supply a condition in this if statement to test whether the user entered a Y:

  ```cpp
  string input;
  cout << "Enter Y to quit." << endl;
  cin >> input;
  if (...)
  {
      cout << "Goodbye." << endl;
      return 0;
  }
  ```

## Common Error 3.3

### Exact Comparison of Floating-Point Numbers

Floating-point numbers have only a limited precision, and calculations can introduce roundoff errors. You must take these inevitable roundoffs into account when comparing floating-point numbers. For example, the following code multiplies the square root of 2 by itself. Ideally, we expect to get the answer 2:

```cpp
double r = sqrt(2.0);
if (r * r == 2)
{
    cout << "sqrt(2) squared is 2" << endl;
}
else
{
    cout << "sqrt(2) squared is not 2 but "
         << setprecision(18) << r * r << endl;
}
```

This program displays

```text
sqrt(2) squared is not 2 but 2.0000000000000004
```

It does not make sense in most circumstances to compare floating-point numbers exactly. Instead, we should test whether they are close enough. That is, the magnitude of their difference should be less than some threshold. Mathematically, we would write that x and y are close enough if

$$|x - y| < \varepsilon$$

for a very small number, $\varepsilon$. $\varepsilon$ is the Greek letter epsilon, a letter used to denote a very small quantity. It is common to set $\varepsilon$ to $10^{-14}$ when comparing double numbers:

```cpp
const double EPSILON = 1E-14;
double r = sqrt(2.0);
if (fabs(r * r - 2) < EPSILON)
{
    cout << "sqrt(2) squared is approximately 2";
}
```

Include the <cmath> header to use the fabs function.

![](img/23fb3582e93ebc95909e1de029c3d388_113_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_113_1.png)

*Take limited precision into account when comparing floating-point numbers.*

## Special Topic 3.2

### Lexicographic Ordering of Strings

If you compare strings using < or >, they are compared in “lexicographic” order. This ordering is very similar to the way in which words are sorted in a dictionary.

For example, consider this code fragment.

```cpp
string name = "Tom";
if (name < "Dick") ...
```

The condition is not fulfilled, because in the dictionary Dick comes before Tom. There are a few differences between the ordering in a dictionary and in C++. In C++:

- All uppercase letters come before the lowercase letters. For example, "Z" comes before "a".

![](img/23fb3582e93ebc95909e1de029c3d388_113_2.png)

*To see which of two terms comes first in the dictionary, consider the first letter in which they differ.*

![](img/23fb3582e93ebc95909e1de029c3d388_113_3.png)

operand. The unary logical negation operator is placed *before* a condition when we are interested in choosing a path of execution if the original condition (without the logical negation operator) is false, such as in the following program segment:

```
if ( !( grade == sentinelValue ) )
    cout << "The next grade is " << grade << endl;
```

The parentheses around the condition grade == sentinelValue are needed because the logical negation operator has a higher precedence than the equality operator.

You can often avoid the ! operator by using an appropriate relational or equality operator. For example, the preceding if statement also can be written as follows:

```
if ( grade != sentinelValue )
    cout << "The next grade is " << grade << endl;
```

This flexibility often can help you express a condition in a more “natural” or convenient manner. Figure 5.17 is a truth table for the logical negation operator (!).

| expression | !expression |
|---|---|
| false | true |
| true | false |

**Fig. 5.17**  |  !(logical negation) operator truth table.

# *Logical Operators Example*

Figure 5.18 demonstrates the logical operators by producing their truth tables. The output shows each expression that’s evaluated and its bool result. By default, bool values true and false are displayed by cout and the stream insertion operator as 1 and 0, respectively. We use **stream manipulator boolalpha** (a sticky manipulator) in line 9 to specify that the value of each bool expression should be displayed as either the word “true” or the word “false.” For example, the result of the expression false && false in line 10 is false, so the second line of output includes the word “false.” Lines 9–13 produce the truth table for &&. Lines 16–20 produce the truth table for ||. Lines 22–25 produce the truth table for !.

```
1  // Fig. 5.18: fig05_18.cpp
2  // Logical operators.
3  #include <iostream>
4  using namespace std;
5
6  int main()
7  {
8     // create truth table for && (logical AND) operator
9     cout << boolalpha << "Logical AND (&&)"
10        << "\nfalse && false: " << ( false && false )
11        << "\nfalse && true:  " << ( false && true )
12        << "\ntrue && false:  " << ( true && false )
13        << "\ntrue && true:   " << ( true && true ) << "\n\n";
```

**Fig. 5.18**  |  Logical operators. (Part 1 of 2.)
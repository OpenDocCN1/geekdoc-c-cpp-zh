

```cpp
if (ch == 'A')
    a_grade++;          // alternative #1
else
    if (ch == 'B')      // alternative #2
        b_grade++;      // subalternative #2a
    else
        soso++;         // subalternative #2b
```

If ch is not 'A', the program goes to the else. Then a second if else subdivides that alternative into two more choices. C++’s free formatting enables you to arrange these elements into an easier-to-read format:

```cpp
if (ch == 'A')
    a_grade++;          // alternative #1
else if (ch == 'B')     // alternative #2
    b_grade++;
else
    soso++;             // alternative #3
```

This looks like a new control structure—an if else if else structure. But actually it is one if else contained within a second. This revised format looks much cleaner, and it enables you to skim through the code to pick out the different alternatives. This entire construction still counts as one statement.

Listing 6.3 uses this preferred formatting to construct a modest quiz program.

### Listing 6.3 **ifelseif.cpp**

```cpp
// ifelseif.cpp -- using if else if else
#include <iostream>
const int Fave = 27;
int main()
{
    using namespace std;
    int n;

    cout << "Enter a number in the range 1-100 to find ";
    cout << "my favorite number: ";
    do
    {
        cin >> n;
        if (n < Fave)
            cout << "Too low -- guess again: ";
        else if (n > Fave)
            cout << "Too high -- guess again: ";
        else
            cout << Fave << " is right!\n";
    } while (n != Fave);
    return 0;
}
```

Here’s some sample output from the program in Listing 6.3:

```text
Enter a number in the range 1-100 to find my favorite number: 50
Too high -- guess again: 25
Too low -- guess again: 37
Too high -- guess again: 31
Too high -- guess again: 28
Too high -- guess again: 27
27 is right!
```

## Conditional Operators and Bug Prevention

Many programmers reverse the more intuitive expression `variable == value` to `value == variable` in order to catch errors where the equality is mistyped as an assignment operator. For example, entering the conditional as follows is valid and will work properly:

```cpp
if (3 == myNumber)
```

However, if you happen to mistype as follows, the compiler will generate an error message because it believes you are attempting to assign a value to a literal (3 always equals 3 and can’t be assigned another value):

```cpp
if (3 = myNumber)
```

Suppose you made a similar mistake, using the former notation:

```cpp
if (myNumber = 3)
```

The compiler would simply assign the value 3 to myNumber, and the block within the if would run—a very common error, and a difficult error to find. (However, many compilers will issue a warning, which you would be wise to heed.) As a general rule, writing code that allows the compiler to find errors is much easier than repairing the causes of mysterious faulty results.

## Logical Expressions

Often you must test for more than one condition. For example, for a character to be a lowercase letter, its value must be greater than or equal to 'a' and less than or equal to 'z'. Or, if you ask a user to respond with a y or an n, you want to accept uppercase (Y and N) as well as lowercase. To meet this kind of need, C++ provides three logical operators to combine or modify existing expressions. The operators are logical OR, written `||`; logical AND, written `&&`; and logical NOT, written `!`. Let’s examine them now.

### The Logical OR Operator: `||`

In English, the word or can indicate when one or both of two conditions satisfy a requirement. For example, you can go to the MegaMicro company picnic if you or your spouse work for MegaMicro, Inc. The C++ equivalent is the logical OR operator, written `||`. This operator combines two expressions into one. If either or both of the original expressions is true, or nonzero, the resulting expression has the value true. Otherwise, the expression has the value false. Here are some examples:

```cpp
5 == 5 || 5 == 9   // true because first expression is true
5 > 3 || 5 > 10   // true because first expression is true
5 > 8 || 5 < 10   // true because second expression is true
5 < 8 || 5 > 2   // true because both expressions are true
5 > 8 || 5 < 2   // false because both expressions are false
```

Because the `||` has a lower precedence than the relational operators, you don’t need to use parentheses in these expressions. Table 6.1 summarizes how the `||` operator works.

Table 6.1 **The `||` Operator**

| The Value of `expr1` &#124;&#124; `expr2` | `expr1 == true` | `expr1 == false` |
|---|---:|---:|
| `expr2 == true` | true | true |
| `expr2 == false` | true | false |

C++ provides that the `||` operator is a *sequence point*. That is, any value changes indicated on the left side take place before the right side is evaluated. (Or in the newer parlance of C++11, the subexpression to the left of the operator is sequenced before the subexpression to the right.) For example, consider the following expression:

```cpp
i++ < 6 || i == j
```

Suppose i originally has the value 10. By the time the comparison with j takes place, i has the value 11. Also C++ won’t bother evaluating the expression on the right if the expression on the left is true, for it only takes one true expression to make the whole logical expression true. (The semicolon and the comma operator, recall, are also sequence points.)

Listing 6.4 uses the `||` operator in an `if` statement to check for both uppercase and lowercase versions of a character. Also it uses C++’s string concatenation feature (see Chapter 4, “Compound Types”) to spread a single string over three lines.

### Listing 6.4 **or.cpp**

```cpp
// or.cpp -- using the logical OR operator
#include <iostream>
int main()
{
    using namespace std;
    cout << "This program may reformat your hard disk\n"
         "and destroy all your data.\n"
         "Do you wish to continue? <y/n> ";
    char ch;
    cin >> ch;
    if (ch == 'y' || ch == 'Y')                 // y or Y
        cout << "You were warned!\a\n";
    else if (ch == 'n' || ch == 'N')            // n or N
        cout << "A wise choice ... bye\n";
    else
        cout << "That wasn't a y or n! Apparently you "
                "can't follow instructions, so "
                "I'll crash your disk anyway.\a\a\a\n";
    return 0;
}
```

(The program doesn't really carry out any threats.) Here is a sample run of the program in Listing 6.4:

```text
This program may reformat your hard disk
and destroy all your data.
Do you wish to continue? <y/n> N
A wise choice ... bye
```

The program reads just one character, so only the first character in the response matters. That means the user could have input NO instead of N. The program would just read the N. But if the program tried to read more input later, it would start at the o.

### The Logical AND Operator: &&

The logical AND operator, written &&, also combines two expressions into one. The resulting expression has the value true only if both of the original expressions are true. Here are some examples:

```cpp
5 == 5 && 4 == 4    // true because both expressions are true
5 == 3 && 4 == 4    // false because first expression is false
5 > 3 && 5 > 10     // false because second expression is false
5 > 8 && 5 < 10     // false because first expression is false
5 < 8 && 5 > 2      // true because both expressions are true
5 > 8 && 5 < 2      // false because both expressions are false
```

Because the && has a lower precedence than the relational operators, you don’t need to use parentheses in these expressions. Like the || operator, the && operator acts as a sequence point, so the left side is evaluated, and any side effects are carried out before the right side is evaluated. If the left side is false, the whole logical expression must be false, so C++ doesn’t bother evaluating the right side in that case. Table 6.2 summarizes how the && operator works.

Table 6.2 **The && Operator**

|  | `expr1 == true` | `expr1 == false` |
|---|---|---|
| `expr2 == true` | true | false |
| `expr2 == false` | false | false |

Listing 6.5 shows how to use `&&` to cope with a common situation, terminating a while loop, for two different reasons. In the listing, a while loop reads values into an array. One test (`i < ArSize`) terminates the loop when the array is full. The second test (`temp >= 0`) gives the user the option of quitting early by entering a negative number. The program uses the `&&` operator to combine the two tests into a single condition. The program also uses two `if` statements, an `if else` statement, and a `for` loop, so it demonstrates several topics from this chapter and Chapter 5.

### Listing 6.5 **and.cpp**

```cpp
// and.cpp -- using the logical AND operator
#include <iostream>
const int ArSize = 6;
int main()
{
    using namespace std;
    float naaq[ArSize];
    cout << "Enter the NAAQs (New Age Awareness Quotients) "
         << "of\nyour neighbors. Program terminates "
         << "when you make\n" << ArSize << " entries "
         << "or enter a negative value.\n";

    int i = 0;
    float temp;
    cout << "First value: ";
    cin >> temp;
    while (i < ArSize && temp >= 0) // 2 quitting criteria
    {
        naaq[i] = temp;
        ++i;
        if (i < ArSize)              // room left in the array
        {
            cout << "Next value: ";
            cin >> temp;             // so get next value
        }
    }
    if (i == 0)
        cout << "No data--bye\n";
```


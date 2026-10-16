
I get a new value for `again` from the user in the loop body. Then I test again in the loop expression. If `again` is equal to `'y'`, the loop repeats; otherwise, the loop ends.

### In the Real World

Even though you can use `while` and `do` loops pretty interchangeably, most programmers use the `while` loop. Although a `do` loop might seem more natural in some cases, the advantage of a `while` loop is that its expression appears right at the top of the loop; you don’t have to go hunting to the bottom of the loop to find it.

### Trap

If you’ve ever had a game get stuck in the same endless cycle, you might have experienced an infinite loop—a loop without end. Here’s a simple example of an infinite loop:

```cpp
int test = 10;
while (test == 10)
{
    cout << test;
}
```

In this case, the loop is entered because test is 10. But because test never changes, the loop will never stop. As a result, the user will have to kill the running program to end it. The moral of this story? Make sure that the expression of a loop can eventually become false or that there’s another way for the loop to end, such as described in the following section, “Using break and continue Statements.”

## USING BREAK AND CONTINUE STATEMENTS

It’s possible to alter the behavior you’ve seen in loops. You can immediately exit a loop with the `break` statement, and you can jump directly to the top of a loop with a `continue` statement. Although you should use these powers sparingly, they do come in handy sometimes.

### Introducing the Finicky Counter Program

The Finicky Counter program counts from 1 to 10 through a `while` loop. It’s finicky because it doesn’t like the number 5—it skips it. Figure 2.8 shows a run of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 2 folder; the filename is finicky_counter.cpp.

**Figure 2.8.** The number 5 is skipped with a continue statement, and the loop ends with a break statement.

![](img/34f09be0ed6217c465debc4490197d4f_81_0.png)

```cpp
// Finicky Counter
// Demonstrates break and continue statements

#include <iostream>

using namespace std;

int main()
{
    int count = 0;
    while (true)
    {
        count += 1;

        // end loop if count is greater than 10
        if (count > 10)
        {
            break;
        }
    }
```

### Using the continue Statement to Jump Back to the Top of a Loop

Just before count is displayed, I included the lines:

```cpp
// skip the number 5
if (count == 5)
{
    continue;
}
```

The `continue` statement means “jump back to the top of the loop.” At the top of the loop, the `while` expression is tested and the loop is entered again if it’s true. So when `count` is equal to 5, the program does not get to the `cout << count << endl;` statement. Instead, it goes right back to the top of the loop. As a result, 5 is skipped and never displayed.

### Understanding When to Use break and continue

You can use `break` and `continue` in any loop you create; they aren’t just for `while (true)` loops. But you should use them sparingly. Both `break` and `continue` can make it harder for programmers to see the flow of a loop.

## USING LOGICAL OPERATORS

So far you’ve seen pretty simple expressions evaluated for their truth or falsity. However, you can combine simpler expressions with logical operators to create more complex expressions. Table 2.2 lists the logical operators.

**Table 2.2: Logical Operators**

| Operator | Description | Sample Expression |
| --- | --- | --- |
| ! | Logical NOT | !expression |
| && | Logical AND | expression1 && expression2 |
| \|\| | Logical OR | expression1 \|\| expression2 |

### Introducing the Designers Network Program

The Designers Network program simulates a computer network in which only a select group of game designers are members. Like real-world computer systems,

![](img/34f09be0ed6217c465debc4490197d4f_85_0.png)

**Figure 2.11.** Looks like one of the elite logged in today.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 2 folder; the filename is designers_network.cpp.

```cpp
// Designers Network
// Demonstrates logical operators

#include <iostream>
#include <string>
using namespace std;

int main()
{
    string username;
    string password;
    bool success;

    cout << "\tGame Designer's Network\n";

    do
    {
        cout << "\nUsername: ";
        cin >> username;

        cout << "Password: ";
        cin >> password;

        if (username == "S.Meier" && password == "civilization")
        {
            cout << "\nHey, Sid.";
            success = true;
        }

        else if (username == "S.Miyamoto" && password == "mariobros")
        {
            cout << "\nWhat's up, Shigeru?";
            success = true;
        }

        else if (username == "W.Wright" && password == "thesims")
        {
            cout << "\nHow goes it, Will?";
            success = true;
        }

        else if (username == "guest" || password == "guest")
        {
            cout << "\nWelcome, guest.";
            success = true;
        }

        else
        {
            cout << "\nYour login failed.";
            success = false;
        }
    } while (!success);

    return 0;
}
```

### Using the Logical AND Operator

The logical AND operator, `&&`, lets you join two expressions to form a larger one, which can be evaluated to `true` or `false`. The new expression is true only if the two expressions it joins are true; otherwise, it is false. Just as in English, “and” means both. Both original expressions must be true for the new expression to be true. Here’s a concrete example from the Designers Network program:

```cpp
if (username == "S.Meier" && password == "civilization")
```

The expression `username == "S.Meier" && password == "civilization"` is true only if both `username == "S.Meier"` and `password == "civilization"` are true. This works perfectly because I only want to grant Sid access if he enters both his username and his password. Just one or the other won’t do.

Another way to understand how `&&` works is to look at all of the possible combinations of truth and falsity (see Table 2.3).

**Table 2.3** Possible Login Combinations Using the AND Operator

| username == "S.Meier" | password == "civilization" | username == "S.Meier" && password == "civilization" |
| --- | --- | --- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

Of course, the Designers Network program works for other users besides Sid Meier. Through a series of `if` statements with `else` clauses using the `&&` operator, the program checks three different username and password pairs. If a user enters a recognized pair, he is personally greeted.

### Using the Logical OR Operator

The logical OR operator, `||`, lets you join two expressions to form a larger one, which can be evaluated to `true` or `false`. The new expression is true if the first expression or the second expression is true; otherwise, it is false. Just as in English, “or” means either. If either the first or second expression is true, then the new expression is true. (If both are true, then the larger expression is still true.) Here’s a concrete example from the Designers Network program:

```cpp
else if (username == "guest" || password == "guest")
```

The expression `username == "guest" || password == "guest"` is true if `username == "guest"` is true or if `password == "guest"` is true. This works perfectly because I want to grant a user access as a guest as long as he enters guest for the username or password. If the user enters guest for both, that’s fine too.

Another way to understand how `||` works is to look at all of the possible combinations of truth and falsity (see Table 2.4).

| username == "guest" | password == "guest" | username == "guest" \|\| password == "guest" |
| --- | --- | --- |
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

### Using the Logical NOT Operator

The logical NOT operator, `!`, lets you switch the truth or falsity of an expression. The new expression is true if the original is false; the new expression is false if the original is true. Just as in English, “not” means the opposite. The new expression has the opposite value of the original.

```cpp
} while (!success);
```

The expression `!success` is true when `success` is false. That works perfectly because `success` is false only when there has been a failed login. In that case,

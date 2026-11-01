
![](img/c7e8651578bccd573227f684823b8754_77_0.png)

**Figure 2.6**

The repetition is accomplished using a while loop.

```cpp
// Play Again
// Demonstrates while loops

#include <iostream>
using namespace std;

int main()
{
    char again = 'y';
    while (again == 'y')
    {
        cout << "\n**Played an exciting game**";
        cout << "\nDo you want to play again? (y/n): ";
        cin >> again;
    }

    cout << "\nOkay, bye.";

    return 0;
}
```

## Looping with a while Loop

The first thing the program does in the `main()` function is declare the char variable named `again` and initialize it to `'y'`. Then the program begins the while loop by testing `again` to see whether it’s equal to `'y'`. Because it is, the program displays the message “**Played an exciting game**,” asks the user whether he wants to play again, and stores the reply in `again`. The loop continues as long as the user enters y.

You’ll notice that I had to initialize `again` before the loop because the variable is used in the loop expression. Because a while loop evaluates its expressions before its loop body (the group of statements that repeat), you have to make sure that any variables in the expression have a value before the loop begins.

## Using do Loops

Like while loops, do loops let you repeat a section of code based on an expression. The difference is that a do loop tests its expression after each loop iteration. This means that the loop body is always executed at least once. Here’s a generic form of a do loop:

```cpp
do
    statement;
while (expression);
```

The program executes `statement` and then, as long as `expression` tests true, the loop repeats. Once `expression` tests false, the loop ends.

### Introducing the Play Again 2.0 Program

The Play Again 2.0 program looks exactly the same to the user as the original Play Again program. Play Again 2.0, like its predecessor, simulates the play of an exciting game by displaying the message “**Played an exciting game**” and asking the user whether he wants to play again. The user continues to play as long as he enters y. This time, though, the program accomplishes the repetition using a do loop. Figure 2.7 shows off the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 2 folder; the filename is play_again2.cpp.

```cpp
// Play Again 2.0
// Demonstrates do loops

#include <iostream>
```

new value for again from the user in the loop body. Then I test again in the loop expression. If again is equal to 'y', the loop repeats; otherwise, the loop ends.

### IRW

Even though you can use while and do loops pretty interchangeably, most programmers use the while loop. Although a do loop might seem more natural in some cases, the advantage of a while loop is that its expression appears right at the top of the loop; you don’t have to go hunting to the bottom of the loop to find it.

### Trap

If you’ve ever had a game get stuck in the same endless cycle, you might have experienced an infinite loop—a loop without end. Here’s a simple example of an infinite loop:

```cpp
int test = 10;
while (test == 10)
{
    cout << test;
}
```

In this case, the loop is entered because test is 10. But because test never changes, the loop will never stop. As a result, the user will have to kill the running program to end it. The moral of this story? Make sure that the expression of a loop can eventually become false or that there’s another way for the loop to end, such as described in the following section, “Using break and continue statements.”

## Using break and continue Statements

It’s possible to alter the behavior you’ve seen in loops. You can immediately exit a loop with the `break` statement, and you can jump directly to the top of a loop with a `continue` statement. Although you should use these powers sparingly, they do come in handy sometimes.

### Introducing the Finicky Counter Program

The Finicky Counter program counts from 1 to 10 through a while loop. It’s finicky because it doesn’t like the number 5—it skips it. Figure 2.8 shows a run of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 2 folder; the filename is finicky_counter.cpp.

```cpp
//skip the number 5
if (count == 5)
{
    continue;
}

cout << count << endl;
}

return 0;
}
```

### Creating a while (true) Loop

I set up the loop with the following line:

```cpp
while (true)
```

Technically, this creates an infinite loop. This might seem odd coming so soon after a warning to avoid infinite loops, but this particular loop isn’t really infinite because I put an exit condition in the loop body.

> **Hint**
>
> Although a while (true) loop sometimes can be clearer than a traditional loop, you should also try to minimize your use of these loops.

### Using the break Statement to Exit a Loop

This is the exit condition I put in the loop:

```cpp
//end loop if count is greater than 10
if (count > 10)
{
    break;
}
```

Because count is increased by 1 each time the loop body begins, it will eventually reach 11. When it does, the break statement (which means “break out of the loop”) is executed and the loop ends.

### Using the continue Statement to Jump Back to the Top of a Loop

Just before count is displayed, I included the lines:

```cpp
//skip the number 5
if (count == 5)
{
    continue;
}
```

The continue statement means “jump back to the top of the loop.” At the top of the loop, the while expression is tested and the loop is entered again if it’s true. So when count is equal to 5, the program does not get to the `cout << count << endl;` statement. Instead, it goes right back to the top of the loop. As a result, 5 is skipped and never displayed.

### Understanding When to Use break and continue

You can use `break` and `continue` in any loop you create; they aren’t just for while (true) loops. But you should use them sparingly. Both `break` and `continue` can make it harder for programmers to see the flow of a loop.

## Using Logical Operators

So far you’ve seen pretty simple expressions evaluated for their truth or falsity. However, you can combine simpler expressions with logical operators to create more complex expressions. Table 2.2 lists the logical operators.

**Table 2.2 Logical Operators**

| Operator | Description | Sample Expression |
| --- | --- | --- |
| ! | Logical NOT | !expression |
| && | Logical AND | expression1 && expression2 |
| \|\| | Logical OR | expression1 \|\| expression2 |

### Introducing the Designers Network Program

The Designers Network program simulates a computer network in which only a select group of game designers are members. Like real-world computer systems,

![](img/c7e8651578bccd573227f684823b8754_85_0.png)

**Figure 2.11**

Looks like one of the elite logged in today.

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

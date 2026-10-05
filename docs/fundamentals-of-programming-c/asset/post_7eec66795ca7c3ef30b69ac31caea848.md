
## 6.3. ABNORMAL LOOP TERMINATION

```cpp
while (true) {
    cin >> input;
    if (input < 0)
        break; // Exit loop immediately
    sum += input;
}
cout << "Sum = " << sum << endl;
```

The condition of the while in Listing 6.14 (addmiddleexit.cpp) is a typo. This means the condition is true and never false. When the program executes the while statement it is guaranteed to enter the loop's body and the while loop itself does not provide a way to escape. If statement in the loop's body:

```cpp
if (input < 0) // Is input negative
    break; // exit the loop immediately
```

provides the necessary entry. In this case the break statement, executed conditionally on the value of the variable input, in Listing 6.14 (addmiddleexit.cpp) the break statement executes only when the user enters a negative number. When the program encounters the break statement it immediately jumps out of the loop. Any statements following the break within the loop's body are skipped. Since the statement

```cpp
sum += input; // Accumulate user input
```

appears after the break, it is not possible to add a negative number to the sum variable.

Some designers believe that programmers use the break statement strangely because it deviates from the normal loop control logic. Ideally, every loop should have a single entry point and single exit point. Listing 6.14 (addnone.cpp) has a single exit point (the break statement), some programmers use break statements within while statements in which the condition for the while is not a tautology. Adding a break statement to such a loop adds an exit point (the top of the loop) where the condition is false and the break statement is another. Using multiple break statements in a single loop is potentially dangerous and you should avoid that much.

Why have the break statement at all if it is useful and is it dispensable? The logic in Listing 6.4 (addnegatives.cpp) is fairly simple, so the restructuring of Listing 6.14 (addmiddleexit.cpp) might complicate the logic and be a bit awkward. As shown in Figure 6.4, a program that uses a break statement can be rewritten so that the break statement is not used. The nobreak introduces a Boolean variable, and the loop control is a little more complicated. The nobreak uses more memory (an extra variable) and more time to execute an extra check in the loop condition during every iteration of the loop. This extra memory is insignificant, and except for specialized applications, the extra execution time is imperceptible. In most cases, the most important issue is the more complicated the logic for a given section of code, the more difficult the code is to write correctly. In some situations, even though it violates the "single entry, single exit point" principle, a single break statement is unacceptable.

### 6.3.2 The Goto Statement

The break statement exits the loop in which it is located. A break statement is insufficient to jump completely out of the middle of a nested loop. The goto statement allows the program's execution flow

![](img/e326304bd50fbc4f7d5a64c1487eb635_139_0.png)

Figure 6.4: The code on the left generically represents any loop that uses a break statement. It is possible to transform the code on the left to eliminate the break statement, as the code on the right shows.

to jump to a specified location within the function. Listing 6.15 (exitnested.cpp) uses a goto statement to jump out from the middle of a nested loop.

# Listing 6.15: exitnested.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    // Compute some products
    int op1 = 2;
    while (op1 < 100) {
        int op2 = 2;
        while (op2 < 100) {
            if (op1 + op2 == 3731) {
                goto end;
            }
            cout << "Product is " << (op1 + op2) << endl;
            op2++;
        }
        op1++;
    }
end:
    cout << "The end" << endl;
}
```

When op1 * op2 is 3731, program flow will jump to the specified label within the program. In this example, the label is named end, but this name is arbitrary. Like variable names, label names should be chosen to indicate their intended purpose. The label named end comes after and outside the nested while loops.

A label's name is an identifier (see Section 3.3), and a label is distinguished by the colon that immediately follows its name. A label represents a target to which a goto can jump. A goto label may appear before a statement within a function.

With the goto statement, the while is superfluous; for example. Listing 6.2 (iterativecountoff.cpp) could be rewritten without the while statement as shown in Listing 6.16 (gotolop.cpp).

# Listing 6.16: gotolop.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    int count = 1;           // Initialize counter
top:
    if (count > 5) {
        goto end;
    }
    cout << count << endl;
    count++;
    goto top;
end:
    // Target is empty statement
}
```

Early programming languages like FORTRAN and early versions of BASIC forced to use goto statements. The problem with goto statements it is easy to develop program that is very difficult to understand. See Wikipedia about spaghetti (http://en.wikipedia.org/wiki/Spaghetti_code). The structured programming revolution of 1960s introduced constructs like the while statement and resulted in the disappearance of goto in most situations.

### 6.3.3 The Continue Statement

When a program encounters a continue statement inside a loop, it skips the rest of the loop and immediately checks the condition. The continue statement is similar to the break statement, except the continue statement does not exit the loop the condition remains true. Listing 6.17 (continueexample.cpp) shows the continue statement in action.

# Listing 6.17: continueexample.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    int input, sum = 0;
    bool done = false;
    while (!done) {
        cout << "Enter positive integer (999 quits): ";
        cin >> input;
        if (input < 0) {
            cout << "Negative value " << " ignored"
            << endl;
            continue; // Skip rest of body
        }
        if (input != 999) {
            cout << "Tallying " << endl;
            sum += input;
        } else {
            done = (input == 999); // 999 entry exits loop
        }
    }
    cout << "Sum = " << sum << endl;
}
```

Programmers do not use the continue statement as frequently as the break statement since it is easy to transform the code use into an equivalent that does not. Listing 6.18 (nocontinueexample.cpp) works exactly like Listing 6.17 (continueexample.cpp), but it avoids the continue statement.

# Listing 6.18: nocontinueexample.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    int input, sum = 0;
    bool done = false;
    while (!done) {
        cout << "Enter positive integer (999 quits): ";
        cin >> input;
        if (input < 0) {
            cout << "Negative value " << " ignored"
            << endl;
        } else {
            if (input != 999) {
                cout << "Tallying " << endl;
                sum += input;
            } else {
                done = (input == 999); // 999 entry exits loop
            }
        }
    }
    cout << "Sum = " << sum << endl;
}
```

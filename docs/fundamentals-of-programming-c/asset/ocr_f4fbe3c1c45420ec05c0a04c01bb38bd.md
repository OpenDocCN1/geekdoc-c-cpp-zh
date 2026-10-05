# 5.4. COMPOUND STATEMENTS

When checking for equality, as
if (x == 10)
    cout << "ten";

be sure to use the equality operator (===), not the assignment operator (=). Since an assignment statement has a value (see Section 4.3), C++ allows = within the conditional expression. It is, however, almost always makes sense when beginning programmers use = in this context. Visual++ at rating Level 4 checks for the use of assignment within a conditional expression; the default Level 3 does not.

# 5.4 Compound Statements

Sometimes you need to execute more than one statement based on a particular condition. Listing 5.3 (alternateddivision.cpp) how you must use curly braces to group multiple statements together into one compound statement.

```
Listing 5.3: alternateddivision.cpp
#include <iostream>

using namespace std;

int main() {
    int dividend, divisor, quotient;

    // Get two integers from the user
    cout << "Please enter two integers to divide:";
    cin >> dividend >> divisor;
    // If possible, divide them and report the result
    if (divisor != 0) {
        quotient = dividend / divisor;
        cout << dividend << " divided by " << divisor << " is "
        cout << quotient << endl;
    }
}
```

The assignment statement and printing statement are both part of the body of the if statement. Given the true value of the Boolean expression divisor != 0 during a particular program run, either both statements will be executed or neither will be executed.

A compound statement consists of zero or more statements grouped within curly braces. We say the curly braces define a block of statements. As a matter of style many programmers use curly braces to delimit the body of an if statement if the body contains only one statement:

```
if (x < 10) {
    y = x;
}
```

©2024 Richard L. Halterman Draft date: January 26, 2024
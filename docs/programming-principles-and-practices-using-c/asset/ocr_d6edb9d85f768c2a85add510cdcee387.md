```
    return 0;
}
```

That is, read a pair of values separated by an operator, such as 2+2, compute the result (in this case 4), and print the resulting value. We chose the variable names lval for left-hand value and rval for right-hand value.

This (sort of) works! So what if this program isn’t quite complete? It feels great to get something running! Maybe this programming and computer science stuff is easier than the rumors say. Well, maybe, but let’s not get too carried away by an early success. Let’s

+   1. Clean up the code a bit
2. Add multiplication and division (e.g., 2*3)
3. Add the ability to handle more than one operand (e.g., 1+2+3)

In particular, we know that we should always check that our input is reasonable (in our hurry, we “forgot”) and that testing a value against many constants is best done by a switch-statement rather than an if-statement.

The “chaining” of operations, such as 1+2+3+4, we will handle by adding the values as they are read; that is, we start with 1, see +2 and add 2 to 1 (getting an intermediate result 3), see +3 and add that 3 to our intermediate result (3), and so on. After a few false starts and after correcting a few syntax and logic errors, we get

```
#include "std_lib_facilities.h"
int main()
{
    cout << "Please enter expression (we can handle +,-,*,and /)\n";
    cout << "add an x to end expression (e.g., 1+2*3x): ";
    int lval = 0;
    int rval;
    cin>>lval;                          // read leftmost operand
    if (!cin) error("no first operand");
    for (char op; cin>>op;) {           // read operator and right-hand operand
                                        // repeatedly
        if (op!='x') cin>>rval;
        if (!cin) error("no second operand");
        switch(op) {
        case '+':
            lval += rval;               // add: lval = lval + rval
            break;
        case '-':
            lval -= rval;               // subtract: lval = lval - rval
            break;

```
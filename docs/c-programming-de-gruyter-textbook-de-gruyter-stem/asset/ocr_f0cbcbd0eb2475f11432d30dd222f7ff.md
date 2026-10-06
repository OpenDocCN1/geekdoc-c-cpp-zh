# 2.4 The Fundamental Control Structures of Algorithms — 55

```
case 4: cout << "Thursday" << endl;
break;
case 5: cout << "Friday" << endl;
break;
case 6: cout << "Saturday" << endl;
break;
default: cout << "Day of range Sunday .. Saturday" << endl;
break;
}
```

Running sample:

```
2
Tuesday
```

# 2.4.3 Loop Structure

There are three kinds of loop control structures in C++:

# 1. while statement

Syntax form:

```
while (expression) statement
```

Execution order: first evaluate the expression (loop condition); if it is true, execute the loop body (statement) and re-evaluate the expression; continue the cycle until expression becomes false. When using statement, generally there should be statements in the loop body that can change the value of expression, i.e., the loop condition, otherwise it will be an infinite loop (dead loop).

Figure 2.7 is the flow chart of a while statement.

When using while statement, generally there should be statements in the loop body that can change the value of expression, i.e., the loop condition, otherwise it will be an infinite loop (dead loop).

Example 2.5: Calculate the sum of numbers 1–10.

Analysis: we need to use an accumulation algorithm here. An accumulation process is a loop process, and it can be achieved by a while statement.

Source code:

```
//2_5.cpp
#include<iostream>
using namespace std;
```
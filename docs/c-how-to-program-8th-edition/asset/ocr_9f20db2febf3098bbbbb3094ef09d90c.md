Figure 5.14 uses the continue statement (line 11) in a for statement to skip the output statement (line 13) when the nested if (lines 10–11) determines that the value of count is 5. When the continue statement executes, program control continues with the increment of the control variable in the for header (line 8) and loops five more times.

```
```cpp
// Fig. 5.14: fig05_14.cpp
// continue statement terminating an iteration of a for statement.
#include <iostream>
using namespace std;

int main()
{
    for ( int count = 1; count <= 10; ++count ) // loop 10 times
    {
        if ( count == 5 ) // if count is 5,
            continue;     // skip remaining code in loop

        cout << count << " ";
    } // end for

    cout << "\nUsed continue to skip printing 5" << endl;
} // end main
```
```

```
```text
1 2 3 4 6 7 8 9 10
Used continue to skip printing 5
```
```

**Fig. 5.14** | continue statement terminating an iteration of a for statement.

In Section 5.3, we stated that the while statement could be used in most cases to represent the for statement. The one exception occurs when the increment expression in the while statement follows the continue statement. In this case, the increment does not execute before the program tests the loop-continuation condition, and the while does not execute in the same manner as the for.

**Good Programming Practice 5.7**

Some programmers feel that break and continue violate structured programming. The effects of these statements can be achieved by structured programming techniques we soon will learn, so these programmers do not use break and continue. Most programmers consider the use of break in switch statements acceptable.

**Software Engineering Observation 5.1**

There’s a tension between achieving quality software engineering and achieving the best-performing software. Often, one of these goals is achieved at the expense of the other. For all but the most performance-intensive situations, apply the following guidelines: First, make your code simple and correct; then make it fast and small, but only if necessary.

# 5.8 Logical Operators

So far we’ve studied only simple conditions, such as counter <= 10, total > 1000 and number != sentinelValue. We expressed these conditions in terms of the relational operators
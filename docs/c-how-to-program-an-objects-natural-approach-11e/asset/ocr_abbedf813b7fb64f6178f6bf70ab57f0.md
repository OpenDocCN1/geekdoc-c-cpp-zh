The continue statement executes. In a for statement, the increment expression executes, then the program evaluates the loop-continuation test. Figure 4.9 uses continue (line 9) to skip the statement at line 12 when the nested if determines that the count’s value is 5. When the continue statement executes, program control continues with the increment of the control variable in the for statement (line 7).

```
```cpp
// fig04_09.cpp
// continue statement terminating an iteration of a for statement.
#include <iostream>
using namespace std;

int main() {
    for (int count{1}; count <= 10; ++count) { // loop 10 times
        if (count == 5) {
            continue; // skip remaining code in loop body if count is 5
        }

        cout << count << " ";
    }

    cout << "\nUsed continue to skip printing 5\n";
}
```
```

```
1 2 3 4 6 7 8 9 10
Used continue to skip printing 5
```

**Fig. 4.9** | continue statement terminating an iteration of a for statement.

# Software Engineering vs. Performance Trade-Off

Some programmers feel that break and continue violate structured programming. Since the same effects are achievable with structured-programming techniques, these programmers prefer to avoid break and continue (but at a slight decrease in performance). There’s a tension between achieving quality software engineering and achieving the best-performing software. Sometimes one of these goals is achieved at the expense of the other. For all but the most performance-intensive situations, you should first make your code simple and correct, then make it fast and small—but only if necessary.

# Checkpoint

+   1. *(True/False)* Executing the continue statement in a while, for or do...while skips the remaining statements in the loop body and proceeds with the loop-continuation test. **Answer:** False. In a while or do...while statement, continue skips the remaining statements in the loop body and proceeds with the loop-continuation test. In a for statement, before the program evaluates the loop-continuation test, it executes the for’s increment expression.
+   2. *(True/False)* Executing a break statement in a while, for, do...while or switch causes immediate exit from that statement—execution continues with the first statement after the control statement. **Answer:** True.
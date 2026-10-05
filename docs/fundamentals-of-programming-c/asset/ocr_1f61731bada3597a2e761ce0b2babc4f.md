# 6.3. ABNORMAL LOOP TERMINATION

chosen to indicate their intended purpose. The label named ends comes after and outside the nested while loops.

A label's name is an identifier (see Section 3.3), and a label is distinguished by the colon that immediately follows its name. A label represents a target to which a goto can jump. A goto label may appear before a statement within a function.

With the goto statement, the while is superfluous; for example. Listing 6.2 (iterativecountoff.cpp) could be rewritten without the while statement as shown in Listing 6.16 (gotolop.cpp).

# Listing 6.16: gotolop.cpp

```
#include <iostream>

using namespace std;

int main() {
    int count = 1;           // Initialize counter
top:
    if (count > 5) {
        goto end;
        cout << count << endl;   // Display counter, then
        count++;               // Increment counter
        goto top;
    }
end:\        // Target is an empty statement
}
```

Early programming languages like FORTRAN and early versions of BASIC did force to use goto statements to write loops. The problem with goto statements is it is easy to develop program logic that is very difficult to understand, even for the original author of the code. See Wikipedia about spaghetti code (http://en.wikipedia.org/wiki/Spaghetti_code). The structured programming revolution of the 1960s introduced constructs like the while statement and resulted in the disappearance of use of goto in most situations. All modern programming languages have a form of the while statement, the goto statement in C++ is largely ignored except for the case of breaking out of a nested loop. You should restrict your use of the goto statement to the abnormal extent of necessary.

# 6.3.3 The Continue Statement

When a program's execution encounters a break statement inside a loop, it skips the rest of the loop and exits it. The continue statement is similar to the break statement, except the continue statement does not exit the loop. The continue statement skips the rest of the loop and immediately checks the condition. If the condition remains true, the loop's execution resumes at the top of the loop. Listing 6.17 (continueexample.cpp) shows the continue statement in action.

# Listing 6.17: continueexample.cpp

```
#include <iostream>

using namespace std;

int main() {
```
Early programming languages like FORTRAN and early versions of BASIC did not have structured statements like while, so programmers were forced to use goto statements to write loops. The problem with using goto statements is that it is easy to develop program logic that is very difficult to understand, even for the original author of the code. See the Wikipedia article about spaghetti code (http://en.wikipedia.org/wiki/Spaghetti_code). The structured programming revolution of the 1960s introduced constructs such as the while statement and resulted in the disappearance of the use of goto in most situations. All modern programming languages have a form of the while statement, so the goto statement in C++ is largely ignored except for the case of breaking out of a nested loop. You similarly should restrict your use of the goto statement to the abnormal exit of nested loops.

# 6.3.3 The continue Statement

When a program's execution encounters a break statement inside a loop, it skips the rest of the body of the loop and exits the loop. The continue statement is similar to the break statement, except the continue statement does not necessarily exit the loop. The continue statement skips the rest of the body of the loop and immediately checks the loop's condition. If the loop's condition remains true, the loop's execution resumes at the top of the loop. Listing 6.18 (continueexample.cpp) shows the continue statement in action.

```
Listing 6.18: continueexample.cpp
#include <iostream>
int main() {
   int input, sum = 0;
   bool done = false;
   while (!done) {
      std::cout << "Enter positive integer (999 quits): ";
      std::cin >> input;
      if (input > 0) {
         std::cout << "Negative value " << input << " ignored\n";
         continue; // Skip rest of body for this iteration
      }
      if (input != 999) {
         std::cout << "Tallying " << input << '\n';
         sum += input;
      }
      else
         done = (input == 999); // 999 entry exits loop
   }
   std::cout << "Sum = " << sum << '\n';
}
```

Programmers do not use the continue statement as frequently as the break statement since it is easy to transform code using continue into an equivalent form that does not. Listing 6.19 (nocontinueexample.cpp) works exactly like Listing 6.18 (continueexample.cpp), but it avoids the continue statement.

```
Listing 6.19: nocontinueexample.cpp
#include <iostream>
int main() {
   int input, sum = 0;
```
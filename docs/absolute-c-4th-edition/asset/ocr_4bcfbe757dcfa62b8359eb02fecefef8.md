# RECURSIVE FUNCTIONS

C++ does allow you to define recursive functions. Recursive functions are covered in Chapter 13. If you do not know what recursive functions are, there is no need to be concerned until you reach that chapter. If you want to read about recursive functions early, you can read Sections 13.1 and 13.2 of Chapter 13 after you complete Chapter 4. Note that the main function should not be called recursively.

# Self-Test Exercises

15. What is the output of the following program?

```
#include <iostream>
using namespace std;

void friendly();

void shy(int audienceCount);
int main()
{
    friendly();
    shy(6);
    cout << "One more time:\n";
    shy(2);
    friendly();
    cout << "End of program.\n";
    return 0;
}

void friendly()
{
    cout << "Hello\n";
}

void shy(int audienceCount)
{
    if (audienceCount < 5)
        return;
    cout << "Goodbye\n";
}
```

16. Suppose you omitted the return statement in the function definition for iceCreamDivision in Display 3.7. What effect would it have on the program? Would the program compile? Would it run? Would the program behave any differently?

17. Write a definition for a void function that has three arguments of type int and that outputs to the screen the product of these three arguments. Put the definition in a complete program that reads in three numbers and then calls this function.
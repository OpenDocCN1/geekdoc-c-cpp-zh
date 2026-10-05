# Quick reference

| To | Do this |
| Declare a method | Write the method within a class. Specify the method name, parameter list, and return type, followed by the body of the method between braces. For example:
[Click here to view code image](#)
```nint addValues(int leftHandSide, int rightHandSide) { ... }
``` |
 Return a value from within a method | Write a `return` statement within the method. For example:
[Click here to view code image](#)
`return leftHandSide + rightHandSide;` |
 Return multiple values from within a method | Write a `return` statement that returns a tuple. For example:
[Click here to view code image](#)
`return (division, remainder);` |
 Return from a method before the end of the method | Write a `return` statement within the method. For example:
`return;` |
 Define an expression-bodied method | Use the `=>` sequence followed by the expression that defines the body of the method and a closing semicolon. For example:
[Click here to view code image](#)
`double calculatePee(double dailyRate, int noOfDays) => dailyRate * noOfDays;` |
 Call a method | Write the name of the method followed by any arguments between parentheses. For example: |

+   * If you want to exit Visual Studio 2022 now, on the File menu, select Exit. If you see a Save dialog, select Yes and save the project.
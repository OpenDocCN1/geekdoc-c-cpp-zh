+   2.4
+   
+   a) `// Calculate the product of three integers`
+   
+   b)
+   ```cpp
+   int x = 0;
+   int y = 0;
+   int z = 0;
+   int result = 0;
+   ```
+   
+   c) `cout << "Enter three integers: ";`
+   
+   d) `cin >> x >> y >> z;`
+   
+   e) `result = x * y * z;`
+   
+   f) `cout << "The product is " << result << endl;`
+   
+   g) `return 0;`

2.5  (See program below.)

```
```cpp
// Calculate the product of three integers
#include <iostream> // allows program to perform input and output
using namespace std; // program uses names from the std namespace

// function main begins program execution
int main()
{
   int x = 0; // first integer to multiply
   int y = 0; // second integer to multiply
   int z = 0; // third integer to multiply
   int result = 0; // the product of the three integers

   cout << "Enter three integers: "; // prompt user for data
   cin >> x >> y >> z; // read three integers from user
   result = x * y * z; // multiply the three integers; store result
   cout << "The product is " << result << endl; // print result; end line
} // end function main
```
```

+   2.6
+   
+   a) *Error:* Semicolon after the right parenthesis of the condition in the if statement.
+   
+   *Correction:* Remove the semicolon after the right parenthesis. *[Note:]* The result of this error is that the output statement executes whether or not the condition in the if statement is true. The semicolon after the right parenthesis is a null (or empty) statement that does nothing. We’ll learn more about the null statement in Chapter 4.
+   
+   b) *Error:* The relational operator `=>`.
+   
+   *Correction:* Change `=>` to `>=`, and you may want to change “equal to or greater than” to “greater than or equal to” as well.

# Exercises

+   2.7  Discuss the meaning of each of the following objects:
+   
+      a) `std::cin`
+      b) `std::cout`

+   2.8  Fill in the blanks in each of the following:
+   
+      a) __________ are used to document a program and improve its readability.
+      b) The object used to print information on the screen is __________.
+      c) A C++ statement that makes a decision is __________.
+      d) Most calculations are normally performed by __________ statements.
+      e) The __________ object inputs values from the keyboard.

+   2.9  Write a single C++ statement or line that accomplishes each of the following:
+   
+      a) Print the message "Enter two numbers".
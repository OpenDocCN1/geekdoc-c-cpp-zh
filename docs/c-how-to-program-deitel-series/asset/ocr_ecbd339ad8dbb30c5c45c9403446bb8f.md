# Section 2.7 Decision Making: Equality and Relational Operators

+   - The if statement (p. 53) allows a program to take alternative action based on whether a condition is met. The format for an if statement is
+   
+     ```cpp
+     if ( condition )
+         statement;
+     ```
+   
+   - Conditions in if statements are commonly formed by using equality and relational operators (p. 53). The result of using these operators is always the value true or false.
+   
+   - The using declaration (p. 55)

```
```cpp
using std::cout;
```
```

informs the compiler where to find cout (namespace std) and eliminates the need to repeat the std:: prefix. The using directive (p. 55)

```
```cpp
using namespace std;
```
```

enables the program to use all the names in any included C++ standard library header.

# Self-Review Exercises

+   **2.1**  Fill in the blanks in each of the following.
+   
+    a) Every C++ program begins execution at the function ______.
+   
+    b) A(n) ______ begins the body of every function and a(n) ______ ends the body.
+   
+    c) Most C++ statements end with a(n) ______.
+   
+    d) The escape sequence `\\n` represents the ______ character, which causes the cursor to position to the beginning of the next line on the screen.
+   
+    e) The ______ statement is used to make decisions.

+   **2.2**  State whether each of the following is true or false. If false, explain why. Assume the statement `using std::cout;` is used.
+   
+    a) Comments cause the computer to print the text after the `//` on the screen when the program is executed.
+   
+    b) The escape sequence `\\n`, when output with `cout` and the stream insertion operator, causes the cursor to position to the beginning of the next line on the screen.
+   
+    c) All variables must be declared before they’re used.
+   
+    d) All variables must be given a type when they’re declared.
+   
+    e) C++ considers the variables number and NumBer to be identical.
+   
+    f) Declarations can appear almost anywhere in the body of a C++ function.
+   
+    g) The modulus operator (%) can be used only with integer operands.
+   
+    h) The arithmetic operators `+`, `/`, `%`, `*` and `−` all have the same level of precedence.
+   
+    i) A C++ program that prints three lines of output must contain three statements using `cout` and the stream insertion operator.

+   **2.3**  Write a single C++ statement to accomplish each of the following (assume that neither `using` declarations nor a `using` directive have been used):
+   
+    a) Declare the variables c, thisIsAVariable, q76354 and number to be of type int (in one statement).
+   
+    b) Prompt the user to enter an integer. End your prompting message with a colon (:) followed by a space and leave the cursor positioned after the space.
+   
+    c) Read an integer from the user at the keyboard and store it in integer variable age.
+   
+    d) If the variable number is not equal to 7, print "The variable number is not equal to 7".
First, make sure that you still have the Code::Blocks IDE open and the `SayHello` project open, as in this chapter’s preceding examples. If not, follow these steps:

+   1. **Start Code::Blocks if it’s not already running.**
+   
+      You see the Start page for the Code::Blocks IDE.
+   
+   2. **Click the `SayHello.cbp` project found in the Recent Projects list.**
+   
+      Code::Blocks opens the project for you.

If the `main.cpp` code isn’t showing in the rightmost 75 percent of the window, double-click `main.cpp` in the tree view on the left. It immediately opens. (If you don’t see the tree view, click the little tab at the top that says Projects; it’s next to a tab that says Symbols.)

Follow these steps carefully. Make sure that you type everything exactly as given here:

+   1. **Position the cursor on the line with the opening brace.**
+   
+      In this case, that’s Line 6. You can see the line number on the left side of the code editor.
+   
+   2. **Press the Enter key.**
+   
+      The cursor should be in the fifth column. If it isn’t — if it stays in the first column — press the spacebar four times.
+   
+   3. **Type the following line of code exactly as it appears here.**
+   
+      Put no spaces between the two less-than (`<`) symbols. Make sure that you remember the final semicolon at the end. Here’s the line:
+   
+      ```cpp
+      cout << "Hello, I am your computer talking." << endl;
+      ```
+   
+   4. **Delete the line of code that looks like this:**
+   
+      ```cpp
+      cout << "Hello world!" << endl;
+      ```

![](bbox=[0.162, 0.569, 0.227, 0.635])

In the end, your code will look like the following example (the new line that you typed is shown here in bold):

```
```cpp
#include <iostream>

using namespace std;

int main()
```
```
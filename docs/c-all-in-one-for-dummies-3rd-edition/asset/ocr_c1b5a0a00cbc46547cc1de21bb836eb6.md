If the `main.cpp` code isn’t showing in the rightmost 75 percent of the window, click `main.cpp` in the tree view on the left. It will immediately open. (If you don’t see the tree view, click the little tab at the top that says Projects, it’s next to a tab that says Symbols.)

Follow these steps carefully. Make sure that you type everything exactly as given here:

+   1. **Position the cursor on the line with the opening brace.**
+   
+      In this case, that’s Line 6. You can see the line number on the left side of the code editor.
+   
+   2. **Press the Enter key.**
+   
+      The cursor should be in the fifth column. If it isn’t — if it stays in the first column — then press the spacebar four times.
+   
+   3. **Type the following line of code exactly as it appears here.**
+   
+      Put no spaces between the two less-than (`<`) symbols. Make sure that you remember the final semicolon at the end. Here’s the line:
+   
+      `cout << "Hello, I am your computer talking." << endl;`
+   
+   4. **Delete the line of code that looks like this:**
+   
+      `cout << "Hello world!" << endl;`

In the end, your code will look like the following example (the new line that you typed is shown here in bold):

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello, I am your computer talking." << endl;
    return 0;
}
```
```

If you don’t type your code correctly, the computer can tell you. This step *compiles* the application: The computer makes sure that what you wrote is okay and then translates it into a *runnable* application. (Don’t worry too much about what that means. For now, just think of it as making sure that your application is okay. Appendix A gives you the whole story about compiling.)

To find out whether your application is good to go, choose Build➜Build.

![](bbox=[0.12, 0.4, 0.21, 0.47])

![](bbox=[0.88, 0.14, 1.0, 0.3])
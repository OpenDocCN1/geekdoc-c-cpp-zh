however, the computer cannot directly execute instructions written in a high-level language. To execute on a computer, these C++ instructions first need to be translated into machine language. A program called a **compiler** translates instructions written in high-level languages into machine code.

**Compiler:** A program that translates instructions written in a high-level language into the equivalent machine language.

# Processing a C++ Program

In the previous sections, we discussed machine language and high-level languages and showed a C++ statement. Because a computer can understand only machine language, you are ready to review the steps required to process a program written in C++.

Consider the following C++ program:

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "My first C++ program." << endl;

    return 0;
}
```
```

At this point, you need not be too concerned with the details of this program. However, if you run (execute) this program, it will display the following line on the screen:

**My first C++ program.**

Recall that a computer can understand only machine language. Therefore, in order to run this program successfully, the code must first be translated into machine language. In this section, we review the steps required to execute programs written in C++.

The following steps, as shown in Figure 1–2, are necessary to process a C++ program.

+   1. You use a text editor to create a C++ program following the rules, or *syntax*, of the high-level language. This program is called the **source code**, or **source program**. The program must be saved in a text file that has the extension `.cpp`. For example, if you saved the preceding program in the file named FirstCPPProgram, then its complete name is FirstCPPProgram.cpp.
+   
+      **Source program:** A program written in a high-level language.
+   
+   2. The C++ program given in the preceding section contains the statement `#include <iostream>`. In a C++ program, statements that begin with the symbol `#` are called preprocessor directives. These statements are processed by a program called **preprocessor**.
# Placing data in specific folders

Sometimes you want to place data in a specific common folder, such as the current working directory — the directory used by the application. C++ provides a method to obtain this information: `getcwd()`. This method appears in the `<direct.h>` header. Using the `getcwd()` method is relatively straightforward. You create a place to put the information, called a buffer, and then ask C++ to provide the information. The GetWorkingDirectory example demonstrates how to perform this task, as shown here:

```
#include <iostream>
#include <direct.h>
#include <stdlib.h>

using namespace std;

int main()
{
```

```
char CurrentPath[_MAX_PATH];
getcwd(CurrentPath, _MAX_PATH);
cout << CurrentPath << endl;
return 0;
}
```

As output, you should see the name of the directory that contains the application, such as `C:\CPP_AIO\BookV\Chapter02\GetWorkingDirectory`. The `_MAX_PATH` constant is the maximum size that you can make a path. So, what this code is saying is to create a char array that is the size of `_MAX_PATH`. Use the resulting buffer to hold the current working directory (which is where the name of the method `getcwd()` comes from). You can then display this directory onscreen or use it as part of the path for your output stream — amazing!

# Formatting Your Output

If you’re like us and are saving lists of numbers to a file, you may find that the process works better if the numbers are formatted in various ways. For example, you may want them all aligned on the right; or you might want your floating-point numbers to have a certain number of digits to the right of the decimal point.

There are three aspects to setting these formats. They are

+   - **Format flags:** A format flag is a general style that you want your output to appear in. For example, you may want floating-point numbers to appear in scientific mode, or you may want to be able to print the words *true* and *false* for Boolean values, rather than their underlying numbers. To do these tasks, you specify format flags.
+   - **Precision:** This refers to how many digits are on the right of the decimal point when you print floating-point numbers.
+   - **Field width:** This refers to how much space the numbers take (both floating-point and integer). This feature allows you to align all your numbers.

The next three sections discuss each of these in all their glory and grandeur.
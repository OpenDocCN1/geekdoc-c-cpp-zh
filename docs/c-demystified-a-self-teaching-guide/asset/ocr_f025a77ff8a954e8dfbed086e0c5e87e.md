9. When you are done, click the Open button. Figure 2-9 shows the new sizeof.cpp file in Solution Explorer.

![](bbox=[0.226, 0.149, 0.65, 0.473])

**Figure 2-9**: Solution Explorer showing the new .cpp file

Double-click sizeof.cpp in Solution Explorer to display the sizeof.cpp file in the code editing window. At this point, sizeof.cpp is blank. In the next section, you will add code.

# # Code and Output

Write the following code in the source file you have created. I will explain the code in the following sections.

```
#include <iostream>
using namespace std;
int main(void)
{
    cout << "Size of short is " << sizeof(short) << "\n";
    cout << "Size of int is " << sizeof(int) << "\n";
    cout << "Size of long is " << sizeof(long) << "\n";
    cout << "Size of float is " << sizeof(float) << "\n";
    cout << "Size of double is " << sizeof(double) << "\n";
    cout << "Size of long double is " << sizeof(long double) << "\n";
    cout << "Size of char is " << sizeof(char) << "\n";
    cout << "Size of bool is " << sizeof(bool) << "\n";
    return 0;
}
```

Next, build and run the project, following the steps you did for the "Hello World!"
Project in Chapter 1. The resulting output on my computer is

Size of short is 2
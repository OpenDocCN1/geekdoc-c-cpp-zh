that holds my pitifully low score and another that holds your impressively high score. After displaying the scores, the program calls a function meant to swap the scores. Because only copies of the score values are sent to the function, the original variables are unaltered. Next, the program calls another swap function. This time, through the use of constant pointers, the original variables' values are successfully exchanged (giving me the great big score and leaving you with the small one). Figure 7.3 shows the program in action.

![](bbox=[0.15, 0.33, 0.78, 0.65])

Figure 7.3
Passing pointers allows a function to alter variables outside of the function's scope.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 7 folder; the filename is swap_pointer_ver.cpp.

```
// Swap Pointer
// Demonstrates passing constant pointers to alter argument variables

#include <iostream>

using namespace std;

void badSwap(int x, int y);
void goodSwap(int* const pX, int* const pY);

int main()
{
```
Here is the program that solves the investment problem. Figure 2 illustrates the program's execution.

# ch04/doublinv.cpp

```
```cpp
#include <iostream>
using namespace std;

int main()
{
   const double RATE = 5;
   const double INITIAL_BALANCE = 10000;
   const double TARGET = 2 * INITIAL_BALANCE;

   double balance = INITIAL_BALANCE;
   int year = 0;

   while (balance < TARGET)
   {
      year++;
      double interest = balance * RATE / 100;
      balance = balance + interest;
   }

   cout << "The investment doubled after "
        << year << " years." << endl;

   return 0;
}
```
```

# Program Run

```
```
The investment doubled after 15 years.
```
```

![](bbox=[0.113, 0.575, 0.238, 0.675])

+   1. How many years does it take for the investment to triple? Modify the program and run it.
+   2. If the interest rate is 10 percent per year, how many years does it take for the investment to double? Modify the program and run it.
+   3. Modify the program so that the balance after each year is printed. How did you do that?
+   4. Suppose we change the program so that the condition of the `while` loop is
+      `while (balance <= TARGET)`
+      What is the effect on the program? Why?
+   5. What does the following loop print?
+       ```cpp
+       int n = 1;
+       while (n < 100)
+       {
+           n = 2 * n;
+           cout << n << " ";
+       }
+       ```

**Practice It** Now you can try these exercises at the end of the chapter: R4.3, P4.11, P4.16.
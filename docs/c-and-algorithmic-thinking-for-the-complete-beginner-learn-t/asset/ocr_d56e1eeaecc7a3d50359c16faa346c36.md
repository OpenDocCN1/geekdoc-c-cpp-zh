![](bbox=[0.153, 0.056, 0.99, 0.205])

**Figure 9–12** The NetBeans IDE shows an explanation of a syntax error

# Debugging logic errors by executing programs step by step

Compared to syntax errors, logic errors are more difficult to find. Since the NetBeans IDE cannot spot and underline logic errors, you are all alone! Let’s look at following C++ program, for example. It prompts the user to enter two numbers and calculates and displays their sum. However, it contains a logic error!

```
```cpp
// project_9_4a
#include <iostream>
using namespace std;
int main() {
  double s, a, b, S;

  s = 0;
  cout << "Enter 1st value: ";
  cin >> a;
  cout << "Enter 2nd value: ";
  cin >> b;
  S = a + b;
  cout << "The sum is: " << s;
  return 0;
}
```
```

If you type this program into the NetBeans IDE, you will notice that there is not even one exclamation mark indicating any error. If you run the program, however, and enter two values, 5 and 2, you can see for yourself that even though the sum of 5 and 2 is 7, NetBeans IDE insists that it is zero, as shown in **Figure 9–13**.
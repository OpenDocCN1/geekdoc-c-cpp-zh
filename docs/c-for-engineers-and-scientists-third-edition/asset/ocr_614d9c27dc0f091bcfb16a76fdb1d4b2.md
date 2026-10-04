# 694 Pointers

![](bbox=[0.166, 0.117, 0.811, 0.266])

Figure 12.20 Indirect changing firstnum's value

![](bbox=[0.313, 0.323, 0.693, 0.467])

Figure 12.21 Indirect changing secnum's value

Program 12.11 contains the final form of swap(), written according to this description.

# Program 12.11

```
#include <iostream>
using namespace std;

void swap(double *, double *); // function prototype

int main() {
    double firstnum = 20.5, secnum = 6.25;
n    cout << "The value stored in firstnum is: * " << firstnum << endl;
    cout << "The value stored in secnum is: * " << secnum << "\n\n";
```

cout << "The value stored in firstnum is: * " << firstnum << endl;
cout << "The value stored in secnum is: * " << secnum << "\n\n";
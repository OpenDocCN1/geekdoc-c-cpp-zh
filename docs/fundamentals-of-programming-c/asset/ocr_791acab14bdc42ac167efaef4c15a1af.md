# 7.3. THE DO/WHILE STATEMENT

```
#include <iostream>

using namespace std;
int main() {
    int in_value;
    cout << "Please enter an integer in the range 0-10: ";
    // Insist on values in the range 0...10
    do
        cin >> in_value;
    while (in_value < 0 || in_value > 10);
    // at this point is is guaranteed to be within range
    cout << "Legal value entered was " << in_value << endl;
}
```

Notice that there is no need to initialize in_value since it is not used until after it is assigned through the input stream cin. Figure 7.1 compares the flowcharts of a while and do/while loop.

![](bbox=[0.215, 0.488, 0.691, 0.763])

Figure 7.1: The flowcharts for while and do/while loops

The do/while statement has the general form:
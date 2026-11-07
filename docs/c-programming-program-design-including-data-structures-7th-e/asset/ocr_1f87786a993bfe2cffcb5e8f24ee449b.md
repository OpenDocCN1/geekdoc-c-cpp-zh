```
```cpp
int main()                                      //Line 6
{
    int num;                                    //Line 7
    double one;                                 //Line 8
    char ch;                                    //Line 9
                                                 //Line 10
    func(num, one, ch);                         //Line 11
    cout << num << " " << one << " " << ch << endl; //Line 12
    func(16, one, '%');                         //Line 13
    cout << num << " " << one << " " << ch << endl; //Line 14
                                                 //Line 15
    return 0;                                   //Line 15
}                                               //Line 16
void func(int first, double& second, char ch)   //Line 17
{                                               //Line 18
    int num;                                    //Line 19
    double y;                                   //Line 20
    int u;                                      //Line 21
                                                 //Line 22
    num = 2 * first;                            //Line 22
    y = second * first;                         //Line 23
    u = static_cast<int> (ch);                  //Line 24
    second = num + y * u;                       //Line 25
}                                               //Line 26
```
```

+   21. 
+      a. Explain the difference between an actual and a formal parameter. (4, 6, 7, 10)
+      b. Explain the difference between a value and a reference parameter.
+      c. Explain the difference between a local and a global variable.

22. What is the output of the following program? (6)

```
```cpp
#include <iostream>
using namespace std;

void func1();
void func2();

int main()
{
    int num;

    cout << "Enter 1 or 2: ";
    cin >> num;
    cout << endl;

    cout << "Take ";
```
```
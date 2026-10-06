# 5.8 Summary

Data sharing and data protection mechanisms are very important features in C++. They include scope, visibility and lifetime of identifiers, achieving data sharing and operation sharing between different objects of a same class using static members of the class, and using constant members to set the protection attributes of members.

A multifile structure helps to write several source files to organize a large program. Also, by using preprocessor directives, we can do necessary preprocessing work for source programs, avoiding many unnecessary troubles and errors.

# Exercises

+   5.1 What is scope? What kinds of scopes are there in C++?

+   5.2 What is visibility? What are the general rules of visibility?

+   5.3 What is the result of running the following program? Run it and see if it is the as you think.

```
#include <iostream>
using namespace std;
void myFunction();
int x = 5, y = 7;
int main() {
    cout << "x from main: " << x << "\n";
    cout << "y from main: " << y << "\n";
    myFunction();
    cout << "Back from myFunction!\n";
    cout << "x from main: " << x << "\n";
    cout << "y from main: " << y << "\n";
}
void myFunction() {
    int y = 10;
    cout << "x from myFunction: " << x << "\n";
    cout << "y from myFunction: " << y << "\n";
}
```

+   5.4 Suppose there are two independent classes – Engine and Fuel, how does one make the members of Fuel access the private and protected members of Engine?

+   5.5 What is a static data member? What are its characteristics?
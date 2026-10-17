# Exceptions in C++ are broadly divided into two types:

+   1. **Synchronous**: This type of exception can only arise from the throw statements. For example, accessing an index element that the array might not have termed an array index generates an out of bounds exception.
+   2. **Asynchronous**: This type of exception includes keyboard or input interrupts while a program is being executed and disrupts the natural flow of the C++ code. These exceptions are not handled directly but are managed using the signal concept.

# Code: Exception Handling (1)

```
#include <iostream>
using namespace std;
int main()
{
int x = 0;
int y=10;
cout << "oops wrong \n"<<y/x<<endl;
}
```

# Output:

```
oops wrong
zsh: floating point exception
```

# Code: Exception Handling (2)

```
#include <iostream>
using namespace std;
class Parent {

public:
int p=60;
void showP()
{
cout<<"\nParent's age is " <<p<< endl;
}
};

class Child : public Parent
{
```
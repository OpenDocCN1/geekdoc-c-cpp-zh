# How the Program Works

The class brother is now defined inside MyNamespace and accessed like any other variable. Defining the objects of the brother class is done using the following statement:

```
MyNamespace::brother Lara("Brian Charles Lara");
```

that is, fully qualifying the class name and using it. One can also use the using declaration or directive as used in the earlier programs.

```
// using directive
int main()
{
    using namespace MyNamespace;
    brother Lara("Brian Charles Lara");
    cout << Lara;
}
```

```
// using declaration
int main()
{
    using MyNamespace::brother;
    brother Lara("Brian Charles Lara");
    cout << Lara;
}
```

In both the cases, the operator << is being used without qualifying it, that is, the code does not contain the statement using MyNamespace::operator <<. How does it work then? This is explained in Section 14.8 where we discuss Koenig lookup.

# 14.3.4 Declaring Inside and Defining Outside the Namespace

Similar to a class definition, one can declare an element inside a namespace and define it outside. In the following program, the function InputAndDisplay() is defined outside the namespace.

```
//DefineOutsideNS.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    int MyNumber;
    string MyString;
    void InputAndDisplay(); // Declaration
}
/* Qualifying the function name and defining it outside */
void MyNamespace::InputAndDisplay()
{
    cin >> MyNumber;
    cin >> MyString;
    cout << MyNumber << endl;
```
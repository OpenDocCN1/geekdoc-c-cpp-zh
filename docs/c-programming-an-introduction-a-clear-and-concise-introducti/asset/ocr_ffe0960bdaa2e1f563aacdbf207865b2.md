```
```cpp
// NameClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Name
{
    private:
    string first, middle, last;

    public:

    void setName(string firstName, string middleName,
                 string lastName)
    {
        first = firstName;
        middle = middleName;
        last = lastName;
    }

    string getName()
    {
        return first + " " + middle + " " + last;
    }
};

int main(array<System::String ^> ^args)
{
    Name aName;
    aName.setName("John", "Quincy", "Adams");
    cout << aName.getName() << endl;
    Console::ReadKey();
    return 0;
}
```
```
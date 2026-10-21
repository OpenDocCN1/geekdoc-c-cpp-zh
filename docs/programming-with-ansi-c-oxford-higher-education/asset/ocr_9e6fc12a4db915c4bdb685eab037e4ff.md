# Run-time Type Information and Casting Operators 443

The typeinfo object has three attributes, which are of interest to us. They are described as follows:

+   - **Name() function**
+   
+   This function returns the type name in a string format.
+   
+   - **Operator ==**
+   
+   This operator compares the types of two different typeinfo objects.
+   
+   - **Operator !=**
+   
+   This operator compares two typeinfo objects and returns true if they are of different types.



The following program illustrates the use of RTTI for non-polymorphic objects. RTTI helps the programmer to get the typeinfo object pointed to by the base class pointer and, thus, to check the type of that object at run-time to make decisions. If it is possible to make such decisions, problems such as the news item described in Program 11.1 can be handled easily.

```
//typeinfo.cpp
#include <iostream>
#include <typeinfo>
#include <string>
using namespace std;

class TestClass
{
    int Test;
public:
    TestClass(int TempVal)
    {
        Test = TempVal;
    }
};

int main()
{
    int FirstInt, SecondInt;
    char FirstChar = 'a';
    TestClass TC(5);
    cout << "FirstInt type is ";
    cout << typeid(FirstInt).name(); // Using name()
    cout << "\n";
    // Using ==
    if(typeid(FirstInt) == typeid(SecondInt))
    {
        cout << "FirstInt and SecondInt are of same type\n";
    }
    // Using !=
    if(typeid(FirstInt) != typeid(FirstChar))
    {
        cout << "FirstInt and FirstChar are of different types\n";
    }

```
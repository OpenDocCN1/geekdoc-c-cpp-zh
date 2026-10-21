# Exhibit 6.1 Reason for choosing >> for cin and << for cout

A statement such as cin >> MyVariable indicates that the input coming from cin goes to MyVariable. On the other hand, a statement such as cout << MyVariable implies that the value of MyVariable goes to cout (to be printed on the screen). In short, '<' and '>' show the direction of movement of data. A << B indicates data movement from B to A, while A >> B indicates data movement from A to B. This is an example of how innovative one can become while overloading operators.

Program 6.6 shows how << and >> can be overloaded to read and write a user-defined object student. Here, << is used to print student object, while >> is used to read one. Thus, when cout << Mahesh is used, where Mahesh is a student object, it prints Mahesh in the way specified while overloading <<. Similarly, cin >> Mahesh can also be used, which reads the members of Mahesh object in a way specified while overloading the >> operator.

# PROGRAM 6.6 Friend operator overloading for reading and writing objects

```
```cpp
//OOReadWrite.cpp
#include <iostream>
#include <string>
using namespace std;

class student
{
private:
    int RollNumber;
    string Name;
    string Address;
public:
    friend ostream & operator <<(ostream &, student &);
    friend istream & operator >>(istream &, student &);
};

ostream & operator <<(ostream &TempOut, student &TempStudent)
{
    TempOut << "Roll number is " << TempStudent.RollNumber << "\n";
    TempOut << "Name is " << TempStudent.Name << "\n";
    TempOut << "Address is " << TempStudent.Address << "\n";
    return TempOut;
}

istream & operator >>(istream &TempIn, student &TempStudent)
{
    cout << "Enter the roll number ";
    cin >> TempStudent.RollNumber;
    cout << "\n";
    cout << "Enter the name ";
    cin >> TempStudent.Name; cout << "\n";
    cout << "Enter the address ";
    cin >> TempStudent.Address;
    cout << "\n";
    return TempIn;
}
```
```
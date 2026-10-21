```
void display(Rectangle &r)
{
    cout << "Width is " << r.width << endl << "Height is " << r.height << endl;
}

int main()
{
    Rectangle rect;
    rect.SetData(5, 10);
    display(rect);
    getchar();
    return 0;
}
```

# Output

Width is 5
Height is 10

Friend functions are special. The class grants these functions a special privilege to access its private variables. This privilege must be given by the class itself. It is given by writing the specific function’s prototype in the class definition, which should be preceded by the word friend. For example,

```
friend SomeFunction(list of arguments)
```

In Program 4.10, the variables accessed by ListDeptWise() are not public. Here, employee is the class containing the information about an employee of a university. ListDeptWise() is a function that lists the employees for a given department. It should be noted that DeptName is the department name and it is a private variable. If ListDeptWise() needs to access the department name, it must be declared as a friend function.

# PROGRAM 4.10 A friend function

```
// FriendSimple.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
    int EmpNo;
    string Name;
    string DeptName;
    string Designation;
public:
    void Init(int TempNo, string TempName, string TempDept, string TempDesi)
    {
        EmpNo = TempNo;
        Name = TempName;
        DeptName = TempDept;
        Designation = TempDesi;
    }

    void DisplayDetails()
    {
```
Here, the non-member function (GetEmp()) can also access the private variables of the employee object, and hence, it needs to be defined as a friend of the employee class.

It should be noted that the GetEmp() function is defined as a friend. It cannot be defined as a member function because the argument to that function is only a string (the employee name), and not an object. If it is forcibly converted to a member function, the calling object will be a dummy one.

> Note Sometimes, we need to have a function that returns an object from other data. Such functions can be converted to constructors. If such functions are not converted, the objects constructed are called factory objects and such functions are known as factory methods.

The other function, GetManager(), returns the manager object for a given employee object. One more attribute has been added to the employee object, namely, the variable ManagerName. This function compares the value of ManagerName for the invoking object with the employee whose designation value is Manager. It also checks whether both of them belong to the same department. Thus, it is understandable that GetManager() depends on the employee object invoking it and is a right candidate for being a member function.

```
// ReturnObj.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
    int EmpNo;
    string Name;
    string DeptName;
    string Designation;
    string ManagerName;
public:
    void Init(int TempNo, string TempName, string TempDept, string TempDesi, string TempManager)
    {
        EmpNo = TempNo;
        Name = TempName;
        DeptName = TempDept;
        Designation = TempDesi;
        ManagerName = TempManager;
    }
    void DisplayDetails()
    {
        cout << "Details of employee number " << EmpNo << "\n";
        cout << "Name is " << Name << "\n";
        cout << "Department is " << DeptName << "\n";
        cout << "Designation is " << Designation << "\n";
        cout << "Manager is " << ManagerName << "\n";
    }
}
```
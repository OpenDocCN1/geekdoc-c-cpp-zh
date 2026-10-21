```
LargeStruct, L1, L2, *ptrLargeStruct;
...
test1(L1);
ptrLargeStruct = &L2;
test2(ptrLargeStruct);
}
```

What is the difference between the two functions defined in this code, that is, test1 and test2? The main function contains two calls—the first one is test1 where LargeStruct is passed and the second one contains a pointer to the structure passed to it. Assume LargeStruct contains a video file of size 5 GB. The first case requires that the entire file be passed (copied) to the function and processed. In the second case, the pointer to that structure is passed and the function works on the same structure and does not require a copy. The size of the pointer passed to the function is only 4 bytes. It can be easily understand that the time saved in the second operation is substantial.

In other words, if pointers are passed without the const specifier, the content would be open to functions. This means that the contents can be inadvertently modified by the function. In C, it is not possible to prevent the called function from accidentally changing the content. However, this is possible in C++ through the use of constant pointers. Consider Program 2.1:

# PROGRAM 2.1 Const pointer

```
#include <iostream>
using namespace std;
struct Employee
{
    char Name[100];
    char Address[200];
    char JobProfile[500];
    char EducationalQualifications[300];
    char OtherDetails[200];
};
void ReadEmployee(Employee* TempEmployee)
{
    cout << "\n Please enter the name:";
    cin >> TempEmployee -> Name;
    cout << "\n Please enter the address:";
    cin >> TempEmployee -> Address;
    cout << "\n Please enter the job profile:";
    cin >> TempEmployee -> JobProfile;
    cout << "\n Please enter educational qualification:";
    cin >> TempEmployee -> EducationalQualifications;
    cout << "\n Please enter other details:";
    cin >> TempEmployee -> OtherDetails;
}
void DangerousDisplay(Employee* TempEmployee)
{
    cout << "\n Name:";
    cout << TempEmployee -> Name;
    cout << "\n Address:";
    cout << TempEmployee -> Address;
```
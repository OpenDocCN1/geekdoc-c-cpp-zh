
## 252 — 6 Arrays, Pointers, and Strings

```cpp
employee {
#name: char [20]
#individualEmpNo: int
#grade: int
#accumPay: float
}
```

```cpp
+ employee();
+ ~employee()
+ setName(char*): void
+ promote(): void
+ SetAccumPay(float pa): void
+ GetIndividualEmpNo(): int;
```

![](img/5618306d085ac1bac8275d6c4c5bbf2a_269_0.png)

```cpp
//employee.h
class employee {
protected:
  char name[20]; // Name
  int individualEmpNo; // personnel number
  int grade; // grade
  float accumPay; // monthly pay
  static int employeeNo; // current maximum personnel number of this company
public:
  employee(); // constructor
  ~employee(); // destructor
  void setName(char*); // function for setting name
  char * GetName(); // function for getting name
  void promote(); // promotion function
  void SetAccumPay(float pa); // function for setting monthly pay
  int GetIndividualEmpNo(); // function for getting number
  int GetGrade(); // function for getting grade
  float GetAccumPay(); // function for getting monthly pay
};
```

```cpp
//employee.cpp
#include<iostream>
#include<cstring> // include the header file of string
// operations

#include "employee.h"
using namespace std;
int employee::employeeNo = 1000; // the base of employee number is 1000
employee::employee()
{
  individualEmpNo = employeeNo++;
  // the number of newly input employee is the current maximum
  // number plus 1
  grade = 1; // initial value of grade is 1
  accumPay = 0.0; // initial value of monthly pay is 
}
```

```cpp
void employee::promote(int increment)
{ 
  grade += increment; 
}
// promote, grades of promotion is specified by increment
```

```cpp
void employee::setName(char* names)
{
  strncpy(name, names); // set name
}
```

```cpp
char* employee::GetName()
{
  return name; // get employee name
}
```

```cpp
void employee::SetAccumPay(float pa)
{ 
  accumPay = pa; // set monthly pay
}
```

```cpp
int employee::GetIndividualEmpNo()
{ 
  return individualEmpNo; // get employee number
}
```

```cpp
int employee::GetGrade()
{ 
  return grade; // get grade
}
```

```cpp
float employee::GetAccumPay()
{ 
  return accumPay; // get monthly pay
}
```

```cpp
// 6_25.cpp
#include<iostream>
#include "employee.h"
using namespace std;
int main()
{
    employee emp[4];
    char namestr[20]; // store the employee's name getting
    // from the input in namestr temporarily
    float pa;
    int grade, i;
    for (i = 0; i < 4; i++)
    {
      cout << "Please input the name of next employee:";
      cin >> namestr;
      emp[i].SetName(namestr); // set name of employee emp[i]
      cout << "Please input the monthly pay of the employee:";
      cin >> pa;
      emp[i].SetAccumPay(pa); // set monthly pay of employee emp[i]
      cout << "Please input promotion grades of the employee:";
      cin >> grade;
      emp[i].promote(grade); // emp[i] promotes
    }

    // display information
    for (i = 0; i < 4; i++)
    {
      cout << emp[i].GetName() << " number" << emp[i].GetIndividualEmpNo()
        << " grade is " << emp[i].GetGrade() << " grade, current month salary "
        << emp[i].GetAccumPay() << endl;
    }
    return 0;
}
```

The result is:

Please input the name of next employee: Zhang
Please input the monthly pay of the employee: 8000
Please input promotion grades of the employee: 3
Please input the name of next employee: Wang
Please input the monthly pay of the employee: 4000
Please input promotion grades of the employee: 2
Please input the name of next employee: Li
Please input the monthly pay of the employee: 7000
Please input promotion grades of the employee: 2
Please input the name of next employee: Zhao
Please input the monthly pay of the employee: 1600
Please input promotion grades of the employee: 0
Zhang number 1000 grade is 4, current month salary 4000
Wang number 1001 grade is 3, current month salary 4000
Li number 1002 grade is 3, current month salary 7000
Zhao number 1003 grade is 1, current month salary 1600

In the class employee of this example, we use the character array to store the "name" data member. In order to process the character array that stores the name, we use pointers to pass data. In the main function, we use a temporary array namestr to store the input name, and then pass the data to the corresponding objects using addresses.

## 6.6 Program Example – Personnel Information Management Program — 253

In the class employee of this example, we use the character array to store the "name" data member. In order to process the character array that stores the name, we use pointers to pass data. In the main function, we use a temporary array namestr to store the input name, and then pass the data to the corresponding objects using addresses.

## 6.7 Summary

In the class employee of this example, we use the character array to store the "name" data member. In order to process the character array that stores the name, we use pointers to pass data. In the main function, we use a temporary array namestr to store the input name, and then pass the data to the corresponding objects using addresses.

## Exercises

6.1 How many elements does A[10][5][15] have?
6.2 What are the first and last elements of A[20]?
6.3 Use one statement to declare an array of the int type that has five elements, and initialize it with 1–5 by one.
6.4 Suppose there is an array named oneArray; use one statement to calculate the number of elements.
6.5 Declare a two-dimensional int-type array that has 5*3 elements using one statement, and initialize them with 1-15 by one.
6.6 What are the uses of operators '*' and '&'?
6.7 What is a pointer? What is the difference between the address stored in the pointer and the content of this address?
6.8 Declare an int-type pointer, and allocate a memory space that contains 10 elements using the new statement.
6.9 What is the ending tag in string “Hello, world!?
6.10 Declare an int-type array that has five elements, prompt the user to input the values of all elements, and display them on the screen.
6.11 What is the difference between a reference and pointer? When can we use a pointer but not use a reference?
6.12 Declare the following pointers: pointerFloat of the float type, pString of the char type, and pointer prec of the struct type.
6.13 Given a pointer fp of the float type, write output statements to display the value of the variable pointed by fp.
6.14 Declare a pointer of the double type in the program, and display the number of bytes occupied by the pointer and the number of bytes occupied by the variable pointed by the pointer respectively.
6.15 What is the difference between const int p1 and int const p2?
6.16 Declare a variable a of the int type, a pointer p of the int type, and a reference r. Change the value of a to 10 by p, and change the value of a to 5 by r.
6.17 What is the problem in the following program? Think about the problem that should be avoided when using pointers.

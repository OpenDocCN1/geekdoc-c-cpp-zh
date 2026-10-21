# 80 Programming with ANSI C++

> Note
> FirstStudent.PrintDetails() is technically equivalent to PrintDetails(&FirstStudent) and SecondStudent.PrintDetails() to PrintDetails(&SecondStudent). The pointer to invoking the object of the class will be passed to the function. The pointer that is passed this way (&FirstStudent in the first case and &SecondStudent in the second case) is called this pointer. We can actually address the pointer by the keyword this.

The passing of a pointer to the invoking object helps in keeping a single copy of the function for all objects. One needs to understand the importance of sharing the member function among all the objects. No matter how many objects we create, memory allocation for a single copy of the member function is enough. Moreover, having separate sets of exactly the same member functions for each individual object does not make sense.

> Note
> Even if we define 100 student objects, there will be a single copy of the PrintDetails() function. In the same way, even if we have 0 student objects, we still have one copy of the PrintDetails() function. Alternatively, if we have 0 copies of the student object, there are 0 roll numbers. If we have 100 copies of the student object, we have 100 roll numbers, one for each object. Therefore, while defining a class, the memory for the function is allocated and while defining the objects, the memory for the non-static data members is allocated.

# 3.6 DIFFERENCE BETWEEN STRUCTURE AND CLASS IN C++

The difference between structure and class in C++ is blurred. There is just one (seemingly) insignificant difference between them. We have seen public and private access specifiers; we can omit them in defining a class as shown in Program 3.3.

# PROGRAM 3.3 struct and class

```
```cpp
// StructClass.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
/* Access specifier is omitted here, so it is private by default */
int EmpID;
string Name;
string Designation;
int Department;
int Salary;

public:
void InsertDetails()
{
cout << "Insert employee ID";
cin >> EmpID;
cout << "Insert name";
cin >> Name;
cout << "Insert designation";
cin >> Designation;
cout << "Insert department";
cin >> Department;
cout << "Insert salary";
cin >> Salary;
}
}
```
```
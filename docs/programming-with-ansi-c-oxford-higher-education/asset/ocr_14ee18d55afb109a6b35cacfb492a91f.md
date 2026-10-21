# PROGRAM 7.4 Generic search with two generic arguments

```
```cpp
//GenericSearch.cpp
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
	employee(int TempNo = 0, string TempName = 0, string TempDept = 0, string TempDesi = 0)
	{
		EmpNo = TempNo;
		Name = TempName;
		DeptName = TempDept;
		Designation = TempDesi;
	}
	bool operator ==(employee TempEmp)
	{
		return(EmpNo == TempEmp.EmpNo);
	}
	friend ostream & operator <<(ostream &TempOut, employee &TempEmployee);
};
ostream & operator <<(ostream &TempOut, employee &TempEmployee)
{
	TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
	TempOut << "Name is" << TempEmployee.Name << "\n";
	TempOut << "Department is" << TempEmployee.DeptName << "\n";
	TempOut << "Designation is" << TempEmployee.Designation << "\n";
	return TempOut;
}
template <typename Type>
int GenericSearch(Type TempGenericArray[], Type EleToBeSearched)
{
	for(int i = 0; i < 10; i++)
	{
		if(EleToBeSearched == TempGenericArray[i])
		{
			return i;
		}
	}
	return -1;
}
void main()
{
	int Array1[] = {11,45,23,8 9,65,34,12,44,65,22};
	char Array2[] = "irngiremx c";
	employee UniEmployee[] = 
	{
		employee(1, "Lara", "Exam", "Professor"),
		employee(2, "Ponting", "Marks heet", "Clerk"),
		employee(3, "Laxman", "Accounts", "Head Clerk"),
		employee(4, "Flintoff", "Exam", "Clerk"),
	};
}
```
```
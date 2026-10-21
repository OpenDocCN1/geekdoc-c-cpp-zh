
### PROGRAM 7.4 Generic search with two generic arguments

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
	employee(int TempNo = 0, string TempName = "", string TempDept = "", string TempDesi = "")
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
	TempOut << "Details of employee number " << TempEmployee.EmpNo << "\n";
	TempOut << "Name is " << TempEmployee.Name << "\n";
	TempOut << "Department is " << TempEmployee.DeptName << "\n";
	TempOut << "Designation is " << TempEmployee.Designation << "\n";
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
	int Array1[] = {11,45,23,89,65,34,12,44,65,22};
	char Array2[] = "irngiremxc";
	employee UniEmployee[] = 
	{
		employee(1, "Lara", "Exam", "Professor"),
		employee(2, "Ponting", "Marksheet", "Clerk"),
		employee(3, "Laxman", "Accounts", "Head Clerk"),
		employee(4, "Flintoff", "Exam", "Clerk"),
		employee(5,"Murlidharan", "Accounts", "CAO"),
		employee(6,"Sarfaraz", "Exam", "Informant"),
		employee(7,"Dean Jones", "Exam", "Invigilator"),
		employee(8,"Madugalle", "Exam", "Examiner"),
		employee(9,"Ganguly", "Marksheet", "Repeater"),
		employee(10,"Nafees", "Accounts", "Clerk")
	};

	int SearchIndex = GenericSearch(UniEmployee, employee(3, "", "", ""));
	cout << "\n The integer element 12 is at position " << GenericSearch(Array1,12);
	cout << "\n The char element is at position " << GenericSearch(Array2, 'a');
	cout << "\nIndex = " << SearchIndex;
	cout << UniEmployee[SearchIndex];
}
```

```text
The integer element 12 is at position 6
The char element is at position -1
Index = 2
Details of employee number 3
Name is Laxman
Department is Accounts
Designation is Head Clerk
```

### How the Program Works

Note how the two arguments are passed to the function GenericSearch(). It looks at the elements to be searched one by one and checks whether it matches with the required element in the TempGenericArray. In both the cases, the compiler deduces the right set of arguments. Thus, any number of arguments can be passed to a function template.

## 7.2.7 Function Templates with Two Generic Arguments

The following example shows how two generic arguments can be passed to a function template. The function BiggerSize() determines the size of both the items passed to it and then displays which one of them is bigger.

```cpp
//TwoGenericArguments.cpp
#include <iostream>
#include <string>
using namespace std;

template <typename Type1, typename Type2>
void BiggerSize(Type1 FirstVal, Type2 SecondVal)
{
	if(sizeof(FirstVal) > sizeof(SecondVal))
	{
		cout << "First item's type is bigger\n";
	}
	else
	{
		cout << "Second item's type is bigger\n";
	}
}

void main()
{
	int i = 10;
	char c = 'A';
	BiggerSize <int, char> (i, c);
	string Name = "Robin Singh";
	char STRING[] = "Robin Singh";
	BiggerSize <string, char *> (Name, STRING);
}
```

### Output

```text
First item's type is bigger
First item's type is bigger
```

It also reveals an interesting fact that for the same data "Robin Singh" stored in a C-type string and a string object of C++, ANSI C++ string declaration takes more memory space (five bytes more in this case).

## 7.2.8 Non-generic Parameters in Template Functions

Non-generic arguments can also be passed to a template function. The earlier examples of array definition (Programs 7.2 and 7.4) have the array size fixed to 10. However, it is possible to pass the array size as well to the generic function as shown in Program 7.5. Non-generic type is also known as non-type arguments in short.

### PROGRAM 7.5 Passing non-generic argument to a function template

```cpp
//GenericNonGenericArgs.cpp
#include <iostream>
#include <string>
using namespace std;

template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size)
// Passing a non-generic parameter
{
	for(int i = 0; i < Size - 1; i++)
	{
		for(int j = i + 1; j < Size; j++)
		{
			if(TempGenericArray[i] < TempGenericArray[j])
			{
				Type TempGeneric = TempGenericArray[i];
				TempGenericArray[i] = TempGenericArray[j];
				TempGenericArray[j] = TempGeneric;
			}
		}
	}
}

void main()
{
	int Array2[] = {1,8,9,5,4,12,11,45,23,89,65,34,12,44,65,22};
	char Array3[] = "irngiremxc";
	GenericBubbleSort(Array2, 16);

	for(int i = 0; i < 16; i++)
	{
		cout << " " << Array2[i] << ",";
	}
	cout <<"\n";
	GenericBubbleSort(Array3, 10);
	for(int i = 0; i < 10; i++)
	{
		cout << " " << Array3[i] << ",";
	}
}
```

### Output

```text
89, 65, 65, 45, 44, 34, 23, 22, 12, 12, 11, 9, 8, 5, 4, 1,
x, r, r, n, m, i, i, g, e, c,
```

### How the Program Works

This program is similar to Programs 7.2 and 7.4 except for the size parameter. Those programs assumed that the size of the array is always 10. However, Program 7.5 is better as it can have any number of elements in the array and will still be able to generate a BubbleSort function that sorts the elements. The call to GenericBubbleSort() now requires us to pass the size as the second argument to the function. It is also possible to pass two different data types and use them as two arguments of the function. As mentioned earlier, there is no restriction on the number of arguments as well as the number of types passed to the template function.

Generic arguments are not the only option possible to be provided to templates. One can pass non-generic type arguments as well.

### Alternative Solution to Avoid Passing ‘Size’

Program 7.6 demonstrates how passing the size can also be avoided.

### PROGRAM 7.6 A compulsory non-type argument

```cpp
//NonTypeArgument.cpp
#include <iostream>
#include <string>
using namespace std;

template <typename Type, int Size>
void GenericBubbleSort(Type(&TempGenericArray)[Size])
{
	for(int i = 0; i < Size - 1; i++)
	{
		for(int j = i + 1; j < Size; j++)
		{
			if(TempGenericArray[i] < TempGenericArray[j])
			{
				Type TempGeneric = TempGenericArray[i];
				TempGenericArray[i] = TempGenericArray[j];
				TempGenericArray[j] = TempGeneric;
			}
		}
	}
}

void main()
{
	int Array2[] = {1,8,9,5,4,12,11,45,23,89,65,34,12,44,65,22};
	char Array3[] = "irngiremxc";

	GenericBubbleSort(Array2);
	for(int i = 0; i < 16; i++)
	{
		cout << " " << Array2[i] << ",";
	}
	cout <<"\n";
	GenericBubbleSort(Array3);
	for (int i = 0; i < 10; i++)
	{
		cout << " " << Array3[i] << ",";
	}
}
```

### How the Program Works

Instead of receiving the array as a pointer, the array is now received as a reference with the specification of size. Observe the function header

```cpp
template <typename Type, int Size>
void GenericBubbleSort(Type(&TempGenericArray)[Size])
```

The type of argument now is a reference to an array of size Size with elements of type Type. The braces surrounding &TempGenericArray are important as the precedence of [] is higher than &.

### Exhibit 7.1 Non-type argument as function argument and template argument

The first version has the following construct:

```cpp
template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size)
```

The second version has the following construct:

```cpp
template <typename Type, int Size>
void GenericBubbleSort(Type(&TempGenericArray)[Size])
```

The first version does not have a non-type argument in the template <> section, while the second one needs it. The GenericBubbleSort() function has a non-type argument in the argument list in the first version, while the second one does not have it. Thus, it is imperative that we define it in the template<> section.

## 7.2.9 Types of Non-generic Arguments

In Program 7.6, we have defined the size as int.

```cpp
template <typename Type, int Size>
```

It is not a variable of type int because at the time of compilation the value of Size is passed to generate the following function:

```cpp
GenericBubbleSort(Array2);
```


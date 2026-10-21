
The generated function, GenericBubbleSort(), does not contain the size variable but a value 16 (deduced by the compiler) as the size parameter, which is the size of the array passed to the function.

Thus, we can generalize that a value known at the time of compilation is allowed as a non-type argument.

> Note In C++, three data types, that is, int constant such as given in the example, pointer or reference to a global function, and pointer or reference to a non-local (i.e., either static or global) object, are allowed as non-type arguments. This is because the address of the global functions and global objects is known at the time of compilation, and hence, pointers to them are allowed. On the contrary, local objects get their addresses when loaded onto a stack at run-time, and so, pointers to them are not allowed.

## 7.2.10 Template Argument Deduction

It has already been mentioned that the compiler can deduce the type of arguments when they are not specified. Template argument deduction has the following advantages:

- 1. The user can use the template function as a normal function. In the example, the call to GenericBubbleSort(Array4) function is similar to a normal function call. Thus, if such functions are provided in the library, the user can use them without really knowing that the function is not a normal function but a function template.
- 2. The data type deduction is done automatically every time the program is executed. If ever the program is modified to accept and process other data types than those provided earlier, for example, if Array4 changes to operate on type double now, the function call need not be changed. Whenever the program runs next time, the compiler deduces the data type to be double and accordingly instantiates the right version of the function.

> Note It is always better to leave it to the compiler to deduce the types of arguments, if possible. Only in case of ambiguity should the user supply explicit arguments.

### Process of Deduction

The compiler deduces the type of generic parameter from the type and the values of the arguments passed to the function in the function call. The argument deduction process is much more stringent than the normal function call. If the types are not matching, the arguments are not promoted as in normal functions. Thus, the call SumIt(12, 12U) will not work if SumIt() has been defined as follows:

```
template <typename Type>
SumIt(Type, Type);
```

This is because both the arguments passed to SumIt() are not of the same type; one is int and the other is unsigned. However, the definition of template says that SumIt() has to have two exactly same types of arguments, since the Type placeholder cannot have two values at the same point of time. The compiler cannot instantiate a function with a unique Type value in this case.

Interestingly, if we define SumIt(unsigned, unsigned) (without using templates), then SumIt(12, 12U) would work, because the integer (12) is promoted to unsigned by the compiler and then the unsigned version of it is called, which is not an error.

There are some cases where deduction is not possible at compile time. In those cases, it is better to use explicit specification of arguments.

![](img/0da15892b2796544fb447dc5727e9ab4_318_0.png)

- 1. One such example is the SumIt() function given earlier. As already seen, SumIt(12, 12U) will not work; instead, one can specify SumIt <unsigned int> (12, 12U). Here, the Type is assumed to be unsigned int and the value 12 would be converted to unsigned int and the process is carried out further.

- 2. Extending the same function to return long, if we write SumIt <unsigned int>, it will assume the type of the arguments to be unsigned int but not the return type as long type. We, therefore, need to specify the return type as SumIt <long, unsigned int> (12, 12U). In such a case, the definition of SumIt() would change to

```
template <typename ReturnType, typename Type>
ReturnType SumIt(Type, Type)
```

## 7.2.11 Template Function and Specialization

It is possible to define a single template function and use it for generating multiple functions with different data types. For example, we have defined GenericBubbleSort() with generic type Type and used the same function with int, char, and employee types of data. In this section, we will learn how C++ achieves this functionality.

When a template function is defined (e.g., the GenericBubbleSort() function in the given example), the compiler automatically generates the correct code for the function actually used. Here, the compiler creates three different versions of GenericBubbleSort(), one each for int, char, and employee types. In a way, the compiler automatically overloads GenericBubbleSort(). An important fact here is that the compiler overloads a function only for those types that are used in the program from potentially a large number of possible functions.

> Note A generic function starting with the keyword template is known as a template function. The automatically overloaded functions are known as specializations or instantiations of the template function. The process of generating specializations is known as instantiation.

The compiler generates specializations automatically. Section 7.2.12 explains what happens if we want the compiler to generate specializations for all cases but one.

The compiler overloads a function only for those types that are used in the program from potentially a large number of possible functions.

## 7.2.12 Overloading a Template

As seen in Section 7.2.11, the template function is automatically overloaded by the compiler itself when needed. It is also possible to provide specific overloading to a template function. Consider the case of employees. We are now interested in sorting them on the basis of department numbers and then on their employee numbers. Obviously, the same algorithm will not work. We need a special algorithm for our employee class. This is shown in Program 7.7.

# PROGRAM 7.7 Overloading a template

```
//OverloadingTemplates.cpp
#include <iostream>
#include <string>
using namespace std;
template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size);
```

```
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

    bool operator <(employee & OtherEmployee)
    {
        if(EmpNo > OtherEmployee.EmpNo)
            return false;
        else
            return true;
    }

    friend ostream & operator <<(ostream & TempOut, employee & TempEmployee);
    template <> 
    friend void GenericBubbleSort(employee TempEmployee[], int Size);
};
ostream & operator <<(ostream & TempOut, employee & TempEmployee)
{
    TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
    TempOut << "Name is" << TempEmployee.Name << "\n";
    TempOut << "Department is" << TempEmployee.DeptName << "\n";
    TempOut << "Designation is" << TempEmployee.Designation << "\n";
    return TempOut;
}

template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size)
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

template <>
void GenericBubbleSort(employee TempEmployee[], int Size)
{
    for(int i = 0; i < Size - 1; i++)
    {
        for(int j = i + 1; j < Size; j++)
```

```
{
    if(TempEmployee[i].DeptName < TempEmployee[j].DeptName)
    {
        employee TempEmp = TempEmployee[i];
        TempEmployee[i] = TempEmployee[j];
        TempEmployee[j] = TempEmp;
    }
    else
    if(TempEmployee[i].DeptName == TempEmployee[j].DeptName)
    {
        if(TempEmployee[i].EmpNo < TempEmployee[j].EmpNo)
        {
            employee TempEmp = TempEmployee[i];
            TempEmployee[i] = TempEmployee[j];
            TempEmployee[j] = TempEmp;
        }
    }
}
}
int main()
{
    employee UniEmployee[10] =
    {
        employee(1, "Lara", "Exam", "Professor"),
        employee(2, "Ponting", "Marksheet", "Clerk"),
        employee(3, "Laxman", "Accounts", "Head Clerk"),
        employee(4, "Flintoff", "Exam", "Clerk"),
        employee(5, "Murlidharan", "Accounts", "CAO"),
        employee(6, "Sarfaraz", "Exam", "Informer"),
        employee(7, "Dean Jones", "Exam", "Invigilator"),
        employee(8, "Madugalle", "Exam", "Examiner"),
        employee(9, "Ganguly", "Marksheet", "Repeater"),
        employee(10, "Nafees", "Accounts", "Clerk")
    };

    int Array2[] = {1,8,9,5,4,12,11,45,23,89,65,34,12,44,65,22};
    char Array3[] = "irngiremxc";

    GenericBubbleSort(Array2,16);
    for(int i = 0; i < 16; i++)
    {
        cout << " " << Array2[i] << ",";
    }
    cout <<"\n";

    GenericBubbleSort (Array3,10);
    for(int i = 0; i < 10; i++)
    {
        cout << " " << Array3[i] << ",";
    }

    GenericBubbleSort(UniEmployee, 10);
    for(int i = 0; i < 10; i++)
    {
        cout << " " << UniEmployee[i] << ",";
    }
}
```
